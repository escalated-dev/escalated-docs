## 1. Agregar la gema

```bash
$ bundle add escalated
```

## 2. Ejecutar el instalador

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Montar el engine

Agrega el engine a tu `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
