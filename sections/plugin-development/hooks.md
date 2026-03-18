# Hooks

Hooks are the primary way plugins interact with Escalated's event system. There are two kinds: **actions** (fire-and-forget) and **filters** (data transformation).

## Actions

Actions are event handlers that run when something happens in Escalated. They are fire-and-forget — the host dispatches the event and does not wait for a meaningful return value. If an action handler throws, the error is logged but does not affect the host.

```typescript
actions: {
  'ticket.created': async (event, ctx) => {
    const settings = await ctx.config.all()
    await ctx.http.post('https://example.com/notify', {
      json: { text: `New ticket: ${event.title}` },
    })
  },
  'ticket.assigned': async (event, ctx) => {
    ctx.log.info('Ticket assigned', { ticketId: event.id, agentId: event.assignee_id })
  },
},
```

**Default timeout:** 30 seconds. If an action handler exceeds this, a warning is logged and the handler is abandoned.

## Filters

Filters intercept data as it flows through Escalated and must return a (possibly modified) value. They are chained sequentially — the output of one plugin's filter feeds into the next.

```typescript
filters: {
  // Shorthand — priority defaults to 10
  'notification.channels': (channels, ctx) => [
    ...channels,
    { id: 'slack', name: 'Slack', icon: 'slack', enabled: true },
  ],

  // Explicit priority — lower runs first
  'ticket.actions': {
    priority: 5,
    handler: (actions, ctx) => [
      ...actions,
      { id: 'create-jira', label: 'Create Jira Issue', icon: 'jira' },
    ],
  },
},
```

### Filter priority and chaining

Filters with lower priority numbers run first (default is 10). When multiple plugins register for the same filter, the output of each feeds into the next:

```
Plugin A (priority 5):  channels = handler(channels)  → [email, slack]
Plugin B (priority 10): channels = handler(channels)  → [email, slack, sms]
Plugin C (priority 20): channels = handler(channels)  → [email, slack, sms, whatsapp]
```

**Default timeout:** 5 seconds. If a filter handler times out, the unmodified value is passed through and a warning is logged.

## Plugin-to-plugin communication

Plugins can emit custom actions that other plugins listen to, enabling cross-plugin workflows:

```typescript
// In the Jira plugin — emit a custom action after creating an issue
actions: {
  'ticket.created': async (event, ctx) => {
    const issue = await createJiraIssue(event)
    // Emit a custom action — other plugins can listen
    await ctx.emit('jira.issue.created', { ticketId: event.id, issueKey: issue.key })
  },
},

// In the Slack plugin — listen to Jira's custom action
actions: {
  'jira.issue.created': async (event, ctx) => {
    await postToSlack(`Jira issue ${event.issueKey} linked to ticket ${event.ticketId}`)
  },
},
```

Custom hooks must be namespaced with the plugin name prefix (e.g., `jira.*`, `slack.*`). The runtime routes `ctx.emit()` calls to all plugins that have registered a handler for that hook.

## Available hooks

### Action hooks

| Hook | Event data | Description |
|------|-----------|-------------|
| `ticket.created` | `{ id, title, status, priority, contact_id, department_id }` | New ticket submitted |
| `ticket.assigned` | `{ id, assignee_id, previous_assignee_id }` | Agent assigned or reassigned |
| `ticket.status_changed` | `{ id, status, previous_status }` | Status transition |
| `ticket.priority_changed` | `{ id, priority, previous_priority }` | Priority updated |
| `ticket.resolved` | `{ id, resolved_at }` | Ticket marked resolved |
| `ticket.closed` | `{ id, closed_at }` | Ticket closed |
| `ticket.reopened` | `{ id }` | Ticket moved back to active state |
| `reply.created` | `{ id, ticket_id, author_id, body, is_private }` | Reply or internal note added |
| `ticket.escalated` | `{ id, rule_id }` | Ticket escalated by automation rule |
| `sla.warning` | `{ ticket_id, policy_id, deadline }` | Ticket approaching SLA deadline |
| `sla.breached` | `{ ticket_id, policy_id, breached_at }` | SLA deadline missed |

### Filter hooks

| Hook | Value type | Description |
|------|-----------|-------------|
| `notification.channels` | `Channel[]` | Notification channel list (email, SMS, etc.) |
| `ticket.actions` | `Action[]` | Action buttons in the ticket view |
| `ticket.sidebar_tabs` | `Tab[]` | Tabs shown in the ticket sidebar |
| `dashboard.widgets` | `Widget[]` | Available dashboard widgets |
| `reply.body` | `string` | Reply body before sending (e.g., append signatures) |
