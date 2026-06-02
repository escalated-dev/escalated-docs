# Inbound Email

Create and reply to tickets directly from incoming emails. Escalated supports **Postmark** and **Mailgun** webhooks out of the box, with an open parser interface for plugging in additional providers.

## How It Works

1. Your email provider receives a message at your support address (e.g., `support@yourapp.com`).
2. The provider forwards it to your app via webhook.
3. Escalated normalizes the payload and resolves the message to an existing ticket using, in order: canonical `Message-ID` headers (`<ticket-{id}@{domain}>`), signed `Reply-To` verification (`reply+{id}.{hmac8}@{domain}`), and subject-reference tags (`[ESC-00001]`).
4. Matched emails add a reply; unmatched emails create a new ticket (or are skipped if they're noise — SNS subscription confirmations, empty body+subject).

## Webhook model

All greenfield framework ports (.NET, Spring, Go, Phoenix, Symfony) expose a **single unified webhook endpoint** and select the parser via the `adapter` query parameter or `X-Escalated-Adapter` header. Per-framework routes:

| Framework | Webhook URL |
| --- | --- |
| .NET | `POST /support/webhook/email/inbound?adapter=<postmark\|mailgun>` |
| Spring Boot | `POST /escalated/webhook/email/inbound?adapter=<postmark\|mailgun>` |
| Go | `POST /escalated/webhook/email/inbound?adapter=<postmark\|mailgun>` |
| Phoenix | `POST /support/webhook/email/inbound?adapter=<postmark\|mailgun>` |
| Symfony | `POST /escalated/webhook/email/inbound?adapter=<postmark\|mailgun>` |

The legacy host-app integrations (Laravel, Rails, Django, Adonis, Filament, WordPress) expose provider-specific endpoints — see the respective framework page for the exact URL.

## Authentication

Webhooks are guarded by a shared secret. Your provider forwards it as `X-Escalated-Inbound-Secret`; the framework verifies it with a timing-safe comparison. The same secret is used to sign outbound `Reply-To` addresses (`reply+{id}.{hmac8}@{domain}`), so forged emails targeting a stolen reply address are rejected.

## Features

- **Thread detection** via canonical `Message-ID` / `In-Reply-To` / `References` headers, signed `Reply-To` verification, and subject-reference tags.
- **Signed Reply-To addresses** — outbound email embeds an HMAC so replies that strip threading headers still find the right ticket, and forged addresses are rejected.
- **Guest tickets** for unknown senders with auto-derived display names.
- **Noise filtering** — SNS subscription confirmations and empty body+subject messages are skipped rather than creating a ticket.
- **Attachment passthrough** — provider-hosted attachments (Mailgun's larger files) surface as `pending_attachment_downloads` for a background worker to fetch and persist out-of-band.
- **Audit logging** — every inbound email is recorded for debugging and compliance.
