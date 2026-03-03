# 테마 설정

Escalated 페이지는 애플리케이션의 레이아웃을 상속하며, Vue 플러그인을 통해 CSS 커스텀 속성으로 테마를 설정할 수 있습니다.

## 플러그인 등록

인증된 레이아웃을 전달하면 Escalated 페이지가 앱의 외부 레이아웃 안에서 렌더링됩니다:

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

> **CSS 커스텀 속성**
>
> - `--esc-primary` -- 기본 액션 색상 (기본값: `#4f46e5`)
> - `--esc-primary-hover` -- 호버 변형 (생략 시 자동으로 어두워짐)
> - `--esc-radius` -- 입력 필드와 버튼의 테두리 반경 (기본값: `0.5rem`)
> - `--esc-radius-lg` -- 카드와 패널의 테두리 반경 (생략 시 자동 조정)
> - `--esc-font-family` -- 글꼴 오버라이드 (기본적으로 호스트 앱에서 상속)

## 레이아웃 요구사항

레이아웃은 `#header` 슬롯과 기본 슬롯을 제공해야 합니다. Escalated는 페이지 제목과 내비게이션을 헤더에 삽입합니다.

## 패널 테마

관리자 패널과 에이전트 패널은 브랜딩이나 화이트라벨링을 위해 독립적으로 테마를 설정할 수 있습니다. 패널 테마는 `theme.panel` 옵션으로 구성하며, 빠른 커스터마이징과 전체 화이트라벨 오버라이드의 두 가지 수준을 지원합니다.

### 빠른 커스터마이징

모드, 강조 색상, 앱 이름, 로고를 설정합니다:

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

| 옵션 | 타입 | 기본값 | 설명 |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | 관리자 및 에이전트 패널의 기본 색상 스킴 |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | 버튼 및 링크의 기본 강조 색상 |
| `appName` | string | `'Escalated'` | 사이드바와 에이전트 내비게이션에 표시되는 브랜드 이름 |
| `logo` | string \| Component | `null` | 기본 로고를 대체할 이미지 URL 또는 Vue 컴포넌트 |

`logo`가 문자열인 경우 `<img>` 태그로 렌더링됩니다. Vue 컴포넌트인 경우 `<component :is>`로 렌더링됩니다. 생략하면 기본 Escalated 로고가 사용됩니다.

### 전체 화이트라벨

개별 디자인 토큰을 오버라이드하여 패널 외관을 완전히 제어할 수 있습니다:

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

각 토큰은 `:root`의 CSS 커스텀 속성에 매핑됩니다. 자체 CSS에서 이러한 속성을 직접 오버라이드할 수도 있습니다.

### 패널 CSS 커스텀 속성

모든 패널 토큰에는 다크 모드와 라이트 모드 모두에 적절한 기본값이 설정되어 있습니다. `mode: 'light'`를 설정하면 전체 기본 팔레트가 자동으로 전환됩니다.

| CSS 속성 | 설정 키 | 다크 기본값 | 라이트 기본값 | 설명 |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | 페이지 배경 |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | 사이드바 배경 |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | 상단바 배경 |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | 카드 및 패널 |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | 입력 필드 및 중첩 서피스 |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | 테두리 및 구분선 |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | 입력 필드 테두리 |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | 기본 텍스트 |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | 라벨 및 본문 텍스트 |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | 보조 라벨 |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | 힌트 및 플레이스홀더 |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | 기본 강조 |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | 그라데이션 끝점 / 보조 강조 |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | 강조 호버 상태 |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | 보조 강조 호버 |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | 행 및 항목 호버 배경 |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | 활성 내비게이션 항목 배경 |

> **참고:** 상태 및 우선순위 표시 색상(open, closed, escalated 등)은 패널 테마의 영향을 받지 않습니다. 모든 브랜드 배포에서 의미론적 의미를 유지하기 위해 고정되어 있습니다.

### CSS 전용 오버라이드

JavaScript 설정 없이 패널 스타일을 오버라이드하려면 CSS 커스텀 속성을 직접 설정하면 됩니다:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

이 방법은 `theme.panel` 설정과 함께 사용하거나 대신 사용할 수 있습니다. CSS 오버라이드는 플러그인 초기화 후에 적용될 때 우선합니다.
