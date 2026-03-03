## 1. gemの追加

```bash
$ bundle add escalated
```

## 2. インストーラーの実行

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. エンジンのマウント

`config/routes.rb`にエンジンを追加します：

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
