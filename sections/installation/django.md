## 1. Install the package

```bash
$ pip install escalated-django
```

## 2. Add to installed apps

In your `settings.py`:

```python
INSTALLED_APPS = [
    ...
    "escalated",
]
```

## 3. Run migrations and add URLs

```bash
$ python manage.py migrate
```

In your `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    ...
    path("support/", include("escalated.urls")),
]
```

## Headless mode (optional)

To run Escalated without the built-in Inertia UI, add this to your settings:

```python
ESCALATED = {
    "UI_ENABLED": False,
}
```

API routes, management commands, signals, and the plugin runtime continue to work normally.
