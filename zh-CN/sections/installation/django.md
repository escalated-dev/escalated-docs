## 1. 安装包

```bash
$ pip install escalated-django
```

## 2. 添加到已安装应用

在`settings.py`中：

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. 运行迁移并添加URL

```bash
$ python manage.py migrate
```

在`urls.py`中：

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
