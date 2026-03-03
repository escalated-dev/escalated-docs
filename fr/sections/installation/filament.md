## 1. Installer les packages

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Executer l'installateur Escalated

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Enregistrer le plugin Filament

Dans votre panel provider Filament :

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

> **Remarque :** Filament utilise des composants natifs Livewire + Blade -- pas besoin d'Inertia.js ni de Vue. L'interface suit le systeme de design de Filament. Les fonctionnalites de base sont les memes que le frontend Inertia, mais certaines interactions peuvent differer legerement.
