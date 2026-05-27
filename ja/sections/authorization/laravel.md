`AppServiceProvider`で2つのゲートを定義します：

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

ゲート名は`config/escalated.php`の`authorization.admin_gate`と`authorization.agent_gate`で設定可能です。
