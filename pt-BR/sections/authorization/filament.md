Defina dois gates Laravel e depois referencie-os no plugin do Filament:

```php
Gate::define('escalated-agent', fn ($user) => $user->is_agent);
Gate::define('escalated-admin', fn ($user) => $user->is_admin);
```

```php
EscalatedFilamentPlugin::make()
    ->agentGate('escalated-agent')
    ->adminGate('escalated-admin')
```
