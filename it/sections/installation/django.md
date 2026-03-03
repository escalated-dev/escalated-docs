## 1. Installare il pacchetto

```bash
$ pip install escalated-django
```

## 2. Aggiungere alle app installate

Nel tuo `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Eseguire le migrazioni e aggiungere gli URL

```bash
$ python manage.py migrate
```

Nel tuo `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
