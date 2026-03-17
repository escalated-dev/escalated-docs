# Importing from Intercom

## Prerequisites

- An Intercom workspace with **Developer Hub** access
- A Bearer token generated from your Intercom app (see below)
- The app must have the following permission scopes granted

### Required permission scopes

| Scope | Why it is needed |
| --- | --- |
| `Read admins` | Import agents |
| `Read conversations` | Import tickets (conversations) and replies |
| `Read contacts` | Import contacts |
| `Read tags` | Import tags |
| `Read teams` | Import departments (teams) |

### Generating a Bearer token

1. Go to the [Intercom Developer Hub](https://app.intercom.com/a/apps/_/developer-hub).
2. Click **New app** (or open an existing app you have created for integrations).
3. Under **Authentication**, select **Use access token**.
4. Grant the permission scopes listed above.
5. Copy the **Access token** shown at the top of the Authentication page.

> **Note:** The access token has the same permissions as the workspace admin who created it. Use a dedicated app to keep the token's scope minimal.

## Using the import wizard

1. In Escalated, go to **Admin → Import** and select **Intercom**.
2. Enter your access token, then click **Test connection**.
3. Review the field mappings. Defaults are pre-filled (see table below). Adjust any mappings you want to change.
4. Click **Start import**. The wizard moves to a progress view showing each entity type as it is processed.

The import fetches entity types in dependency order: agents → tags → departments (teams) → contacts → tickets (conversations) → replies (conversation parts) → attachments.

## Using the CLI

```bash
$ php artisan escalated:import intercom
```

You will be prompted for your access token. Pass `--no-interaction` to read credentials from environment variables instead:

```bash
ESCALATED_IMPORT_INTERCOM_TOKEN=your-access-token \
php artisan escalated:import intercom --no-interaction
```

## Default field mappings

| Intercom field | Escalated field |
| --- | --- |
| `title` (or first message excerpt) | `title` |
| `state` | `status` |
| `priority` | `priority` |
| `assignee` (admin only) | `assigned_to` |
| `contacts` (first contact) | `requester` |
| `team_assignee_id` | `department` |
| `tags` | `tags` |

### Status mapping

| Intercom state | Escalated status |
| --- | --- |
| `open` | `open` |
| `closed` | `closed` |
| `snoozed` | `waiting_on_agent` |

### Priority mapping

| Intercom priority | Escalated priority |
| --- | --- |
| `not_priority` | `medium` |
| `priority` | `high` |

### Conversation titles
Intercom conversations do not always have an explicit title. When no title is set, the adapter uses the first 100 characters of the source message body (HTML stripped) as the ticket title.

## Rate limits

Intercom allows **1,000 requests per minute**, which is generous compared to most helpdesk APIs. The adapter distributes requests evenly across 10-second windows and backs off automatically on HTTP 429 responses. Even very large Intercom workspaces typically import without significant throttling delays.

## Resuming a failed import

If an import job is interrupted, you can resume it from **Admin → Import** by clicking **Resume** next to the failed job.

From the CLI:

```bash
$ php artisan escalated:import intercom --resume=<job-id>
```

## Troubleshooting

**"Authentication failed" on test connection**
Confirm the access token is correct and that the app has not been deleted or had its access token rotated in the Developer Hub.

**Missing permission scope error**
If the test connection succeeds but certain entity types fail to import, the access token may be missing a required scope. Return to the Developer Hub, add the missing scope, and regenerate the token.

**Conversation parts are missing**
The adapter only imports content-bearing conversation parts: `comment` and `note`. Administrative event parts (assignment, open, close, snooze, etc.) are intentionally skipped.

**Attachment download URLs expire**
Intercom attachment URLs are temporary signed URLs. If a download fails due to expiry, the framework re-fetches the parent conversation part to obtain a fresh URL before retrying.

**Contacts show as "user" or "lead" — which is imported?**
Intercom's API v2 unifies leads and users into a single contacts resource. Both roles are imported and mapped to Escalated contacts. The role value (`user` or `lead`) is stored in the contact's metadata.
