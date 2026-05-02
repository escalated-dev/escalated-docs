### Webhook endpoint

The Go module exposes a single webhook handler for all providers. Configure Postmark, Mailgun, or AWS SES (via SNS) to POST inbound mail to:

```
POST /escalated/webhook/email/inbound?adapter=postmark
POST /escalated/webhook/email/inbound?adapter=mailgun
```

You can also pass the adapter via the `X-Escalated-Adapter` header instead of a query parameter.

### Configuration

Set the shared inbound secret and mail domain (used for signed `Reply-To` and canonical `Message-ID` headers) via environment variables or directly on `email.Config`:

```bash
ESCALATED_MAIL_DOMAIN=support.yourapp.com
ESCALATED_INBOUND_SECRET=a-long-random-value
```

```go
cfg := email.Config{
    MailDomain:     os.Getenv("ESCALATED_MAIL_DOMAIN"),
    InboundSecret:  os.Getenv("ESCALATED_INBOUND_SECRET"),
}
```

The `InboundSecret` is symmetric — it signs outbound `Reply-To` addresses *and* verifies inbound webhook requests, so forged emails that target a stolen reply address are rejected via timing-safe HMAC comparison (`hmac.Equal`).

### Wiring

Register the handler on your `http.ServeMux`:

```go
svc := email.NewInboundEmailService(router, writer)
handler := handlers.NewInboundEmailHandler(svc, parsers, cfg.InboundSecret)
mux.Handle("POST /escalated/webhook/email/inbound", handler)
```

### Provider setup

Each provider signs its webhook and expects you to forward that signature via the `X-Escalated-Inbound-Secret` header.

**Postmark** — in your server settings under *Inbound → Webhook URL*:

```
https://yourapp.com/escalated/webhook/email/inbound?adapter=postmark
```

Add a custom header `X-Escalated-Inbound-Secret: <your secret>`.

**Mailgun** — under *Receiving → Routes*, create a "Forward" action pointing at:

```
https://yourapp.com/escalated/webhook/email/inbound?adapter=mailgun
```

Set the HMAC header the same way.

**AWS SES** — create an SES receipt rule that publishes to an SNS topic, then subscribe your webhook URL to that topic:

```
https://yourapp.com/escalated/webhook/email/inbound?adapter=ses
```

SES-specific notes:
- **Subscription confirmation** — AWS SNS sends a one-time `SubscriptionConfirmation` envelope when you first subscribe the endpoint. The parser returns a sentinel `email.ErrSESSubscriptionConfirmation` wrapping an `*email.SESSubscriptionConfirmation` that carries the `SubscribeURL`. Use `errors.As` to unwrap it; your handler should GET that URL to activate the subscription (then return 200).
- **Custom headers** — SNS doesn't forward per-request custom headers, but it signs each delivery itself. Since the endpoint is secret-key-guarded, configure your infrastructure (load balancer, API gateway, or CDN) to inject the `X-Escalated-Inbound-Secret` header on requests to the SES path.
- **Body extraction** — configure the SES receipt rule with action type `SNS` and encoding `BASE64` to receive the full raw MIME body. The module decodes `text/plain`, `text/html`, and `multipart/alternative` bodies using stdlib `net/mail` + `mime/multipart`. Without full content, threading metadata is still extracted and tickets still route correctly via Message-ID threading.

### Testing

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "X-Escalated-Inbound-Secret: <your secret>" \
  -d '{
    "FromFull": {"Email": "customer@example.com", "Name": "Customer"},
    "To": "support@example.com",
    "Subject": "Hello",
    "TextBody": "Help please",
    "MessageID": "<abc@mail>"
  }' \
  "https://yourapp.com/escalated/webhook/email/inbound?adapter=postmark"
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

The module ships `email.AttachmentDownloader` for persisting the URLs in `pending_attachment_downloads`. Run it from a goroutine (or a queue worker) after `InboundEmailService.Process` returns, so the webhook response goes back to the provider without waiting for the download.

```go
import "github.com/escalated-dev/escalated-go/services/email"

storage, err := email.NewLocalFileStorage("/var/escalated/attachments")
if err != nil {
    log.Fatal(err)
}

downloader := email.NewAttachmentDownloader(
    email.DownloadConfig{
        MaxBytes:  25 * 1024 * 1024,                         // 25 MB size cap
        BasicAuth: &email.BasicAuth{Username: "api", Password: mailgunAPIKey},
    },
    storage,
    store, // your store.Store — already implements CreateAttachment
)

results, errs := downloader.DownloadAll(ctx, result.PendingAttachmentDownloads, result.TicketID, nil)
for i, err := range errs {
    if err != nil {
        log.Printf("download %d failed: %v", i, err)
    }
}
```

`DownloadAll` continues past per-attachment failures so a single bad URL doesn't block the rest. Parallel slices report each input's outcome: a non-nil `*models.Attachment` on success and a non-nil `error` on failure.

Over-sized attachments return `email.ErrAttachmentTooLarge` (check with `errors.Is`) — the partial body isn't persisted. Crafted filenames like `../../etc/passwd` are neutralized via `filepath.Base` before they hit the storage backend.

Host apps with durable cloud storage (S3, GCS, Azure Blob) implement `email.AttachmentStorage` themselves and pass it to `NewAttachmentDownloader` in place of the reference `LocalFileStorage`.
