# Tema Özelleştirme

Escalated sayfaları uygulamanızın düzenini miras alır ve Vue eklentisi aracılığıyla CSS özel özellikleriyle temaya uyarlanabilir.

## Eklentiyi kaydedin

Kimlik doğrulamalı düzeninizi iletin, böylece Escalated sayfaları uygulamanızın arayüzü içinde görüntülenir:

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

> **CSS özel özellikleri**
>
> - `--esc-primary` -- Birincil eylem rengi (varsayılan: `#4f46e5`)
> - `--esc-primary-hover` -- Üzerine gelme varyantı (belirtilmezse otomatik koyulaştırılır)
> - `--esc-radius` -- Giriş alanları ve düğmeler için kenar yuvarlaklığı (varsayılan: `0.5rem`)
> - `--esc-radius-lg` -- Kartlar ve paneller için kenar yuvarlaklığı (belirtilmezse otomatik ölçeklenir)
> - `--esc-font-family` -- Yazı tipi geçersiz kılma (varsayılan olarak ana uygulamadan miras alır)

## Düzen gereksinimleri

Düzeniniz bir `#header` yuvası ve varsayılan bir yuva sağlamalıdır. Escalated sayfa başlığını ve navigasyonu başlığa enjekte eder.

## Panel tema özelleştirme

Yönetici ve temsilci panelleri markalaşma veya beyaz etiketleme için bağımsız olarak temaya uyarlanabilir. Panel tema özelleştirme `theme.panel` seçeneğiyle yapılandırılır ve iki seviyeyi destekler: hızlı özelleştirme ve tam beyaz etiket geçersiz kılmaları.

### Hızlı özelleştirme

Mod, vurgu rengi, uygulama adı ve logo ayarlayın:

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

| Seçenek | Tür | Varsayılan | Açıklama |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | Yönetici ve temsilci panelleri için temel renk şeması |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | Düğmeler ve bağlantılar için birincil vurgu rengi |
| `appName` | string | `'Escalated'` | Kenar çubuğunda ve temsilci navigasyonunda gösterilen marka adı |
| `logo` | string \| Component | `null` | Varsayılan logoyu değiştirmek için resim URL'si veya Vue bileşeni |

`logo` bir dize olduğunda `<img>` etiketi olarak görüntülenir. Bir Vue bileşeni olduğunda `<component :is>` aracılığıyla görüntülenir. Belirtilmezse varsayılan Escalated logosu kullanılır.

### Tam beyaz etiket

Panel görünümü üzerinde tam kontrol için bireysel tasarım belirteçlerini geçersiz kılın:

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

Her belirteç `:root` üzerindeki bir CSS özel özelliğine karşılık gelir. Bu özellikleri doğrudan kendi CSS'inizde de geçersiz kılabilirsiniz.

### Panel CSS özel özellikleri

Tüm panel belirteçleri hem koyu hem de açık modlar için makul varsayılan değerlere sahiptir. `mode: 'light'` ayarlandığında tüm varsayılan palet otomatik olarak değişir.

| CSS Özelliği | Yapılandırma Anahtarı | Koyu Varsayılan | Açık Varsayılan | Açıklama |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | Sayfa arka planı |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | Kenar çubuğu arka planı |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | Üst çubuk arka planı |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | Kartlar ve paneller |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | Giriş alanları ve iç içe yüzeyler |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | Kenarlıklar ve ayırıcılar |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | Giriş alanı kenarlıkları |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | Birincil metin |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | Etiketler ve gövde metni |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | İkincil etiketler |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | İpuçları ve yer tutucular |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | Birincil vurgu |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | Gradyan sonu / ikincil vurgu |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | Vurgu üzerine gelme durumu |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | İkincil vurgu üzerine gelme |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | Satır ve öğe üzerine gelme arka planı |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | Aktif navigasyon öğesi arka planı |

> **Not:** Durum ve öncelik gösterge renkleri (open, closed, escalated vb.) panel tema özelleştirmesinden etkilenmez. Tüm markalı dağıtımlarda anlamsal tutarlılığı korumak için sabit kalırlar.

### Yalnızca CSS ile geçersiz kılma

Panel stillerini JavaScript yapılandırması olmadan geçersiz kılmayı tercih ediyorsanız, CSS özel özelliklerini doğrudan ayarlayın:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

Bu, `theme.panel` yapılandırmasıyla birlikte veya onun yerine çalışır. CSS geçersiz kılmaları, eklenti başlatıldıktan sonra uygulandığında öncelik kazanır.
