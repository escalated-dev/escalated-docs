## 1. Установите пакет

```bash
$ pip install escalated-django
```

## 2. Добавьте в установленные приложения

В `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Запустите миграции и добавьте URL-адреса

```bash
$ python manage.py migrate
```

В `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
