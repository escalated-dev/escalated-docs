## 1. Instalar los paquetes

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Ejecutar el instalador de Escalated

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Registrar el plugin de Filament

En tu panel provider de Filament:

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

> **Nota:** Filament utiliza componentes nativos de Livewire + Blade -- no se necesita Inertia.js ni Vue. La interfaz sigue el sistema de diseno de Filament. La funcionalidad principal es la misma que el frontend de Inertia, pero algunas interacciones pueden diferir ligeramente.
