## 1. パッケージのインストール

```bash
$ pip install escalated-django
```

## 2. インストール済みアプリへの追加

`settings.py`に以下を追加します：

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. マイグレーションの実行とURLの追加

```bash
$ python manage.py migrate
```

`urls.py`に以下を追加します：

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```
