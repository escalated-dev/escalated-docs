## 1. Require the package

```bash
composer require escalated-dev/escalated-laravel
```

## 2. Run the installer

This publishes migrations, config, and sets up the database tables.

```bash
php artisan escalated:install
php artisan migrate
```

## 3. Publish the configuration (optional)

```bash
php artisan vendor:publish --tag=escalated-config
```

> **Note:** Routes register automatically via the service provider. No need to add anything to `routes/web.php`.

## Headless mode (optional)

To run Escalated without the built-in Inertia UI, add this to your `.env`:

```
ESCALATED_UI_ENABLED=false
```

In headless mode, API routes, management commands, events, and the plugin runtime continue to work. See [Configuration](../configuration.md) for details on custom renderers.
