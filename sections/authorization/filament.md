Define two Laravel gates, then reference them in the Filament plugin:

```php
Gate::define('escalated-agent', fn ($user) => $user->is_agent);
Gate::define('escalated-admin', fn ($user) => $user->is_admin);
```

```php
EscalatedFilamentPlugin::make()
    ->agentGate('escalated-agent')
    ->adminGate('escalated-admin')
```
