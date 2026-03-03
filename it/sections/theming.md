# Personalizzazione Grafica

Le pagine di Escalated ereditano il layout della tua applicazione e possono essere personalizzate con proprietà CSS custom tramite il plugin Vue.

## Registrare il plugin

Passa il tuo layout autenticato affinché le pagine di Escalated vengano renderizzate all'interno della struttura della tua app:

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

> **Proprietà CSS custom**
>
> - `--esc-primary` -- Colore dell'azione primaria (predefinito: `#4f46e5`)
> - `--esc-primary-hover` -- Variante hover (scurito automaticamente se omesso)
> - `--esc-radius` -- Raggio del bordo per input e pulsanti (predefinito: `0.5rem`)
> - `--esc-radius-lg` -- Raggio del bordo per card e pannelli (scalato automaticamente se omesso)
> - `--esc-font-family` -- Override del font (eredita dall'app host per impostazione predefinita)

## Requisiti del layout

Il tuo layout deve fornire uno slot `#header` e uno slot predefinito. Escalated inserisce il titolo della pagina e la navigazione nell'header.

## Personalizzazione dei pannelli

I pannelli admin e agente possono essere personalizzati in modo indipendente per il branding o il whitelabeling. La personalizzazione dei pannelli è configurata tramite l'opzione `theme.panel` e supporta due livelli: personalizzazione rapida e override completo per whitelabel.

### Personalizzazione rapida

Imposta una modalità, un colore d'accento, il nome dell'app e un logo:

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

| Opzione | Tipo | Predefinito | Descrizione |
|---------|------|-------------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Schema di colori base per i pannelli admin e agente |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Colore d'accento primario per pulsanti e link |
| `appName` | string | `'Escalated'` | Nome del brand mostrato nella sidebar e nella navigazione agente |
| `logo` | string \| Component | `null` | URL dell'immagine o componente Vue per sostituire il logo predefinito |

Quando `logo` è una stringa, viene renderizzato come tag `<img>`. Quando è un componente Vue, viene renderizzato tramite `<component :is>`. Se omesso, viene utilizzato il logo predefinito di Escalated.

### Whitelabel completo

Sovrascrivi i singoli token di design per un controllo totale sull'aspetto del pannello:

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

Ogni token corrisponde a una proprietà CSS custom su `:root`. Puoi anche sovrascrivere queste proprietà direttamente nel tuo CSS.

### Proprietà CSS custom dei pannelli

Tutti i token dei pannelli hanno valori predefiniti sensati sia per la modalità dark che per quella light. Quando imposti `mode: 'light'`, l'intera palette predefinita cambia automaticamente.

| Proprietà CSS | Chiave di configurazione | Predefinito Dark | Predefinito Light | Descrizione |
|--------------|-------------------------|-----------------|-------------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Sfondo della pagina |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Sfondo della sidebar |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Sfondo della barra superiore |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Card e pannelli |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Input e superfici annidate |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Bordi e divisori |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Bordi dei campi di input |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Testo primario |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Etichette e testo del corpo |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Etichette secondarie |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Suggerimenti e segnaposto |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Accento primario |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Fine gradiente / accento secondario |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Stato hover dell'accento |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Hover dell'accento secondario |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Sfondo hover di righe e elementi |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Sfondo dell'elemento di navigazione attivo |

> **Nota:** I colori degli indicatori di stato e priorità (open, closed, escalated, ecc.) non sono influenzati dalla personalizzazione dei pannelli. Rimangono fissi per preservare il significato semantico in tutti i deployment con branding personalizzato.

### Override solo CSS

Se preferisci sovrascrivere gli stili dei pannelli senza la configurazione JavaScript, imposta direttamente le proprietà CSS custom:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Questo funziona insieme o in alternativa alla configurazione `theme.panel`. Gli override CSS hanno la precedenza quando applicati dopo l'inizializzazione del plugin.
