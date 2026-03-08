Events are dispatched server-side through your backend's native event system. The Flutter package does not implement a client-side event bus.

## Reactive Data

The package uses Riverpod providers that automatically refresh data when mutations occur. When a user creates a ticket, adds a reply, or changes a status, the relevant providers invalidate and re-fetch automatically.

```dart
// Ticket list stays up-to-date after creating a new ticket
final tickets = ref.watch(ticketListProvider);

// Replies refresh after posting
final replies = ref.watch(ticketRepliesProvider(ticketId));
```

No manual event listeners or refresh logic is needed — the provider system handles cache invalidation for you.

> **Note:** If you need to react to server-side events (e.g., real-time agent replies), configure push notifications through your backend and handle them at the platform level.
