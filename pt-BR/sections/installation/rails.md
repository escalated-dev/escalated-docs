## 1. Adicione a gem

```bash
$ bundle add escalated
```

## 2. Execute o instalador

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Monte o engine

Adicione o engine ao seu `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
