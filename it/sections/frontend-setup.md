# Configurazione Frontend

Escalated include un'interfaccia condivisa Inertia.js + Vue 3 sotto forma di pacchetto npm. Tutti i framework utilizzano lo stesso frontend.

## 1. Installare il pacchetto npm

```bash
$ npm install @escalated-dev/escalated
```

## 2. Aggiungere al contenuto Tailwind

Assicurati che Tailwind analizzi i componenti di Escalated per i nomi delle classi:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

## 3. Configurare il resolver delle pagine Inertia

Le pagine con prefisso `Escalated/` vengono risolte dal pacchetto npm:

```js
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';

// Pre-glob delle pagine Escalated
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
