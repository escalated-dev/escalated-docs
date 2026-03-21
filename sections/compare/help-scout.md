# Escalated vs Help Scout

Help Scout is an email-first customer support platform designed for small to mid-size teams that value simplicity. Escalated offers a comparable experience as an open-source, self-hosted solution that embeds directly into your existing application, with no per-user fees and a broader range of channels through its plugin system.

## Feature comparison

| Feature | Escalated | Help Scout |
|---------|-----------|------------|
| **Core Ticketing** | | |
| Ticket management | ✓ | ✓ (conversations) |
| Assignment & routing | ✓ | ✓ |
| Ticket merging | ✓ | ✓ |
| Ticket linking | ✓ | ✗ |
| Bulk actions | ✓ | ✓ |
| Custom statuses | ✓ | Limited (open/pending/closed) |
| Custom fields | ✓ | ✓ |
| Tags | ✓ | ✓ |
| **Agent Tools** | | |
| Macros | ✓ | ✓ (saved replies) |
| Canned responses | ✓ | ✓ |
| Collision detection | ✓ | ✓ |
| Keyboard shortcuts | ✓ | ✓ |
| Side conversations | ✓ | ✓ (notes, @mentions) |
| SLA timers | ✓ | ✗ |
| **Automation** | | |
| Triggers & automations | ✓ | ✓ (workflows) |
| Escalation rules | ✓ | Limited |
| Skills-based routing | ✓ | ✗ |
| Round-robin assignment | ✓ | ✓ |
| Capacity management | ✓ | ✗ |
| **Self-Service** | | |
| Knowledge base | ✓ | ✓ (Docs) |
| Customer portal | ✓ | ✗ |
| Guest tickets | ✓ | ✗ |
| Community forums | ✓ (plugin) | ✗ |
| **Channels** | | |
| Email | ✓ | ✓ |
| Live chat | ✓ (plugin) | ✓ (Beacon) |
| Phone | ✓ (plugin) | ✗ |
| SMS | ✓ (plugin) | ✗ |
| WhatsApp | ✓ (plugin) | ✗ |
| Social media | ✓ (plugin) | ✓ (limited, via integrations) |
| Web widget | ✓ (plugin) | ✓ (Beacon) |
| **AI & Intelligence** | | |
| AI copilot | ✓ (plugin) | ✓ (AI Drafts, Plus plan) |
| KB AI search | ✓ (plugin) | ✓ (AI Answers) |
| Sentiment analysis | ✓ (plugin) | ✗ |
| Auto-categorization | ✓ (plugin) | ✗ |
| **Analytics** | | |
| Reports dashboard | ✓ | ✓ |
| Agent metrics | ✓ | ✓ |
| SLA reports | ✓ | ✗ |
| CSAT | ✓ | ✓ |
| NPS | ✓ (plugin) | ✗ |
| Scheduled reports | ✓ (plugin) | ✗ |
| **Admin & Security** | | |
| Custom roles / RBAC | ✓ | Limited (predefined roles) |
| Audit log | ✓ | ✗ |
| SSO | ✓ | ✓ (Plus plan) |
| Two-factor auth | ✓ | ✓ |
| IP restriction | ✓ (plugin) | ✗ |
| Data retention controls | ✓ | Limited |
| Sandbox environment | ✓ | ✗ |
| Compliance (HIPAA/SOC2) | ✓ (plugin) | ✓ (Plus plan, HIPAA add-on) |
| **Platform** | | |
| Open source | ✓ | ✗ |
| Self-hosted | ✓ | ✗ |
| REST API | ✓ | ✓ |
| Webhooks | ✓ | ✓ |
| Custom objects | ✓ | ✗ |
| Plugin / app system | ✓ | ✓ (limited integrations) |
| Multi-framework | ✓ (Laravel, Rails, Django, AdonisJS, WordPress, Filament) | ✗ |
| **Integrations** | | |
| Jira | ✓ (plugin) | ✓ |
| Slack | ✓ (plugin) | ✓ |
| Import tools | Freshdesk, Intercom importers | ✗ |
| **Mobile & Desktop** | | |
| Mobile SDK (React Native) | ✓ | ✗ |
| Mobile SDK (Flutter) | ✓ | ✗ |
| Desktop app | ✓ | ✗ |

## Key differentiators

- **Open source and self-hosted.** Escalated gives you full access to the source code and runs on your servers. Help Scout is closed-source SaaS with no self-hosted option, meaning your customer data always lives on Help Scout's infrastructure.

- **More channels out of the box.** Help Scout is primarily email and chat (Beacon). Escalated's plugin system adds phone, SMS, WhatsApp, and social media channels, giving you a true omnichannel helpdesk.

- **Deeper customization.** Escalated supports custom statuses, custom objects, SLAs with escalation rules, skills-based routing, and capacity management — areas where Help Scout has limited or no coverage. Help Scout intentionally keeps things simple, which works for some teams but can be limiting as you scale.

- **No per-user pricing.** Help Scout charges $50–$75+ per user per month. Escalated is free for unlimited agents.

## Migrating from Help Scout

Escalated includes a dedicated **Help Scout importer plugin** (`escalated-plugin-import-helpscout`) that helps you migrate conversations, customers, and mailbox data from your Help Scout account. See the [Importing Data](#importing) section for setup instructions.

## Pricing comparison

| | Escalated | Help Scout |
|--|-----------|------------|
| Starting price | Free (open source) | $50/user/month (Standard) |
| Mid-tier | Free | $75/user/month (Plus) |
| Per-user fees | None | Yes, all plans |
| AI features | Included (plugin) | Included on Plus plan |

Help Scout's pricing is straightforward but adds up quickly with team growth. A 20-agent team on the Standard plan costs $1,000/month ($12,000/year). Escalated provides more features — including SLAs, custom roles, audit logs, and additional channels — at no licensing cost.
