# Framework Bridges

Each framework runs plugins through a thin **bridge** that handles subprocess management, route registration, and context proxying. This page documents the bridge configuration and behavior for each framework.

## How bridges work

Escalated plugins run in a shared Node.js subprocess communicating with the host framework over JSON-RPC 2.0 via stdio. The bridge package spawns and manages this process, reads the plugin manifest, registers routes and menu items, and proxies all `ctx.*` calls (database queries, config reads, broadcasts) back to the native ORM.

```
Host Framework              Plugin Process (Node.js)
┌──────────────────┐  JSON-RPC  ┌──────────────────────┐
│ Bridge Package   │◄──────────►│ Plugin Runtime       │
│                  │   stdio    │                      │
│ - Spawn runtime  │            │ ┌──────────────────┐ │
│ - Register routes│            │ │ Slack Plugin    │ │
│ - Proxy ctx.*    │            │ │ Jira Plugin     │ │
│ - Handle events  │            │ │ ... more        │ │
└──────────────────┘            │ └──────────────────┘ │
                                └──────────────────────┘
```

Plugins declare what they need in a **manifest** (`plugin.json`), and the bridge reads this at startup to register routes, menu items, permissions, and event subscriptions automatically — no manual wiring required.

## Plugin store table

Every Escalated installation has a shared `escalated_plugin_store` table (regardless of framework) that persists plugin configuration and metadata:

| Column | Type | Purpose |
|--------|------|---------|
| `id` | int | Primary key |
| `slug` | string | Plugin identifier (must be unique) |
| `name` | string | Display name |
| `description` | string | Short description |
| `enabled` | boolean | Whether the plugin is active |
| `config` | json | Plugin settings (key-value pairs) |
| `manifest` | json | Cached plugin manifest |
| `created_at` | timestamp | Installation time |
| `updated_at` | timestamp | Last modified time |

Configuration values are stored as JSON and accessed in plugins via `ctx.config.get()` and `ctx.config.set()`. The Admin UI renders config fields based on the `config` array in your plugin definition.

---

## Laravel Bridge

**Package:** `escalated/plugin-bridge` (Composer)

The Laravel bridge spawns the Node.js plugin runtime as a subprocess managed by the service container. It communicates with the runtime via JSON-RPC over stdio.

### Installation

```bash
composer require escalated/plugin-bridge
php artisan vendor:publish --provider="Escalated\PluginBridge\PluginBridgeServiceProvider"
```

### Configuration

Configuration is set in `config/escalated.php`:

```php
'plugins' => [
    // Path where npm packages are installed
    'path' => env('ESCALATED_PLUGIN_PATH', base_path('node_modules')),

    // Enable or disable plugin support
    'enabled' => env('ESCALATED_PLUGINS_ENABLED', true),

    // Node.js executable (useful if not in PATH)
    'node_binary' => env('ESCALATED_NODE_BIN', 'node'),

    // Plugin runtime log level
    'log_level' => env('ESCALATED_PLUGIN_LOG_LEVEL', 'info'),
],
```

### Enabling plugins

Set in your `.env`:

```bash
ESCALATED_PLUGINS_ENABLED=true
ESCALATED_PLUGIN_PATH=/path/to/node_modules
```

If `ESCALATED_PLUGINS_ENABLED=false`, the bridge won't spawn the runtime and all plugin hooks are skipped — useful for testing or disabling plugins without uninstalling them.

### Dual dispatch

The Laravel bridge implements **dual dispatch**: when a plugin emits an action (e.g., `ctx.broadcast('ticket.created')`), the bridge both:

1. **Broadcasts to active connections** via Laravel's `broadcast()` helper (WebSocket, Server-Sent Events)
2. **Queues job** to Escalated's job queue for persistence and reliable delivery

This ensures UI updates are immediate (real-time) while background tasks are resilient.

```php
// In your Laravel event listener
Event::listen(TicketCreated::class, function ($event) {
    // Bridge automatically broadcasts to plugin subscribers
    // and queues any plugin actions
});
```

---

## Django Bridge

**Package:** `escalated-plugin-bridge` (PyPI)

The Django bridge spawns the Node.js runtime as a subprocess and manages it via the Django application lifecycle.

### Installation

```bash
pip install escalated-plugin-bridge
```

Add to `INSTALLED_APPS` in `settings.py`:

```python
INSTALLED_APPS = [
    # ...
    'escalated',
    'escalated_plugin_bridge',
]
```

### Configuration

Configuration is set in `settings.py`:

