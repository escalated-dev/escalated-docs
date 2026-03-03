```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Eventos disponibles**

- `TicketCreated` -- Nuevo ticket enviado
- `TicketStatusChanged` -- Transicion de estado
- `TicketPriorityChanged` -- Prioridad actualizada
- `TicketAssigned` -- Agente asignado al ticket
- `TicketUnassigned` -- Agente removido del ticket
- `ReplyCreated` -- Respuesta publica agregada
- `InternalNoteAdded` -- Nota interna del agente
- `TicketUpdated` -- Metadatos del ticket modificados
- `TicketReopened` -- Ticket devuelto a estado activo
- `DepartmentChanged` -- Departamento reasignado
- `TagAddedToTicket` -- Etiqueta aplicada al ticket
- `TagRemovedFromTicket` -- Etiqueta removida del ticket
- `SlaWarning` -- Ticket acercandose al limite de SLA
- `SlaBreached` -- Limite de SLA incumplido
- `TicketEscalated` -- Ticket escalado por regla
- `TicketResolved` -- Ticket marcado como resuelto
- `TicketClosed` -- Ticket cerrado
