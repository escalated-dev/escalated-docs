# フロントエンドセットアップ

EscalatedはInertia.js + Vue 3の共通UIをnpmパッケージとして提供しています。すべてのフレームワークで同じフロントエンドを使用します。

## 1. npmパッケージのインストール

```bash
$ npm install @escalated-dev/escalated
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

## 3. Inertiaページリゾルバーの設定

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
