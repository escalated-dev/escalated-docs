## 1. Installer le package

```bash
$ pip install escalated-django
```

## 2. Ajouter aux applications installees

Dans votre `settings.py` :

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Executer les migrations et ajouter les URLs

```bash
$ python manage.py migrate
```

Dans votre `urls.py` :

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
