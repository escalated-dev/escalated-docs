## 1. إضافة الجوهرة

```bash
$ bundle add escalated
```

## 2. تشغيل المُثبِّت

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. تركيب المحرك

أضف المحرك إلى `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
