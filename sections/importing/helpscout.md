# Importing from Help Scout

## Prerequisites

- A Help Scout account with access to **My Apps** (any paid plan)
- An OAuth app created in Help Scout with an App ID and App Secret (see below)

### Creating a Help Scout OAuth app

1. In Help Scout, click your avatar in the top-right corner and select **Your Profile**.
2. In the left sidebar, click **My Apps**, then click **Create My App**.
3. Give the app a name (e.g. "Escalated Import"), enter any valid redirect URL (not used for this flow), and click **Create**.
4. Copy the **App ID** and **App Secret** shown on the app detail page.

The adapter uses the OAuth 2.0 client credentials grant, so no browser redirect or user interaction is required during the import. The App ID and App Secret are used directly.

## Using the import wizard

1. In Escalated, go to **Admin → Import** and select **Help Scout**.
2. Enter your App ID and App Secret, then click **Test connection**.
3. Review the field mappings. Defaults are pre-filled (see table below). Adjust any mappings you want to change.
4. Click **Start import**. The wizard moves to a progress view showing each entity type as it is processed.

The import fetches entity types in dependency order: agents → tags → departments (mailboxes) → contacts → tickets (conversations) → replies (threads) → attachments.

## Using the CLI

```bash
$ php artisan escalated:import helpscout
```

You will be prompted for your App ID and App Secret. Pass `--no-interaction` to read credentials from environment variables instead:

```bash
ESCALATED_IMPORT_HELPSCOUT_APP_ID=your-app-id \
ESCALATED_IMPORT_HELPSCOUT_APP_SECRET=your-app-secret \
php artisan escalated:import helpscout --no-interaction
```

## Default field mappings

| Help Scout field | Escalated field |
| --- | --- |
| `subject` | `title` |
| `status` | `status` |
| `assignee` | `assigned_to` |
| `primaryCustomer` | `requester` |
| `mailboxId` | `department` |
| `tags` | `tags` |

### Status mapping

| Help Scout status | Escalated status |
| --- | --- |
| `active` | `open` |
| `pending` | `waiting_on_customer` |
| `closed` | `closed` |
| `spam` | `closed` |

> **Note:** Help Scout does not have a ticket priority field. All imported tickets are assigned `medium` priority by default. You can update priorities in bulk after the import using Escalated's bulk actions.

## Rate limits

Help Scout's API allows **200 requests per minute**. The adapter respects `Retry-After` headers on HTTP 429 responses and backs off automatically. Large accounts with tens of thousands of conversations may take longer to import than accounts on higher-rate-limit platforms. Plan accordingly and avoid running other API-heavy integrations concurrently during the import.

## Resuming a failed import

If an import job is interrupted, you can resume it from **Admin → Import** by clicking **Resume** next to the failed job.

From the CLI:

```bash
$ php artisan escalated:import helpscout --resume=<job-id>
```

## Troubleshooting

**"Authentication failed" on test connection**
Confirm the App ID and App Secret are copied exactly as shown in Help Scout My Apps. Note that App ID is distinct from App Secret — double-check you have not swapped the two values.

**Some conversations are missing**
Help Scout's conversations endpoint returns active, pending, and closed conversations. Spam conversations are imported as closed. Deleted conversations are not returned by the API and cannot be recovered.

**Merged conversations appear as a 301 redirect**
When a conversation has been merged in Help Scout, the API returns a 301 redirect to the surviving conversation. The adapter follows redirects automatically; merged conversations will not appear as duplicates.

**Thread types other than messages and notes are not imported**
The adapter only imports thread types that carry content: `message`, `customer`, and `note`. System thread types (reassign, move, lineitem, forward, phone, chat) are skipped.
