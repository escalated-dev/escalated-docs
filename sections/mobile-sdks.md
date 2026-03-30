# Mobile SDKs

Escalated provides pre-built mobile SDKs for Flutter and React Native. Both SDKs offer a complete customer-facing support experience that connects to any Escalated backend via the REST API.

## Features

Both SDKs include:

- Login and registration screens
- Ticket list with search, status/priority filters, and pagination
- Ticket detail with reply thread, SLA timers, and status badges
- Create ticket with priority, department, and file attachments
- Knowledge base with article search and category filtering
- Guest ticket creation and viewing (no auth required)
- Settings with dark/light theme and language selection
- Internationalization (English, Spanish, French, German)
- Configurable auth hooks for custom authentication flows

## Flutter SDK

### Installation

```yaml
# pubspec.yaml
dependencies:
  escalated: ^1.0.0
```

### Usage

```dart
import 'package:escalated/escalated.dart';

// Configure the SDK
final config = EscalatedConfig(
  baseUrl: 'https://yourapp.com/support/api/v1',
);

// Use the pre-built widget
EscalatedApp(config: config)
```

### Auth Hooks

The Flutter SDK uses a hook-based auth system. The default implementation uses Bearer token auth with `flutter_secure_storage`. Override for custom flows:

```dart
class CustomAuthHooks extends DefaultAuthHooks {
  @override
  Future<Map<String, String>> getAuthHeaders() async {
    // Return your custom auth headers
    return {'Authorization': 'Bearer ${await getToken()}'};
  }
}
```

### Screens

| Screen | Description |
|--------|-------------|
| `LoginScreen` | Email/password login with error handling |
| `RegisterScreen` | Name, email, password registration |
| `TicketListScreen` | Pull-to-refresh list with filters and FAB |
| `TicketDetailScreen` | Full ticket with replies, SLA, close/reopen |
| `CreateTicketScreen` | Form with priority, department, attachments |
| `KBListScreen` | Searchable article list with categories |
| `KBArticleScreen` | Rendered HTML body with feedback buttons |
| `GuestCreateScreen` | Unauthenticated ticket submission |
| `GuestTicketScreen` | Token-based guest ticket viewing |
| `SettingsScreen` | Theme, language, logout |

---

## React Native SDK

### Installation

```bash
npm install @escalated-dev/escalated-react-native
```

### Usage

```tsx
import { EscalatedProvider } from '@escalated-dev/escalated-react-native';

function App() {
  return (
    <EscalatedProvider
      baseUrl="https://yourapp.com/support/api/v1"
    >
      {/* Your app content, or use the pre-built navigator */}
    </EscalatedProvider>
  );
}
```

### Pre-built Navigator

```tsx
import { createEscalatedNavigator } from '@escalated-dev/escalated-react-native';

const { EscalatedTabs, AuthStack, GuestStack } = createEscalatedNavigator();
```

### Auth Hooks

```typescript
import { AuthHooks } from '@escalated-dev/escalated-react-native';

const customAuth: AuthHooks = {
  onLogin: async (email, password) => { /* ... */ },
  onLogout: async () => { /* ... */ },
  getAuthHeaders: async () => ({ Authorization: `Bearer ${token}` }),
};
```

### Components

All components are exported individually for custom layouts:

| Component | Description |
|-----------|-------------|
| `StatusBadge` | Color-coded ticket status |
| `PriorityBadge` | Color-coded priority indicator |
| `SlaTimer` | Countdown with breach detection |
| `ReplyThread` | Chronological reply list |
| `ReplyComposer` | Text input with send button |
| `AttachmentList` | File list with icons |
| `FilePicker` | File selection with preview |
| `SatisfactionRating` | 5-star rating with comment |
| `EmptyState` | Placeholder for empty lists |
| `LoadingSkeleton` | Shimmer loading placeholder |

### Hooks

| Hook | Description |
|------|-------------|
| `useAuth` | Login, register, logout, current user |
| `useTickets` | Ticket list with filters and pagination |
| `useCreateTicket` | Create ticket mutation |
| `useReplyTicket` | Reply mutation |
| `useArticles` | Knowledge base articles |
| `useDepartments` | Department list |
| `useTheme` | Dark/light theme with system detection |
| `useI18n` | Translation function |

## Design Tokens

Both SDKs share the same design tokens for visual consistency:

| Token | Value |
|-------|-------|
| Primary | `#4f46e5` (Indigo 600) |
| Status: Open | `#3b82f6` (Blue) |
| Status: In Progress | `#f59e0b` (Amber) |
| Status: Resolved | `#10b981` (Green) |
| Status: Closed | `#6b7280` (Gray) |
| Priority: Low | `#6b7280` |
| Priority: High | `#f59e0b` |
| Priority: Critical | `#ef4444` (Red) |
