# Escalated vs Jira Service Management

Jira Service Management (JSM) by Atlassian is an IT service management (ITSM) platform built on the Jira ecosystem. It excels at IT operations, incident management, and change management. Escalated is an open-source, embeddable helpdesk focused on customer support ticketing that integrates directly into your application across multiple frameworks.

## Feature comparison

| Feature | Escalated | Jira Service Management |
|---------|-----------|------------------------|
| **Core Ticketing** | | |
| Ticket management | ✓ | ✓ (issues/requests) |
| Assignment & routing | ✓ | ✓ |
| Ticket merging | ✓ | ✓ (link as duplicate) |
| Ticket linking | ✓ | ✓ |
| Bulk actions | ✓ | ✓ |
| Custom statuses | ✓ | ✓ (workflow statuses) |
| Custom fields | ✓ | ✓ |
| Tags / labels | ✓ | ✓ |
| **Agent Tools** | | |
| Macros | ✓ | ✓ (automation templates) |
| Canned responses | ✓ | ✓ |
| Collision detection | ✓ | ✗ |
| Keyboard shortcuts | ✓ | ✓ |
| Side conversations | ✓ | ✓ (internal comments) |
| SLA timers | ✓ | ✓ |
| **Automation** | | |
| Triggers & automations | ✓ | ✓ (Jira Automation) |
| Escalation rules | ✓ | ✓ |
| Skills-based routing | ✓ | ✗ |
| Round-robin assignment | ✓ | ✓ (via automation) |
| Capacity management | ✓ | ✗ |
| **Self-Service** | | |
| Knowledge base | ✓ | ✓ (Confluence integration) |
| Customer portal | ✓ | ✓ |
| Guest tickets | ✓ | ✓ |
| Community forums | ✓ (plugin) | ✓ (Confluence/Community) |
| **Channels** | | |
| Email | ✓ | ✓ |
| Live chat | ✓ (plugin) | ✓ (Halp / chat integrations) |
| Phone | ✓ (plugin) | ✗ (via third-party) |
| SMS | ✓ (plugin) | ✗ (via third-party) |
| WhatsApp | ✓ (plugin) | ✗ (via third-party) |
| Social media | ✓ (plugin) | ✗ (via third-party) |
| Web widget | ✓ (plugin) | ✓ |
| **AI & Intelligence** | | |
| AI copilot | ✓ (plugin) | ✓ (Atlassian Intelligence) |
| KB AI search | ✓ (plugin) | ✓ (Atlassian Intelligence) |
| Sentiment analysis | ✓ (plugin) | ✗ |
| Auto-categorization | ✓ (plugin) | ✓ (via automation) |
| **Analytics** | | |
| Reports dashboard | ✓ | ✓ |
| Agent metrics | ✓ | ✓ |
| SLA reports | ✓ | ✓ |
| CSAT | ✓ | ✓ |
| NPS | ✓ (plugin) | ✗ (via third-party) |
| Scheduled reports | ✓ (plugin) | ✓ (via Jira dashboards) |
| **Admin & Security** | | |
| Custom roles / RBAC | ✓ | ✓ |
| Audit log | ✓ | ✓ |
| SSO | ✓ | ✓ |
| Two-factor auth | ✓ | ✓ |
| IP restriction | ✓ (plugin) | ✓ |
| Data retention controls | ✓ | ✓ |
| Sandbox environment | ✓ | ✓ (Premium+) |
| Compliance (HIPAA/SOC2) | ✓ (plugin) | ✓ (Enterprise) |
| **ITSM Features** | | |
| Incident management | ✗ | ✓ |
| Change management | ✗ | ✓ |
| Asset management | ✗ | ✓ |
| Problem management | ✗ | ✓ |
| Service catalog | ✗ | ✓ |
| **Platform** | | |
| Open source | ✓ | ✗ |
| Self-hosted | ✓ | Partial (Data Center — being deprecated) |
| REST API | ✓ | ✓ |
| Webhooks | ✓ | ✓ |
| Custom objects | ✓ | ✓ (Assets) |
| Plugin / app system | ✓ | ✓ (Atlassian Marketplace) |
| Multi-framework | ✓ (Laravel, Rails, Django, AdonisJS, WordPress, Filament) | ✗ |
| **Integrations** | | |
| Jira | ✓ (plugin) | Native |
| Slack | ✓ (plugin) | ✓ |
| Import tools | Freshdesk, Help Scout, Intercom importers | ✓ (various) |
| **Mobile & Desktop** | | |
| Mobile SDK (React Native) | ✓ | ✗ |
| Mobile SDK (Flutter) | ✓ | ✗ |
| Desktop app | ✓ | ✗ |
| Mobile app | ✗ | ✓ (Jira Mobile) |

## Key differentiators

- **Purpose-built for customer support.** JSM is rooted in ITSM and IT operations. Its workflows, terminology, and UX reflect that heritage. Escalated is designed specifically for customer support teams — the interface, automation, and agent tools are built around support workflows, not IT service requests.

- **Open source and self-hosted.** Escalated is fully open source and runs on your infrastructure. Atlassian is phasing out JSM's self-hosted Data Center option and pushing teams to their cloud platform. With Escalated, your deployment model is always your choice.

- **Embeds into your application.** Escalated installs as a package in your existing codebase, sharing authentication, database, and UI. JSM is a standalone Atlassian product that connects to your application only through APIs.

- **Simpler pricing.** JSM offers a free tier for up to 3 agents, but paid plans charge $19.04–$44.27 per agent per month. Escalated is free for unlimited agents with no feature gating.

## Where JSM has the advantage

JSM is a strong choice if your primary need is IT service management. Its incident management, change management, asset tracking, and service catalog features are mature and well-integrated with the broader Atlassian ecosystem (Jira Software, Confluence, Statuspage, Opsgenie). If you need ITSM capabilities, JSM is purpose-built for that. Escalated focuses on customer-facing support.

## Migrating from Jira Service Management

Escalated does not currently include a dedicated JSM importer, but the importing system supports building custom import adapters. You can use the Jira plugin (`escalated-plugin-jira`) to maintain a live integration between Escalated tickets and Jira issues during or after migration. See the [Importing Data](#importing) section for details.

## Pricing comparison

| | Escalated | Jira Service Management |
|--|-----------|------------------------|
| Starting price | Free (open source) | Free (up to 3 agents) |
| Mid-tier | Free | $19.04/agent/month (Standard) |
| Full-featured | Free | $44.27/agent/month (Premium) |
| Enterprise | Free | Custom pricing (Enterprise) |
| Per-agent fees | None | Yes, on paid plans |

JSM's free tier works for very small teams (3 agents or fewer), but it lacks multi-site support, advanced SLAs, and asset management. A 40-agent team on the Premium plan would pay approximately $1,771/month ($21,250/year). Escalated is free regardless of team size.
