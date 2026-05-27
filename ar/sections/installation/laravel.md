## 1. تثبيت الحزمة

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. تشغيل المُثبِّت

ينشر هذا عمليات الترحيل والتكوين ويُعد جداول قاعدة البيانات.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. نشر التكوين (اختياري)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **ملاحظة:** تُسجل المسارات تلقائيًا عبر مزود الخدمة. لا حاجة لإضافة أي شيء إلى `routes/web.php`.
