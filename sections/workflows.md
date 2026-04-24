# Workflows

Workflows are event-driven automation rules that run in response to ticket lifecycle events (new ticket, status change, SLA breach, inbound reply, etc.). Unlike [automations](automations.md), which run on a recurring scheduler, workflows fire **the moment the triggering event happens** -- an agent assigning a ticket, a customer replying, an SLA tipping over.

Use workflows when you want reactive side effects. Use automations when you want periodic sweeps of the ticket database.

## How workflows work

Every workflow has three parts:

1. **Trigger event** -- the event that starts evaluation (e.g. `ticket.created`, `reply.created`, `sla.breached`).
2. **Conditions** -- a filter evaluated on the ticket when the event fires. All conditions must match (AND logic).
3. **Actions** -- the side effects applied when conditions match. Actions run in order; a failure in one does not abort the rest (the error is logged to the workflow run history).

When an event fires, Escalated dispatches it to the workflow engine, which looks up every active workflow subscribed to that event, evaluates conditions against the current ticket state, and executes each matched workflow's actions. The run is recorded in the workflow log for auditability.

## Trigger events

| Event | Fires when |
|---|---|
| `ticket.created` | A new ticket is created (via API, inbound email, widget, or agent UI) |
| `ticket.updated` | Any field on the ticket changes |
| `ticket.assigned` | The `assignee_id` changes |
| `ticket.status_changed` | The ticket status transitions (e.g. `open -> solved`) |
| `reply.created` | Any reply is added (agent or customer) |

A workflow subscribes to exactly one trigger event. For rules that should react to multiple events, define a workflow per event.

Fine-grained event subtypes (priority changed, tagged, reopened, SLA warnings, inbound received, signup invites) all fire on the Escalated event bus too, but today they are not bridged into the Workflow runner — they are consumed by the built-in email + activity-log listeners instead. Use the five events above combined with per-field conditions to approximate per-subtype behavior.

## Conditions

