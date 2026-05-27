## 1. Pakete einbinden

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Escalated-Installer ausführen

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Filament-Plugin registrieren

In Ihrem Filament Panel Provider:

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

> **Hinweis:** Filament verwendet native Livewire + Blade-Komponenten -- kein Inertia.js oder Vue erforderlich. Die Oberfläche folgt dem Filament-Designsystem. Die Kernfunktionalität ist identisch mit dem Inertia-Frontend, einige Interaktionen können sich jedoch leicht unterscheiden.
