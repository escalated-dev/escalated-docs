# Status & Prioritäten

Escalated behandelt Tickets als Zustandsmaschinen. Statusübergänge werden erzwungen und sind konfigurierbar.

## Status

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Prioritäten

- Low
- Medium
- High
- Urgent
- Critical

Übergänge sind über `config/escalated.php` unter dem Schlüssel `transitions` konfigurierbar.

Admins können benutzerdefinierte Status im Admin-Panel erstellen und verwalten (`/support/admin/statuses`).
