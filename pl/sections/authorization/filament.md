Zdefiniuj dwie bramki Laravel, a następnie odwołaj się do nich we wtyczce Filament:

```php
Gate::define('escalated-agent', fn ($user) => $user->is_agent);
Gate::define('escalated-admin', fn ($user) => $user->is_admin);
```

```php
EscalatedFilamentPlugin::make()
    ->agentGate('escalated-agent')
    ->adminGate('escalated-admin')
```
