# Tickets

Tickets are the core of Escalated. Each ticket is a long-lived state machine with a full conversation history, priority levels, assignment tracking, and SLA monitoring.

> **Note:** Every ticket gets a unique reference (e.g., `ESC-00001`) and supports custom statuses, priority levels, department assignment, tags, SLA tracking, and rich conversations with file attachments. All data lives in your database.

## Ticket types

Every ticket has a **type** that describes the nature of the request. Set the type from the ticket sidebar or during creation.

- **Question** -- The requester is asking for information. No underlying fault exists.
- **Problem** -- Something is broken or not working as expected. Problems can have many linked incidents.
- **Incident** -- A single occurrence of a known problem. Link incidents to a parent problem to resolve them together.
- **Task** -- An internal to-do item that may or may not originate from a customer request.

Ticket type is available as a condition in automations, macros, and SLA policies.

## Searching tickets

### Basic search

The search bar at the top of the ticket list performs a basic search across four fields:

- Subject
- Reference (e.g., `ESC-00042`)
- Description body text
- Requester name or email

Type a keyword and press Enter to filter the list instantly.

### Advanced search

Click the filter icon next to the search bar to open the advanced search panel. Combine any of the following filters:

- **Date range** -- filter by created or updated date
- **Tag name** -- match tickets that have a specific tag
- **Requester** -- filter by requester name or email
- **Has attachments** -- show only tickets with file attachments

Filters stack with AND logic. Remove a filter chip to broaden results.

## View tabs

The ticket list includes tab views for common workflows:

- **All Tickets** -- every ticket in the system (filtered by department if applicable)
- **Assigned to Me** -- tickets where you are the assigned agent
- **Unassigned** -- tickets with no agent assigned
- **Urgent** -- tickets with urgent or high priority
- **SLA Breaching** -- tickets that have breached or are about to breach an SLA target
- **Following** -- tickets you are following as a follower

## Column configuration

Click the **gear icon** in the top-right corner of the ticket list to toggle visible columns on or off. Choose which columns to display -- for example, requester, department, SLA status, last reply, or tags. Your column preferences are persisted in your browser's local storage, so they survive page reloads and sessions.

## Bulk actions

Select multiple tickets using the checkboxes and apply batch operations such as status changes, reassignment, tagging, and more. See [Bulk Actions](bulk-actions.md) for the full list of available operations.

## Advanced ticket workflows

- Ticket merge flow to combine duplicates while preserving history
- Linked tickets for related incident/problem workflows
- Side conversations for parallel internal/external coordination
- Light-agent support for restricted operational roles
- Custom field forms with conditional rules based on ticket context
