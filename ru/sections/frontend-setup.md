# Настройка фронтенда

Escalated поставляется с общим интерфейсом на Inertia.js + Vue 3 в виде npm-пакета. Все фреймворки используют один и тот же фронтенд.

## 1. Установите npm-пакет

```bash
$ npm install @escalated-dev/escalated
```

## 2. Добавьте в конфигурацию Tailwind

Убедитесь, что Tailwind сканирует компоненты Escalated для поиска имён классов:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

## 3. Настройте резолвер страниц Inertia

Страницы с префиксом `Escalated/` разрешаются из npm-пакета:

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
