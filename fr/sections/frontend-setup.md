# Configuration du frontend

Escalated fournit une interface partagee Inertia.js + Vue 3 sous forme de package npm. Tous les frameworks utilisent le meme frontend.

## 1. Installer le package npm

```bash
npm install @escalated-dev/escalated
```

## 2. Ajouter au contenu Tailwind

Assurez-vous que Tailwind analyse les composants Escalated pour les noms de classes :

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

## 3. Configurer le resolveur de pages Inertia

This step assumes Inertia and Vue are already installed and configured.

Les pages prefixees par `Escalated/` sont resolues depuis le package npm :

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
