### Webhook endpoint

The .NET bundle exposes a single webhook for all providers. Configure Postmark, Mailgun, or AWS SES (via SNS) to POST inbound mail to:

```
POST /support/webhook/email/inbound?adapter=postmark
POST /support/webhook/email/inbound?adapter=mailgun
```

You can also pass the adapter via the `X-Escalated-Adapter` header instead of a query parameter.

### Configuration

Set the shared inbound secret and the mail domain (used for signed `Reply-To` and canonical `Message-ID` headers) in `appsettings.json` or via environment variables:

```json
{
  "Escalated": {
    "Mail": {
      "Domain": "support.yourapp.com",
      "InboundSecret": "a-long-random-value"
    }
  }
}
```

```bash
# .env
Escalated__Mail__Domain=support.yourapp.com
Escalated__Mail__InboundSecret=a-long-random-value
```

The `InboundSecret` is symmetric — it's used to sign outbound `Reply-To` addresses *and* to verify inbound webhook requests, so forged emails that target a stolen reply address are rejected via timing-safe HMAC comparison.

### Provider setup

Each provider signs its webhook and expects you to forward that signature via the `X-Escalated-Inbound-Secret` header.

**Postmark** — in your server settings under *Inbound → Webhook URL*:

```
https://yourapp.com/support/webhook/email/inbound?adapter=postmark
```

Add a custom header `X-Escalated-Inbound-Secret: <your secret>`.

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
- **Subscription confirmation** — AWS SNS sends a one-time `SubscriptionConfirmation` envelope when you first subscribe the endpoint. The bundle throws `SESSubscriptionConfirmationException` carrying the `SubscribeUrl`; your host controller should catch it and GET that URL to activate the subscription (then return `200 OK`).
- **Custom headers** — SNS doesn't forward per-request custom headers from you, but it signs each delivery itself. Since the endpoint is secret-key-guarded, configure your infrastructure (load balancer, API gateway, or CloudFront) to inject the `X-Escalated-Inbound-Secret` header on requests to the SES path.
- **Body extraction** — configure the SES receipt rule with action type `SNS` and encoding `BASE64` to receive the full raw MIME body. The bundle decodes `text/plain`, `text/html`, and `multipart/alternative` bodies. Without full content, metadata (from/to/subject/threading headers) is still extracted and tickets still route correctly via Message-ID threading.

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
  "https://yourapp.com/support/webhook/email/inbound?adapter=postmark"
```

The response shape:

```json
{
  "inboundId": 42,
  "status": "created",
  "outcome": "created_new",
  "ticketId": 7,
  "replyId": null,
  "pendingAttachmentDownloads": []
}
```

Provider-hosted attachments (Mailgun's larger files, for example) appear in `pendingAttachmentDownloads` so a background worker can fetch and persist them out-of-band.

### Downloading provider-hosted attachments

The bundle ships `AttachmentDownloader` for persisting the URLs in `pendingAttachmentDownloads`. Run it after `InboundEmailService.ProcessAsync` returns — typically from a background job queue so the webhook response is sent back to the provider without waiting for the download.

```csharp
using Escalated.Services.Email.Inbound;

var storage = new LocalFileAttachmentStorage("/var/escalated/attachments");

var downloader = new AttachmentDownloader(
    httpClient: new HttpClient(),
    storage: storage,
    db: dbContext,
    logger: logger,
    options: new AttachmentDownloaderOptions
    {
        MaxBytes = 25 * 1024 * 1024,                            // 25 MB size cap
        BasicAuth = new BasicAuth("api", mailgunApiKey),        // required for Mailgun
    });

var results = await downloader.DownloadAllAsync(
    result.PendingAttachmentDownloads,
    ticketId: result.TicketId.Value,
    replyId: result.ReplyId);
```

`DownloadAllAsync` continues past per-attachment failures so a single bad URL doesn't block the rest. Each input gets an `AttachmentDownloadResult` with either `Persisted` (the new `Attachment` row) or `Error` (the exception) set.

Over-sized attachments raise `AttachmentTooLargeException` — the partial body isn't persisted. Crafted filenames like `../../etc/passwd` are neutralized via `Path.GetFileName` before they hit the storage backend.

Host apps with durable cloud storage (S3, Azure Blob, GCS) implement `IAttachmentStorage` themselves and pass it to `AttachmentDownloader` in place of the reference `LocalFileAttachmentStorage`.
