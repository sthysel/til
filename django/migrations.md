# migrations

When clearing out old migrations, remeber that the new built-in migration system is 
only switched on when a "migrations" module exists in the app.
```
migrations/__init__.py
```

It would have been nice if Django were more explicit with its erorr messages about that...
