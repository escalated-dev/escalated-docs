كوّن دوال لامدا في المُهيِّئ:

```ruby
Escalated.configure do |config|
  config.admin_check = ->(user) { user.admin? }
  config.agent_check = ->(user) { user.agent? || user.admin? }
end
```
