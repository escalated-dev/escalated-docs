## 1. Установите пакет

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Запустите установщик

Публикует миграции, конфигурацию и создаёт таблицы базы данных.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Опубликуйте конфигурацию (опционально)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Примечание:** Маршруты регистрируются автоматически через сервис-провайдер. Добавлять что-либо в `routes/web.php` не нужно.
