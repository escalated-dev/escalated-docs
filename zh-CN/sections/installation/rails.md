## 1. 添加gem

```bash
$ bundle add escalated
```

## 2. 运行安装程序

```bash
$ rails generate escalated:install
$ rails db:migrate
```

## 3. 挂载引擎

将引擎添加到`config/routes.rb`：

```ruby
Rails.application.routes.draw do
  mount Escalated::Engine, at: "/support"
end
```
