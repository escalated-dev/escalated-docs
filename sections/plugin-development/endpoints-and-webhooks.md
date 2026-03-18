# Endpoints, Webhooks & Cron

## Data endpoints

Endpoints expose JSON API routes that your plugin's Vue pages call to fetch or update data. They are declared in the `endpoints` map using `METHOD /path` keys. The bridge mounts them at `/api/plugins/{slug}{path}`.

```typescript
endpoints: {
  'GET /settings': {
    capability: 'manage_settings',  // Optional access control
    handler: async (ctx) => {
      return await ctx.config.all()
    },
  },
  'PUT /settings': {
    capability: 'manage_settings',
    handler: async (ctx, req) => {
      await ctx.config.set(req.body)
      return { success: true }
    },
  },
  'GET /stats': {
    capability: 'escalated-agent',
    handler: async (ctx, req) => {
      const messages = await ctx.store.query('messages', { status: 'pending' })
      return { pending: messages.length }
    },
  },
},
```

The `req` object contains `body`, `params` (URL path parameters), `query` (query string), and `headers`.

**Default timeout:** 30 seconds. Exceeding this returns a 504 to the client.

## Webhook handlers

Webhooks receive inbound HTTP requests from external services. Unlike endpoints, webhooks are public routes — no Escalated authentication is required. Signature verification is the plugin's responsibility within the handler.

Webhook routes are mounted at `/webhooks/plugins/{slug}{path}`.

```typescript
webhooks: {
  'POST /events': async (ctx, req) => {
    // Verify Slack signature
    const signature = req.headers['x-slack-signature']
    if (!verifySlackSignature(signature, req.body)) {
      return { error: 'Invalid signature' }  // Bridge returns 401
    }

    const payload = req.body
    if (payload.type === 'url_verification') {
      // Respond to Slack's challenge during webhook setup
      return { challenge: payload.challenge }
    }

    // Handle the event asynchronously
    if (payload.event?.type === 'message') {
      await ctx.store.insert('slack_messages', {
        channel: payload.event.channel,
        text: payload.event.text,
        ts: payload.event.ts,
        read: false,
      })
    }

    return { ok: true }
  },
  'POST /interactions': async (ctx, req) => {
    // Handle Slack interactive components
    const interaction = JSON.parse(req.body.payload)
    // ...
  },
},
```

**Default timeout:** 60 seconds. Exceeding this returns a 504 to the external caller.

## Cron schedules

Cron tasks run on a schedule managed by the bridge. Use the `every:` prefix with a duration unit:

```typescript
cron: {
  'every:1h': async (ctx) => {
    // Runs every hour — sync data, send digests, clean up state, etc.
    const pending = await ctx.store.query('messages', { status: { $in: ['pending', 'failed'] } })
    for (const msg of pending) {
      await retryDelivery(msg, ctx)
    }
  },
  'every:1d': async (ctx) => {
    // Runs once daily — generate reports, purge old records, etc.
    const cutoff = new Date(Date.now() - 30 * 24 * 60 * 60 * 1000).toISOString()
    const old = await ctx.store.query('audit_log', { created_at: { $lt: cutoff } })
    for (const entry of old) {
      await ctx.store.delete('audit_log', entry.id)
    }
  },
},
```

**Supported intervals:** `every:1m`, `every:5m`, `every:15m`, `every:30m`, `every:1h`, `every:6h`, `every:12h`, `every:1d`, `every:1w`.

**Default timeout:** 300 seconds (5 minutes). If a cron task exceeds this, the error is logged and the task is marked as failed. The next scheduled run will still execute normally.

Cron tasks receive a `ctx` object identical to action handlers, but `ctx.currentUser()` returns `null` since there is no authenticated user in a scheduled context.
