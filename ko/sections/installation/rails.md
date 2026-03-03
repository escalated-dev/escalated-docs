## 1. gem 추가

```bash
$ bundle add escalated
```

## 2. 인스톨러 실행

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. 엔진 마운트

`config/routes.rb`에 엔진을 추가합니다:

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
