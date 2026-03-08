Events are dispatched server-side through your backend's native event system. The React Native package does not implement a client-side event bus.

## Reactive Data

The package uses React Query, which automatically handles cache invalidation when mutations succeed. When a user creates a ticket, adds a reply, or changes a status, the relevant queries re-fetch automatically.

```tsx
import { useCreateTicket, useTickets } from '@escalated-dev/escalated-react-native';

function TicketListScreen() {
  const { data: tickets } = useTickets();
  const createTicket = useCreateTicket(); // invalidates ticket list query on success

  return (
    // Ticket list stays current — no manual refresh needed
  );
}
```

No manual event listeners or refresh logic is needed — React Query handles cache invalidation for you.

> **Note:** If you need to react to server-side events (e.g., real-time agent replies), configure push notifications through your backend and handle them at the platform level.
