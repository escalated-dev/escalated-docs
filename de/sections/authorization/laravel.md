Definieren Sie zwei Gates in Ihrem `AppServiceProvider`:

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

Gate-Namen sind über `config/escalated.php` unter `authorization.admin_gate` und `authorization.agent_gate` konfigurierbar.
