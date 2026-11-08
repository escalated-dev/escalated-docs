# Automations

The condition and action names below describe the Laravel AutomationRunner. Other adapters must be checked separately.

Automations are **admin-configured, time-based rules** that run on a recurring schedule and update tickets automatically. They are designed for things you can't react to with an event — for example, "close any ticket that's been waiting more than 7 days." Silence has no trigger, so a [Workflow](workflows.md) can't handle this case; an Automation can.

> **Picking the right tool:** Escalated has three automation surfaces — [Workflows](workflows.md) (admin, event-driven), Automations (admin, time-based), and [Macros](macros.md) (agent, manual). See [Workflows, Automations, and Macros](automation-types.md) for the comparison and a decision tree.

> **Note:** Automations require a running scheduler. See [Scheduling](scheduling.md) for setup instructions.

## How automations work

Each automation has three parts:

1. **Conditions** -- criteria a ticket must match for the automation to fire
2. **Actions** -- changes applied to matching tickets
3. **Scheduler** -- how often the host runs the automation command

When the scheduler ticks, Escalated evaluates every active automation against open tickets. Tickets that satisfy all conditions receive the configured actions.

## Available conditions

Combine any of the following conditions. All conditions use AND logic -- every condition must be true for the automation to match.

- **status** -- ticket has a specific status (e.g., open, pending, solved)
- **priority** -- ticket priority matches a value (low, normal, high, urgent)
- **ticket_type** -- ticket type is question, problem, incident, or task
- **subject_contains** -- ticket subject includes a keyword or phrase
- **assigned** -- ticket is assigned to any agent (or a specific agent)
- **assigned** -- use `unassigned` or `assigned` as the value
- **department_id** -- ticket belongs to a specific department

- **hours_since_created** -- age threshold in hours
- **hours_since_updated** -- time since last update
- **hours_since_assigned** -- approximates assignment age using updated_at on assigned tickets

## Available actions

Each automation can perform one or more actions in order:

- **change_status** -- change the ticket status
- **change_priority** -- change the ticket priority
- **set_ticket_type** -- change the ticket type
- **assign** -- assign the ticket to a specific agent
- **add_tag** -- add a tag to the ticket

## Example: auto-categorization

Automatically set the ticket type to Problem when the subject contains "bug":

- **Condition:** `subject_contains` = `bug`
- **Condition:** `ticket_type` = `question` (only recategorize questions)
- **Action:** `set_ticket_type` = `problem`
- **Action:** `add_tag` = `auto-categorized`

This keeps your reporting accurate without requiring agents to manually triage every ticket.

## Managing automations

Admins create and edit automations from `Admin -> Automations`. The builder interface lets you add conditions and actions visually, toggle automations on or off, and configure your host scheduler.

## Scheduler setup

Automations depend on the application scheduler. If the scheduler is not running, automations will not execute. See [Scheduling](scheduling.md) for instructions on configuring the cron entry or queue worker for your framework.
