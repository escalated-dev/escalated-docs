# Configuracion del frontend

Escalated incluye una interfaz compartida de Inertia.js + Vue 3 como paquete npm. Todos los frameworks usan el mismo frontend.

## 1. Instalar el paquete npm

```bash
$ npm install @escalated-dev/escalated
```

## 2. Agregar al contenido de Tailwind

Asegurate de que Tailwind escanee los componentes de Escalated para detectar los nombres de clases:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

## 3. Configurar el resolver de paginas de Inertia

Las paginas con prefijo `Escalated/` se resuelven desde el paquete npm:

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
