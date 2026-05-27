# Frontend Setup

> **Note:** Frontend setup is only required when the built-in UI is enabled (`ui.enabled = true`, the default). If you are running Escalated in headless mode, skip this section entirely.

Escalated ships a shared Inertia.js + Vue 3 UI as an npm package. All frameworks use the same frontend.

## 1. Install the npm package

```bash
npm install @escalated-dev/escalated
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

For Tailwind CSS v4+, add Escalated as a source in your app CSS file instead:

```css
/* resources/css/app.css */
@source '../../node_modules/@escalated-dev/escalated/src/**/*.vue';
```

Adjust the relative path if your CSS file lives somewhere else.


### Using Escalated without a Tailwind build

Escalated's Vue components are written with Tailwind utility classes, so **some Tailwind-compatible class processor must be available in the host page**. If you don't want to add a Tailwind toolchain to your build pipeline, you have a few options:

#### Option A: Tailwind Play CDN (zero build)

Best for prototyping and internal tools. Drop this `<script>` into the page that hosts Escalated:

```html
<script src="https://cdn.tailwindcss.com"></script>
```

The CDN JIT-compiles classes at runtime. **Trade-offs:** ~3 MB script tag, no class purging, slight FOUC. Not recommended for high-traffic production traffic.

#### Option B: Tailwind standalone CLI (no npm needed)

Generates a static stylesheet without Vite/Webpack integration:

```bash
# Download the standalone CLI for your platform from
# https://tailwindcss.com/blog/standalone-cli, then:
tailwindcss \
  -i ./input.css \
  -o ./public/escalated.css \
  --content './node_modules/@escalated-dev/escalated/src/**/*.vue' \
  --minify
```

Link the resulting stylesheet from your page (`<link rel="stylesheet" href="/escalated.css">`). Re-run when you upgrade Escalated.

The `input.css` needs only the three Tailwind directives:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

#### Option C: UnoCSS or Twind (Tailwind-compatible atomic CSS engines)

If your project already uses one of these, configure the Tailwind preset and point it at the Escalated package:

```js
// uno.config.ts
import { defineConfig, presetWind } from 'unocss'

export default defineConfig({
  presets: [presetWind()],
  content: {
    filesystem: ['node_modules/@escalated-dev/escalated/src/**/*.vue'],
  },
})
```

Class semantics match Tailwind 3 closely. Some bleeding-edge utility classes may differ — file an issue if you hit one.

#### Option D: Forking with hand-rolled CSS

Last resort. Replace every utility class with scoped per-component CSS. Substantial maintenance burden; not officially supported.

> If none of A–D fits your constraints, [open a discussion](https://github.com/escalated-dev/escalated/discussions) — we're tracking interest in a pre-compiled CSS distribution.

## 3. Configure the Inertia page resolver

This step assumes Inertia and Vue are already installed and configured.

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

