`AppServiceProvider`에서 두 개의 게이트를 정의합니다:

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

게이트 이름은 `config/escalated.php`의 `authorization.admin_gate`와 `authorization.agent_gate`에서 설정할 수 있습니다.
