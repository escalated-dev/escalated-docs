# Workflows, Automations, and Macros

Escalated has three distinct ways to automate ticket actions. They look similar at a glance — all three apply changes to tickets — but they answer **different questions** and run at **different times**. Picking the right one matters.

This page is the canonical comparison. Each individual feature has its own dedicated page:

- **[Workflows](workflows.md)** — admin, event-driven
- **[Automations](automations.md)** — admin, time-based
- **[Macros](macros.md)** — agent, manual

---

## Quick comparison

| | Workflows | Automations | Macros |
|---|---|---|---|
| **Who configures it** | Admin | Admin | Any agent (or admin) |
| **When does it run** | The moment something happens to a ticket | On a schedule (every few minutes) | When an agent clicks a button |
| **What triggers it** | Domain events: `ticket.created`, `reply.created`, `ticket.assigned`, `ticket.status_changed`, `ticket.updated` | Cron tick — scans every open ticket | Agent on a specific ticket |
| **Conditions** | Field-level filters on the triggering ticket | Time-based filters: `hours_since_created`, `hours_since_updated`, etc. | None |
| **Scope** | One ticket — the one the event fires on | Every ticket that currently matches | One ticket — the one the agent is viewing |
| **Cancellable** | No (runs to completion) | Author-determined | Confirmed before running |

---

## Decision tree

Use this to pick the right tool when you're designing a new automation rule.

### 1. Does the action need to run **the moment something happens** on a ticket?

For example:
- "When a ticket is created with subject containing 'refund', auto-assign to billing"
- "When a customer replies, change status from `waiting_on_customer` back to `open`"
- "When a high-priority ticket is created, notify the on-call channel"

**→ Workflow.** Subscribe to the appropriate event, set conditions, configure actions.

Workflows fire synchronously with the event, so the side effect happens immediately. They're the right choice for any reactive rule that should trigger on a state change.

### 2. Does the action need to run on tickets based on **how long they've been in some state**?

For example:
- "Auto-close any ticket that's been resolved for more than 7 days"
- "Send a reminder to agents about tickets unassigned for more than 4 hours"
- "Escalate any high-priority ticket idle for more than 30 minutes"

**→ Automation.** Define a `hours_since_*` condition; the runner sweeps every few minutes.

Workflows can't do this because *no event fires when nothing happens*. Silence has no trigger. The cron-driven Automation runner is the right tool for stale-ticket handling and time-based escalations.

### 3. Is a human (agent) deciding when to apply it to a specific ticket?

For example:
- One-click "Escalate to tier 2" — sets tag, priority, status, clears assignee
- "Mark spam" — sets status to `closed`, adds an internal note, applies a tag
- "Apply standard greeting" — inserts a canned response

**→ Macro.** No conditions, no triggers — just "agent clicks a button, all the actions in the bundle execute."

Agents pick from a dropdown on the ticket detail page. Each macro can be shared across all agents or scoped to a single agent.

---

## Why three separate systems?

You might wonder: can't one rules engine cover all three? In practice, no — each one has a different operational profile.

- **Workflows can't be time-triggered.** The Workflow engine listens for events. To make Workflows handle "auto-close after 48h" you'd need a synthetic time-tick event and a "stale ticket" condition vocabulary — that's just an Automation reinvented inside a Workflow.

- **Automations can't react to events.** The Automation runner fires every few minutes. By the time it fires, an event-driven side effect (like assigning a ticket the moment it's created) is already several minutes late.

- **Macros could be a "manual-trigger Workflow" in theory** — but in practice agents need a **short curated list** on the ticket detail page, with no conditions to think about. Adding the Workflow data model (triggers, condition trees, stop-on-match logic) to Macros would just clutter the UX.

So the three systems are deliberately distinct, and each is purpose-built for its job.

---

## Often-confused situations

### "I want to apply X every time a ticket is opened"

→ **Workflow** with trigger `ticket.created`. The action runs the instant the ticket exists.

### "I want to apply X if a ticket has been waiting more than 24h"

→ **Automation** with condition `hours_since_updated > 24`. The runner sweeps periodically and applies the action to every match.

### "I want a one-click button to escalate a ticket"

→ **Macro**. Bundle the actions; agents apply them with one click on the specific ticket.

### "I want to send a follow-up email 3 days after a ticket is resolved"

→ **Automation** with condition `status = resolved AND hours_since_updated > 72` and an `add_note` or `send_reply` action. (You might also use a Workflow's `delay` action — see Workflows for the deferred-action pattern.)

### "I want to auto-merge duplicate tickets"

Either could work, depending on your detection strategy:
- A **Workflow** on `ticket.created` could detect duplicates if you have a synchronous duplicate-detection condition (subject match, etc.)
- An **Automation** could sweep periodically for duplicates using a more expensive check

If freshness matters (avoid double-routing), use a Workflow. If the check is heavy and stale-by-a-few-minutes is fine, use an Automation.

---

## See also

- [Workflows](workflows.md) — full reference for the event-driven engine
- [Automations](automations.md) — full reference for the time-based engine
- [Macros](macros.md) — full reference for agent-applied bundles
- [Scheduling](scheduling.md) — how the Automation cron is configured per framework
