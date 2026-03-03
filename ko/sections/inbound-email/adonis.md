### 설정

```typescript
// config/escalated.ts
inboundEmail: {
  enabled: true,
  adapter: 'mailgun',
  address: 'support@yourapp.com',
  mailgunSigningKey: Env.get('ESCALATED_MAILGUN_SIGNING_KEY'),
}
```

### IMAP 폴링

```bash
# Cron or @adonisjs/scheduler
node ace escalated:poll-imap
```
