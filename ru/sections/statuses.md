# Статусы и приоритеты

Escalated обрабатывает тикеты как конечные автоматы. Переходы между статусами контролируются и настраиваются.

## Статусы

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Приоритеты

- Low
- Medium
- High
- Urgent
- Critical

Переходы настраиваются через `config/escalated.php` в разделе `transitions`.

Администраторы могут создавать и управлять настраиваемыми статусами в панели администрирования (`/support/admin/statuses`).
