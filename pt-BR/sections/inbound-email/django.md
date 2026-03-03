### Configuracao

```python
# settings.py
ESCALATED = {
    "INBOUND_EMAIL_ENABLED": True,
    "INBOUND_EMAIL_ADAPTER": "mailgun",
    "INBOUND_EMAIL_ADDRESS": "support@yourapp.com",
    "MAILGUN_SIGNING_KEY": os.environ.get("ESCALATED_MAILGUN_SIGNING_KEY"),
}
```

### Polling IMAP

```bash
# crontab ou Celery beat
python manage.py poll_imap
```
