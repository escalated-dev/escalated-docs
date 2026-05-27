Define two gates in `App\Providers\AppServiceProvider::boot()` for Laravel 12+, or `App\Providers\AuthServiceProvider::boot()` for Laravel 11 and earlier:

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
