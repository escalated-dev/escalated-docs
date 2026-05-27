Definiere zwei Gates in `App\Providers\AppServiceProvider::boot()` fuer Laravel 12+ oder in `App\Providers\AuthServiceProvider::boot()` fuer Laravel 11 und aelter:

```php
use Illuminate\Support\Facades\Gate;

// Wer auf das Agent-Dashboard zugreifen und Tickets verwalten kann
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Wer auf Admin-Einstellungen zugreifen kann (Abteilungen, SLAs, Regeln usw.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Gate-Namen sind über `config/escalated.php` unter `authorization.admin_gate` und `authorization.agent_gate` konfigurierbar.
