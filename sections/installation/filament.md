## 1. Require the packages

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Run the Escalated installer

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Register the Filament plugin

In your Filament panel provider:

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

> **Note:** Filament uses native Livewire + Blade components -- no Inertia.js or Vue needed. The UI follows Filament's design system. Core functionality is the same as the Inertia frontend, but some interactions may differ slightly.
