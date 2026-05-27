Definisci due gate nel tuo `AppServiceProvider`:

```php
use Illuminate\Support\Facades\Gate;

// Chi può accedere alla dashboard agente e gestire i ticket
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent || $user->is_admin
);

// Chi può accedere alle impostazioni admin (dipartimenti, SLA, regole, ecc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

I nomi dei gate sono configurabili tramite `config/escalated.php` sotto `authorization.admin_gate` e `authorization.agent_gate`.
