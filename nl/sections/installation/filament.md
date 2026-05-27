## 1. Installeer de pakketten

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Voer het Escalated-installatieprogramma uit

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Registreer de Filament-plugin

In je Filament-panelprovider:

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

> **Let op:** Filament gebruikt native Livewire + Blade-componenten -- geen Inertia.js of Vue nodig. De UI volgt het designsysteem van Filament. De kernfunctionaliteit is dezelfde als de Inertia-frontend, maar sommige interacties kunnen enigszins afwijken.
