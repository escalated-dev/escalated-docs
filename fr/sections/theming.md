# Personnalisation visuelle

Les pages Escalated heritent du layout de votre application et peuvent etre personnalisees avec des proprietes CSS personnalisees via le plugin Vue.

## Enregistrer le plugin

Passez votre layout authentifie pour que les pages Escalated s'affichent dans le cadre de votre application :

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

> **Proprietes CSS personnalisees**
>
> - `--esc-primary` -- Couleur d'action principale (par defaut : `#4f46e5`)
> - `--esc-primary-hover` -- Variante de survol (assombrie automatiquement si omise)
> - `--esc-radius` -- Rayon de bordure pour les champs et boutons (par defaut : `0.5rem`)
> - `--esc-radius-lg` -- Rayon de bordure pour les cartes et panneaux (mis a l'echelle automatiquement si omis)
> - `--esc-font-family` -- Police personnalisee (heritee de l'application hote par defaut)

## Exigences du layout

Votre layout doit fournir un slot `#header` et un slot par defaut. Escalated injecte le titre de la page et la navigation dans l'en-tete.

## Personnalisation des panneaux

Les panneaux d'administration et d'agent peuvent etre personnalises independamment pour le branding ou la marque blanche. La personnalisation des panneaux se configure via l'option `theme.panel` et prend en charge deux niveaux : personnalisation rapide et remplacement complet en marque blanche.

### Personnalisation rapide

Definissez un mode, une couleur d'accent, un nom d'application et un logo :

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

| Option | Type | Par defaut | Description |
|--------|------|------------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Schema de couleurs de base pour les panneaux d'administration et d'agent |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Couleur d'accent principale pour les boutons et les liens |
| `appName` | string | `'Escalated'` | Nom de marque affiche dans la barre laterale et la navigation des agents |
| `logo` | string \| Component | `null` | URL d'image ou composant Vue pour remplacer le logo par defaut |

Lorsque `logo` est une chaine, il est rendu sous forme de balise `<img>`. Lorsqu'il s'agit d'un composant Vue, il est rendu via `<component :is>`. S'il est omis, le logo Escalated par defaut est utilise.

### Marque blanche complete

Remplacez les tokens de design individuels pour un controle total sur l'apparence du panneau :

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

Chaque token correspond a une propriete CSS personnalisee sur `:root`. Vous pouvez egalement remplacer ces proprietes directement dans votre propre CSS.

### Proprietes CSS des panneaux

Tous les tokens de panneau ont des valeurs par defaut adaptees pour les modes clair et sombre. Lorsque vous definissez `mode: 'light'`, toute la palette par defaut bascule automatiquement.

| Propriete CSS | Cle de config | Par defaut sombre | Par defaut clair | Description |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Arriere-plan de la page |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Arriere-plan de la barre laterale |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Arriere-plan de la barre superieure |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Cartes et panneaux |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Champs de saisie et surfaces imbriquees |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Bordures et separateurs |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Bordures des champs de saisie |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Texte principal |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Libelles et corps de texte |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Libelles secondaires |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Indices et textes de remplacement |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Accent principal |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Fin de degrade / accent secondaire |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Etat de survol de l'accent |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Survol de l'accent secondaire |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Arriere-plan de survol des lignes et elements |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Arriere-plan de l'element de navigation actif |

> **Remarque :** Les couleurs des indicateurs de statut et de priorite (open, closed, escalated, etc.) ne sont pas affectees par la personnalisation des panneaux. Elles restent fixes pour preserver la signification semantique dans tous les deploiements personnalises.

### Remplacements CSS uniquement

Si vous preferez remplacer les styles de panneau sans la configuration JavaScript, definissez les proprietes CSS personnalisees directement :

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Cela fonctionne en complement ou a la place de la configuration `theme.panel`. Les remplacements CSS ont la priorite lorsqu'ils sont appliques apres l'initialisation du plugin.
