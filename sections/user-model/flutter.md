The Flutter package retrieves user data from your backend API via the auth hooks system. There is no local User model to configure — authentication and user resolution happen server-side.

## Auth Hooks

Override `AuthHooks` to plug in your own authentication logic:

```dart
class MyAuthHooks extends AuthHooks {
  @override
  Future<AuthResult> onLogin(String email, String password) async {
    // Call your auth API, return token + user info
    final response = await myAuthService.login(email, password);
    return AuthResult(
      token: response.token,
      user: AuthUser(
        name: response.user.name,
        email: response.user.email,
      ),
    );
  }

  @override
  Future<void> onLogout() async {
    await myAuthService.logout();
  }
}
```

Pass your hooks to the config:

```dart
EscalatedConfig(
  apiBaseUrl: 'https://yourapp.com/support/api/v1',
  authHooks: MyAuthHooks(),
)
```

> **Note:** The package sends a Bearer token with every API request. Your backend's `Ticketable` user model handles the rest.
