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

في Tailwind CSS v4+، أضف Escalated كمصدر في ملف CSS الخاص بتطبيقك بدلاً من ذلك:

```css
/* resources/css/app.css */
@source '../../node_modules/@escalated-dev/escalated/src/**/*.vue';
```

عدّل المسار النسبي إذا كان ملف CSS في مكان آخر.

## 3. تكوين محلل صفحات Inertia

تفترض هذه الخطوة أن Inertia وVue مثبتان ومكوّنان مسبقاً.

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
