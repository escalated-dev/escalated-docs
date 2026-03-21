# Automations

Automations are time-based rules that run on a recurring schedule to update tickets automatically. Unlike macros (which agents trigger manually), automations execute in the background and apply to every ticket that matches their conditions.

> **Note:** Automations require a running scheduler. See [Scheduling](scheduling.md) for setup instructions.

## How automations work

Each automation has three parts:

1. **Conditions** -- criteria a ticket must match for the automation to fire
2. **Actions** -- changes applied to matching tickets
3. **Schedule** -- how often the automation runs (e.g., every 15 minutes, hourly, daily)

When the scheduler ticks, Escalated evaluates every active automation against all tickets. Tickets that satisfy all conditions receive the configured actions.

## Available conditions

Combine any of the following conditions. All conditions use AND logic -- every condition must be true for the automation to match.

- **status** -- ticket has a specific status (e.g., open, pending, solved)
- **priority** -- ticket priority matches a value (low, normal, high, urgent)
- **ticket_type** -- ticket type is question, problem, incident, or task
- **subject_contains** -- ticket subject includes a keyword or phrase
- **assigned** -- ticket is assigned to any agent (or a specific agent)
- **unassigned** -- ticket has no agent assigned
- **department** -- ticket belongs to a specific department
- **tags** -- ticket has (or does not have) specific tags
- **created_before** -- ticket was created before a relative time (e.g., 48 hours ago)
- **created_after** -- ticket was created after a relative time
- **sla_breached** -- ticket has breached its SLA first-response or resolution target

## Available actions

Each automation can perform one or more actions in order:

- **set_status** -- change the ticket status
- **set_priority** -- change the ticket priority
- **set_ticket_type** -- change the ticket type
- **assign_to** -- assign the ticket to a specific agent
- **add_tag** -- add a tag to the ticket
- **remove_tag** -- remove a tag from the ticket
- **send_notification** -- send an email notification to the requester, assigned agent, or a custom address
- **close** -- close the ticket
- **escalate** -- escalate the ticket according to the configured escalation rules

## Example: auto-categorization

Automatically set the ticket type to Problem when the subject contains "bug":

- **Condition:** `subject_contains` = `bug`
- **Condition:** `ticket_type` = `question` (only recategorize questions)
- **Action:** `set_ticket_type` = `problem`
- **Action:** `add_tag` = `auto-categorized`

This keeps your reporting accurate without requiring agents to manually triage every ticket.

## Managing automations

Admins create and edit automations from `Admin -> Automations`. The builder interface lets you add conditions and actions visually, toggle automations on or off, and set the run frequency.

## Scheduler setup

Automations depend on the application scheduler. If the scheduler is not running, automations will not execute. See [Scheduling](scheduling.md) for instructions on configuring the cron entry or queue worker for your framework.
