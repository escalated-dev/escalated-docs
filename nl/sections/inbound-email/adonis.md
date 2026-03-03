### Configuratie

```typescript
// config/escalated.ts
inboundEmail: {
  enabled: true,
  adapter: 'mailgun',
  address: 'support@yourapp.com',
  mailgunSigningKey: Env.get('ESCALATED_MAILGUN_SIGNING_KEY'),
}
```

### IMAP-polling

```bash
# Cron of @adonisjs/scheduler
node ace escalated:poll-imap
```
