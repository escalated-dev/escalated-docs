# REST API

Escalated includes a full REST API for programmatic access to tickets, agents, departments, and more.

## Authentication

All API requests require a Bearer token in the `Authorization` header:

```
Authorization: Bearer your-api-token
```

Tokens are created in the admin panel under **API Tokens**. Each token has:

- **Name** — descriptive label
- **Abilities** — granular permissions (e.g. `tickets:read`, `tickets:write`)
- **Expiration** — optional expiry date

### Validate a token

```
POST /auth/validate
```

Returns the token owner's info, abilities, and role.

## Base URL

All endpoints are prefixed with your configured API prefix (default: `/support/api/v1`).

## Endpoints

### Dashboard

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/dashboard` | Agent dashboard stats (open, assigned, unassigned, SLA breached, resolved today) |

### Tickets

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/tickets` | List tickets (paginated, filterable) |
| `POST` | `/tickets/create` | Create a new ticket |
| `GET` | `/tickets/{reference}` | Ticket detail with replies and activities |
| `POST` | `/tickets/{reference}/reply` | Add reply or internal note |
| `PATCH` | `/tickets/{reference}/status` | Change ticket status |
| `PATCH` | `/tickets/{reference}/priority` | Change ticket priority |
| `POST` | `/tickets/{reference}/assign` | Assign to agent |
| `POST` | `/tickets/{reference}/follow` | Toggle follow/unfollow |
| `POST` | `/tickets/{reference}/macro` | Apply a macro |
| `POST` | `/tickets/{reference}/tags` | Sync tags |
| `DELETE` | `/tickets/{reference}` | Delete ticket |

### Resources (read-only)

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/agents` | List all agents |
| `GET` | `/departments` | List active departments |
| `GET` | `/tags` | List all tags |
| `GET` | `/canned-responses` | List available canned responses |
| `GET` | `/macros` | List available macros |
| `GET` | `/realtime/config` | WebSocket/realtime configuration |

### Admin: API Tokens

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/admin/api-tokens` | List tokens |
| `POST` | `/admin/api-tokens/create` | Create token |
| `PATCH` | `/admin/api-tokens/{id}/update` | Update token |
| `DELETE` | `/admin/api-tokens/{id}/delete` | Delete token |

## Filtering & Pagination

### Ticket list query parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `status` | string | Filter by status (`open`, `in_progress`, `resolved`, etc.) |
| `priority` | string | Filter by priority (`low`, `medium`, `high`, `urgent`, `critical`) |
| `department_id` | integer | Filter by department |
| `assigned_to` | integer | Filter by assigned agent ID |
| `unassigned` | boolean | `1` or `true` for unassigned only |
| `ticket_type` | string | Filter by type (`question`, `problem`, `incident`, `task`) |
| `search` | string | Search subject, description, and reference |
| `sla_breached` | boolean | `1` or `true` for SLA-breached only |
| `following` | boolean | `1` or `true` for tickets you follow |
| `sort_by` | string | Sort field: `created_at`, `updated_at`, `priority`, `status`, `subject` |
| `sort_dir` | string | `asc` or `desc` (default: `desc`) |
| `per_page` | integer | Results per page, max 100 (default: 25) |
| `page` | integer | Page number (default: 1) |

## Response Format

All responses follow the same envelope:

```json
{
  "data": { ... },
  "meta": {
    "current_page": 1,
    "last_page": 5,
    "per_page": 25,
    "total": 100
  },
  "message": "Ticket created."
}
```

### Error responses

```json
{
  "message": "Validation failed.",
  "errors": {
    "subject": "Subject is required."
  }
}
```

| Status | Meaning |
|--------|---------|
| `200` | Success |
| `201` | Created |
| `400` | Bad request (invalid JSON) |
| `401` | Unauthorized (missing/invalid token) |
| `403` | Forbidden (insufficient abilities) |
| `404` | Not found |
| `422` | Validation failed |
| `429` | Rate limited |

## Rate Limiting

API requests are rate-limited per token (default: 60 requests per minute). Rate limit headers are included in every response:

```
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 58
```

When exceeded, a `429` response is returned with a `Retry-After` header.
