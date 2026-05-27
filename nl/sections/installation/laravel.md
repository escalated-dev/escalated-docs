## 1. Installeer het pakket

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Voer het installatieprogramma uit

Dit publiceert migraties, configuratie en stelt de databasetabellen in.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Publiceer de configuratie (optioneel)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Let op:** Routes worden automatisch geregistreerd via de service provider. Het is niet nodig iets toe te voegen aan `routes/web.php`.
