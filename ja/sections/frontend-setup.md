# フロントエンドセットアップ

EscalatedはInertia.js + Vue 3の共通UIをnpmパッケージとして提供しています。すべてのフレームワークで同じフロントエンドを使用します。

## 1. npmパッケージのインストール

```bash
npm install @escalated-dev/escalated
```

## 2. Tailwindのコンテンツに追加

TailwindがEscalatedコンポーネントのクラス名をスキャンするように設定します：

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

## 3. Inertiaページリゾルバーの設定

This step assumes Inertia and Vue are already installed and configured.

`Escalated/`プレフィックスのページはnpmパッケージから解決されます：

```js
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';

// Escalatedページを事前にglobする
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
