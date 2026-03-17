# Importing from Freshdesk

## Prerequisites

- A Freshdesk account on the **Growth plan or above** (API access is not available on the free Sprout plan)
- A Freshdesk API key (see below)
- Your Freshdesk domain (the part before `.freshdesk.com`, e.g. `acme`)

### Finding your Freshdesk API key

1. Log in to Freshdesk as an agent with admin permissions.
2. Click your avatar in the top-right corner and select **Profile Settings**.
3. Your API key is shown in the right-hand panel under **Your API Key**.

> **Note:** The API key is tied to the agent account you are logged in as. Use an admin account to ensure the importer has access to all tickets and groups.

## Using the import wizard

1. In Escalated, go to **Admin → Import** and select **Freshdesk**.
2. Enter your domain and API key, then click **Test connection**.
3. Review the field mappings. Defaults are pre-filled (see table below). Adjust any mappings you want to change.
4. Click **Start import**. The wizard moves to a progress view showing each entity type as it is processed.

The import fetches entity types in dependency order: agents → custom fields → departments → contacts → tickets → replies → attachments.

> **Note:** Freshdesk does not have a dedicated tags endpoint. Tags are collected from ticket records during ticket extraction and written as a separate entity type automatically — no manual step is needed.

## Using the CLI

```bash
$ php artisan escalated:import freshdesk
```

You will be prompted for your domain and API key. Pass `--no-interaction` to read credentials from environment variables instead:

```bash
ESCALATED_IMPORT_FRESHDESK_DOMAIN=acme \
ESCALATED_IMPORT_FRESHDESK_API_KEY=your-api-key \
php artisan escalated:import freshdesk --no-interaction
```

## Default field mappings

| Freshdesk field | Escalated field |
| --- | --- |
| `subject` | `title` |
| `description` | `body` |
| `status` | `status` |
| `priority` | `priority` |
| `responder_id` | `assigned_to` |
| `requester_id` | `requester` |
| `group_id` | `department` |
| `tags` | `tags` |

### Status mapping

| Freshdesk status (code) | Escalated status |
| --- | --- |
| `2` (Open) | `open` |
| `3` (Pending) | `waiting_on_customer` |
| `4` (Resolved) | `resolved` |
| `5` (Closed) | `closed` |

### Priority mapping

| Freshdesk priority (code) | Escalated priority |
| --- | --- |
| `1` (Low) | `low` |
| `2` (Medium) | `medium` |
| `3` (High) | `high` |
| `4` (Urgent) | `urgent` |

## Page 300 limit and adaptive date windowing

Freshdesk's ticket list API has a hard limit of 300 pages (30,000 records) per query. For accounts with large ticket histories, the adapter works around this limit automatically using **adaptive date windowing**:

1. The adapter splits the full ticket history into 30-day windows starting from 2010-01-01.
2. Within each window it pages through tickets filtered by `updated_since`.
3. If a window fills all 300 pages, it is automatically split in half and re-paged from the midpoint. This process repeats recursively until the window is small enough to fit within the page limit.

No configuration is required. The process is transparent and progress is tracked in the import job so it can be resumed if interrupted.

## Resuming a failed import

If an import job is interrupted, you can resume it from **Admin → Import** by clicking **Resume** next to the failed job. The adapter's cursor format encodes the current date window and page number, so it resumes from the exact point of failure.

From the CLI:

```bash
$ php artisan escalated:import freshdesk --resume=<job-id>
```

## Troubleshooting

**"Authentication failed" on test connection**
Verify the API key in your Freshdesk **Profile Settings**. Make sure you are using an admin account — agent-only accounts may not have access to all resources.

**"API access not available" error**
API access requires the Growth plan or above. Upgrade your Freshdesk subscription or contact Freshdesk support.

**Tickets appear to be missing**
The adapter imports tickets ordered by `updated_at` ascending within each date window. Tickets that have never been updated since creation may fall in an earlier window than expected. If specific tickets are missing, verify they exist in Freshdesk and have not been deleted.

**Attachment download URLs expire**
Freshdesk returns temporary signed URLs for attachments. If a download fails, the framework automatically re-fetches the parent conversation to obtain a fresh URL before retrying.
