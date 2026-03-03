## 1. Gem'i ekleyin

```bash
$ bundle add escalated
```

## 2. Yükleyiciyi çalıştırın

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Motoru bağlayın

Motoru `config/routes.rb` dosyanıza ekleyin:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
