# Importing from Zendesk

## Prerequisites

- A Zendesk account with **Admin** role
- A Zendesk API token (see below)
- Your Zendesk subdomain (the part before `.zendesk.com`, e.g. `acme`)

### Generating a Zendesk API token

1. In Zendesk, go to **Admin Center → Apps and Integrations → APIs → Zendesk API**.
2. Under **Token Access**, enable API token access if it is not already on.
3. Click **Add API token**, give it a description, and copy the token.

> **Note:** The token is only shown once. Store it securely before closing the dialog.

## Using the import wizard

1. In Escalated, go to **Admin → Import** and select **Zendesk**.
2. Enter your subdomain, admin email address, and API token, then click **Test connection**.
3. Review the field mappings. Defaults are pre-filled (see table below). Adjust any mappings you want to change.
4. Click **Start import**. The wizard moves to a progress view showing each entity type as it is processed.

The import fetches entity types in dependency order: agents → tags → custom fields → departments → contacts → tickets → replies → attachments.

## Using the CLI

```bash
$ php artisan escalated:import zendesk
```

You will be prompted for your subdomain, admin email, and API token. Pass `--no-interaction` to read credentials from environment variables instead:

```bash
ESCALATED_IMPORT_ZENDESK_SUBDOMAIN=acme \
ESCALATED_IMPORT_ZENDESK_EMAIL=admin@example.com \
ESCALATED_IMPORT_ZENDESK_TOKEN=your-api-token \
php artisan escalated:import zendesk --no-interaction
```

## Default field mappings

| Zendesk field | Escalated field |
| --- | --- |
| `subject` | `title` |
| `status` | `status` |
| `priority` | `priority` |
| `assignee_id` | `assigned_to` |
| `requester_id` | `requester` |
| `group_id` | `department` |
| `tags` | `tags` |

### Status mapping

| Zendesk status | Escalated status |
| --- | --- |
| `new` | `open` |
| `open` | `in_progress` |
| `pending` | `waiting_on_customer` |
| `hold` | `waiting_on_agent` |
| `solved` | `resolved` |
| `closed` | `closed` |

### Priority mapping

| Zendesk priority | Escalated priority |
| --- | --- |
| `low` | `low` |
| `normal` | `medium` |
| `high` | `high` |
| `urgent` | `urgent` |

## Resuming a failed import

If an import job is interrupted (server restart, timeout, etc.), you can resume it from **Admin → Import** by clicking **Resume** next to the failed job. The adapter uses cursor-based pagination, so it picks up from the last successfully processed batch without re-importing records.

From the CLI, pass the job ID:

```bash
$ php artisan escalated:import zendesk --resume=<job-id>
```

## Troubleshooting

**"Authentication failed" on test connection**
Confirm that your email is entered in the form `admin@example.com` (not `admin@example.com/token`) and that Token Access is enabled in Zendesk Admin Center.

**Tickets are missing**
Zendesk's incremental export API only returns tickets updated since epoch 0. Deleted tickets are excluded. Archived tickets in Zendesk's long-term storage may not appear in the incremental export.

**Rate limit errors during import**
The adapter backs off automatically on HTTP 429 responses, respecting the `Retry-After` header. If you see persistent throttling, contact Zendesk support to request a temporary rate limit increase.

**Custom field values are not imported**
Only non-system custom fields are imported. System fields (subject, description, status, priority, group, assignee) are mapped directly and are not surfaced as custom fields.
