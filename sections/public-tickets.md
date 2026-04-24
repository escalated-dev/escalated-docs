# Public Tickets

The public ticket system lets unauthenticated users submit tickets without a host-app account. Two entry points share the same pipeline:

- **Embeddable widget** (`POST /escalated/widget/tickets`) — a support button you drop into marketing pages.
- **Inbound email** (`POST /escalated/webhook/email/inbound`) — a Postmark/Mailgun/SES webhook that routes messages to the right ticket.

Both paths look up or create a `Contact` by email, so repeat submissions from the same address are deduplicated. Once a contact exists, they can reply to confirmation emails and those replies thread back into the same conversation via RFC 5322 `Message-ID` + a signed `Reply-To` address.

## Guest policy

The **guest policy** decides which identity a public ticket is attributed to. Three modes, all runtime-switchable from the admin settings page:

| Mode | `ticket.requester_id` | `ticket.contact_id` | Behavior |
|---|---|---|---|
| `unassigned` (default) | `0` | set | Ticket has no authenticated requester. Agents see the guest email on the Contact row. |
| `guest_user` | configured shared user id | set | Every public ticket is owned by one pre-created host-app user (typical: `guest@yourcompany.com`). Lets existing authorization rules treat guests uniformly. |
| `prompt_signup` | `0` (until promoted) | set | Same as `unassigned`, plus a signup-invite email goes out with the confirmation. If the guest accepts, `ContactService.promoteToUser` back-stamps `requester_id` on all prior tickets with that `contact_id`. |

The policy is global — it applies to every public submission. Host apps that need per-department or per-rule routing should combine it with a Workflow that reassigns the ticket after creation.

## Configuration

### Boot-time defaults

Every host-framework plugin accepts a compile-time default in its configuration block (the exact syntax varies per framework — see each plugin's README or the [installation](installation.md) page).

```json
{
  "guest_policy": {
    "mode": "unassigned",
    "guest_user_id": null,
    "signup_url_template": null
  }
}
```

### Runtime switching (admin settings page)

Every host-framework plugin ships an admin page at `Admin → Settings → Public tickets` that writes to the plugin's settings table. The runtime value overrides the compile-time default.

Under the hood, the page calls:

```
GET  /escalated/admin/settings/public-tickets
PUT  /escalated/admin/settings/public-tickets
```

with JSON body (all fields snake_case to match the wire format):

```json
{
  "guest_policy_mode": "guest_user",
  "guest_policy_user_id": 42,
  "guest_policy_signup_url_template": "https://app.example.com/signup?email={{email}}"
}
```

Validation the API performs for you:

- Unknown `guest_policy_mode` values coerce silently to `unassigned` — the endpoint never 500s on a bad mode.
- Switching mode clears the other mode's fields so stale values (e.g. a leftover `guest_user_id` from an earlier `guest_user` run) don't leak into `prompt_signup` behavior.
- `guest_policy_user_id` ≤ 0 or non-numeric is stored as empty; GET surfaces that as JSON `null`.
- `guest_policy_signup_url_template` is trimmed and truncated to 500 characters.

### Template variable in signup URL

When `mode = prompt_signup`, the `guest_policy_signup_url_template` supports a single `{token}` placeholder (single braces) that Escalated replaces with a URL-encoded, HMAC-scoped signup token derived from the contact's id and your configured `inbound.webhookSecret`. A typical template:

```
https://app.example.com/signup?from_ticket={token}
```

The token is one-time use and lets your host app identify the originating `Contact` when the user completes signup. Your app verifies the token by round-tripping it through the same secret that signs Reply-To addresses.

## Widget submission

Place the widget snippet on any page. Config is read from `data-*` attributes on the script tag (or from a `window.EscalatedWidget` object set before the script loads):

```html
<script src="https://yourhost.example/escalated-widget.js"
        data-base-url="https://yourhost.example"
        data-color="#4F46E5"
        data-position="bottom-right"
        async></script>
```

Only `data-base-url` is required; `data-color` (hex, defaults to indigo `#4F46E5`) and `data-position` (`bottom-right` | `bottom-left`, defaults to `bottom-right`) are optional. The widget mounts itself into a shadow-DOM host so host-app CSS can't leak in.

On open, the widget optionally fetches `/support/widget/config` (host-framework-dependent — some plugins implement this to serve admin-configured branding overrides, others fall back to the `data-*` attributes) and renders a ticket form collecting `email` (required), `name` (optional), `subject`, `description`, and an optional `priority`. On submit it POSTs to the host framework's widget tickets endpoint (`/escalated/widget/tickets` on NestJS; `/support/widget/tickets` on Laravel/Rails/Django/etc.).

Per-email rate limit: 10 submissions per hour, enforced by `PublicSubmitThrottleGuard`. Requests exceeding the limit get a `429` and no ticket is created.

> **Deployment note:** The shipped guard keeps its counter in-memory, which is fine for single-instance deployments and tests but lets the limit leak under horizontal scale-out. For multi-instance production, swap the backing store for Redis (or your framework's equivalent shared cache). The guard is a pluggable class — override it when you bind the Escalated module.

## Inbound email

Point your transactional mail provider's inbound webhook at `/escalated/webhook/email/inbound`. The plugin supports three providers natively: **Postmark**, **Mailgun**, and **AWS SES** (via SNS HTTP subscription). See [Inbound Email](inbound-email.md) for per-framework setup details.

The inbound router resolves the target ticket in this order:

1. **`In-Reply-To` header** → ticket id parsed from our outbound `Message-ID`
2. **`References` header** → same parse, walks the whole chain for clients that drop `In-Reply-To`
3. **Envelope `To`** → matches our signed `Reply-To` address `reply+{id}.{hmac8}@{domain}` (HMAC-SHA256, timing-safe compare)
4. **Subject line** → contains a `[TK-XXX]` ticket reference

If none match, the router resolves/creates a `Contact` by sender email and creates a new ticket under the current guest policy.

## Workflow integration

Public-submission events fire the same `ticket.created` and `reply.created` events as authenticated flows, so [Workflows](workflows.md) you configure will automatically fire against them. Common use cases:

- **Auto-tag all public tickets** with a `from-widget` or `from-email` tag so agents can filter the queue
- **Assign public tickets to a specific department** (e.g. Billing) when the subject contains keywords
- **Delay auto-close** — close tickets after 7 days of no response using a `delay` action on `reply.created`

See the [Workflows](workflows.md) page for the full action catalog and decision table.

## Promoting a guest to a real user

When a guest accepts a signup invite (only fires under `prompt_signup` mode), the host app calls:

```
ContactService.promoteToUser(contactId, userId)
```

That single call:

1. Sets `contact.user_id = userId` on the Contact row
2. Back-stamps every ticket carrying that `contact_id` with `requester_id = userId`

After promotion, the former guest logs in and sees their full public-ticket history as if they'd been authenticated the whole time.

## Data model

Two key relationships:

- `escalated_contacts.id` (unique email index, case-insensitive) ← `escalated_tickets.contact_id` (nullable FK)
- `escalated_contacts.user_id` (nullable host-app user FK) — set post-promotion

Existing host-app users submitting via the widget: the widget controller resolves a `Contact` for them but also fills `ticket.requester_id` with their host-app user id, so both paths work.
