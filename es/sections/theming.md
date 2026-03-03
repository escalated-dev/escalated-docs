# Personalizacion visual

Las paginas de Escalated heredan el layout de tu aplicacion y pueden personalizarse con propiedades CSS personalizadas a traves del plugin de Vue.

## Registrar el plugin

Pasa tu layout autenticado para que las paginas de Escalated se rendericen dentro del marco de tu aplicacion:

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

> **Propiedades CSS personalizadas**
>
> - `--esc-primary` -- Color de accion principal (predeterminado: `#4f46e5`)
> - `--esc-primary-hover` -- Variante de hover (oscurecido automaticamente si se omite)
> - `--esc-radius` -- Radio de borde para campos y botones (predeterminado: `0.5rem`)
> - `--esc-radius-lg` -- Radio de borde para tarjetas y paneles (escalado automaticamente si se omite)
> - `--esc-font-family` -- Fuente personalizada (hereda de la aplicacion principal por defecto)

## Requisitos del layout

Tu layout debe proporcionar un slot `#header` y un slot predeterminado. Escalated inyecta el titulo de la pagina y la navegacion en el encabezado.

## Personalizacion de paneles

Los paneles de administracion y agentes se pueden personalizar de forma independiente para branding o marca blanca. La personalizacion de paneles se configura a traves de la opcion `theme.panel` y admite dos niveles: personalizacion rapida y sobreescrituras completas de marca blanca.

### Personalizacion rapida

Establece un modo, color de acento, nombre de la aplicacion y logotipo:

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

| Opcion | Tipo | Predeterminado | Descripcion |
|--------|------|----------------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Esquema de color base para paneles de administracion y agentes |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Color de acento principal para botones y enlaces |
| `appName` | string | `'Escalated'` | Nombre de marca mostrado en la barra lateral y navegacion de agentes |
| `logo` | string \| Component | `null` | URL de imagen o componente Vue para reemplazar el logotipo predeterminado |

Cuando `logo` es una cadena, se renderiza como una etiqueta `<img>`. Cuando es un componente Vue, se renderiza mediante `<component :is>`. Si se omite, se usa el logotipo predeterminado de Escalated.

### Marca blanca completa

Sobreescribe tokens de diseno individuales para un control total sobre la apariencia del panel:

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

Cada token se mapea a una propiedad CSS personalizada en `:root`. Tambien puedes sobreescribir estas propiedades directamente en tu propio CSS.

### Propiedades CSS de panel

Todos los tokens de panel tienen valores predeterminados adecuados para los modos claro y oscuro. Cuando estableces `mode: 'light'`, toda la paleta predeterminada cambia automaticamente.

| Propiedad CSS | Clave de config | Predeterminado oscuro | Predeterminado claro | Descripcion |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Fondo de pagina |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Fondo de barra lateral |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Fondo de barra superior |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Tarjetas y paneles |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Campos de entrada y superficies anidadas |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Bordes y divisores |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Bordes de campos de entrada |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Texto principal |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Etiquetas y texto del cuerpo |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Etiquetas secundarias |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Sugerencias y textos de marcador |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Acento principal |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Fin de degradado / acento secundario |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Estado hover del acento |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Hover del acento secundario |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Fondo de hover en filas y elementos |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Fondo de elemento de navegacion activo |

> **Nota:** Los colores de los indicadores de estado y prioridad (open, closed, escalated, etc.) no se ven afectados por la personalizacion de paneles. Se mantienen fijos para preservar el significado semantico en todos los despliegues con marca personalizada.

### Sobreescrituras solo con CSS

Si prefieres sobreescribir los estilos de panel sin la configuracion de JavaScript, establece las propiedades CSS personalizadas directamente:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Esto funciona junto con o en lugar de la configuracion `theme.panel`. Las sobreescrituras CSS tienen prioridad cuando se aplican despues de que el plugin se inicializa.
