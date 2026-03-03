# Gestaltung

Escalated-Seiten übernehmen das Layout Ihrer Anwendung und können über CSS Custom Properties mithilfe des Vue-Plugins gestaltet werden.

## Plugin registrieren

Übergeben Sie Ihr authentifiziertes Layout, damit Escalated-Seiten innerhalb Ihrer Anwendungsoberfläche gerendert werden:

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

> **CSS Custom Properties**
>
> - `--esc-primary` -- Primäre Aktionsfarbe (Standard: `#4f46e5`)
> - `--esc-primary-hover` -- Hover-Variante (automatisch abgedunkelt, wenn nicht angegeben)
> - `--esc-radius` -- Eckenradius für Eingabefelder und Buttons (Standard: `0.5rem`)
> - `--esc-radius-lg` -- Eckenradius für Karten und Panels (automatisch skaliert, wenn nicht angegeben)
> - `--esc-font-family` -- Schriftart-Überschreibung (erbt standardmäßig von der Host-Anwendung)

## Layout-Anforderungen

Ihr Layout muss einen `#header`-Slot und einen Standard-Slot bereitstellen. Escalated fügt seinen Seitentitel und die Navigation in den Header ein.

## Panel-Gestaltung

Die Admin- und Agenten-Panels können unabhängig voneinander für Branding oder Whitelabeling gestaltet werden. Die Panel-Gestaltung wird über die Option `theme.panel` konfiguriert und unterstützt zwei Stufen: Schnellanpassung und vollständige Whitelabel-Überschreibungen.

### Schnellanpassung

Legen Sie einen Modus, eine Akzentfarbe, einen App-Namen und ein Logo fest:

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

| Option | Typ | Standard | Beschreibung |
|--------|-----|----------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Basis-Farbschema für Admin- und Agenten-Panels |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Primäre Akzentfarbe für Buttons und Links |
| `appName` | string | `'Escalated'` | Markenname in der Seitenleiste und Agenten-Navigation |
| `logo` | string \| Component | `null` | Bild-URL oder Vue-Komponente als Ersatz für das Standard-Logo |

Wenn `logo` ein String ist, wird es als `<img>`-Tag gerendert. Bei einer Vue-Komponente wird es über `<component :is>` gerendert. Ohne Angabe wird das Standard-Escalated-Logo verwendet.

### Vollständiges Whitelabel

Überschreiben Sie einzelne Design-Tokens für vollständige Kontrolle über das Panel-Erscheinungsbild:

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

Jeder Token wird einer CSS Custom Property auf `:root` zugeordnet. Sie können diese Properties auch direkt in Ihrem eigenen CSS überschreiben.

### CSS Custom Properties für Panels

Alle Panel-Tokens haben sinnvolle Standardwerte für den dunklen und hellen Modus. Wenn Sie `mode: 'light'` setzen, wechselt die gesamte Standardpalette automatisch.

| CSS Property | Config Key | Dark Standard | Light Standard | Beschreibung |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Seitenhintergrund |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Seitenleisten-Hintergrund |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Kopfleisten-Hintergrund |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Karten und Panels |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Eingabefelder und verschachtelte Oberflächen |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Rahmen und Trennlinien |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Eingabefeld-Rahmen |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Primärer Text |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Beschriftungen und Fließtext |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Sekundäre Beschriftungen |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Hinweise und Platzhalter |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Primärer Akzent |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Verlaufsende / sekundärer Akzent |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Akzent-Hover-Zustand |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Sekundärer Akzent-Hover |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Hover-Hintergrund für Zeilen und Elemente |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Aktiver Navigations-Hintergrund |

> **Hinweis:** Status- und Prioritäts-Indikatorfarben (Open, Closed, Escalated usw.) werden durch die Panel-Gestaltung nicht beeinflusst. Sie bleiben unverändert, um die semantische Bedeutung über alle Markenbereitstellungen hinweg zu bewahren.

### Reine CSS-Überschreibungen

Wenn Sie die Panel-Stile ohne JavaScript-Konfiguration überschreiben möchten, setzen Sie die CSS Custom Properties direkt:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Dies funktioniert zusammen mit oder anstelle der `theme.panel`-Konfiguration. CSS-Überschreibungen haben Vorrang, wenn sie nach der Plugin-Initialisierung angewendet werden.
