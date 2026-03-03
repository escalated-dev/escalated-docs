```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Доступные события**

- `TicketCreated` -- Новый тикет создан
- `TicketStatusChanged` -- Изменение статуса
- `TicketPriorityChanged` -- Обновление приоритета
- `TicketAssigned` -- Агент назначен на тикет
- `TicketUnassigned` -- Агент удалён с тикета
- `ReplyCreated` -- Добавлен публичный ответ
- `InternalNoteAdded` -- Внутренняя заметка агента
- `TicketUpdated` -- Изменены метаданные тикета
- `TicketReopened` -- Тикет возвращён в активное состояние
- `DepartmentChanged` -- Отдел переназначен
- `TagAddedToTicket` -- Тег применён к тикету
- `TagRemovedFromTicket` -- Тег удалён с тикета
- `SlaWarning` -- Тикет приближается к дедлайну SLA
- `SlaBreached` -- Дедлайн SLA пропущен
- `TicketEscalated` -- Тикет эскалирован по правилу
- `TicketResolved` -- Тикет помечен как решённый
- `TicketClosed` -- Тикет закрыт
