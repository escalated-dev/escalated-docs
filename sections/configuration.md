# Configuration

Escalated works out of the box with sensible defaults. Configuration is optional but available for customization.

> **Configuration options**
>
> - `routes.prefix` -- The URL prefix for all Escalated routes (default: `support`)
> - `routes.middleware` -- Middleware applied to customer routes (default: `['web', 'auth']`)
> - `user_model` -- The user model class (default: `App\Models\User`)
> - `table_prefix` -- Prefix for database tables (default: `escalated_`)
> - `tickets.allow_customer_close` -- Whether customers can close their own tickets (default: `true`)
> - `tickets.auto_close_resolved_after_days` -- Auto-close resolved tickets after N days (default: `7`)
> - `sla.business_hours_only` -- Only count business hours for SLA targets (default: `false`)
> - `ui.enabled` -- Enable or disable the built-in Inertia UI (default: `true`)
> - `notifications.channels` -- Notification channels (default: `['mail', 'database']`)

## Admin settings and modules

Recent platform updates add configuration and management screens for:

- Custom fields with conditional visibility rules
- Custom statuses and business hours schedules
- Roles (RBAC), skills-based routing, and agent capacity
- Audit log review
- Automations and outbound webhooks
- CSAT survey behavior
- SSO and two-factor authentication
- Data retention policies and purge behavior
- Email channel settings
- Custom objects and records

## Headless mode

Escalated can run without the built-in Inertia UI. Set the UI toggle to disabled and the package provides only the backend: API routes, management commands, events, migrations, and the plugin runtime. Teams that want Blade, Livewire, Django templates, ERB, or any custom frontend can use Escalated as a headless ticketing engine.

When the UI is disabled:

- Agent, admin, customer, and guest web routes are not registered
- Inertia shared props / middleware are skipped
- The rendering layer is not loaded
- API routes, inbound email webhooks, commands, and plugin endpoints still work normally

> **Framework configuration**
>
> - **Laravel** -- set `ESCALATED_UI_ENABLED=false` in `.env` or `'ui' => ['enabled' => false]` in `config/escalated.php`
> - **Django** -- set `"UI_ENABLED": False` in your `ESCALATED` settings dict
> - **Rails** -- set `config.escalated.ui_enabled = false` in your initializer
> - **Filament** -- the Filament plugin is UI-only by design; disable it by removing the plugin from your panel provider. The underlying `escalated-laravel` package continues to provide core functionality.

### Custom rendering

When the UI is enabled, all controllers use a renderer abstraction instead of calling the UI framework directly. You can swap the default renderer with your own implementation:

**Laravel**

```php
// In a service provider
$this->app->singleton(
    \Escalated\Laravel\Contracts\EscalatedUiRenderer::class,
    \App\Support\BladeUiRenderer::class
);
```

**Django**

```python
# settings.py
ESCALATED = {
    "UI_RENDERER": "myapp.renderers.DjangoTemplateRenderer",
}
```

**Rails**

```ruby
# config/initializers/escalated.rb
Escalated.configure do |config|
  config.ui_renderer = MyApp::ErbRenderer.new
end
```

## Publishing assets

```bash
# Publish config file
php artisan vendor:publish --tag=escalated-config

# Publish email templates for customization
php artisan vendor:publish --tag=escalated-views

# Publish migrations (if you need to customize)
php artisan vendor:publish --tag=escalated-migrations
```
