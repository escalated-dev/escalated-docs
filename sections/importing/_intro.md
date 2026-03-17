# Importing from Another Helpdesk

Escalated includes a built-in import system that lets you migrate tickets, contacts, agents, and conversation history from your existing helpdesk. A separate adapter plugin is required for each source platform.

## Supported platforms

| Platform | Plugin slug |
| --- | --- |
| Zendesk | `escalated-plugin-import-zendesk` |
| Freshdesk | `escalated-plugin-import-freshdesk` |
| Help Scout | `escalated-plugin-import-helpscout` |
| Intercom | `escalated-plugin-import-intercom` |

## How it works

The import system is split into two layers:

- **Core framework** — built into Escalated. Manages import jobs, tracks progress, writes records to the database, and handles retries. You do not need to configure this separately.
- **Adapter plugins** — one per source platform. Each adapter knows how to authenticate with the source API, page through its data, and normalize records into the format the core framework expects.

The adapter registers itself via the `import.adapters` filter hook, and the core framework discovers it automatically at runtime.

## General setup

1. Install the adapter plugin for your source platform (see the platform-specific guide for the plugin slug and any platform prerequisites).
2. In the Escalated admin panel, navigate to **Admin → Import**.
3. Select your source platform from the list of available adapters.
4. Enter the required credentials and click **Test connection**.
5. Review the default field mappings and adjust as needed.
6. Click **Start import** to begin.

The import runs in the background. You can monitor progress from the **Admin → Import** page and resume any interrupted job from the same screen.
