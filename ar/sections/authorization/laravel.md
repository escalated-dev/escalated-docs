حدد بوابتين في `AppServiceProvider`:

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

أسماء البوابات قابلة للتكوين عبر `config/escalated.php` تحت `authorization.admin_gate` و `authorization.agent_gate`.
