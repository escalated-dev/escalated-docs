# Getting Started

## Install the SDK

```bash
npm install @escalated-dev/plugin-sdk
```

For TypeScript projects (recommended), also install the TypeScript compiler:

```bash
npm install -D typescript
```

## Create your first plugin

All plugins are defined with `definePlugin()`. Create `src/index.ts`:

```typescript
import { definePlugin } from '@escalated-dev/plugin-sdk'

export default definePlugin({
  name: 'my-plugin',
  version: '0.1.0',
  description: 'My first Escalated plugin',

  // Configuration fields — rendered in Admin UI, stored as JSON
  config: [
    { name: 'api_key', label: 'API Key', type: 'password', required: true },
    { name: 'notify_channel', label: 'Notify Channel', type: 'text' },
  ],

  onActivate: async (ctx) => {
    // Runs when the plugin is activated in the Admin UI
    // Set up defaults, seed initial config, etc.
    const config = await ctx.config.all()
    if (!config.notify_channel) {
      await ctx.config.set({ notify_channel: '#support' })
    }
  },

  onDeactivate: async (ctx) => {
    // Runs when the plugin is deactivated — clean up resources
  },

  actions: {
    'ticket.created': async (event, ctx) => {
      const settings = await ctx.config.all()
      if (!settings.api_key) return
      ctx.log.info('New ticket', { id: event.id, title: event.title })
      // Call your external service here...
    },
  },
})
```

## Config fields

The `config` array defines the settings form shown in the Admin UI. Each field is stored as JSON and accessible via `ctx.config`.

| Type | Renders as | Example use |
|------|-----------|-------------|
| `text` | Text input | Domain, channel name |
| `password` | Masked input | API tokens, secrets |
| `number` | Number input | Timeout values |
| `boolean` | Toggle switch | Enable/disable features |
| `select` | Dropdown | `{ type: 'select', options: [{value, label}] }` |
| `multiselect` | Multi-select | Event type selection |
| `textarea` | Textarea | Templates, message formats |
| `json` | Code editor | Complex configuration objects |
| `url` | URL input with validation | Webhook URLs, API base URLs |

Example with multiple field types:

```typescript
config: [
  { name: 'bot_token', label: 'Bot Token', type: 'password', required: true },
  { name: 'channel', label: 'Default Channel', type: 'text' },
  { name: 'notify_on', label: 'Notify On', type: 'multiselect', options: [
    { value: 'ticket.created', label: 'New Ticket' },
    { value: 'ticket.assigned', label: 'Assignment' },
    { value: 'reply.created', label: 'New Reply' },
  ]},
  { name: 'enabled', label: 'Enable Notifications', type: 'boolean' },
],
```

## Testing your plugin locally

Install the runtime alongside the SDK:

```bash
npm install @escalated-dev/plugin-runtime
```

Run your plugin against a local Escalated instance by pointing the bridge at your development directory. For Laravel:

```bash
# In your Laravel .env
ESCALATED_PLUGIN_PATH=/path/to/your/plugin-project/node_modules
```

The runtime loads all packages matching `@escalated-dev/plugin-*` from the configured path. During development you can symlink your plugin into a local `node_modules` directory and the runtime will pick it up on next restart.

To run the plugin in isolation and inspect JSON-RPC messages:

```bash
npx @escalated-dev/plugin-runtime --dev --verbose
```

The `--dev` flag enables source maps and detailed error output. The `--verbose` flag logs every JSON-RPC message to stderr.
