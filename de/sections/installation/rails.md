## 1. Gem hinzufügen

```bash
$ bundle add escalated
```

## 2. Installer ausführen

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. Engine einbinden

Fügen Sie die Engine zu Ihrer `config/routes.rb` hinzu:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
