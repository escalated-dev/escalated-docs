Define dos gates en tu `AppServiceProvider`:

```php
use Illuminate\Support\Facades\Gate;

// Who can access the agent dashboard and manage tickets
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent || $user->is_admin
);

// Who can access admin settings (departments, SLAs, rules, etc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Los nombres de los gates son configurables a traves de `config/escalated.php` bajo `authorization.admin_gate` y `authorization.agent_gate`.
