```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Eventos disponiveis**

- `TicketCreated` -- Novo ticket enviado
- `TicketStatusChanged` -- Transicao de status
- `TicketPriorityChanged` -- Prioridade atualizada
- `TicketAssigned` -- Agente atribuido ao ticket
- `TicketUnassigned` -- Agente removido do ticket
- `ReplyCreated` -- Resposta publica adicionada
- `InternalNoteAdded` -- Nota interna do agente
- `TicketUpdated` -- Metadados do ticket alterados
- `TicketReopened` -- Ticket movido de volta para estado ativo
- `DepartmentChanged` -- Departamento reatribuido
- `TagAddedToTicket` -- Tag aplicada ao ticket
- `TagRemovedFromTicket` -- Tag removida do ticket
- `SlaWarning` -- Ticket se aproximando do prazo de SLA
- `SlaBreached` -- Prazo de SLA perdido
- `TicketEscalated` -- Ticket escalonado por regra
- `TicketResolved` -- Ticket marcado como resolvido
- `TicketClosed` -- Ticket fechado
