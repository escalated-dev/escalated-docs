# テーマ設定

Escalatedのページはアプリケーションのレイアウトをそのまま継承し、Vueプラグインを通じてCSSカスタムプロパティでテーマを設定できます。

## プラグインの登録

認証済みレイアウトを渡すことで、Escalatedのページがアプリケーションの外枠の中に描画されます：

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

> **CSSカスタムプロパティ**
>
> - `--esc-primary` -- プライマリアクションカラー（デフォルト：`#4f46e5`）
> - `--esc-primary-hover` -- ホバー時のバリエーション（省略時は自動的に暗くなります）
> - `--esc-radius` -- 入力欄とボタンのボーダー半径（デフォルト：`0.5rem`）
> - `--esc-radius-lg` -- カードとパネルのボーダー半径（省略時は自動スケーリング）
> - `--esc-font-family` -- フォントのオーバーライド（デフォルトではホストアプリから継承）

## レイアウトの要件

レイアウトは`#header`スロットとデフォルトスロットを提供する必要があります。Escalatedはページタイトルとナビゲーションをヘッダーに挿入します。

## パネルテーマ

管理者パネルとエージェントパネルは、ブランディングやホワイトラベル化のために個別にテーマを設定できます。パネルテーマは`theme.panel`オプションで設定し、クイックカスタマイズと完全なホワイトラベルオーバーライドの2つのレベルに対応しています。

### クイックカスタマイズ

モード、アクセントカラー、アプリ名、ロゴを設定します：

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

| オプション | 型 | デフォルト | 説明 |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | 管理者パネルとエージェントパネルの基本カラースキーム |
| `accent` | string | `'#06b6d4'`（dark） / `'#3b82f6'`（light） | ボタンとリンクのプライマリアクセントカラー |
| `appName` | string | `'Escalated'` | サイドバーとエージェントナビに表示されるブランド名 |
| `logo` | string \| Component | `null` | デフォルトロゴを置き換える画像URLまたはVueコンポーネント |

`logo`が文字列の場合、`<img>`タグとして描画されます。Vueコンポーネントの場合は`<component :is>`で描画されます。省略した場合、デフォルトのEscalatedロゴが使用されます。

### フルホワイトラベル

個々のデザイントークンをオーバーライドして、パネルの外観を完全にコントロールできます：

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

各トークンは`:root`上のCSSカスタムプロパティにマッピングされます。独自のCSSでこれらのプロパティを直接オーバーライドすることもできます。

### パネルのCSSカスタムプロパティ

すべてのパネルトークンにはダークモードとライトモードの両方に適切なデフォルト値が設定されています。`mode: 'light'`を設定すると、デフォルトパレット全体が自動的に切り替わります。

| CSSプロパティ | 設定キー | ダークデフォルト | ライトデフォルト | 説明 |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | ページ背景 |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | サイドバー背景 |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | トップバー背景 |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | カードとパネル |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | 入力欄とネストされたサーフェス |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | ボーダーとディバイダー |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | 入力フィールドのボーダー |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | プライマリテキスト |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | ラベルと本文 |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | セカンダリラベル |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | ヒントとプレースホルダー |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | プライマリアクセント |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | グラデーション終点 / セカンダリアクセント |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | アクセントホバー状態 |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | セカンダリアクセントホバー |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | 行とアイテムのホバー背景 |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | アクティブなナビアイテムの背景 |

> **注意：** ステータスと優先度のインジケーターカラー（open、closed、escalatedなど）はパネルテーマの影響を受けません。すべてのブランドデプロイメントでセマンティックな意味を維持するために固定されています。

### CSSのみのオーバーライド

JavaScript設定を使わずにパネルスタイルをオーバーライドしたい場合は、CSSカスタムプロパティを直接設定できます：

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

これは`theme.panel`設定と併用することも、代わりに使用することもできます。CSSオーバーライドはプラグインの初期化後に適用された場合に優先されます。
