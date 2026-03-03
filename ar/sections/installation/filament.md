## 1. تثبيت الحزم

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. تشغيل مُثبِّت Escalated

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. تسجيل إضافة Filament

في مزود لوحة Filament الخاص بك:

```php
use Escalated\Filament\EscalatedFilamentPlugin;

public function panel(Panel $panel): Panel
{
    return $panel
        ->plugin(
            EscalatedFilamentPlugin::make()
                ->navigationGroup('Support')
                ->agentGate('escalated-agent')
                ->adminGate('escalated-admin')
        );
}
```

> **ملاحظة:** يستخدم Filament مكونات Livewire + Blade الأصلية -- لا حاجة لـ Inertia.js أو Vue. تتبع الواجهة نظام تصميم Filament. الوظائف الأساسية هي نفسها مع واجهة Inertia، لكن بعض التفاعلات قد تختلف قليلاً.