```python
ESCALATED_PLUGINS = {
    'enabled': os.environ.get('ESCALATED_PLUGINS_ENABLED', True),

    # Path where npm packages are installed
    'path': os.environ.get('ESCALATED_PLUGIN_PATH', os.path.join(BASE_DIR, 'node_modules')),

    # Node.js executable
    'node_binary': os.environ.get('ESCALATED_NODE_BIN', 'node'),

    # Plugin runtime log level
    'log_level': os.environ.get('ESCALATED_PLUGIN_LOG_LEVEL', 'info'),
}
```

### SDK_ENABLED setting

The `SDK_ENABLED` flag controls whether the bridge spawns the runtime:

```python
# settings.py
ESCALATED_PLUGINS['enabled'] = True  # Enable plugins
```

When disabled, plugin hooks are skipped but configured plugins remain in the database — useful for temporary deactivation.

```bash
# .env
ESCALATED_PLUGINS_ENABLED=true
ESCALATED_PLUGIN_PATH=/path/to/node_modules
```

---

## AdonisJS Bridge

**Package:** `@escalated-dev/plugin-bridge` (npm)

AdonisJS is unique: plugins load **in-process** directly into the main application. No subprocess, no JSON-RPC, no interprocess overhead.

### Installation

```bash
npm install @escalated-dev/plugin-bridge
```

Register the provider in `start/app.ts`:

```typescript
import { configure } from '@adonisjs/core/app'

export const plugins = await configure({
  providers: [
    () => import('@escalated-dev/plugin-bridge/providers/plugin_provider'),
  ],
})
```

### In-process mode

In-process plugins have full access to the AdonisJS application instance. They load directly via ES modules:

```typescript
// In your plugin src/index.ts
import { definePlugin } from '@escalated-dev/plugin-sdk'

export default definePlugin({
  name: 'my-plugin',

  // AdonisJS plugins can import native modules directly
  onActivate: async (ctx) => {
    // ctx.app is the AdonisJS application instance
    const db = ctx.app.container.make('lucid.db')
    // Can query directly without JSON-RPC serialization
  },
})
```

### Native context & zero overhead

The `PluginContext` interface is identical across all frameworks, but AdonisJS's implementation calls Lucid ORM directly instead of proxying via JSON-RPC. This means:

- **Zero serialization overhead** — no JSON encoding/decoding of ORM calls
- **Direct database access** — use Lucid models and query builder natively
- **Full transaction support** — participate in application transactions
- **Type safety** — TypeScript types are preserved end-to-end

```typescript
// AdonisJS plugin — direct ORM access
const tickets = await ctx.models.Ticket.where('status', 'open').fetch()

// Same code in Laravel/Django/Rails gets serialized to JSON-RPC
// but produces identical results
```

Plugin behavior is guaranteed identical across all modes — the context contract ensures this.

---

## Rails Bridge

**Package:** `escalated-plugin-bridge` (RubyGems)

The Rails bridge spawns the Node.js plugin runtime and manages its lifecycle via Rails initializers and job queue integration.

### Installation

```bash
bundle add escalated-plugin-bridge
```

### Configuration

Configuration is set in `config/escalated.yml` or via environment variables:

```ruby
# config/initializers/escalated.rb
Escalated::PluginBridge.configure do |config|
  # Path where npm packages are installed
  config.plugin_path = ENV.fetch('ESCALATED_PLUGIN_PATH', Rails.root.join('node_modules').to_s)

  # Enable or disable plugin support
  config.enabled = ENV.fetch('ESCALATED_PLUGINS_ENABLED', true)

  # Node.js executable
  config.node_binary = ENV.fetch('ESCALATED_NODE_BIN', 'node')

  # Plugin runtime log level
  config.log_level = ENV.fetch('ESCALATED_PLUGIN_LOG_LEVEL', 'info')
end
```

### sdk_plugins_enabled setting

The `sdk_plugins_enabled` setting controls whether the bridge spawns the runtime. When set to `false`, plugins are loaded from the database but the runtime is not spawned — useful for disabling plugins without removing them:

```bash
# .env
ESCALATED_PLUGINS_ENABLED=true
ESCALATED_PLUGIN_PATH=/path/to/node_modules
```

Or in code:

```ruby
Escalated::PluginBridge.configure do |config|
  config.enabled = ENV['ESCALATED_PLUGINS_ENABLED'].present?
end
```

### Event handling

The Rails bridge uses Active Job to queue plugin actions and ensure reliable delivery:

```ruby
# In your Rails event
EscalatedBus.publish('ticket.created', ticket_data)

# Bridge queues this to ActiveJob, which persists to the job queue
# and the runtime processes it asynchronously
```

Broadcasts are sent immediately via ActionCable, while durable actions go to the job queue.
