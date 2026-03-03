## 1. Instale o pacote

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. Execute o instalador

Isso publica migracoes, configuracao e configura as tabelas do banco de dados.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Publique a configuracao (opcional)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **Nota:** As rotas sao registradas automaticamente pelo service provider. Nao e necessario adicionar nada ao `routes/web.php`.
