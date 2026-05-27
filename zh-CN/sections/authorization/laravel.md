在`AppServiceProvider`中定义两个门禁：

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

门禁名称可在`config/escalated.php`的`authorization.admin_gate`和`authorization.agent_gate`下配置。
