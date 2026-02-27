# Routes

Escalated registers three groups of routes under the configured prefix (default: `/support`).

## Customer routes

| Method | URL | Description |
| ------ | --- | ----------- |
| GET | /support | Customer ticket list |
| GET | /support/create | New ticket form |
| POST | /support | Create ticket |
| GET | /support/kb | Knowledge base home |
| GET | /support/kb/{slug} | Knowledge base article |
| POST | /support/kb/{slug}/feedback | Article feedback |
| GET | /support/{reference} | Ticket detail |
| POST | /support/{reference}/reply | Reply to ticket |
| POST | /support/{reference}/close | Close ticket |
| POST | /support/{reference}/reopen | Reopen ticket |
| POST | /support/{reference}/rate | Submit satisfaction rating |

## Agent routes

Requires the `escalated-agent` gate.

| Method | URL | Description |
| ------ | --- | ----------- |
| GET | /support/agent | Agent dashboard |
| GET | /support/agent/tickets | Ticket queue |
| GET | /support/agent/tickets/{reference} | Ticket detail |
| POST | /support/agent/tickets/{reference}/reply | Public reply |
| POST | /support/agent/tickets/{reference}/note | Internal note |
| POST | /support/agent/tickets/{reference}/assign | Assign agent |
| POST | /support/agent/tickets/{reference}/status | Change status |
| POST | /support/agent/tickets/{reference}/priority | Change priority |
| POST | /support/agent/tickets/bulk | Bulk ticket actions |
| POST | /support/agent/tickets/{reference}/follow | Toggle follow |
| POST | /support/agent/tickets/{reference}/macro | Apply macro |
| POST | /support/agent/tickets/{reference}/presence | Report presence |
| POST | /support/agent/tickets/{reference}/typing | Report typing status |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Toggle pin on note |

## Admin routes

Requires the `escalated-admin` gate. Admins have all agent routes plus management pages.

| Method | URL | Description |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Analytics dashboard |
| GET | /support/admin/departments | Department management |
| GET | /support/admin/sla-policies | SLA policy management |
| GET | /support/admin/escalation-rules | Escalation rule builder |
| GET | /support/admin/tags | Tag management |
| GET | /support/admin/canned-responses | Canned response templates |
| GET | /support/admin/macros | Macro management |
| GET | /support/admin/custom-fields | Custom fields and forms |
| GET | /support/admin/statuses | Custom statuses |
| GET | /support/admin/business-hours | Business hours schedules |
| GET | /support/admin/roles | Agent roles and permissions |
| GET | /support/admin/audit-log | Audit trail |
| GET | /support/admin/skills | Skills management |
| GET | /support/admin/capacity | Agent capacity controls |
| GET | /support/admin/automations | Time-based automations |
| GET | /support/admin/webhooks | Outbound webhooks |
| GET | /support/admin/webhooks/{webhook}/deliveries | Webhook delivery log |
| GET | /support/admin/kb-articles | Knowledge base articles |
| GET | /support/admin/kb-categories | Knowledge base categories |
| GET | /support/admin/reports/dashboard | Reports dashboard |
| GET | /support/admin/reports/agents | Agent productivity report |
| GET | /support/admin/reports/sla | SLA achievement report |
| GET | /support/admin/reports/csat | CSAT report |
| GET | /support/admin/settings/csat | CSAT survey settings |
| GET | /support/admin/settings/sso | SSO settings |
| GET | /support/admin/settings/two-factor | Two-factor settings |
| GET | /support/admin/settings/data-retention | Data retention settings |
| GET | /support/admin/settings/email | Email channel settings |
| GET | /support/admin/custom-objects | Custom objects |
| GET | /support/admin/custom-objects/{customObject}/records | Custom object records |
| GET | /support/admin/tickets/merge-search | Search merge targets |
| POST | /support/admin/tickets/{reference}/merge | Merge ticket into target |
| GET | /support/admin/tickets/{reference}/links | List linked tickets |
| POST | /support/admin/tickets/{reference}/links | Link related ticket |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Unlink related ticket |
| GET | /support/admin/tickets/{reference}/side-conversations | Side conversations list |
| POST | /support/admin/tickets/{reference}/side-conversations | Start side conversation |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Reply in side conversation |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Close side conversation |
| POST | /support/admin/macros | Create macro |
| PUT | /support/admin/macros/{macro} | Update macro |
| DELETE | /support/admin/macros/{macro} | Delete macro |

## Guest routes

No authentication required. Accessed via unique token.

| Method | URL | Description |
| ------ | --- | ----------- |
| GET | /support/guest/create | Guest ticket form |
| POST | /support/guest | Create guest ticket |
| GET | /support/guest/{token} | View guest ticket |
| POST | /support/guest/{token}/reply | Reply to guest ticket |
| POST | /support/guest/{token}/rate | Submit satisfaction rating |
