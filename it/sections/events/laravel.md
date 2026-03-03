```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Eventi disponibili**

- `TicketCreated` -- Nuovo ticket inviato
- `TicketStatusChanged` -- Transizione di stato
- `TicketPriorityChanged` -- Priorità aggiornata
- `TicketAssigned` -- Agente assegnato al ticket
- `TicketUnassigned` -- Agente rimosso dal ticket
- `ReplyCreated` -- Risposta pubblica aggiunta
- `InternalNoteAdded` -- Nota interna dell'agente
- `TicketUpdated` -- Metadati del ticket modificati
- `TicketReopened` -- Ticket riportato allo stato attivo
- `DepartmentChanged` -- Dipartimento riassegnato
- `TagAddedToTicket` -- Tag applicato al ticket
- `TagRemovedFromTicket` -- Tag rimosso dal ticket
- `SlaWarning` -- Ticket in avvicinamento alla scadenza SLA
- `SlaBreached` -- Scadenza SLA superata
- `TicketEscalated` -- Ticket sottoposto a escalation dalla regola
- `TicketResolved` -- Ticket contrassegnato come risolto
- `TicketClosed` -- Ticket chiuso
