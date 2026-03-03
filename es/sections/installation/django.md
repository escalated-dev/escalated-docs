## 1. Instalar el paquete

```bash
$ pip install escalated-django
```

## 2. Agregar a las aplicaciones instaladas

En tu `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Ejecutar migraciones y agregar URLs

```bash
$ python manage.py migrate
```

En tu `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
