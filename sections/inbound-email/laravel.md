### Configuration

```bash
# .env
ESCALATED_INBOUND_EMAIL=true
ESCALATED_INBOUND_ADDRESS=support@yourapp.com

# Mailgun
ESCALATED_INBOUND_ADAPTER=mailgun
ESCALATED_MAILGUN_SIGNING_KEY=your-signing-key

# Postmark
ESCALATED_INBOUND_ADAPTER=postmark
ESCALATED_POSTMARK_INBOUND_TOKEN=your-token

# AWS SES
ESCALATED_INBOUND_ADAPTER=ses
ESCALATED_SES_TOPIC_ARN=arn:aws:sns:us-east-1:...

# IMAP
ESCALATED_INBOUND_ADAPTER=imap
ESCALATED_IMAP_HOST=imap.gmail.com
ESCALATED_IMAP_USERNAME=support@yourapp.com
ESCALATED_IMAP_PASSWORD=your-app-password
```

### IMAP Polling

```php
// routes/console.php
Schedule::command('escalated:poll-imap')->everyMinute();
```
