## 1. Paketi kurun

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Yükleyiciyi çalıştırın

Bu, migration'ları, yapılandırmayı yayınlar ve veritabanı tablolarını oluşturur.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Yapılandırmayı yayınlayın (isteğe bağlı)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Not:** Rotalar servis sağlayıcı aracılığıyla otomatik olarak kaydedilir. `routes/web.php` dosyasına herhangi bir şey eklemenize gerek yoktur.
