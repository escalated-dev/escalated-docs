# Temas

As paginas do Escalated herdam o layout da sua aplicacao e podem ser personalizadas com propriedades CSS customizadas atraves do plugin Vue.

## Registre o plugin

Passe seu layout autenticado para que as paginas do Escalated sejam renderizadas dentro da estrutura da sua aplicacao:

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

> **Propriedades CSS customizadas**
>
> - `--esc-primary` -- Cor da acao principal (padrao: `#4f46e5`)
> - `--esc-primary-hover` -- Variante de hover (escurecida automaticamente se omitida)
> - `--esc-radius` -- Raio de borda para campos e botoes (padrao: `0.5rem`)
> - `--esc-radius-lg` -- Raio de borda para cards e paineis (ajustado automaticamente se omitido)
> - `--esc-font-family` -- Sobrescrita de fonte (herda da aplicacao host por padrao)

## Requisitos de layout

Seu layout deve fornecer um slot `#header` e um slot padrao. O Escalated injeta o titulo da pagina e a navegacao no header.

## Temas de painel

Os paineis de administracao e de agente podem ser personalizados independentemente para marca ou white-labeling. A personalizacao de painel e configurada pela opcao `theme.panel` e suporta dois niveis: personalizacao rapida e sobrescrita completa de white-label.

### Personalizacao rapida

Defina um modo, cor de destaque, nome do aplicativo e logotipo:

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

| Opcao | Tipo | Padrao | Descricao |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Esquema de cores base para paineis de administracao e agentes |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Cor de destaque principal para botoes e links |
| `appName` | string | `'Escalated'` | Nome da marca exibido na barra lateral e na navegacao do agente |
| `logo` | string \| Component | `null` | URL de imagem ou componente Vue para substituir o logotipo padrao |

Quando `logo` e uma string, e renderizado como uma tag `<img>`. Quando e um componente Vue, e renderizado via `<component :is>`. Se omitido, o logotipo padrao do Escalated e utilizado.

### White-label completo

Sobrescreva tokens de design individuais para controle completo sobre a aparencia do painel:

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

Cada token e mapeado para uma propriedade CSS customizada em `:root`. Voce tambem pode sobrescrever essas propriedades diretamente no seu proprio CSS.

### Propriedades CSS customizadas do painel

Todos os tokens do painel possuem valores padrao adequados para os modos escuro e claro. Quando voce define `mode: 'light'`, toda a paleta padrao muda automaticamente.

| Propriedade CSS | Chave de Configuracao | Padrao Escuro | Padrao Claro | Descricao |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Fundo da pagina |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Fundo da barra lateral |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Fundo da barra superior |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Cards e paineis |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Campos de entrada e superficies aninhadas |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Bordas e divisores |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Bordas de campos de entrada |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Texto principal |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Rotulos e texto de corpo |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | Rotulos secundarios |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | Dicas e placeholders |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Destaque principal |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Final de gradiente / destaque secundario |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Estado de hover do destaque |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | Hover do destaque secundario |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Fundo de hover em linhas e itens |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Fundo do item de navegacao ativo |

> **Nota:** As cores dos indicadores de status e prioridade (open, closed, escalated, etc.) nao sao afetadas pelo tema do painel. Elas permanecem fixas para preservar o significado semantico em todas as implantacoes com marca personalizada.

### Sobrescrita apenas por CSS

Se voce preferir sobrescrever os estilos do painel sem a configuracao JavaScript, defina as propriedades CSS customizadas diretamente:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Isso funciona junto com ou no lugar da configuracao `theme.panel`. As sobrescritas CSS tem precedencia quando aplicadas apos a inicializacao do plugin.
