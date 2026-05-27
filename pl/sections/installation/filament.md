## 1. Zainstaluj pakiety

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Uruchom instalator Escalated

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Zarejestruj wtyczkę Filament

W swoim providerze panelu Filament:

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

> **Uwaga:** Filament korzysta z natywnych komponentów Livewire + Blade -- nie wymaga Inertia.js ani Vue. Interfejs jest zgodny z systemem projektowym Filament. Podstawowa funkcjonalność jest taka sama jak w frontendzie Inertia, ale niektóre interakcje mogą się nieznacznie różnić.
