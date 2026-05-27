# إعداد الواجهة الأمامية

يأتي Escalated بواجهة مستخدم مشتركة مبنية على Inertia.js + Vue 3 كحزمة npm. تستخدم جميع أطر العمل نفس الواجهة الأمامية.

## 1. تثبيت حزمة npm

```bash
npm install @escalated-dev/escalated
```

## 2. إضافتها إلى محتوى Tailwind

تأكد من أن Tailwind يفحص مكونات Escalated للعثور على أسماء الأصناف:

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

## 3. تكوين محلل صفحات Inertia

This step assumes Inertia and Vue are already installed and configured.

يتم حل الصفحات التي تبدأ بـ `Escalated/` من حزمة npm:

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
