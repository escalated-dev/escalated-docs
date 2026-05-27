## 1. パッケージのインストール

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. インストーラーの実行

マイグレーション、設定を公開し、データベーステーブルをセットアップします。

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. 設定の公開（任意）

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **注意：** ルートはサービスプロバイダー経由で自動的に登録されます。`routes/web.php`への追加は不要です。
