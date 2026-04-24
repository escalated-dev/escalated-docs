### Webhook endpoint

The .NET bundle exposes a single webhook for all providers. Configure Postmark and/or Mailgun to POST inbound mail to:

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
