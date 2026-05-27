Definissez deux gates dans votre `AppServiceProvider` :

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

Les noms des gates sont configurables via `config/escalated.php` sous `authorization.admin_gate` et `authorization.agent_gate`.
