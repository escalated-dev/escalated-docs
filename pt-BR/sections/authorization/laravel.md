Defina dois gates no seu `AppServiceProvider`:

```php
use Illuminate\Support\Facades\Gate;

// Quem pode acessar o painel do agente e gerenciar tickets
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent || $user->is_admin
);

// Quem pode acessar as configuracoes de administracao (departamentos, SLAs, regras, etc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Os nomes dos gates sao configuraveis em `config/escalated.php` nas chaves `authorization.admin_gate` e `authorization.agent_gate`.
