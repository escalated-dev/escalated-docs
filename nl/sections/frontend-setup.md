# Frontend-installatie

Escalated biedt een gedeelde Inertia.js + Vue 3 UI als npm-pakket. Alle frameworks gebruiken dezelfde frontend.

## 1. Installeer het npm-pakket

```bash
npm install @escalated-dev/escalated
```

## 2. Voeg toe aan Tailwind-content

Zorg ervoor dat Tailwind de Escalated-componenten scant voor klassenamen:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

Voeg voor Tailwind CSS v4+ Escalated in plaats daarvan als source toe in het CSS-bestand van je app:

```css
/* resources/css/app.css */
@source '../../node_modules/@escalated-dev/escalated/src/**/*.vue';
```

Pas het relatieve pad aan als je CSS-bestand ergens anders staat.

## 3. Configureer de Inertia-paginaresolver

Deze stap gaat ervan uit dat Inertia en Vue al zijn geinstalleerd en geconfigureerd.

Pagina's met het voorvoegsel `Escalated/` worden opgelost vanuit het npm-pakket:

```js
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';

// Pre-glob de Escalated-pagina's
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
