## 1. تثبيت الحزمة

```bash
$ pip install escalated-django
```

## 2. الإضافة إلى التطبيقات المثبتة

في `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. تشغيل عمليات الترحيل وإضافة الروابط

```bash
$ python manage.py migrate
```

في `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
