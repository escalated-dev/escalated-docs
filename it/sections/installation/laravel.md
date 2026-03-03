## 1. Installare il pacchetto

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Eseguire l'installer

Questo pubblica le migrazioni, la configurazione e imposta le tabelle del database.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Pubblicare la configurazione (opzionale)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Nota:** Le route vengono registrate automaticamente tramite il service provider. Non è necessario aggiungere nulla a `routes/web.php`.
