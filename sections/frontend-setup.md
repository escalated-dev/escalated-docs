# Frontend Setup

> **Note:** Frontend setup is only required when the built-in UI is enabled (`ui.enabled = true`, the default). If you are running Escalated in headless mode, skip this section entirely.

Escalated ships a shared Inertia.js + Vue 3 UI as an npm package. All frameworks use the same frontend.

## 1. Install the npm package

```bash
$ npm install @escalated-dev/escalated
```

## 2. Add to Tailwind content

Ensure Tailwind scans the Escalated components for class names:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

## 3. Configure the Inertia page resolver

Pages prefixed with `Escalated/` are resolved from the npm package:

```js
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';

// Pre-glob the Escalated pages
const escalatedPages = import.meta.glob(
  '../../node_modules/@escalated-dev/escalated/src/pages/**/*.vue'
);

createInertiaApp({
  resolve: (name) => {
    if (name.startsWith('Escalated/')) {
      const path = name.replace('Escalated/', '');
      return resolvePageComponent(
        `../../node_modules/@escalated-dev/escalated/src/pages/${path}.vue`,
        escalatedPages
      );
    }
    return resolvePageComponent(
      `./Pages/${name}.vue`,
      import.meta.glob('./Pages/**/*.vue')
    );
  },
});
```

## 4. Provide a `window.route()` helper

The Escalated frontend generates URLs to its own named routes through a global `route(name, params)` helper with the same signature as [Ziggy](https://github.com/tighten/ziggy) — Laravel's named-route URL generator.

- **Laravel hosts:** install Ziggy (`composer require tightenco/ziggy`) and call `route()` is already on `window`. Nothing else to do.
- **Non-Laravel hosts (Rails, Django, NestJS, Phoenix, Symfony, Adonis, Go, .NET, Spring, WordPress):** you need to ship a compatible shim that speaks Ziggy's API against your host framework's named-route table. At minimum, `route(name)` must return a URL string, and `route(name, params)` must return a URL string with the given params interpolated.

If no `window.route` is installed when `EscalatedPlugin.install()` runs, the plugin installs a stub that throws a descriptive error on first call — this keeps a missing shim from surfacing as a cryptic `ReferenceError` deep inside a component render. You still need to replace the stub with a real helper before the UI is usable.

```js
// Minimal shim shape
window.route = function (name, params) {
  // lookup by `name` in your route table, interpolate `params`, return URL
}
```

