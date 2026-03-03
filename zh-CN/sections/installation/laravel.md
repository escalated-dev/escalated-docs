## 1. 安装包

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. 运行安装程序

发布迁移文件、配置并设置数据库表。

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. 发布配置（可选）

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **注意：** 路由通过服务提供者自动注册。无需在`routes/web.php`中添加任何内容。
