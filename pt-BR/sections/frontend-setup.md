# Configuracao do Frontend

Escalated disponibiliza uma interface compartilhada em Inertia.js + Vue 3 como um pacote npm. Todos os frameworks utilizam o mesmo frontend.

## 1. Instale o pacote npm

```bash
$ npm install @escalated-dev/escalated
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

## 3. Configure o resolvedor de paginas do Inertia

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
