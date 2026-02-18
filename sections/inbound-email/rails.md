### Configuration

```ruby
# config/initializers/escalated.rb
Escalated.configure do |config|
  config.inbound_email_enabled = true
  config.inbound_email_adapter = :mailgun
  config.inbound_email_address = "support@yourapp.com"
  config.mailgun_signing_key = ENV["ESCALATED_MAILGUN_SIGNING_KEY"]
end
```

### IMAP Polling

```yaml
# config/recurring.yml (Solid Queue)
poll_imap:
  class: Escalated::PollImapJob
  schedule: every minute
```
