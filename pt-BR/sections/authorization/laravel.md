Define two gates in `App\Providers\AppServiceProvider::boot()` for Laravel 12+, or `App\Providers\AuthServiceProvider::boot()` for Laravel 11 and earlier:

```php
use Illuminate\Support\Facades\Gate;

// Quem pode acessar o painel do agente e gerenciar tickets
Gate::define('escalated-agent', fn ($user) =>
    $user->is_agent
);

// Quem pode acessar as configuracoes de administracao (departamentos, SLAs, regras, etc.)
Gate::define('escalated-admin', fn ($user) =>
    $user->is_admin
);
```

Os nomes dos gates sao configuraveis em `config/escalated.php` nas chaves `authorization.admin_gate` e `authorization.agent_gate`.
