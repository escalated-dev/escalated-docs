# Escalated vs Intercom

Intercom is a conversational support platform that combines live chat, a help center, and product messaging into a single tool. Escalated provides a full-featured ticketing and support system as an open-source, self-hosted package that embeds into your existing application, with channels like live chat, phone, and messaging available through plugins.

## Feature comparison

| Feature | Escalated | Intercom |
|---------|-----------|----------|
| **Core Ticketing** | | |
| Ticket management | ✓ | ✓ |
| Assignment & routing | ✓ | ✓ |
| Ticket merging | ✓ | ✓ |
| Ticket linking | ✓ | ✗ |
| Bulk actions | ✓ | ✓ |
| Custom statuses | ✓ | Limited |
| Custom fields | ✓ | ✓ (ticket attributes) |
| Tags | ✓ | ✓ |
| **Agent Tools** | | |
| Macros | ✓ | ✓ |
| Canned responses | ✓ | ✓ (saved replies) |
| Collision detection | ✓ | ✓ |
| Keyboard shortcuts | ✓ | ✓ |
| Side conversations | ✓ | ✓ |
| SLA timers | ✓ | ✓ |
| **Automation** | | |
| Triggers & automations | ✓ | ✓ (workflows) |
| Escalation rules | ✓ | ✓ |
| Skills-based routing | ✓ | ✓ |
| Round-robin assignment | ✓ | ✓ |
| Capacity management | ✓ | ✓ |
| **Self-Service** | | |
| Knowledge base | ✓ | ✓ (Help Center) |
| Customer portal | ✓ | ✗ |
| Guest tickets | ✓ | ✓ |
| Community forums | ✓ (plugin) | ✗ |
| **Channels** | | |
| Email | ✓ | ✓ |
| Live chat | ✓ (plugin) | ✓ (Messenger — core feature) |
| Phone | ✓ (plugin) | ✓ (add-on) |
| SMS | ✓ (plugin) | ✓ |
| WhatsApp | ✓ (plugin) | ✓ |
| Social media | ✓ (plugin) | ✓ |
| Web widget | ✓ (plugin) | ✓ (Messenger) |
| **AI & Intelligence** | | |
| AI copilot | ✓ (plugin) | ✓ (Fin AI Copilot) |
| KB AI search | ✓ (plugin) | ✓ (Fin AI Agent) |
| Sentiment analysis | ✓ (plugin) | ✓ |
| Auto-categorization | ✓ (plugin) | ✓ |
| **Analytics** | | |
| Reports dashboard | ✓ | ✓ |
| Agent metrics | ✓ | ✓ |
| SLA reports | ✓ | ✓ |
| CSAT | ✓ | ✓ |
| NPS | ✓ (plugin) | ✓ (Surveys) |
| Scheduled reports | ✓ (plugin) | ✓ |
| **Admin & Security** | | |
| Custom roles / RBAC | ✓ | ✓ |
| Audit log | ✓ | ✓ |
| SSO | ✓ | ✓ |
| Two-factor auth | ✓ | ✓ |
| IP restriction | ✓ (plugin) | ✓ |
| Data retention controls | ✓ | ✓ |
| Sandbox environment | ✓ | ✗ |
| Compliance (HIPAA/SOC2) | ✓ (plugin) | ✓ (Advanced plan) |
| **Platform** | | |
| Open source | ✓ | ✗ |
| Self-hosted | ✓ | ✗ |
| REST API | ✓ | ✓ |
| Webhooks | ✓ | ✓ |
| Custom objects | ✓ | ✓ (custom attributes) |
| Plugin / app system | ✓ | ✓ (App Store) |
| Multi-framework | ✓ (Laravel, Rails, Django, AdonisJS, WordPress, Filament) | ✗ |
| **Integrations** | | |
| Jira | ✓ (plugin) | ✓ |
| Slack | ✓ (plugin) | ✓ |
| Import tools | Freshdesk, Help Scout importers | ✓ (limited) |
| **Mobile & Desktop** | | |
| Mobile SDK (React Native) | ✓ | ✓ |
| Mobile SDK (Flutter) | ✓ | ✓ |
| Desktop app | ✓ | ✓ |

## Key differentiators

- **Open source with full data ownership.** Escalated runs on your infrastructure with complete source code access. Intercom is a closed-source SaaS platform — all your customer conversations and data live on Intercom's servers.

- **Embedded in your app, not bolted on.** Both Escalated and Intercom can appear in your product, but Escalated is architecturally part of your application — sharing your database, authentication, and deployment. Intercom's Messenger is a JavaScript widget that communicates with Intercom's servers.

- **No per-seat pricing.** Intercom's seat-based pricing starts at $29/seat/month and can reach $132+/seat/month on the Expert plan, with AI features adding additional per-resolution costs. Escalated is free for unlimited agents.

- **Traditional ticketing strength.** Intercom is built around conversations and messaging. If your team needs robust traditional ticketing features — SLAs, custom statuses, ticket linking, a customer portal, and community forums — Escalated has deeper support in these areas.

## Migrating from Intercom

Escalated includes a dedicated **Intercom importer plugin** (`escalated-plugin-import-intercom`) that helps you migrate conversations, contacts, and support data from your Intercom workspace. See the [Importing Data](#importing) section for setup instructions.

## Pricing comparison

| | Escalated | Intercom |
|--|-----------|----------|
| Starting price | Free (open source) | $29/seat/month (Essential) |
| Mid-tier | Free | $85/seat/month (Advanced) |
| Full-featured | Free | $132/seat/month (Expert) |
| AI agent | Included (plugin) | $0.99 per resolution (Fin AI) |
| Per-seat fees | None | Yes, all plans |

Intercom's pricing has multiple dimensions: per-seat fees plus per-resolution charges for AI features. A 30-agent team on the Advanced plan would pay approximately $2,550/month ($30,600/year) before AI resolution costs. Escalated has no licensing fees, and AI features are included through plugins.
