# Konfiguracja frontendu

Escalated dostarcza współdzielony interfejs Inertia.js + Vue 3 jako pakiet npm. Wszystkie frameworki korzystają z tego samego frontendu.

## 1. Zainstaluj pakiet npm

```bash
npm install @escalated-dev/escalated
```

## 2. Dodaj do konfiguracji Tailwind

Upewnij się, że Tailwind skanuje komponenty Escalated w poszukiwaniu klas:

```js
export default {
  content: [
    './resources/**/*.vue',
    './node_modules/@escalated-dev/escalated/src/**/*.vue',
  ],
}
```

W Tailwind CSS v4+ dodaj zamiast tego Escalated jako source w pliku CSS aplikacji:

```css
/* resources/css/app.css */
@source '../../node_modules/@escalated-dev/escalated/src/**/*.vue';
```

Dostosuj sciezke wzgledna, jesli plik CSS znajduje sie gdzie indziej.

## 3. Skonfiguruj resolver stron Inertia

Ten krok zaklada, ze Inertia i Vue sa juz zainstalowane i skonfigurowane.

Strony z prefiksem `Escalated/` są rozwiązywane z pakietu npm:

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
