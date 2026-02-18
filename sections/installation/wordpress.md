## 1. Install the plugin

```bash
$ wp plugin install escalated --activate
```

## 2. Configure settings

Navigate to **Escalated -> Settings** in wp-admin to configure departments, SLA policies, escalation rules, and email channels.

## 3. Add shortcodes

Place shortcodes on any page to give customers a support portal:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Note:** The WordPress plugin is self-contained -- it does not use Inertia.js. All UI is rendered via native WordPress admin screens and shortcode-powered frontend templates.
