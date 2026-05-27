Definissez deux gates dans `App\Providers\AppServiceProvider::boot()` pour Laravel 12+, ou dans `App\Providers\AuthServiceProvider::boot()` pour Laravel 11 et les versions anterieures :

```php
use Illuminate\Support\Facades\Gate;

// Qui peut acceder au tableau de bord agent et gerer les tickets
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Qui peut acceder aux parametres admin (departements, SLAs, regles, etc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Les noms des gates sont configurables via `config/escalated.php` sous `authorization.admin_gate` et `authorization.agent_gate`.
