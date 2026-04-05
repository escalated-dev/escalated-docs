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

## Headless mode (optional)

To run Escalated without the built-in Inertia UI:

```ruby
# config/initializers/escalated.rb
Escalated.configure do |config|
  config.ui_enabled = false
end
```

API routes, Rake tasks, ActiveSupport notifications, and the plugin runtime continue to work normally.
