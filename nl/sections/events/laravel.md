```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Beschikbare events**

- `TicketCreated` -- Nieuw ticket ingediend
- `TicketStatusChanged` -- Statusovergang
- `TicketPriorityChanged` -- Prioriteit bijgewerkt
- `TicketAssigned` -- Agent toegewezen aan ticket
- `TicketUnassigned` -- Agent verwijderd van ticket
- `ReplyCreated` -- Openbaar antwoord toegevoegd
- `InternalNoteAdded` -- Interne notitie van agent
- `TicketUpdated` -- Ticketmetadata gewijzigd
- `TicketReopened` -- Ticket terug naar actieve status
- `DepartmentChanged` -- Afdeling opnieuw toegewezen
- `TagAddedToTicket` -- Tag toegepast op ticket
- `TagRemovedFromTicket` -- Tag verwijderd van ticket
- `SlaWarning` -- Ticket nadert SLA-deadline
- `SlaBreached` -- SLA-deadline gemist
- `TicketEscalated` -- Ticket geescaleerd door regel
- `TicketResolved` -- Ticket gemarkeerd als opgelost
- `TicketClosed` -- Ticket gesloten
