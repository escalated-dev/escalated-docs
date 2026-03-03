`AppServiceProvider` dosyanızda iki kapı tanımlayın:

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

Kapı isimleri `config/escalated.php` dosyasında `authorization.admin_gate` ve `authorization.agent_gate` altında yapılandırılabilir.
