Define callables in your settings:

```python
ESCALATED = {
    "ADMIN_CHECK": lambda user: user.is_staff,
    "AGENT_CHECK": lambda user: hasattr(user, "is_agent") and user.is_agent,
}
```
