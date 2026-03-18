# Plugin Development

Escalated's Plugin SDK (`@escalated-dev/plugin-sdk`) lets you extend the platform with custom integrations, UI components, and automation — written once in TypeScript and running across every Escalated backend framework.

## What plugins can do

- **Actions** — fire-and-forget event handlers that respond to ticket lifecycle events (`ticket.created`, `ticket.assigned`, `reply.created`, etc.)
- **Filters** — intercept and transform data as it flows through the system (e.g., adding notification channels, modifying ticket action menus)
- **Pages** — register custom admin or agent pages that appear in the sidebar, backed by Vue components served via Inertia.js
- **Components** — inject Vue components into existing page slots (ticket sidebar, dashboard panels, etc.)
- **Widgets** — add dashboard widgets with optional dynamic badges polled from the plugin backend
- **Endpoints** — expose data API routes that your Vue pages consume
- **Webhooks** — receive inbound HTTP requests from external services (Slack, GitHub, Stripe, etc.)
- **Cron** — schedule recurring background tasks (hourly, daily, or any interval)

## Architecture

The SDK is built on the Grafana/HashiCorp subprocess model. Plugins run as a single shared Node.js process (`@escalated-dev/plugin-runtime`), communicating with the host framework over JSON-RPC 2.0 via stdio. This means your TypeScript plugin code runs on every backend — Laravel, Django, Rails, and AdonisJS — without modification.

```
Host Framework (any)              Plugin Process (Node.js)
┌──────────────┐   JSON-RPC/stdio  ┌─────────────────────┐
│ Laravel      │◄─────────────────►│ Plugin Runtime       │
│ Django       │                    │                      │
│ AdonisJS (*) │                    │ ┌─────────────────┐ │
│ Rails        │   spawn/manage     │ │ Slack Plugin     │ │
│              │──────────────────→│ │ Jira Plugin      │ │
│ Bridge pkg   │                    │ │ ... all plugins  │ │
└──────────────┘                    │ └─────────────────┘ │
                                    └─────────────────────┘
(*) AdonisJS: in-process, no subprocess needed
```

Each framework has a thin native **bridge package** that spawns the runtime, reads the plugin manifest, registers routes and menu items, and proxies `ctx.*` calls (database queries, config reads, broadcasts) back from the plugin process to the host ORM.

| Package | Registry | Purpose |
|---------|----------|---------|
| `@escalated-dev/plugin-sdk` | npm | Plugin authoring SDK — `definePlugin()`, types, runtime |
| `@escalated-dev/plugin-runtime` | npm | Process host — loads plugins, handles JSON-RPC |
| `escalated/plugin-bridge` | Composer | Laravel bridge |
| `escalated-plugin-bridge` | PyPI | Django bridge |
| `escalated-plugin-bridge` | RubyGems | Rails bridge |
| `@escalated-dev/plugin-bridge` | npm | AdonisJS bridge (in-process) |

### AdonisJS in-process mode

On AdonisJS, plugins are loaded directly via `require()` — no subprocess, no JSON-RPC. The same `PluginContext` interface is used, but the implementation calls Lucid ORM directly. Plugin behavior is identical across modes; the `PluginContext` contract guarantees this.

## Quick start

```typescript
import { definePlugin } from '@escalated-dev/plugin-sdk'

export default definePlugin({
  name: 'hello-world',
  version: '0.1.0',
  description: 'A minimal Escalated plugin',

  config: [
    { name: 'greeting', label: 'Greeting Message', type: 'text' },
  ],

  actions: {
    'ticket.created': async (event, ctx) => {
      const { greeting } = await ctx.config.all()
      ctx.log.info(`${greeting ?? 'Hello'}: new ticket #${event.id} — ${event.title}`)
    },
  },
})
```

See [Getting Started](getting-started) for installation and local testing instructions.
