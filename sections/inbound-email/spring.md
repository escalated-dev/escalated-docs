### Webhook endpoint

The Spring Boot starter exposes a single webhook for all providers. Configure Postmark, Mailgun, or AWS SES (via SNS) to POST inbound mail to:

```
POST /escalated/webhook/email/inbound?adapter=postmark
POST /escalated/webhook/email/inbound?adapter=mailgun
```

You can also pass the adapter via the `X-Escalated-Adapter` header instead of a query parameter.

### Configuration

Set the shared inbound secret and mail domain (used for signed `Reply-To` and canonical `Message-ID` headers) in `application.yml`:

```yaml
escalated:
  mail:
    domain: support.yourapp.com
    inbound-secret: ${ESCALATED_INBOUND_SECRET}
```

Or via environment variables:

```bash
ESCALATED_MAIL_DOMAIN=support.yourapp.com
ESCALATED_INBOUND_SECRET=a-long-random-value
```

The `inbound-secret` is symmetric — it signs outbound `Reply-To` addresses *and* verifies inbound webhook requests, so forged emails that target a stolen reply address are rejected via timing-safe HMAC comparison (`MessageDigest.isEqual`).

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
- **Subscription confirmation** — AWS SNS sends a one-time `SubscriptionConfirmation` envelope when you first subscribe the endpoint. The starter throws `SESSubscriptionConfirmationException` carrying `getSubscribeUrl()`; your controller should catch it and GET that URL to activate the subscription (then return 200).
- **Custom headers** — SNS doesn't forward per-request custom headers, but it signs each delivery itself. Since the endpoint is secret-key-guarded, configure your infrastructure (load balancer, API gateway, or ingress) to inject the `X-Escalated-Inbound-Secret` header on requests to the SES path.
- **Body extraction** — configure the SES receipt rule with action type `SNS` and encoding `BASE64` to receive the full raw MIME body. The starter decodes `text/plain`, `text/html`, and `multipart/alternative` bodies via `jakarta.mail`. Without full content, threading metadata is still extracted and tickets still route correctly via Message-ID threading.

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
  "ticketId": 7,
  "replyId": null,
  "pendingAttachmentDownloads": []
}
```

Provider-hosted attachments (Mailgun's larger files, for example) appear in `pendingAttachmentDownloads` so a background worker can fetch and persist them out-of-band.

### Downloading provider-hosted attachments

The starter ships `AttachmentDownloader` for persisting the URLs in `pendingAttachmentDownloads`. Run it after `InboundEmailService.process` returns — typically from an `@Async` method or a Spring Batch job so the webhook response is sent back to the provider without waiting for the download.

```java
import dev.escalated.services.email.inbound.AttachmentDownloader;
import dev.escalated.services.email.inbound.LocalFileAttachmentStorage;

import java.net.http.HttpClient;
import java.nio.file.Path;

var storage = new LocalFileAttachmentStorage(Path.of("/var/escalated/attachments"));

var downloader = new AttachmentDownloader(
    HttpClient.newHttpClient(),
    storage,
    attachmentRepository,
    ticketRepository,
    replyRepository,
    new AttachmentDownloader.Options()
        .maxBytes(25L * 1024 * 1024)             // 25 MB size cap
        .basicAuth("api", mailgunApiKey)         // required for Mailgun
);

List<AttachmentDownloader.Result> results = downloader.downloadAll(
    result.pendingAttachmentDownloads(),
    result.ticketId(),
    result.replyId());
```

`downloadAll` continues past per-attachment failures so a single bad URL doesn't block the rest. Each input gets a `Result` with either `persisted` (the new `Attachment` row) or `error` (the `Throwable`) set.

Over-sized attachments raise `AttachmentTooLargeException` — the partial body isn't persisted. Crafted filenames like `../../etc/passwd` are neutralized via `Path.getFileName` before they hit the storage backend.

Host apps with durable cloud storage (S3, Azure Blob, GCS) implement `AttachmentStorage` themselves and pass it to `AttachmentDownloader` in place of the reference `LocalFileAttachmentStorage`.
