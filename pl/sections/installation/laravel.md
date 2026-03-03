## 1. Zainstaluj pakiet

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Uruchom instalator

Publikuje migracje, konfigurację i przygotowuje tabele bazy danych.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Opublikuj konfigurację (opcjonalnie)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Uwaga:** Trasy rejestrują się automatycznie przez service provider. Nie musisz dodawać niczego do `routes/web.php`.
