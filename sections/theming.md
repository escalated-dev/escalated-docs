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
