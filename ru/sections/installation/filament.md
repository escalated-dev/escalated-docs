## 1. Установите пакеты

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Запустите установщик Escalated

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Зарегистрируйте плагин Filament

В вашем провайдере панели Filament:

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

> **Примечание:** Filament использует встроенные компоненты Livewire + Blade -- Inertia.js или Vue не требуются. Интерфейс следует дизайн-системе Filament. Основной функционал такой же, как у фронтенда на Inertia, но некоторые взаимодействия могут слегка отличаться.
