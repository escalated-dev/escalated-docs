# Routes

Escalated registers three groups of routes under the configured prefix (default: `/support`).

## Customer routes

| Method | URL | Description |
| ------ | --- | ----------- |
| GET | /support | Customer ticket list |
| GET | /support/create | New ticket form |
| POST | /support | Create ticket |
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
| POST | /support/agent/tickets/{reference}/{reply}/pin | Toggle pin on note |

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
| POST | /support/admin/macros | Create macro |
| PUT | /support/admin/macros/{macro} | Update macro |
| DELETE | /support/admin/macros/{macro} | Delete macro |

## Guest routes

No authentication required. Accessed via unique token.

| Method | URL | Description |
| ------ | --- | ----------- |
| GET | /support/guest/{token} | View guest ticket |
| POST | /support/guest/{token}/reply | Reply to guest ticket |
| POST | /support/guest/{token}/rate | Submit satisfaction rating |
