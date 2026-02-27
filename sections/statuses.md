# Statuses & Priorities

Escalated treats tickets as state machines. Status transitions are enforced and configurable.

## Statuses

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Priorities

- Low
- Medium
- High
- Urgent
- Critical

Transitions are configurable via `config/escalated.php` under the `transitions` key.

Admins can create and manage custom statuses in the admin panel (`/support/admin/statuses`).
