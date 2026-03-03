# Statuts et priorites

Escalated traite les tickets comme des machines a etats. Les transitions de statut sont appliquees et configurables.

## Statuts

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Priorites

- Low
- Medium
- High
- Urgent
- Critical

Les transitions sont configurables via `config/escalated.php` sous la cle `transitions`.

Les administrateurs peuvent creer et gerer des statuts personnalises dans le panneau d'administration (`/support/admin/statuses`).
