## 1. Добавьте гем

```bash
$ bundle add escalated
```

## 2. Запустите установщик

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Подключите движок

Добавьте движок в `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
