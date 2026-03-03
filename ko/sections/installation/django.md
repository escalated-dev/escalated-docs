## 1. 패키지 설치

```bash
$ pip install escalated-django
```

## 2. 설치된 앱에 추가

`settings.py`에 다음을 추가합니다:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. 마이그레이션 실행 및 URL 추가

```bash
$ python manage.py migrate
```

`urls.py`에 다음을 추가합니다:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
