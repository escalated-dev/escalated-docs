# Statussen en Prioriteiten

Escalated behandelt tickets als toestandsmachines. Statusovergangen worden afgedwongen en zijn configureerbaar.

## Statussen

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Prioriteiten

- Low
- Medium
- High
- Urgent
- Critical

Overgangen zijn configureerbaar via `config/escalated.php` onder de `transitions`-sleutel.

Beheerders kunnen aangepaste statussen aanmaken en beheren in het beheerpaneel (`/support/admin/statuses`).
