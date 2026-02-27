# Tickets

Tickets are the core of Escalated. Each ticket is a long-lived state machine with a full conversation history, priority levels, assignment tracking, and SLA monitoring.

> **Note:** Every ticket gets a unique reference (e.g., `ESC-00001`) and supports custom statuses, priority levels, department assignment, tags, SLA tracking, and rich conversations with file attachments. All data lives in your database.

## Advanced ticket workflows

- Ticket merge flow to combine duplicates while preserving history
- Linked tickets for related incident/problem workflows
- Side conversations for parallel internal/external coordination
- Light-agent support for restricted operational roles
- Custom field forms with conditional rules based on ticket context
