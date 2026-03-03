```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Evenements disponibles**

- `TicketCreated` -- Nouveau ticket soumis
- `TicketStatusChanged` -- Transition de statut
- `TicketPriorityChanged` -- Priorite mise a jour
- `TicketAssigned` -- Agent assigne au ticket
- `TicketUnassigned` -- Agent retire du ticket
- `ReplyCreated` -- Reponse publique ajoutee
- `InternalNoteAdded` -- Note interne de l'agent
- `TicketUpdated` -- Metadonnees du ticket modifiees
- `TicketReopened` -- Ticket remis en etat actif
- `DepartmentChanged` -- Departement reassigne
- `TagAddedToTicket` -- Etiquette appliquee au ticket
- `TagRemovedFromTicket` -- Etiquette retiree du ticket
- `SlaWarning` -- Ticket approchant de l'echeance SLA
- `SlaBreached` -- Echeance SLA depassee
- `TicketEscalated` -- Ticket escalade par une regle
- `TicketResolved` -- Ticket marque comme resolu
- `TicketClosed` -- Ticket cloture
