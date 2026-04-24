### Webhook endpoint

The Phoenix library exposes a single webhook controller for all providers. Configure Postmark, Mailgun, or AWS SES (via SNS) to POST inbound mail to:

```
POST /support/webhook/email/inbound?adapter=postmark
POST /support/webhook/email/inbound?adapter=mailgun
```

You can also pass the adapter via the `x-escalated-adapter` header instead of a query parameter.

### Configuration

Set the shared inbound secret and mail domain (used for signed `Reply-To` and canonical `Message-ID` headers) in `config/runtime.exs`:

```elixir
config :escalated,
  mail_domain: System.get_env("ESCALATED_MAIL_DOMAIN", "support.yourapp.com"),
  email_inbound_secret: System.fetch_env!("ESCALATED_INBOUND_SECRET"),
  inbound_parsers: [
    Escalated.Services.Email.Inbound.PostmarkParser,
    Escalated.Services.Email.Inbound.MailgunParser
  ]
```

The `email_inbound_secret` is symmetric — it signs outbound `Reply-To` addresses *and* verifies inbound webhook requests, so forged emails that target a stolen reply address are rejected via timing-safe comparison (`Plug.Crypto.secure_compare/2`).

### Wiring

Register the route in your Phoenix router:

```elixir
scope "/support/webhook/email", Escalated.Controllers do
  pipe_through :api
  post "/inbound", InboundEmailController, :inbound
end
```

### Provider setup

Each provider signs its webhook and expects you to forward that signature via the `x-escalated-inbound-secret` header.

**Postmark** — in your server settings under *Inbound → Webhook URL*:

```
https://yourapp.com/support/webhook/email/inbound?adapter=postmark
```

Add a custom header `x-escalated-inbound-secret: <your secret>`.

**Mailgun** — under *Receiving → Routes*, create a "Forward" action pointing at:

```
https://yourapp.com/support/webhook/email/inbound?adapter=mailgun
```

Set the HMAC header the same way.

**AWS SES** — create an SES receipt rule that publishes to an SNS topic, then subscribe your webhook URL to that topic:

```
https://yourapp.com/support/webhook/email/inbound?adapter=ses
```

SES-specific notes:
- **Subscription confirmation** — AWS SNS sends a one-time `SubscriptionConfirmation` envelope when you first subscribe the endpoint. The parser returns `{:error, {:ses_subscription_confirmation, %{subscribe_url: ..., topic_arn: ..., token: ...}}}`. Match on the tuple in your controller and GET the `subscribe_url` to activate the subscription (then return 200).
- **Custom headers** — SNS doesn't forward per-request custom headers, but it signs each delivery itself. Since the endpoint is secret-key-guarded, configure your infrastructure (load balancer, API gateway, or edge proxy) to inject the `x-escalated-inbound-secret` header on requests to the SES path.
- **Body extraction** — configure the SES receipt rule with action type `SNS` and encoding `BASE64` to receive the full raw MIME body. The library's hand-rolled splitter decodes `text/plain`, `text/html`, `multipart/alternative`, and `quoted-printable` transfer encoding — no external MIME dep. Without full content, threading metadata is still extracted and tickets still route correctly via Message-ID threading.

Register the SES parser alongside the others in `config/runtime.exs`:

```elixir
config :escalated,
  inbound_parsers: [
    Escalated.Services.Email.Inbound.PostmarkParser,
    Escalated.Services.Email.Inbound.MailgunParser,
    Escalated.Services.Email.Inbound.SESParser
  ]
```

### Testing

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "x-escalated-inbound-secret: <your secret>" \
  -d '{
    "FromFull": {"Email": "customer@example.com", "Name": "Customer"},
    "To": "support@example.com",
    "Subject": "Hello",
    "TextBody": "Help please",
    "MessageID": "<abc@mail>"
  }' \
  "https://yourapp.com/support/webhook/email/inbound?adapter=postmark"
```

The response shape:

```json
{
  "status": "created",
  "outcome": "created_new",
  "ticket_id": 7,
  "reply_id": null,
  "pending_attachment_downloads": []
}
```

Provider-hosted attachments (Mailgun's larger files, for example) appear in `pending_attachment_downloads` so a background worker can fetch and persist them out-of-band.

### Downloading provider-hosted attachments

The library ships `Escalated.Services.Email.Inbound.AttachmentDownloader` for persisting the URLs in `:pending_attachment_downloads`. Run it from a `Task.async` or a dedicated Oban/Exq job so the webhook response goes back to the provider without waiting for the download.

```elixir
alias Escalated.Services.Email.Inbound.AttachmentDownloader
alias Escalated.Services.Email.Inbound.LocalFileStorage

storage = LocalFileStorage.new("/var/escalated/attachments")

writer = %{
  create_attachment: fn attrs ->
    %Escalated.Schemas.Attachment{}
    |> Escalated.Schemas.Attachment.changeset(attrs)
    |> MyApp.Repo.insert()
  end
}

options = %{
  max_bytes: 25 * 1024 * 1024,                        # 25 MB size cap
  basic_auth: {"api", System.fetch_env!("MAILGUN_API_KEY")}  # required for Mailgun
}

results =
  AttachmentDownloader.download_all(
    result.pending_attachment_downloads,
    result.ticket_id,
    result.reply_id,
    storage,
    writer,
    options
  )
```

`download_all/6` continues past per-attachment failures so a single bad URL doesn't block the rest. Each input gets a `%{pending, persisted, error}` map — `:persisted` is the inserted `Attachment` struct on success, `:error` carries the reason on failure.

Over-sized attachments return `{:error, {:too_large, actual_bytes, max_bytes}}` — the partial body isn't persisted. Crafted filenames like `../../etc/passwd` are neutralized via `Path.basename/1` before they hit the storage backend.

The default HTTP client is `:httpc` from the Erlang stdlib (no external dep). Host apps using Finch / HTTPoison / Req can pass `:http_client` to `options`:

```elixir
options = Map.put(options, :http_client, {MyApp.FinchClient, :get})
```

Host apps with durable cloud storage (S3, GCS, Azure Blob) build their own storage function-map with `put: fn filename, content, content_type -> ...` and pass it in place of `LocalFileStorage.new/1`.
