## 1. Aggiungere la gem

```bash
$ bundle add escalated
```

## 2. Eseguire l'installer

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Montare l'engine

Aggiungi l'engine al tuo `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
