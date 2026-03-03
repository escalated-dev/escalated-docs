## 1. Installeer het pakket

```bash
$ pip install escalated-django
```

## 2. Voeg toe aan geinstalleerde apps

In je `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Voer migraties uit en voeg URL's toe

```bash
$ python manage.py migrate
```

In je `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
