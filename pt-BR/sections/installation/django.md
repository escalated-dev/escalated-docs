## 1. Instale o pacote

```bash
$ pip install escalated-django
```

## 2. Adicione aos apps instalados

No seu `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Execute as migracoes e adicione as URLs

```bash
$ python manage.py migrate
```

No seu `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
