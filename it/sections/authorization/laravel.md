Definisci due gate in `App\Providers\AppServiceProvider::boot()` per Laravel 12+, oppure in `App\Providers\AuthServiceProvider::boot()` per Laravel 11 e versioni precedenti:

```php
use Illuminate\Support\Facades\Gate;

// Chi può accedere alla dashboard agente e gestire i ticket
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Chi può accedere alle impostazioni admin (dipartimenti, SLA, regole, ecc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

I nomi dei gate sono configurabili tramite `config/escalated.php` sotto `authorization.admin_gate` e `authorization.agent_gate`.
