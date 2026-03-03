## 1. Dodaj gem

```bash
$ bundle add escalated
```

## 2. Uruchom instalator

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Zamontuj silnik

Dodaj silnik do swojego `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
