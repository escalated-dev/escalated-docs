## 1. Instalar el paquete

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Ejecutar el instalador

Esto publica las migraciones, la configuracion y prepara las tablas de la base de datos.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Publicar la configuracion (opcional)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Nota:** Las rutas se registran automaticamente a traves del service provider. No es necesario agregar nada a `routes/web.php`.
