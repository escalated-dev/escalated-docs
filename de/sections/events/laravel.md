```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Verfügbare Events**

- `TicketCreated` -- Neues Ticket eingereicht
- `TicketStatusChanged` -- Statusübergang
- `TicketPriorityChanged` -- Priorität aktualisiert
- `TicketAssigned` -- Agent dem Ticket zugewiesen
- `TicketUnassigned` -- Agent vom Ticket entfernt
- `ReplyCreated` -- Öffentliche Antwort hinzugefügt
- `InternalNoteAdded` -- Interne Agenten-Notiz
- `TicketUpdated` -- Ticket-Metadaten geändert
- `TicketReopened` -- Ticket in aktiven Zustand zurückversetzt
- `DepartmentChanged` -- Abteilung neu zugewiesen
- `TagAddedToTicket` -- Tag auf Ticket angewendet
- `TagRemovedFromTicket` -- Tag vom Ticket entfernt
- `SlaWarning` -- Ticket nähert sich der SLA-Frist
- `SlaBreached` -- SLA-Frist überschritten
- `TicketEscalated` -- Ticket durch Regel eskaliert
- `TicketResolved` -- Ticket als gelöst markiert
- `TicketClosed` -- Ticket geschlossen
