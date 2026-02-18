Define two gates in your `AppServiceProvider`:

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

Gate names are configurable via `config/escalated.php` under `authorization.admin_gate` and `authorization.agent_gate`.
