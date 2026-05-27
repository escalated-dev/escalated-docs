Laravel 12+ icin `App\Providers\AppServiceProvider::boot()` icinde, Laravel 11 ve oncesi icin `App\Providers\AuthServiceProvider::boot()` icinde iki gate tanimlayin:

```php
use Illuminate\Support\Facades\Gate;

// Agent paneline erisebilen ve ticketlari yonetebilen kullanicilar
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Admin ayarlarina erisebilen kullanicilar (departmanlar, SLA lar, kurallar vb.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Kapı isimleri `config/escalated.php` dosyasında `authorization.admin_gate` ve `authorization.agent_gate` altında yapılandırılabilir.
