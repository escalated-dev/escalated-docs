The React Native package retrieves user data from your backend API via the auth hooks system. There is no local User model to configure — authentication and user resolution happen server-side.

## Auth Hooks

Provide custom auth callbacks through the provider config:

```tsx
import { EscalatedProvider, AuthHooks } from '@escalated-dev/escalated-react-native';

const customHooks: AuthHooks = {
  onLogin: async (email, password) => {
    const response = await myAuthService.login(email, password);
    return {
      token: response.token,
      user: { name: response.user.name, email: response.user.email },
    };
  },
  onLogout: async () => {
    await myAuthService.logout();
  },
};

export default function App() {
  return (
    <EscalatedProvider config={{ apiBaseUrl: 'https://yourapp.com/support/api/v1', authHooks: customHooks }}>
      {/* ... */}
    </EscalatedProvider>
  );
}
```

> **Note:** The package sends a Bearer token with every API request. Your backend's `Ticketable` user model handles the rest.
