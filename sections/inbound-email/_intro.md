# Inbound Email

Create and reply to tickets directly from incoming emails. Escalated supports **Mailgun**, **Postmark**, **AWS SES** webhooks, and **IMAP** polling as a fallback.

## How It Works

1. Your email provider receives a message at your support address (e.g., `support@yourapp.com`)
2. The provider forwards it to your app via webhook (or IMAP polling fetches it)
3. Escalated normalizes the payload and checks for thread matches via subject reference (e.g., `[ESC-00001]`) or `In-Reply-To` headers
4. Matched emails add a reply; unmatched emails create a new ticket (or guest ticket for unknown senders)

## Configuration

Enable inbound email and configure your adapter in admin settings, or via environment variables. Admin settings take priority over env/config values.

## Webhook URLs

Point your email provider's inbound webhook to these URLs. These routes require no authentication (they use signature verification instead).

| Provider | Webhook URL |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## IMAP Polling

For email providers without webhook support, use the IMAP polling command on a schedule.

## Features

- **Thread detection** via subject reference and In-Reply-To / References headers
- **Guest tickets** for unknown senders with auto-derived display names
- **Auto-reopen** resolved or closed tickets when a reply arrives via email
- **Duplicate detection** via Message-ID headers to prevent duplicate processing
- **Attachment handling** with configurable size and count limits
- **Audit logging** -- every inbound email is recorded for debugging and compliance
- **Admin configurable** -- all settings manageable from the admin panel with env/config fallback
