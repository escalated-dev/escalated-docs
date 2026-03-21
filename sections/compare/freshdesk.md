# Escalated vs Freshdesk

Freshdesk by Freshworks is a popular cloud-based helpdesk known for its free tier and approachable pricing. Escalated offers a similar breadth of features as a fully open-source, self-hosted solution that integrates directly into your application — with no agent limits on any feature.

## Feature comparison

| Feature | Escalated | Freshdesk |
|---------|-----------|-----------|
| **Core Ticketing** | | |
| Ticket management | ✓ | ✓ |
| Assignment & routing | ✓ | ✓ |
| Ticket merging | ✓ | ✓ |
| Ticket linking | ✓ | ✓ (Growth+) |
| Bulk actions | ✓ | ✓ |
| Custom statuses | ✓ | ✓ |
| Custom fields | ✓ | ✓ |
| Tags | ✓ | ✓ |
| **Agent Tools** | | |
| Macros | ✓ | ✓ (canned responses) |
| Canned responses | ✓ | ✓ |
| Collision detection | ✓ | ✓ |
| Keyboard shortcuts | ✓ | ✓ |
| Side conversations | ✓ | ✓ (parent-child tickets) |
| SLA timers | ✓ | ✓ |
| **Automation** | | |
| Triggers & automations | ✓ | ✓ |
| Escalation rules | ✓ | ✓ |
| Skills-based routing | ✓ | ✓ (Pro+) |
| Round-robin assignment | ✓ | ✓ |
| Capacity management | ✓ | ✓ (Enterprise) |
| **Self-Service** | | |
| Knowledge base | ✓ | ✓ |
| Customer portal | ✓ | ✓ |
| Guest tickets | ✓ | ✓ |
| Community forums | ✓ (plugin) | ✓ |
| **Channels** | | |
| Email | ✓ | ✓ |
| Live chat | ✓ (plugin) | ✓ (Freshchat, separate product) |
| Phone | ✓ (plugin) | ✓ (Freshcaller, separate product) |
| SMS | ✓ (plugin) | ✓ |
| WhatsApp | ✓ (plugin) | ✓ (Growth+) |
| Social media | ✓ (plugin) | ✓ |
| Web widget | ✓ (plugin) | ✓ |
| **AI & Intelligence** | | |
| AI copilot | ✓ (plugin) | ✓ (Freddy AI, add-on) |
| KB AI search | ✓ (plugin) | ✓ |
| Sentiment analysis | ✓ (plugin) | ✓ (Pro+) |
| Auto-categorization | ✓ (plugin) | ✓ (Freddy AI) |
| **Analytics** | | |
| Reports dashboard | ✓ | ✓ |
| Agent metrics | ✓ | ✓ |
| SLA reports | ✓ | ✓ |
| CSAT | ✓ | ✓ |
| NPS | ✓ (plugin) | ✓ (via Freshsurvey) |
| Scheduled reports | ✓ (plugin) | ✓ (Pro+) |
| **Admin & Security** | | |
| Custom roles / RBAC | ✓ | ✓ (Enterprise) |
| Audit log | ✓ | ✓ (Enterprise) |
| SSO | ✓ | ✓ |
| Two-factor auth | ✓ | ✓ |
| IP restriction | ✓ (plugin) | ✓ (Estate/Enterprise) |
| Data retention controls | ✓ | ✓ |
| Sandbox environment | ✓ | ✓ (Enterprise) |
| Compliance (HIPAA/SOC2) | ✓ (plugin) | ✓ (Enterprise) |
| **Platform** | | |
| Open source | ✓ | ✗ |
| Self-hosted | ✓ | ✗ |
| REST API | ✓ | ✓ |
| Webhooks | ✓ | ✓ |
| Custom objects | ✓ | ✓ (Pro+) |
| Plugin / app system | ✓ | ✓ (Marketplace) |
| Multi-framework | ✓ (Laravel, Rails, Django, AdonisJS, WordPress, Filament) | ✗ |
| **Integrations** | | |
| Jira | ✓ (plugin) | ✓ |
| Slack | ✓ (plugin) | ✓ |
| Import tools | Help Scout, Intercom importers | ✓ (various) |
| **Mobile & Desktop** | | |
| Mobile SDK (React Native) | ✓ | ✓ |
| Mobile SDK (Flutter) | ✓ | ✗ |
| Desktop app | ✓ | ✗ |

## Key differentiators

- **Truly open source.** Escalated's source code is fully available. Freshdesk has a free tier, but it is closed-source SaaS with limited features on the free plan. Escalated gives you every feature from day one.

- **Embeds into your application.** Escalated lives inside your existing codebase — same database, same authentication, same deployment. Freshdesk is a separate platform that requires customers and agents to work in Freshdesk's environment.

- **Unified platform.** Freshdesk's phone, chat, and CRM features are separate Freshworks products (Freshcaller, Freshchat, Freshsales) with their own pricing. In Escalated, channels like live chat, phone, and SMS are plugins within a single system.

- **No per-agent pricing at any tier.** Freshdesk's free plan is limited to 10 agents with basic features. Paid plans charge $15–$79+ per agent per month. Escalated is free for unlimited agents with full functionality.

## Migrating from Freshdesk

Escalated includes a dedicated **Freshdesk importer plugin** (`escalated-plugin-import-freshdesk`) that helps you migrate tickets, contacts, and other data from your Freshdesk account. See the [Importing Data](#importing) section for setup instructions.

## Pricing comparison

| | Escalated | Freshdesk |
|--|-----------|-----------|
| Starting price | Free (open source) | Free (up to 10 agents, limited features) |
| Mid-tier | Free | $49/agent/month (Pro) |
| Full-featured | Free | $79/agent/month (Enterprise) |
| AI features | Included (plugin) | $29+/agent/month (Freddy AI add-on) |
| Per-agent fees | None | Yes, on all paid plans |

Freshdesk's free tier is attractive for very small teams, but it lacks automation, collision detection, custom roles, and many other features available in paid plans. A 25-agent team on the Pro plan would pay approximately $1,225/month ($14,700/year). Escalated includes all features at no cost.
