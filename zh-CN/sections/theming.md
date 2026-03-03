# 主题设置

Escalated页面继承您应用程序的布局，可通过Vue插件使用CSS自定义属性进行主题设置。

## 注册插件

传入您的认证布局，使Escalated页面在应用程序的外框内渲染：

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

> **CSS自定义属性**
>
> - `--esc-primary` -- 主要操作颜色（默认：`#4f46e5`）
> - `--esc-primary-hover` -- 悬停变体（省略时自动加深）
> - `--esc-radius` -- 输入框和按钮的边框圆角（默认：`0.5rem`）
> - `--esc-radius-lg` -- 卡片和面板的边框圆角（省略时自动缩放）
> - `--esc-font-family` -- 字体覆盖（默认从宿主应用继承）

## 布局要求

您的布局必须提供`#header`插槽和默认插槽。Escalated会将页面标题和导航注入到头部。

## 面板主题

管理员面板和客服面板可以独立设置主题，用于品牌化或白标方案。面板主题通过`theme.panel`选项配置，支持快速自定义和完整白标覆盖两个级别。

### 快速自定义

设置模式、强调色、应用名称和Logo：

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

| 选项 | 类型 | 默认值 | 说明 |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | 管理员和客服面板的基础配色方案 |
| `accent` | string | `'#06b6d4'`（dark）/ `'#3b82f6'`（light） | 按钮和链接的主要强调色 |
| `appName` | string | `'Escalated'` | 侧边栏和客服导航中显示的品牌名称 |
| `logo` | string \| Component | `null` | 替换默认Logo的图片URL或Vue组件 |

当`logo`为字符串时，以`<img>`标签渲染。当为Vue组件时，通过`<component :is>`渲染。省略时使用默认的Escalated Logo。

### 完整白标

覆盖各个设计令牌以完全控制面板外观：

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

每个令牌映射到`:root`上的CSS自定义属性。您也可以在自己的CSS中直接覆盖这些属性。

### 面板CSS自定义属性

所有面板令牌在深色和浅色模式下都有合理的默认值。设置`mode: 'light'`时，整个默认调色板会自动切换。

| CSS属性 | 配置键 | 深色默认值 | 浅色默认值 | 说明 |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | 页面背景 |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | 侧边栏背景 |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | 顶栏背景 |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | 卡片和面板 |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | 输入框和嵌套表面 |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | 边框和分隔线 |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | 输入框边框 |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | 主要文本 |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | 标签和正文 |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | 次要标签 |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | 提示和占位符 |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | 主要强调色 |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | 渐变终点/次要强调色 |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | 强调色悬停状态 |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | 次要强调色悬停 |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | 行和项目悬停背景 |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | 活跃导航项背景 |

> **注意：** 状态和优先级指示器颜色（open、closed、escalated等）不受面板主题影响。它们保持固定，以在所有品牌部署中保留语义含义。

### 纯CSS覆盖

如果您希望不使用JavaScript配置来覆盖面板样式，可以直接设置CSS自定义属性：

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

这可以与`theme.panel`配置配合使用或替代使用。CSS覆盖在插件初始化之后应用时具有优先权。
