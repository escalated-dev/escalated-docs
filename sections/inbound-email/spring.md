### Webhook endpoint

The Spring Boot starter exposes a single webhook for all providers. Configure Postmark and/or Mailgun to POST inbound mail to:

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

The receiver compares `X-Escalated-Inbound-Secret` with the configured shared secret. This header carries the shared value, not a provider signature or a payload HMAC. Use HTTPS and a trusted forwarding service if your provider cannot attach the header.

**Postmark** — in your server settings under *Inbound → Webhook URL*:

```
https://yourapp.com/escalated/webhook/email/inbound?adapter=postmark
```

Add a custom header `X-Escalated-Inbound-Secret: <your secret>`.

**Mailgun** — under *Receiving → Routes*, create a "Forward" action pointing at:

```
https://yourapp.com/escalated/webhook/email/inbound?adapter=mailgun
```

Have your trusted forwarding service attach the configured shared-secret header.

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
  "outcome": "CREATED_NEW",
  "ticketId": 7,
  "replyId": null,
  "pendingAttachmentDownloads": []
}
```

Provider-hosted attachments (Mailgun's larger files, for example) appear in `pendingAttachmentDownloads` so a background worker can fetch and persist them out-of-band.
