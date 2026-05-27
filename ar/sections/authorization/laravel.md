عرّف بوابتين في `App\Providers\AppServiceProvider::boot()` في Laravel 12+، أو في `App\Providers\AuthServiceProvider::boot()` في Laravel 11 والإصدارات الأقدم:

```php
use Illuminate\Support\Facades\Gate;

// من يمكنه الوصول إلى لوحة تحكم الوكيل وإدارة التذاكر
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// من يمكنه الوصول إلى إعدادات الإدارة (الأقسام، SLAs، القواعد، إلخ)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

أسماء البوابات قابلة للتكوين عبر `config/escalated.php` تحت `authorization.admin_gate` و `authorization.agent_gate`.
