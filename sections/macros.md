# Macros

Macros are **agent-applied, manual one-click action bundles**. An agent picks a macro from a dropdown on a specific ticket, clicks "apply," and every action in the bundle runs at once — change the status, set the priority, assign an agent, add a reply, and so on.

Macros are deliberately *not* a rules engine. They have no conditions and no triggers; they just package up a sequence of actions for an agent to apply with a single click.

> **Picking the right tool:** Escalated has three automation surfaces — [Workflows](workflows.md) (admin, event-driven), [Automations](automations.md) (admin, time-based), and Macros (agent, manual). See [Workflows, Automations, and Macros](automation-types.md) for the comparison and a decision tree.

## Macro actions

Each macro contains one or more actions that execute in order:

- **Change status** -- set the ticket status
- **Change priority** -- set the ticket priority
- **Assign agent** -- assign the ticket to a specific agent
- **Change department** -- move the ticket to a department
- **Add tags** -- apply tags to the ticket
- **Send reply** -- add a public reply to the conversation
- **Add note** -- add an internal note visible only to agents

## Shared vs. personal macros

- **Shared macros** are visible to all agents and managed by admins
- **Personal macros** are visible only to the agent who created them

Admins manage macros from the `Admin -> Macros` page. The action builder lets you add, reorder, and configure each step visually.
