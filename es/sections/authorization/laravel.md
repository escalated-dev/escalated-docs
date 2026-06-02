Define dos gates en `App\Providers\AppServiceProvider::boot()` para Laravel 12+, o en `App\Providers\AuthServiceProvider::boot()` para Laravel 11 y anteriores:

```php
use Illuminate\Support\Facades\Gate;

// Quien puede acceder al panel de agentes y gestionar tickets
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Quien puede acceder a la configuracion de administracion (departamentos, SLAs, reglas, etc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Los nombres de los gates son configurables a traves de `config/escalated.php` bajo `authorization.admin_gate` y `authorization.agent_gate`.
