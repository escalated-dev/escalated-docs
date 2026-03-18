# Pages & Components

Plugins can add entirely new admin or agent pages, inject Vue components into existing page slots, and register dashboard widgets — all declared in the plugin definition and auto-registered by the bridge.

## Custom pages

Declare pages in the `pages` array. The bridge reads the plugin manifest at startup and registers an Inertia route for each page automatically.

```typescript
pages: [
  {
    route: 'settings',           // Mounted at /admin/plugins/{slug}/settings
    component: 'SlackSettings',  // Vue component name from your frontend bundle
    menu: {
      label: 'Slack',
      section: 'admin',          // 'admin' | 'agent'
      position: 80,              // Sidebar position (lower = higher)
      icon: 'slack',
    },
    capability: 'manage_settings', // Required capability to access the page
    layout: 'admin',               // 'admin' | 'agent' | 'public'
  },
],
```

The bridge auto-generates a route equivalent to:

```
GET /admin/plugins/slack/settings
→ Inertia::render('Escalated/Plugin/Page', {
    plugin: 'slack',
    component: 'SlackSettings',
    props: <result of GET /settings endpoint>
  })
```

### Capability-based access control

Set `capability` on any page to restrict access. If the authenticated user does not have the required capability, the bridge returns a 403. Built-in capabilities include `manage_settings`, `escalated-agent`, and `escalated-admin`. Custom capabilities can be registered through the authorization system.

## Injecting components into existing pages

Use the `components` array to inject Vue components into slots on existing Escalated pages, without modifying core templates:

```typescript
components: [
  {
    page: 'ticket.show',          // The Escalated page to inject into
    slot: 'sidebar',              // The slot within that page
    component: 'SlackThreadPanel',
    props: { pluginSlug: 'slack' }, // Static props passed to the component
    order: 30,                    // Render order within the slot (lower = first)
    capability: 'escalated-agent',
  },
],
```

### Available slots

| Page | Slot | Description |
|------|------|-------------|
| `ticket.show` | `sidebar` | Ticket detail sidebar panel |
| `ticket.show` | `actions` | Below the ticket action buttons |
| `ticket.show` | `header` | Above the ticket subject |
| `dashboard` | `top` | Top of the dashboard |
| `contacts.show` | `sidebar` | Contact detail sidebar |

## Dashboard widgets

Widgets appear on the Escalated dashboard. They can include a dynamic badge counter polled by the frontend every 30 seconds:

```typescript
widgets: [
  {
    component: 'SlackActivityWidget',
    label: 'Slack Activity',
    size: 'half',               // 'full' | 'half' | 'quarter'
    order: 50,
    capability: 'escalated-agent',
    // Optional: badge function polled every 30s
    badge: async (ctx) => {
      const unread = await ctx.store.query('slack_messages', { read: false })
      return unread.length > 0 ? unread.length : null
    },
  },
],
```

The `badge` function runs in the plugin process. Return a number to display a counter badge, or `null` to hide it. The bridge calls the badge endpoint automatically based on the manifest declaration — no manual endpoint registration is needed.

## Frontend components (Vue)

Your plugin's Vue components live under `frontend/` in your package. The bridge loads `frontend/index.js` which should export components using `defineEscalatedPlugin()`:

```javascript
// frontend/index.js
import SlackSettings from './components/SlackSettings.vue'
import SlackThreadPanel from './components/SlackThreadPanel.vue'
import SlackActivityWidget from './components/SlackActivityWidget.vue'

export default defineEscalatedPlugin({
  components: {
    SlackSettings,
    SlackThreadPanel,
    SlackActivityWidget,
  },
})
```

Components are lazy-loaded — the bridge injects them only on pages where they are declared. Standard Vue 3 Composition API, `<script setup>`, and the full Escalated UI component library are available inside plugin components.