A condition is a `{ field, operator, value }` triple. `field` names any top-level ticket column (framework-specific column names apply — see [Template variables](#template-variables) for the naming convention on your framework). The engine looks up `ticket[field]`, coerces to string, and applies `operator` against `value`.

**Operators:**

| Operator | Meaning |
|---|---|
| `equals` / `not_equals` | String equality |
| `contains` / `not_contains` | Substring match (case-sensitive) |
| `starts_with` / `ends_with` | String prefix / suffix |
| `greater_than` / `less_than` | Numeric comparison (value coerced via `Number()`) |
| `greater_or_equal` / `less_or_equal` | Numeric comparison |
| `is_empty` / `is_not_empty` | Trim + length check (value arg ignored) |

**Example:** to match open tickets from VIPs, combine two conditions:

```json
{
  "all": [
    { "field": "status",             "operator": "equals",   "value": "open" },
    { "field": "requesterEmail",     "operator": "ends_with", "value": "@vip.example.com" }
  ]
}
```

Conditions combine via `all` (AND) or `any` (OR); a bare array is treated as `all`. If you need disjoint OR-semantics across multiple triggers, define separate workflows on the same trigger with different condition sets.

> **Note:** Conditions operate on whatever scalar fields the framework's ticket schema exposes. Relationship-based filters (has_tag, in_department_name, requester_email_matches_pattern) aren't built in — use a `ticket_type`-style discriminator column or write a pre-filter workflow that tags the ticket, then filter by tag downstream.

## Actions

Workflows can perform any of the following actions. Actions execute in the order they are declared:

| Action | Purpose |
|---|---|
| `change_priority` | Set the ticket priority |
| `change_status` | Set the ticket status (accepts status slug or numeric id) |
| `set_department` | Move the ticket to a department |
| `add_tag` | Attach a tag (by slug or id); no-op if already present |
| `remove_tag` | Detach a tag; no-op if not present |
| `assign_agent` | Assign to a specific agent by id, writing a ticket-activity audit row |
| `assign_round_robin` | Assign to the least-loaded active agent in a department (see below) |
| `add_note` | Add an internal note visible only to agents |
| `insert_canned_reply` | Add a public reply with `{{field}}` template interpolation |
| `add_follower` | Add a user as a ticket follower (idempotent) |
| `send_webhook` | POST a JSON payload to a configured webhook |
| `delay` | Pause the workflow and resume remaining actions after N seconds (see below) |

### Template variables

`insert_canned_reply` supports `{{variable}}` interpolation against the ticket. The engine flattens every top-level scalar column on the ticket row into the template context, so the variable names follow your framework's column naming convention.

For the NestJS reference (camelCase):

- `{{subject}}`, `{{description}}`, `{{priority}}`, `{{channel}}`
- `{{referenceNumber}}`, `{{id}}`
- `{{requesterId}}`, `{{contactId}}`, `{{assigneeId}}`, `{{departmentId}}`, `{{statusId}}`

Frameworks whose columns are snake_case (Laravel, Rails, Django, WordPress, Symfony, Phoenix) expose the same fields under snake_case names — e.g. `{{reference_number}}`, `{{requester_id}}`. Check your framework's ticket schema for the exact list.

Non-scalar relationships (the loaded `Tag[]` array, nested `Department`, etc.) are skipped — reach for a workflow hook or a dedicated action if you need to interpolate relation data.

Unknown variable names are left as literal `{{name}}` in the output so gaps are visible in the rendered reply rather than silently disappearing.

### Round-robin assignment

`assign_round_robin` takes a department id as its `value` and picks the **least-loaded active + available agent** in that department — the one with the fewest currently-open tickets assigned to them. This favors the agent most likely to be idle rather than rotating strictly. If two agents tie on open-ticket count, the one with the lower user id wins for determinism. Ineligible inputs (non-numeric or zero department id, empty eligible-agent list) log a warning and skip without assigning.

### Delayed actions

The `delay` action splits a workflow run into two halves. Actions before the delay run inline. Remaining actions are persisted to a deferred-job queue with `run_at = now + N` and picked up by a scheduled poller (runs once per minute by default) after the wait elapses.

**`N` units differ by framework.** NestJS, Spring, and WordPress interpret `delay.value` as **seconds**; Laravel, Rails, Django, Adonis, .NET, Go, Phoenix, and Symfony interpret it as **minutes** (matching the pre-existing `delayed_actions` schema those plugins had before this rollout). Check your plugin's workflow-executor source if you're unsure.

Example: "When a ticket is created by a caller from an urgent priority, tag it, wait 5 minutes, then leave a note to page on-call."

```json
{
  "trigger_event": "ticket.created",
  "conditions": [
    { "field": "priority", "operator": "equals", "value": "urgent" }
  ],
  "actions": [
    { "type": "add_tag",  "value": "needs-fast-response" },
    { "type": "delay",    "value": "300" },
    { "type": "add_note", "value": "Still open after 5 min -- page on-call." }
  ]
}
```

> `"value": "300"` is 5 minutes on the seconds-unit frameworks (NestJS / Spring / WordPress). On the minutes-unit frameworks you'd write `"value": "5"` for the same behavior.

The first two actions happen immediately. If the ticket is still open 5 minutes later, the note is added; if the ticket was already closed in the meantime, the note still fires (the delay does not re-evaluate conditions -- it resumes the saved action sequence verbatim). To make conditional resume-time behavior, fan out to a separate workflow trigger.

The deferred-job queue retains rows after completion (status flips from `pending` to `done` or `failed`) so you can audit when and why each delay fired.

## Webhook action

`send_webhook` takes a webhook id (the numeric id of a row you've configured under `Admin -> Webhooks`) and POSTs a payload to that webhook's configured URL. The HTTP body:

```json
{
  "event": "workflow.triggered",
  "data": {
    "ticket": { "id": 1234, "subject": "...", "priority": "high", ... }
  },
  "timestamp": "2026-04-24T14:00:00.000Z"
}
```

The full ticket entity is passed through as `data.ticket` — relationships present on the in-memory entity at dispatch time (tags, department) are included. Delivery follows the same HMAC-SHA256 signing + retry rules as every other Escalated webhook: the `X-Escalated-Signature` header carries `sha256=<hex>` of the payload body signed with the webhook's configured secret. Delivery failures are recorded on `WebhookDelivery` for the retry scheduler to pick up; they do not block subsequent actions in the same workflow.

## Example workflows

### Auto-tag and assign high-priority VIP tickets

```json
{
  "trigger_event": "ticket.created",
  "conditions": {
    "all": [
      { "field": "requesterEmail", "operator": "ends_with", "value": "@vip.example.com" }
    ]
  },
  "actions": [
    { "type": "change_priority",      "value": "urgent" },
    { "type": "add_tag",              "value": "vip" },
    { "type": "assign_round_robin",   "value": "7" },
    { "type": "send_webhook",         "value": "9" }
  ]
}
```

### Chase stale tickets

```json
{
  "trigger_event": "ticket.status_changed",
  "conditions": [
    { "field": "status", "operator": "equals", "value": "pending" }
  ],
  "actions": [
    { "type": "delay", "value": "86400" },
    { "type": "add_note", "value": "Pending > 24h. Consider following up." }
  ]
}
```

> `"value": "86400"` is 24h on the seconds-unit frameworks; on minutes-unit frameworks use `"value": "1440"`.

### Triage by subject

```json
{
  "trigger_event": "ticket.created",
  "conditions": [
    { "field": "subject", "operator": "contains", "value": "refund" }
  ],
  "actions": [
    { "type": "set_department",        "value": "5" },
    { "type": "add_tag",               "value": "refund-request" },
    { "type": "insert_canned_reply",
      "value": "Hi, we've received your refund request (#{{referenceNumber}}) and will respond within 1 business day." }
  ]
}
```

The canned-reply template uses `{{referenceNumber}}` because the NestJS reference stores ticket reference as a camelCase scalar column. Frameworks with snake_case columns would use `{{reference_number}}`. There is no `{{requester_name}}` variable — contact name is a separate related row that the interpolator doesn't traverse.

## Workflow logs

Every workflow *considered* -- match or no match -- writes a row to `escalated_workflow_logs`, surfaced in the UI at `Admin -> Workflows -> Logs`. Each row records:

- Trigger event string, triggering ticket id (FK), workflow id (FK)
- `conditions_matched` boolean — whether the workflow actually fired
- `actions_executed_raw` JSON — the actions array as stored on the workflow when it fired (not per-action status; re-read the workflow to see current config)
- `error_message` — top-level error from the executor if the whole run threw, else null. Individual action failures within the executor are log-warn and do NOT surface here
- `started_at` / `completed_at` timestamps so you can derive duration

Deferred (`delay`) actions do not get their own log row — inspect `escalated_deferred_workflow_jobs` directly (status + last_error columns) to audit what fired when.

## Managing workflows

Admins create and edit workflows at `Admin -> Workflows`. The UI mirrors the macro builder: pick a trigger, add conditions, add actions, reorder as needed. Workflows can be toggled inactive without deleting them.

## Scheduler dependency

The `delay` action and any other deferred behaviors depend on the application scheduler being live. See [Scheduling](scheduling.md) for how to enable the cron or queue worker your framework uses. If the scheduler is not running, delayed actions will sit in `pending` indefinitely.

## Automations vs. workflows -- when to use which

| Use case | Choice |
|---|---|
| "When a ticket is created, do X" | Workflow (`ticket.created`) |
| "Every 15 minutes, check all pending tickets and close > 7 days" | Automation |
| "When an agent replies, send a webhook" | Workflow (`reply.created` with a condition filtering out customer-authored replies) |
| "Nightly: add the `stale` tag to tickets idle > 72h" | Automation |
| "When a VIP submits, wait 5 min then escalate if still open" | Workflow (`ticket.created` + `delay`) |

Workflows are reactive and surgical. Automations are periodic and sweeping. Both can coexist on the same ticket; they read and write the same tables.
