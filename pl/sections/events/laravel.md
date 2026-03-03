```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Dostępne zdarzenia**

- `TicketCreated` -- Nowe zgłoszenie utworzone
- `TicketStatusChanged` -- Zmiana statusu
- `TicketPriorityChanged` -- Aktualizacja priorytetu
- `TicketAssigned` -- Agent przypisany do zgłoszenia
- `TicketUnassigned` -- Agent usunięty ze zgłoszenia
- `ReplyCreated` -- Dodana odpowiedź publiczna
- `InternalNoteAdded` -- Wewnętrzna notatka agenta
- `TicketUpdated` -- Zmiana metadanych zgłoszenia
- `TicketReopened` -- Zgłoszenie przywrócone do stanu aktywnego
- `DepartmentChanged` -- Zmiana działu
- `TagAddedToTicket` -- Tag dodany do zgłoszenia
- `TagRemovedFromTicket` -- Tag usunięty ze zgłoszenia
- `SlaWarning` -- Zgłoszenie zbliża się do terminu SLA
- `SlaBreached` -- Termin SLA przekroczony
- `TicketEscalated` -- Zgłoszenie eskalowane przez regułę
- `TicketResolved` -- Zgłoszenie oznaczone jako rozwiązane
- `TicketClosed` -- Zgłoszenie zamknięte
