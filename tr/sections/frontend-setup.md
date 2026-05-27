# Ön Yüz Kurulumu

Escalated, Inertia.js + Vue 3 ile oluşturulmuş paylaşılan bir arayüzü npm paketi olarak sunar. Tüm framework'ler aynı ön yüzü kullanır.

## 1. npm paketini kurun

```bash
npm install @escalated-dev/escalated
```

## 2. Tailwind içeriğine ekleyin

Tailwind'in Escalated bileşenlerini sınıf adları için taradığından emin olun:

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

## 3. Inertia sayfa çözümleyicisini yapılandırın

This step assumes Inertia and Vue are already installed and configured.

`Escalated/` ön ekine sahip sayfalar npm paketinden çözümlenir:

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
