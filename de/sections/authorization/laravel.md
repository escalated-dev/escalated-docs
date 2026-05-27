Define two gates in `App\Providers\AppServiceProvider::boot()` for Laravel 12+, or `App\Providers\AuthServiceProvider::boot()` for Laravel 11 and earlier:

```php
use Illuminate\Support\Facades\Gate;

// Who can access the agent dashboard and manage tickets
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Who can access admin settings (departments, SLAs, rules, etc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Gate-Namen sind über `config/escalated.php` unter `authorization.admin_gate` und `authorization.agent_gate` konfigurierbar.
