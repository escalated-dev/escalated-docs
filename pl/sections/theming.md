# Motywy

Strony Escalated dziedziczą układ Twojej aplikacji i mogą być stylizowane za pomocą właściwości CSS custom properties poprzez wtyczkę Vue.

## Rejestracja wtyczki

Przekaż swój uwierzytelniony układ, aby strony Escalated renderowały się wewnątrz Twojej aplikacji:

```js
import { EscalatedPlugin } from '@escalated-dev/escalated';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';

createApp({ ... })
  .use(EscalatedPlugin, {
    layout: AuthenticatedLayout,
    theme: {
      primary: '#3b82f6',
      radius: '0.75rem',
    }
  })
```

> **Właściwości CSS custom properties**
>
> - `--esc-primary` -- Główny kolor akcji (domyślnie: `#4f46e5`)
> - `--esc-primary-hover` -- Wariant hover (automatycznie przyciemniany, jeśli pominięty)
> - `--esc-radius` -- Zaokrąglenie narożników dla pól i przycisków (domyślnie: `0.5rem`)
> - `--esc-radius-lg` -- Zaokrąglenie narożników dla kart i paneli (automatycznie skalowane, jeśli pominięte)
> - `--esc-font-family` -- Nadpisanie czcionki (domyślnie dziedziczy z aplikacji nadrzędnej)

## Wymagania dotyczące układu

Twój układ musi udostępniać slot `#header` oraz slot domyślny. Escalated wstrzykuje tytuł strony i nawigację do nagłówka.

## Motywy paneli

Panele administracyjne i agentów mogą być stylizowane niezależnie na potrzeby brandingu lub whitelabelingu. Motywy paneli konfiguruje się przez opcję `theme.panel` i obsługują dwa poziomy: szybką personalizację oraz pełne nadpisanie whitelabel.

### Szybka personalizacja

Ustaw tryb, kolor akcentu, nazwę aplikacji i logo:

```js
createApp({ ... })
  .use(EscalatedPlugin, {
    layout: AuthenticatedLayout,
    theme: {
      primary: '#3b82f6',
      panel: {
        mode: 'dark',
        accent: '#e94560',
        appName: 'HelpDesk Pro',
        logo: '/img/brand-logo.svg',
      }
    }
  })
```

| Opcja | Typ | Domyślnie | Opis |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Bazowy schemat kolorów dla paneli administracyjnych i agentów |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Główny kolor akcentu dla przycisków i linków |
| `appName` | string | `'Escalated'` | Nazwa marki wyświetlana na pasku bocznym i w nawigacji agenta |
| `logo` | string \| Component | `null` | URL obrazu lub komponent Vue zastępujący domyślne logo |

Gdy `logo` jest ciągiem znaków, renderuje się jako tag `<img>`. Gdy jest komponentem Vue, renderuje się przez `<component :is>`. Jeśli pominięty, używane jest domyślne logo Escalated.

### Pełny whitelabel

Nadpisz poszczególne tokeny projektowe, aby uzyskać pełną kontrolę nad wyglądem panelu:

```js
createApp({ ... })
  .use(EscalatedPlugin, {
    theme: {
      panel: {
        mode: 'dark',
        appName: 'ClientDesk',
        logo: MyLogoComponent,
        accent: '#e94560',
        accentSecondary: '#ff6b6b',
        bg: '#0f0f23',
        sidebarBg: '#1a1a2e',
        topbarBg: 'rgba(15,15,35,0.8)',
        surface: '#16213e',
        surfaceAlt: '#0f0f23',
        border: 'rgba(255,255,255,0.08)',
        borderInput: 'rgba(255,255,255,0.12)',
        text: '#ffffff',
        textSecondary: '#a0aec0',
        textMuted: '#718096',
      }
    }
  })
```

Każdy token jest mapowany na właściwość CSS custom property na `:root`. Możesz również nadpisać te właściwości bezpośrednio w swoim CSS.

### Właściwości CSS paneli

Wszystkie tokeny paneli mają sensowne wartości domyślne zarówno dla trybu ciemnego, jak i jasnego. Po ustawieniu `mode: 'light'` cała domyślna paleta przełącza się automatycznie.

| Właściwość CSS | Klucz konfiguracji | Domyślna ciemna | Domyślna jasna | Opis |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Tło strony |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Tło paska bocznego |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Tło górnego paska |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Karty i panele |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Pola wejściowe i zagnieżdżone powierzchnie |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Obramowania i separatory |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Obramowania pól wejściowych |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Tekst główny |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Etykiety i tekst treści |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Etykiety drugorzędne |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Podpowiedzi i symbole zastępcze |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Główny akcent |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Koniec gradientu / drugorzędny akcent |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Stan hover akcentu |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Hover drugorzędnego akcentu |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Tło hover wierszy i elementów |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Tło aktywnego elementu nawigacji |

> **Uwaga:** Kolory wskaźników statusu i priorytetu (open, closed, escalated itp.) nie są zmieniane przez motywy paneli. Pozostają stałe, aby zachować semantyczne znaczenie we wszystkich wdrożeniach z brandingiem.

### Nadpisywanie wyłącznie przez CSS

Jeśli wolisz nadpisać style paneli bez konfiguracji JavaScript, ustaw właściwości CSS custom properties bezpośrednio:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Działa to obok lub zamiast konfiguracji `theme.panel`. Nadpisania CSS mają pierwszeństwo, gdy są zastosowane po inicjalizacji wtyczki.
