# Frontend-Einrichtung

Escalated liefert eine gemeinsame Inertia.js + Vue 3-Oberfläche als npm-Paket. Alle Frameworks verwenden dasselbe Frontend.

## 1. npm-Paket installieren

```bash
$ npm install @escalated-dev/escalated
```

## 2. Zu Tailwind-Content hinzufügen

Stellen Sie sicher, dass Tailwind die Escalated-Komponenten nach Klassennamen durchsucht:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

## 3. Inertia Page Resolver konfigurieren

Seiten mit dem Präfix `Escalated/` werden aus dem npm-Paket aufgelöst:

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
