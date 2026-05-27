# 前端设置

Escalated以npm包的形式提供共享的Inertia.js + Vue 3 UI。所有框架使用相同的前端。

## 1. 安装npm包

```bash
npm install @escalated-dev/escalated
```

## 2. 添加到Tailwind内容配置

确保Tailwind扫描Escalated组件的类名：

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

## 3. 配置Inertia页面解析器

This step assumes Inertia and Vue are already installed and configured.

以`Escalated/`为前缀的页面将从npm包中解析：

```js
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';

// 预先glob Escalated页面
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
