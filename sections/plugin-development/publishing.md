# Publishing

## Package structure

Escalated plugins are standard npm packages. The recommended structure separates backend logic (`src/`) from Vue frontend components (`frontend/`):

```
@escalated-dev/plugin-slack/
├── package.json
├── src/
│   ├── index.ts          # definePlugin() — backend definition (main entry)
│   ├── client.ts         # External API client (e.g., SlackClient)
│   └── handlers.ts       # Shared handler logic
├── frontend/
│   ├── index.js          # defineEscalatedPlugin() — Vue frontend entry
│   └── components/
│       ├── SlackSettings.vue
│       ├── SlackThreadPanel.vue
│       └── SlackActivityWidget.vue
└── README.md
```

`package.json` should declare both entry points:

```json
{
  "name": "@escalated-dev/plugin-slack",
  "version": "0.1.0",
  "main": "dist/index.js",
  "exports": {
    ".": "./dist/index.js",
    "./frontend": "./frontend/index.js"
  },
  "scripts": {
    "build": "tsc",
    "dev": "tsc --watch"
  },
  "peerDependencies": {
    "@escalated-dev/plugin-sdk": "^1.0.0"
  }
}
```

## Naming convention

Official and community Escalated plugins follow the `@escalated-dev/plugin-{name}` naming convention on npm. The runtime auto-discovers all packages installed under `node_modules/@escalated-dev/plugin-*`, so naming your package correctly is all that is required for it to be loaded.

```bash
# Publish to npm under the @escalated-dev scope (official plugins)
npm publish --access public

# Community plugins can use any scope but should follow the plugin-* naming:
# @your-org/plugin-my-integration
```

Community plugins using a different npm scope can be loaded by adding the scope to the runtime's discovery configuration.

## Backend entry point (`src/index.ts`)

The default export of `src/index.ts` must be the `definePlugin()` call. This is what the runtime loads and introspects for the manifest.

```typescript
import { definePlugin } from '@escalated-dev/plugin-sdk'
import { SlackClient } from './client'
import { handleTicketCreated } from './handlers'

export default definePlugin({
  name: 'slack',
  version: '0.1.0',
  // ...
  actions: {
    'ticket.created': handleTicketCreated,
  },
})
```

## Frontend entry point (`frontend/index.js`)

The `frontend/index.js` entry exports Vue components using `defineEscalatedPlugin()`. The bridge loads this file via the Inertia asset pipeline.

```javascript
import SlackSettings from './components/SlackSettings.vue'
import SlackThreadPanel from './components/SlackThreadPanel.vue'

export default defineEscalatedPlugin({
  components: {
    SlackSettings,
    SlackThreadPanel,
  },
})
```

Component names must match exactly what is declared in the `pages[].component` and `components[].component` fields of `definePlugin()`.

## Vue components

Plugin Vue components have access to the full Escalated UI component library and Vue 3 Composition API. Use `<script setup>` for the cleanest syntax:

```vue
<template>
  <EscalatedCard title="Slack Settings">
    <form @submit.prevent="save">
      <EscalatedInput v-model="form.channel" label="Default Channel" />
      <EscalatedButton type="submit">Save</EscalatedButton>
    </form>
  </EscalatedCard>
</template>

<script setup>
import { ref } from 'vue'
import { usePluginEndpoint } from '@escalated-dev/plugin-sdk/vue'

const { data, save } = usePluginEndpoint('slack', '/settings')
const form = ref({ channel: data.value?.channel ?? '' })
</script>
```

## TypeScript compilation

Compile your backend before publishing:

```bash
npm run build
# Outputs to dist/
```

Add a `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "outDir": "dist",
    "rootDir": "src",
    "strict": true,
    "declaration": true
  },
  "include": ["src"]
}
```

Do not compile the `frontend/` directory — Vue components are consumed as source by the Inertia build pipeline.

## Migration from the PHP plugin system

If you are converting an existing PHP plugin to the SDK format, the following mapping covers the most common patterns:

| PHP | SDK equivalent |
|-----|---------------|
| `escalated_add_action('ticket.created', $handler)` | `actions: { 'ticket.created': handler }` |
| `escalated_apply_filters('notification.channels', $channels)` | `filters: { 'notification.channels': handler }` |
| `escalated_register_page(...)` | `pages: [{ route, component, menu }]` |
| `escalated_add_page_component(...)` | `components: [{ page, slot, component }]` |
| `escalated_register_dashboard_widget(...)` | `widgets: [{ component, label, size }]` |
| `escalated_broadcast(...)` | `ctx.broadcast.toChannel(...)` |
| `escalated_do_action('plugin.*', ...)` | `ctx.emit('plugin.*', ...)` |
| `Support/Config.php` JSON storage | `ctx.config` |
| Custom JSON file storage | `ctx.store` |
| `Services/*Client.php` | TypeScript class in `src/client.ts` using `ctx.http` |
