Authorization is handled entirely server-side. The Flutter package sends a Bearer token with each request, and your backend API controls what the authenticated user can access.

There are no client-side gates to define — the mobile app is a customer-facing UI, so agent and admin authorization checks only apply on the web.

## Checking Auth State

Use the `authProvider` to check whether the current user is authenticated:

```dart
final authState = ref.watch(authProvider);

if (authState.isAuthenticated) {
  // User is logged in, show ticket list
} else {
  // Show login screen
}
```

> **Note:** The `escalated-agent` and `escalated-admin` gates from your backend still apply to all API requests. The mobile app simply doesn't expose agent or admin views.
