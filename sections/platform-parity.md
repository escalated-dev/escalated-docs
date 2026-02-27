# Platform Parity Features

The `feature/platform-parity` work across `escalated` (shared frontend) and `escalated-laravel` (backend adapter) adds a broad set of production features.

## Admin configuration and governance

- Custom fields and forms, including drag-and-drop ordering and conditional visibility rules
- Custom ticket statuses
- Business hours schedules
- Agent roles and permission controls
- Skills management and skills-based routing
- Agent capacity management
- Outbound webhooks with delivery logs and retry support
- Time-based automations
- CSAT survey settings
- SSO settings (SAML/JWT options)
- Two-factor authentication controls
- Email channel settings
- Data retention policies and purge controls
- Custom objects with record CRUD

## Ticket operations and collaboration

- Ticket merging
- Linked tickets for problem/incident workflows
- Side conversations on tickets
- Real-time collision warnings and typing indicators
- Light-agent support for restricted agent roles
- Knowledge panel in the ticket sidebar

## Knowledge base and reporting

- Customer-facing knowledge base (`/support/kb`)
- Admin knowledge base management (articles and categories)
- Expanded reports:
  - Dashboard KPIs
  - Agent productivity
  - SLA achievement
  - CSAT reporting

## Frontend and extension improvements

- New shared components for parity workflows (ticket linking, merge dialog, side conversations, capacity, reports)
- Context panel framework and sandbox placeholder page for extension-oriented UI work
- Expanded plugin hooks for richer extension use-cases
- Storybook stories and screenshot workflow for UI regression visibility
