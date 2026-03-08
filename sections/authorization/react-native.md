Authorization is handled entirely server-side. The React Native package sends a Bearer token with each request, and your backend API controls what the authenticated user can access.

There are no client-side gates to define — the mobile app is a customer-facing UI, so agent and admin authorization checks only apply on the web.

## Checking Auth State

Use the `useAuth` hook to access the current user and authentication status:

```tsx
import { useAuth } from '@escalated-dev/escalated-react-native';

function ProfileScreen() {
  const { user, isAuthenticated } = useAuth();

  if (!isAuthenticated) {
    return <LoginScreen />;
  }

  return <Text>Welcome, {user.name}</Text>;
}
```

> **Note:** The `escalated-agent` and `escalated-admin` gates from your backend still apply to all API requests. The mobile app simply doesn't expose agent or admin views.
