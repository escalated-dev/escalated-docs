# Configuracao do Frontend

Escalated disponibiliza uma interface compartilhada em Inertia.js + Vue 3 como um pacote npm. Todos os frameworks utilizam o mesmo frontend.

## 1. Instale o pacote npm

```bash
npm install @escalated-dev/escalated
```

## 2. Adicione ao conteudo do Tailwind

Certifique-se de que o Tailwind escaneia os componentes do Escalated para os nomes de classes:

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

## 3. Configure o resolvedor de paginas do Inertia

This step assumes Inertia and Vue are already installed and configured.

Paginas com o prefixo `Escalated/` sao resolvidas a partir do pacote npm:

```js
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';

// Pre-glob das paginas do Escalated
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
