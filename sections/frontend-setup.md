# Frontend Setup

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
