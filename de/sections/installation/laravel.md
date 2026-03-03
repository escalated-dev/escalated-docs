## 1. Paket einbinden

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Installer ausführen

Dies veröffentlicht Migrationen, Konfiguration und richtet die Datenbanktabellen ein.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Konfiguration veröffentlichen (optional)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Hinweis:** Routen werden automatisch über den Service Provider registriert. Sie müssen nichts zu `routes/web.php` hinzufügen.
