Zdefiniuj dwie bramki w swoim `AppServiceProvider`:

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

Nazwy bramek są konfigurowalne w pliku `config/escalated.php` pod kluczami `authorization.admin_gate` i `authorization.agent_gate`.
