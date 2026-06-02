### Webhook endpoint

The Phoenix library exposes a single webhook controller for all providers. Configure Postmark and/or Mailgun to POST inbound mail to:

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
