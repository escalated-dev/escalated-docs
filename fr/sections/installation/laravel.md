## 1. Installer le package

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Executer l'installateur

Cela publie les migrations, la configuration et prepare les tables de la base de donnees.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Publier la configuration (optionnel)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Remarque :** Les routes sont enregistrees automatiquement via le service provider. Il n'est pas necessaire d'ajouter quoi que ce soit a `routes/web.php`.
