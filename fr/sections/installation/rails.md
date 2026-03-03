## 1. Ajouter la gem

```bash
$ bundle add escalated
```

## 2. Executer l'installateur

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Monter le engine

Ajoutez le engine a votre `config/routes.rb` :

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
