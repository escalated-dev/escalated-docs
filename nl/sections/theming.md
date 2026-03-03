# Thema's

Escalated-pagina's nemen de lay-out van je applicatie over en kunnen worden gestyled met aangepaste CSS-eigenschappen via de Vue-plugin.

## Registreer de plugin

Geef je geauthenticeerde lay-out door zodat Escalated-pagina's worden weergegeven binnen de opmaak van je app:

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

> **Aangepaste CSS-eigenschappen**
>
> - `--esc-primary` -- Primaire actiekleur (standaard: `#4f46e5`)
> - `--esc-primary-hover` -- Hover-variant (automatisch donkerder als weggelaten)
> - `--esc-radius` -- Randradius voor invoervelden en knoppen (standaard: `0.5rem`)
> - `--esc-radius-lg` -- Randradius voor kaarten en panelen (automatisch geschaald als weggelaten)
> - `--esc-font-family` -- Lettertypeoverschrijving (neemt standaard over van de host-app)

## Lay-outvereisten

Je lay-out moet een `#header`-slot en een standaardslot bevatten. Escalated plaatst de paginatitel en navigatie in de header.

## Paneelthema's

De beheer- en agentpanelen kunnen onafhankelijk worden gestyled voor branding of whitelabeling. Paneelthematisering wordt geconfigureerd via de `theme.panel`-optie en ondersteunt twee niveaus: snelle aanpassing en volledige whitelabel-overschrijving.

### Snelle aanpassing

Stel een modus, accentkleur, app-naam en logo in:

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

| Optie | Type | Standaard | Beschrijving |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Basiskleurschemavoor beheer- en agentpanelen |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Primaire accentkleur voor knoppen en links |
| `appName` | string | `'Escalated'` | Merknaam weergegeven in de zijbalk en agentnavigatie |
| `logo` | string \| Component | `null` | Afbeeldings-URL of Vue-component om het standaardlogo te vervangen |

Wanneer `logo` een string is, wordt het weergegeven als een `<img>`-tag. Wanneer het een Vue-component is, wordt het weergegeven via `<component :is>`. Als het wordt weggelaten, wordt het standaard Escalated-logo gebruikt.

### Volledige whitelabel

Overschrijf individuele designtokens voor volledige controle over het uiterlijk van het paneel:

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

Elk token wordt gekoppeld aan een aangepaste CSS-eigenschap op `:root`. Je kunt deze eigenschappen ook rechtstreeks in je eigen CSS overschrijven.

### Aangepaste CSS-eigenschappen van het paneel

Alle paneeltokens hebben verstandige standaardwaarden voor zowel de donkere als de lichte modus. Wanneer je `mode: 'light'` instelt, schakelt het volledige standaardpalet automatisch om.

| CSS-eigenschap | Configuratiesleutel | Donkere standaard | Lichte standaard | Beschrijving |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Pagina-achtergrond |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Zijbalkachtergrond |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Bovenste balk-achtergrond |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Kaarten en panelen |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Invoervelden en geneste oppervlakken |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Randen en scheidingslijnen |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Randen van invoervelden |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Primaire tekst |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Labels en lopende tekst |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Secundaire labels |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Hints en plaatshouders |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Primair accent |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Gradient-einde / secundair accent |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Accent-hoverstatus |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Secundair accent-hover |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Hover-achtergrond voor rijen en items |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Achtergrond actief navigatie-item |

> **Let op:** Status- en prioriteitsindicatorkleuren (open, closed, escalated, enz.) worden niet beinvloed door het paneelthema. Ze blijven vast om de semantische betekenis te behouden in alle merkimplementaties.

### Alleen-CSS-overschrijvingen

Als je de voorkeur geeft aan het overschrijven van paneelstijlen zonder de JavaScript-configuratie, stel dan de aangepaste CSS-eigenschappen rechtstreeks in:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Dit werkt naast of in plaats van de `theme.panel`-configuratie. CSS-overschrijvingen hebben voorrang wanneer ze worden toegepast na de initialisatie van de plugin.
