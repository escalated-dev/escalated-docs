# التخصيص المرئي

ترث صفحات Escalated تخطيط تطبيقك ويمكن تخصيصها باستخدام خصائص CSS المخصصة عبر إضافة Vue.

## تسجيل الإضافة

مرر التخطيط المصادق عليه حتى تُعرض صفحات Escalated داخل واجهة تطبيقك:

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

> **خصائص CSS المخصصة**
>
> - `--esc-primary` -- لون الإجراء الرئيسي (الافتراضي: `#4f46e5`)
> - `--esc-primary-hover` -- متغير التمرير (يُعتَّم تلقائيًا إذا لم يُحدد)
> - `--esc-radius` -- نصف قطر الحدود لحقول الإدخال والأزرار (الافتراضي: `0.5rem`)
> - `--esc-radius-lg` -- نصف قطر الحدود للبطاقات واللوحات (يُقاس تلقائيًا إذا لم يُحدد)
> - `--esc-font-family` -- تجاوز الخط (يرث من التطبيق المضيف افتراضيًا)

## متطلبات التخطيط

يجب أن يوفر تخطيطك منفذ `#header` ومنفذًا افتراضيًا. يحقن Escalated عنوان الصفحة والتنقل في الرأس.

## تخصيص اللوحة

يمكن تخصيص لوحتي الإدارة والوكلاء بشكل مستقل للعلامة التجارية أو إعادة التسمية البيضاء. يتم تكوين تخصيص اللوحة عبر خيار `theme.panel` ويدعم مستويين: التخصيص السريع وتجاوزات إعادة التسمية البيضاء الكاملة.

### التخصيص السريع

حدد الوضع، ولون التمييز، واسم التطبيق، والشعار:

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

| الخيار | النوع | الافتراضي | الوصف |
|--------|------|---------|-------------|
| `mode` | `'dark'` \| `'light'` | `'dark'` | نظام الألوان الأساسي للوحتي الإدارة والوكلاء |
| `accent` | string | `'#06b6d4'` (dark) / `'#3b82f6'` (light) | لون التمييز الرئيسي للأزرار والروابط |
| `appName` | string | `'Escalated'` | اسم العلامة التجارية المعروض في الشريط الجانبي وتنقل الوكيل |
| `logo` | string \| Component | `null` | رابط صورة أو مكون Vue لاستبدال الشعار الافتراضي |

عندما يكون `logo` نصًا، يُعرض كوسم `<img>`. عندما يكون مكون Vue، يُعرض عبر `<component :is>`. إذا لم يُحدد، يُستخدم شعار Escalated الافتراضي.

### إعادة التسمية البيضاء الكاملة

تجاوز رموز التصميم الفردية للتحكم الكامل في مظهر اللوحة:

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

يُربط كل رمز بخاصية CSS مخصصة على `:root`. يمكنك أيضًا تجاوز هذه الخصائص مباشرة في CSS الخاص بك.

### خصائص CSS المخصصة للوحة

تحتوي جميع رموز اللوحة على قيم افتراضية مناسبة لكلا الوضعين الداكن والفاتح. عند تعيين `mode: 'light'`، تتبدل لوحة الألوان الافتراضية بالكامل تلقائيًا.

| خاصية CSS | مفتاح التكوين | الافتراضي الداكن | الافتراضي الفاتح | الوصف |
|-------------|------------|-------------|--------------|-------------|
| `--esc-panel-bg` | `bg` | `#000000` | `#f9fafb` | خلفية الصفحة |
| `--esc-panel-sidebar-bg` | `sidebarBg` | `#0a0a0a` | `#ffffff` | خلفية الشريط الجانبي |
| `--esc-panel-topbar-bg` | `topbarBg` | `rgba(0,0,0,0.8)` | `rgba(255,255,255,0.95)` | خلفية الشريط العلوي |
| `--esc-panel-surface` | `surface` | `rgba(23,23,23,0.6)` | `#ffffff` | البطاقات واللوحات |
| `--esc-panel-surface-alt` | `surfaceAlt` | `#0a0a0a` | `#f9fafb` | حقول الإدخال والأسطح المتداخلة |
| `--esc-panel-border` | `border` | `rgba(255,255,255,0.06)` | `#e5e7eb` | الحدود والفواصل |
| `--esc-panel-border-input` | `borderInput` | `rgba(255,255,255,0.1)` | `#d1d5db` | حدود حقول الإدخال |
| `--esc-panel-text` | `text` | `#ffffff` | `#111827` | النص الرئيسي |
| `--esc-panel-text-secondary` | `textSecondary` | `#e5e5e5` | `#374151` | التسميات والنص الأساسي |
| `--esc-panel-text-tertiary` | `textTertiary` | `#a3a3a3` | `#6b7280` | التسميات الثانوية |
| `--esc-panel-text-muted` | `textMuted` | `#737373` | `#9ca3af` | التلميحات والنصوص المؤقتة |
| `--esc-panel-accent` | `accent` | `#06b6d4` | `#3b82f6` | لون التمييز الرئيسي |
| `--esc-panel-accent-secondary` | `accentSecondary` | `#8b5cf6` | `#6366f1` | نهاية التدرج / لون التمييز الثانوي |
| `--esc-panel-accent-hover` | `accentHover` | `#22d3ee` | `#2563eb` | حالة تمرير التمييز |
| `--esc-panel-accent-secondary-hover` | `accentSecondaryHover` | `#a78bfa` | `#818cf8` | تمرير التمييز الثانوي |
| `--esc-panel-hover` | `hover` | `rgba(255,255,255,0.03)` | `rgba(0,0,0,0.02)` | خلفية تمرير الصفوف والعناصر |
| `--esc-panel-active` | `active` | `rgba(255,255,255,0.08)` | `#eff6ff` | خلفية عنصر التنقل النشط |

> **ملاحظة:** لا تتأثر ألوان مؤشرات الحالة والأولوية (open، closed، escalated، إلخ) بتخصيص اللوحة. تظل ثابتة للحفاظ على المعنى الدلالي عبر جميع عمليات النشر ذات العلامة التجارية.

### تجاوزات CSS فقط

إذا كنت تفضل تجاوز أنماط اللوحة بدون تكوين JavaScript، قم بتعيين خصائص CSS المخصصة مباشرة:

```css
:root {
  --esc-panel-accent: #e94560;
  --esc-panel-accent-secondary: #ff6b6b;
  --esc-panel-bg: #0f0f23;
  --esc-panel-sidebar-bg: #1a1a2e;
}
```

يعمل هذا جنبًا إلى جنب مع تكوين `theme.panel` أو بدلاً منه. تأخذ تجاوزات CSS الأسبقية عند تطبيقها بعد تهيئة الإضافة.
