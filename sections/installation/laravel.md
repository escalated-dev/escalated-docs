## 1. Require the package

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Run the installer

This publishes migrations, config, and sets up the database tables.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Publish the configuration (optional)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Note:** Routes register automatically via the service provider. No need to add anything to `routes/web.php`.
