## 1. Paketleri kurun

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Escalated yükleyicisini çalıştırın

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Filament eklentisini kaydedin

Filament panel sağlayıcınızda:

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

> **Not:** Filament yerel Livewire + Blade bileşenlerini kullanır -- Inertia.js veya Vue gerekmez. Arayüz, Filament'in tasarım sistemini takip eder. Temel işlevsellik Inertia ön yüzüyle aynıdır, ancak bazı etkileşimler biraz farklılık gösterebilir.
