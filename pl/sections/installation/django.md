## 1. Zainstaluj pakiet

```bash
$ pip install escalated-django
```

## 2. Dodaj do zainstalowanych aplikacji

W swoim `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Uruchom migracje i dodaj adresy URL

```bash
$ python manage.py migrate
```

W swoim `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
