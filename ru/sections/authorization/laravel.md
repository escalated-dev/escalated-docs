Определите два гейта в `AppServiceProvider`:

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

Имена гейтов настраиваются через `config/escalated.php` в разделе `authorization.admin_gate` и `authorization.agent_gate`.
