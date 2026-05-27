Zdefiniuj dwie bramki w `App\Providers\AppServiceProvider::boot()` dla Laravel 12+ albo w `App\Providers\AuthServiceProvider::boot()` dla Laravel 11 i starszych:

```php
use Illuminate\Support\Facades\Gate;

// Kto moze uzyskac dostep do panelu agenta i zarzadzac zgloszeniami
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Kto moze uzyskac dostep do ustawien administracyjnych (dzialy, SLA, reguly itd.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Nazwy bramek są konfigurowalne w pliku `config/escalated.php` pod kluczami `authorization.admin_gate` i `authorization.agent_gate`.
