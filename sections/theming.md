# Theming

Escalated pages inherit your application's layout and can be themed with CSS custom properties via the Vue plugin.

## Register the plugin

Pass your authenticated layout so Escalated pages render inside your app's chrome:

```js
import { EscalatedPlugin } from '@escalated-dev/escalated';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';

createApp({ ... })
  .use(EscalatedPlugin, {
    layout: AuthenticatedLayout,
    theme: {
      primary: '#3b82f6',
      radius: '0.75rem',
    }
  })
```

> **CSS custom properties**
>
> - `--esc-primary` -- Primary action color (default: `#4f46e5`)
> - `--esc-primary-hover` -- Hover variant (auto-darkened if omitted)
> - `--esc-radius` -- Border radius for inputs and buttons (default: `0.5rem`)
> - `--esc-radius-lg` -- Border radius for cards and panels (auto-scaled if omitted)
> - `--esc-font-family` -- Font override (inherits from host app by default)

## Layout requirements

Your layout must provide a `#header` slot and a default slot. Escalated injects its page title and navigation into the header.

## Panel theming

The admin and agent panels can be themed independently for branding or whitelabeling. Panel theming is configured via the `theme.panel` option and supports two tiers: quick customization and full whitelabel overrides.

### Quick customization

Set a mode, accent color, app name, and logo:

```js
createApp({ ... })
  .use(EscalatedPlugin, {
    layout: AuthenticatedLayout,
    theme: {
      primary: '#3b82f6',
      panel: {
        mode: 'dark',
        accent: '#e94560',
        appName: 'HelpDesk Pro',
        logo: '/img/brand-logo.svg',
      }
    }
  })
```

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Base color scheme for admin and agent panels |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Primary accent color for buttons and links |
| `appName` | string | `'Escalated'` | Brand name shown in the sidebar and agent nav |
| `logo` | string \| Component | `null` | Image URL or Vue component to replace the default logo |

When `logo` is a string, it renders as an `<img>` tag. When it's a Vue component, it renders via `<component :is>`. If omitted, the default Escalated logo is used.

### Full whitelabel

Override individual design tokens for complete control over the panel appearance:

```js
createApp({ ... })
  .use(EscalatedPlugin, {
    theme: {
      panel: {
        mode: 'dark',
        appName: 'ClientDesk',
        logo: MyLogoComponent,
        accent: '#e94560',
        accentSecondary: '#ff6b6b',
        bg: '#0f0f23',
        sidebarBg: '#1a1a2e',
        topbarBg: 'rgba(15,15,35,0.8)',
        surface: '#16213e',
        surfaceAlt: '#0f0f23',
        border: 'rgba(255,255,255,0.08)',
        borderInput: 'rgba(255,255,255,0.12)',
        text: '#ffffff',
        textSecondary: '#a0aec0',
        textMuted: '#718096',
      }
    }
  })
```

Each token maps to a CSS custom property on `:root`. You can also override these properties directly in your own CSS.

### Panel CSS custom properties

All panel tokens have sensible defaults for both dark and light modes. When you set `mode: 'light'`, the entire default palette switches automatically.

| CSS Property | Config Key | Dark Default | Light Default | Description |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Page background |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Sidebar background |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Top bar background |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Cards and panels |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Inputs and nested surfaces |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Borders and dividers |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Input field borders |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Primary text |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Labels and body text |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Secondary labels |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Hints and placeholders |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Primary accent |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Gradient end / secondary accent |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Accent hover state |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Secondary accent hover |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Row and item hover background |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Active nav item background |

> **Note:** Status and priority indicator colors (open, closed, escalated, etc.) are not affected by panel theming. They remain fixed to preserve semantic meaning across all branded deployments.

### CSS-only overrides

If you prefer to override panel styles without the JavaScript config, set the CSS custom properties directly:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

This works alongside or instead of the `theme.panel` config. CSS overrides take precedence when applied after the plugin initializes.
