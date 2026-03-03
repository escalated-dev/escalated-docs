## 1. Paket installieren

```bash
$ pip install escalated-django
```

## 2. Zu installierten Apps hinzufügen

In Ihrer `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Migrationen ausführen und URLs hinzufügen

```bash
$ python manage.py migrate
```

In Ihrer `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
