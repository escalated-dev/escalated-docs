Define two gates in `App\Providers\AppServiceProvider::boot()` for Laravel 12+, or `App\Providers\AuthServiceProvider::boot()` for Laravel 11 and earlier:

```php
use Illuminate\Support\Facades\Gate;

// Wie toegang heeft tot het agentdashboard en tickets kan beheren
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Wie toegang heeft tot beheerinstellingen (afdelingen, SLA's, regels, enz.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Gatenamen zijn configureerbaar via `config/escalated.php` onder `authorization.admin_gate` en `authorization.agent_gate`.
