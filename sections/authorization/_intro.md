# Authorization

Escalated uses two authorization gates to control access to agent and admin views. Define these in your application to control who can manage tickets.

> **Note:** Escalated automatically shares `page.props.escalated` to all Inertia responses, containing the route prefix and the current user's agent/admin status.
