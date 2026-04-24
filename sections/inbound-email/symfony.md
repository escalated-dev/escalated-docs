### Webhook endpoint

The Symfony bundle exposes a single webhook controller for all providers. Configure Postmark, Mailgun, or AWS SES (via SNS) to POST inbound mail to:

```
POST /escalated/webhook/email/inbound?adapter=postmark
POST /escalated/webhook/email/inbound?adapter=mailgun
```

You can also pass the adapter via the `X-Escalated-Adapter` header instead of a query parameter.

### Configuration

Set the shared inbound secret and mail domain (used for signed `Reply-To` and canonical `Message-ID` headers) under the `escalated:` bundle config:

```yaml
# config/packages/escalated.yaml
escalated:
    mail_domain: '%env(ESCALATED_MAIL_DOMAIN)%'
    inbound_secret: '%env(ESCALATED_INBOUND_SECRET)%'
```

```bash
# .env
ESCALATED_MAIL_DOMAIN=support.yourapp.com
ESCALATED_INBOUND_SECRET=a-long-random-value
```

The `inbound_secret` is symmetric — it signs outbound `Reply-To` addresses *and* verifies inbound webhook requests, so forged emails that target a stolen reply address are rejected via timing-safe comparison (`hash_equals`).

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
- **Subscription confirmation** — AWS SNS sends a one-time `SubscriptionConfirmation` envelope when you first subscribe the endpoint. The bundle throws `SESSubscriptionConfirmationException` carrying `$subscribeUrl`; your controller should catch it and GET that URL to activate the subscription (then return 202).
- **Custom headers** — SNS doesn't forward per-request custom headers, but it signs each delivery itself. Since the endpoint is secret-key-guarded, configure your infrastructure (load balancer, API gateway, or edge proxy) to inject the `X-Escalated-Inbound-Secret` header on requests to the SES path.
- **Body extraction** — configure the SES receipt rule with action type `SNS` and encoding `BASE64` to receive the full raw MIME body. The bundle's hand-rolled splitter decodes `text/plain`, `text/html`, `multipart/alternative`, and `quoted-printable` transfer encoding — no external MIME dep. Without full content, threading metadata is still extracted and tickets still route correctly via Message-ID threading.

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

The bundle ships `AttachmentDownloader` for persisting those URLs. Run it after `InboundEmailService::process()` returns — typically dispatched through Symfony Messenger so the webhook response goes back to the provider without waiting for the download.

```php
use Escalated\Symfony\Mail\Inbound\AttachmentDownloader;
use Escalated\Symfony\Mail\Inbound\AttachmentDownloaderOptions;
use Escalated\Symfony\Mail\Inbound\BasicAuth;
use Escalated\Symfony\Mail\Inbound\CurlAttachmentHttpClient;
use Escalated\Symfony\Mail\Inbound\LocalFileAttachmentStorage;

$storage = new LocalFileAttachmentStorage('/var/escalated/attachments');

$downloader = new AttachmentDownloader(
    httpClient: new CurlAttachmentHttpClient(),
    storage: $storage,
    em: $entityManager,
    options: new AttachmentDownloaderOptions(
        maxBytes: 25 * 1024 * 1024,                            // 25 MB size cap
        basicAuth: new BasicAuth('api', $_ENV['MAILGUN_API_KEY']),
    ),
);

$results = $downloader->downloadAll(
    $result->pendingAttachmentDownloads,
    ticketId: $result->ticketId,
    replyId: $result->replyId,
);
```

`downloadAll()` continues past per-attachment failures so a single bad URL doesn't block the rest. Each input gets an `AttachmentDownloadResult` with either `persisted` (the new `Attachment` entity) or `error` (the `Throwable`) set.

Over-sized attachments throw `AttachmentTooLargeException` — the partial body isn't persisted. Crafted filenames like `../../etc/passwd` are neutralized via `basename()` before they hit the storage backend.

The default HTTP client uses cURL (no extra Composer dep). Host apps using `symfony/http-client`, Guzzle, etc. can implement `AttachmentHttpClientInterface` with a thin adapter and pass it instead.

Host apps with durable cloud storage (S3, Azure Blob, GCS) implement `AttachmentStorageInterface` themselves and pass it to `AttachmentDownloader` in place of the reference `LocalFileAttachmentStorage`.

### Adding a custom parser

The bundle discovers inbound parsers by the `escalated.inbound_parser` tag. To add a new one, implement `Escalated\Symfony\Mail\Inbound\InboundEmailParser` and autoconfigure:

```yaml
# config/services.yaml
services:
    _instanceof:
        Escalated\Symfony\Mail\Inbound\InboundEmailParser:
            tags: ['escalated.inbound_parser']
```
