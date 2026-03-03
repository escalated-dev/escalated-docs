## 1. Paketi kurun

```bash
$ pip install escalated-django
```

## 2. Yüklü uygulamalara ekleyin

`settings.py` dosyanızda:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Migration'ları çalıştırın ve URL'leri ekleyin

```bash
$ python manage.py migrate
```

`urls.py` dosyanızda:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
