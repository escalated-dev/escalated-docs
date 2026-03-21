# Authorization

Escalated uses two authorization gates to control access to agent and admin views. Define these in your application to control who can manage tickets.

> **Note:** Escalated automatically shares `page.props.escalated` to all Inertia responses, containing the route prefix and the current user's agent/admin status.

## Granular permissions

Escalated ships with **52 granular permissions** organized into logical groups:

| Group | Example permissions |
|---|---|
| **Tickets** | `tickets.view`, `tickets.create`, `tickets.update`, `tickets.delete`, `tickets.merge`, `tickets.assign`, `tickets.change_department` |
| **Conversations** | `conversations.reply`, `conversations.add_note`, `conversations.delete`, `conversations.edit` |
| **Users** | `users.view`, `users.create`, `users.update`, `users.delete`, `users.impersonate` |
| **Knowledge Base** | `kb.view`, `kb.create`, `kb.update`, `kb.delete`, `kb.publish` |
| **Reports** | `reports.view`, `reports.export`, `reports.scheduled` |
| **Admin** | `admin.settings`, `admin.departments`, `admin.sla`, `admin.macros`, `admin.automations`, `admin.roles`, `admin.integrations`, `admin.billing` |
| **Bulk Operations** | `bulk.update`, `bulk.delete`, `bulk.assign` |
| **Tags** | `tags.view`, `tags.create`, `tags.delete` |
| **SLA** | `sla.view`, `sla.manage`, `sla.override` |
| **Satisfaction** | `satisfaction.view`, `satisfaction.manage` |
| **Collaboration** | `collaboration.side_conversations`, `collaboration.followers`, `collaboration.shared_views` |

Each permission can be granted or denied independently per role.

## Default roles

Escalated includes three built-in roles:

### Admin

Full access to all 52 permissions. Admins can manage settings, roles, agents, departments, SLA policies, automations, and billing. Cannot be deleted.

### Agent

Standard support agent with permissions to manage tickets, conversations, and the knowledge base. Cannot access admin-level settings, roles, or billing.

- Tickets: view, create, update, assign
- Conversations: reply, add note
- Knowledge Base: view, create, update
- Tags: view, create
- Reports: view
- Collaboration: side conversations, followers

### Light Agent

Restricted role for part-time or external collaborators. Light agents can view tickets and add internal notes but cannot send public replies or modify ticket properties.

- Tickets: view
- Conversations: add note
- Knowledge Base: view
- Tags: view

## Custom roles

Create custom roles from `Admin -> Roles` to match your team's structure. Each custom role starts with no permissions -- toggle individual permissions on or off using the permission matrix.

### Creating a custom role

1. Navigate to **Admin -> Roles**
2. Click **New Role**
3. Enter a role name and optional description
4. Use the permission matrix to enable or disable each of the 52 permissions
5. Click **Save**

Assign the role to agents from the agent profile page or during agent creation.

## Permission matrix UI

The permission matrix is a grid that shows all permissions grouped by category. Each row is a permission and each column is a role. Toggle a cell to grant or revoke that permission for the role. Changes take effect immediately after saving -- no agent restart is required.
