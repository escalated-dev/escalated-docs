# Workflows

Workflows are event-driven automation rules that run in response to ticket lifecycle events (ticket creation, updates, assignment, status changes, and replies). Unlike [automations](automations.md), which run on a recurring scheduler, workflows fire **the moment the triggering event happens** when a supported ticket event is dispatched.

Use workflows when you want reactive side effects. Use automations when you want periodic sweeps of the ticket database.

## How workflows work

Every workflow has three parts:

1. **Trigger event** -- the event that starts evaluation (e.g. `ticket.created` or `reply.created`).
2. **Conditions** -- a filter evaluated on the ticket when the event fires. Conditions can be grouped with `all` (AND) or `any` (OR).
3. **Actions** -- the side effects applied when conditions match. Actions run in order; error handling and log detail depend on the backend executor.

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

A condition is a `{field, operator, value}` triple. The canonical admin contract includes `status`, `priority`, `ticket_type`, `channel`, `subject`, `description`, `tags`, `department_id`, `assigned_to`, `hours_since_created`, and `hours_since_updated`. A backend may advertise additional fields.

**Operators:**

| Operator | Meaning |
|---|---|
| `equals` / `not_equals` | String equality |
| `contains` / `not_contains` | Substring match (case-sensitive) |
| `starts_with` / `ends_with` | String prefix / suffix |
| `greater_than` / `less_than` | Numeric comparison (value coerced via `Number()`) |
| `greater_or_equal` / `less_or_equal` | Numeric comparison |
| `is_empty` / `is_not_empty` | Trim + length check (value arg ignored) |

**Example:** to match high-priority tickets mentioning "refund" in the subject:

```json
{
  "all": [
    { "field": "priority", "operator": "equals",   "value": "urgent" },
    { "field": "subject",  "operator": "contains", "value": "refund" }
  ]
}
```

Conditions combine via `all` (AND) or `any` (OR); a bare array is treated as `all`. If you need disjoint OR-semantics, define separate workflows on the same trigger with different condition sets.

## Actions

The core action catalog includes priority, status, department, tag, assignment, note, and canned-reply changes. The table below also lists deferred actions from the NestJS reference implementation; confirm them in your backend executor before using them. Actions execute in declaration order:

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
| `send_webhook` | Optional: send to a URL, when advertised by the backend |
| `delay` | Optional: defer remaining actions by a number of minutes |

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

The canonical admin contract defines `delay.value` in minutes. Delayed actions are optional: use them only when your backend advertises `delay` in its action types. Run the required scheduler before enabling a delayed rule.

## Webhook action

The canonical admin contract defines `send_webhook.value` as a URL. This action is optional and should only appear when the backend advertises it. Configure and test the backend's URL validation, delivery, signing, and retry behavior before connecting an external receiver.

## Example workflows

### Auto-tag and route billing tickets

```json
{
  "trigger_event": "ticket.created",
  "conditions": {
    "all": [
      { "field": "subject", "operator": "contains", "value": "billing" }
    ]
  },
  "actions": [
    { "type": "change_priority",      "value": "high" },
    { "type": "add_tag",              "value": "billing" },
    { "type": "assign_agent",         "value": "7" },
    { "type": "send_webhook",         "value": "https://example.com/support-events" }
  ]
}
```

The optional assignment and webhook actions in this example require support in the installed backend. The assignment value identifies a host agent.

### Chase stale tickets

```json
{
  "trigger_event": "ticket.status_changed",
  "conditions": [
    { "field": "status", "operator": "equals", "value": "pending" }
  ],
  "actions": [
    { "type": "delay", "value": "1440" },
    { "type": "add_note", "value": "Pending > 24h. Consider following up." }
  ]
}
```

`1440` minutes is 24 hours. A delayed action resumes saved work; use a time-based automation when the ticket must still match conditions at execution time.

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

In the NestJS reference implementation, every workflow *considered* -- match or no match -- writes a row to `escalated_workflow_logs`, surfaced in the UI at `Admin -> Workflows -> Logs`. Each row records:

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
| "When *any* reply is added, send a webhook" | Workflow (`reply.created`) — note the event fires with the TICKET as payload, not the reply, so you can't filter by `author_type` in conditions; the webhook receives the ticket and your downstream handler decides |
| "Nightly: add the `stale` tag to tickets idle > 72h" | Automation |
| "When a high-priority ticket is created, wait 5 min then leave an escalation note" | Workflow (`ticket.created` + priority condition + `delay`) |

Workflows are reactive and surgical. Automations are periodic and sweeping. Both can coexist on the same ticket; they read and write the same tables.
