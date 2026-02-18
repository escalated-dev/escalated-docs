```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Available events**

- `TicketCreated` -- New ticket submitted
- `TicketStatusChanged` -- Status transition
- `TicketAssigned` -- Agent assigned to ticket
- `ReplyCreated` -- Public reply added
- `InternalNoteAdded` -- Agent internal note
- `SlaBreached` -- SLA deadline missed
- `TicketEscalated` -- Ticket escalated by rule
- `TicketResolved` -- Ticket marked resolved
- `TicketClosed` -- Ticket closed
