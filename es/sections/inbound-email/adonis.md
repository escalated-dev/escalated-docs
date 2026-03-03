### Configuracion

```typescript
// config/escalated.ts
inboundEmail: {
  enabled: true,
  adapter: 'mailgun',
  address: 'support@yourapp.com',
  mailgunSigningKey: Env.get('ESCALATED_MAILGUN_SIGNING_KEY'),
}
```

### Sondeo IMAP

```bash
# Cron or @adonisjs/scheduler
node ace escalated:poll-imap
```
