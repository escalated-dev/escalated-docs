## 1. Instale os pacotes

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Execute o instalador do Escalated

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Registre o plugin do Filament

No seu panel provider do Filament:

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

> **Nota:** O Filament utiliza componentes nativos Livewire + Blade -- nao e necessario Inertia.js ou Vue. A interface segue o sistema de design do Filament. A funcionalidade principal e a mesma do frontend Inertia, mas algumas interacoes podem diferir ligeiramente.
