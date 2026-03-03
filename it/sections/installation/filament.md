## 1. Installare i pacchetti

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Eseguire l'installer di Escalated

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Registrare il plugin Filament

Nel tuo panel provider di Filament:

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

> **Nota:** Filament utilizza componenti nativi Livewire + Blade -- non è necessario Inertia.js o Vue. L'interfaccia segue il design system di Filament. Le funzionalità principali sono le stesse del frontend Inertia, ma alcune interazioni possono differire leggermente.
