### Webhook endpoint

The Symfony bundle exposes a single webhook controller for all providers. Configure Postmark and/or Mailgun to POST inbound mail to:

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

### Adding a custom parser

The bundle discovers inbound parsers by the `escalated.inbound_parser` tag. To add a new one, implement `Escalated\Symfony\Mail\Inbound\InboundEmailParser` and autoconfigure:

```yaml
# config/services.yaml
services:
    _instanceof:
        Escalated\Symfony\Mail\Inbound\InboundEmailParser:
            tags: ['escalated.inbound_parser']
```
