# Statusy i priorytety

Escalated traktuje zgłoszenia jako maszyny stanów. Przejścia między statusami są wymuszane i konfigurowalne.

## Statusy

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Priorytety

- Low
- Medium
- High
- Urgent
- Critical

Przejścia są konfigurowalne w pliku `config/escalated.php` pod kluczem `transitions`.

Administratorzy mogą tworzyć i zarządzać niestandardowymi statusami w panelu administracyjnym (`/support/admin/statuses`).
