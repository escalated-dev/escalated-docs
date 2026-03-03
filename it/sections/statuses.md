# Stati e Priorità

Escalated tratta i ticket come macchine a stati. Le transizioni di stato sono applicate e configurabili.

## Stati

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Priorità

- Low
- Medium
- High
- Urgent
- Critical

Le transizioni sono configurabili tramite `config/escalated.php` sotto la chiave `transitions`.

Gli amministratori possono creare e gestire stati personalizzati nel pannello di amministrazione (`/support/admin/statuses`).
