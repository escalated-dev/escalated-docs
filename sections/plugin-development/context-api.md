# Context API

Every hook handler, endpoint, webhook, and cron task receives a `ctx` (PluginContext) object. When running in subprocess mode, `ctx.*` calls are translated to JSON-RPC requests back to the host framework. When running on AdonisJS (in-process mode), they call the native ORM directly. The interface is identical in both modes.

## ctx.config

Reads and writes the plugin's configuration, as defined in the `config` array and managed through the Admin UI.

```typescript
// Read all config values
const settings = await ctx.config.all()
// → { bot_token: 'xoxb-...', channel: '#support' }

// Read a single key
const token = await ctx.config.get('bot_token')

// Write one or more values (merges with existing config)
await ctx.config.set({ channel: '#general', enabled: true })
```

Configuration is stored as JSON per plugin in the host database and is scoped to the plugin.

## ctx.store

Plugin-scoped key-value document store for persistent plugin state (e.g., Jira issue links, message queues, audit logs). Backed by a single `escalated_plugin_store` table across all plugins, indexed on `(plugin, collection, key)`.

```typescript
// Insert a record (auto-generated key)
const link = await ctx.store.insert('jira_links', {
  ticket_id: 123,
  issue_key: 'PROJ-456',
  created_at: new Date().toISOString(),
})

// Read by key
const link = await ctx.store.get('jira_links', '507f1f77bcf86cd799439011')

// Update by key
await ctx.store.update('jira_links', link.id, { synced: true })

// Delete by key
await ctx.store.delete('jira_links', link.id)

// Query with filters
const links = await ctx.store.query('jira_links', { ticket_id: 123 })

// Query with operators and ordering
const recent = await ctx.store.query(
  'audit_log',
  { created_at: { $gt: '2025-01-01' } },
  { limit: 100, orderBy: 'created_at', order: 'desc' }
)
```

**Supported filter operators:** `$gt`, `$gte`, `$lt`, `$lte`, `$ne`, `$in`, `$nin`. Equality filters use plain values (no operator prefix).

The bridge translates filters into native JSON column queries for MySQL, PostgreSQL, and SQLite.

## ctx.http

Outbound HTTP client for calling external APIs. Runs in-process inside the plugin (not proxied via JSON-RPC). Wraps `fetch()` with retry, timeout, and structured error handling.

```typescript
// GET request
const res = await ctx.http.get('https://api.example.com/data', {
  headers: { Authorization: `Bearer ${token}` },
})

// POST with JSON body
const res = await ctx.http.post('https://slack.com/api/chat.postMessage', {
  headers: { Authorization: `Bearer ${botToken}` },
  json: { channel: '#support', text: 'Hello from Escalated' },
})

// PUT and DELETE
await ctx.http.put('https://api.example.com/resource/1', { json: { status: 'done' } })
await ctx.http.delete('https://api.example.com/resource/1')
```

The host has no visibility into outbound HTTP calls — plugins make external API calls directly.

## ctx.broadcast

Real-time broadcast to connected clients via the host WebSocket infrastructure (Laravel Echo, etc.).

```typescript
// Broadcast to a named channel
await ctx.broadcast.toChannel('slack-activity', 'new-message', { text: 'Hello', ts: '...' })

// Broadcast to a specific user
await ctx.broadcast.toUser(userId, 'plugin.notification', { message: 'Sync complete' })

// Broadcast to all users watching a ticket
await ctx.broadcast.toTicket(ticketId, 'jira.linked', { issueKey: 'PROJ-123' })
```

## ctx.log

Structured logging that writes to the host's log system (Laravel Log, Python logging, Rails logger, etc.).

```typescript
ctx.log.info('Notification sent', { channel: '#support', ts: '1234567890.123' })
ctx.log.warn('Rate limit approaching', { remaining: 10, resetAt: '...' })
ctx.log.error('Delivery failed', { error: err.message, attempt: 3 })
ctx.log.debug('Raw payload', { body: req.body })
```

## ctx.emit

Emit a custom action for plugin-to-plugin communication. The runtime routes the event to all plugins that have registered an action handler for the given hook name.

```typescript
await ctx.emit('jira.issue.created', { ticketId: event.id, issueKey: 'PROJ-123' })
```

Custom hook names must be namespaced with the emitting plugin's name (e.g., `jira.*`).

## ctx.currentUser

Returns the authenticated Escalated user in the current request context, or `null` in webhook handlers and cron tasks.

```typescript
const user = await ctx.currentUser()
if (user) {
  ctx.log.info(`Request from agent ${user.id}`)
}
```

## Data repositories

These repositories proxy to the host ORM via JSON-RPC (or direct ORM calls on AdonisJS).

### ctx.tickets

```typescript
const ticket = await ctx.tickets.find(123)
const open = await ctx.tickets.query({ status: 'open', department_id: 5 })
const ticket = await ctx.tickets.create({ title: 'Help needed', contact_id: 42 })
await ctx.tickets.update(123, { status: 'resolved' })
```

### ctx.replies

```typescript
const reply = await ctx.replies.find(456)
const replies = await ctx.replies.query({ ticket_id: 123 })
await ctx.replies.create({ ticket_id: 123, body: 'Thanks for reaching out!', is_private: false })
```

### ctx.contacts

```typescript
const contact = await ctx.contacts.find(42)
const contact = await ctx.contacts.findByEmail('user@example.com')
const contact = await ctx.contacts.create({ name: 'Jane Doe', email: 'jane@example.com' })
```

### ctx.tags

```typescript
const all = await ctx.tags.all()
const tag = await ctx.tags.create({ name: 'billing' })
```

### ctx.departments

```typescript
const all = await ctx.departments.all()
const dept = await ctx.departments.find(3)
```

### ctx.agents

```typescript
const all = await ctx.agents.all()
const agent = await ctx.agents.find(7)
```

## Timeouts

All `ctx.*` calls have a 10-second default timeout. If the host does not respond in time, the promise rejects with a `TimeoutError`. Design your handlers to fail gracefully when context calls time out.
