```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Available events**

- `TicketCreated` -- New ticket submitted
- `TicketStatusChanged` -- Status transition
- `TicketPriorityChanged` -- Priority updated
- `TicketAssigned` -- Agent assigned to ticket
- `TicketUnassigned` -- Agent removed from ticket
- `ReplyCreated` -- Public reply added
- `InternalNoteAdded` -- Agent internal note
- `TicketUpdated` -- Ticket metadata changed
- `TicketReopened` -- Ticket moved back to active state
- `DepartmentChanged` -- Department reassigned
- `TagAddedToTicket` -- Tag applied to ticket
- `TagRemovedFromTicket` -- Tag removed from ticket
- `SlaWarning` -- Ticket approaching SLA deadline
- `SlaBreached` -- SLA deadline missed
- `TicketEscalated` -- Ticket escalated by rule
- `TicketResolved` -- Ticket marked resolved
- `TicketClosed` -- Ticket closed
