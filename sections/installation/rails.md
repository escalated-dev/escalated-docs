## 1. Add the gem

```bash
$ bundle add escalated
```

## 2. Run the installer

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Mount the engine

Add the engine to your `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
