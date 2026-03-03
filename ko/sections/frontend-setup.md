# 프론트엔드 설정

Escalated는 공유 Inertia.js + Vue 3 UI를 npm 패키지로 제공합니다. 모든 프레임워크에서 동일한 프론트엔드를 사용합니다.

## 1. npm 패키지 설치

```bash
$ npm install @escalated-dev/escalated
```

## 2. Tailwind 콘텐츠에 추가

Tailwind가 Escalated 컴포넌트의 클래스 이름을 스캔하도록 설정합니다:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

## 3. Inertia 페이지 리졸버 설정

`Escalated/` 접두사가 붙은 페이지는 npm 패키지에서 해석됩니다:

```js
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';

// Escalated 페이지를 사전 glob
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
