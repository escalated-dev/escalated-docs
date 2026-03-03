## 1. Voeg de gem toe

```bash
$ bundle add escalated
```

## 2. Voer het installatieprogramma uit

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Koppel de engine

Voeg de engine toe aan je `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
