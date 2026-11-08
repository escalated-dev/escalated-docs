# Management Commands

Each backend framework includes CLI commands for operations, maintenance, and setup.

> Management commands work regardless of the UI setting. All commands listed below function normally in headless mode.

## Setup

### install

Run the interactive setup wizard to configure Escalated.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:install` |
| Django | `python manage.py install` |

**Django installer behavior:**

1. Runs pending database migrations
2. Seeds default permissions and roles
3. Creates a default "General" department
4. Creates a default SLA policy
5. Optionally creates a superuser (interactive mode)
6. Prints URLs for admin panel, agent dashboard, customer portal, and API

Django accepts `--no-input`. Laravel accepts Artisan's `--no-interaction`; its installer publishes config and migrations and offers additional interactive setup. Inspect `php artisan escalated:install --help` for its own options.

## Plugin Management

### plugin

Manage installed plugins from the command line.

| Framework | Command |
|-----------|---------|
| Django | `python manage.py plugin <subcommand>` |
| Laravel | `php artisan escalated:plugin <subcommand>` |

**Subcommands:**

| Subcommand | Description |
|------------|-------------|
| `list` | Show all installed plugins with status |
| `activate <slug>` | Activate a plugin |
| `deactivate <slug>` | Deactivate a plugin |

## Scheduled Tasks

These commands should be run on a cron schedule.

### check-sla

Check all open tickets for SLA breaches and send warnings.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:check-sla` |
| Django | `python manage.py check_sla` |
| Rails | `bundle exec rake escalated:check_sla` |

Options differ by framework. The Laravel `escalated:check-sla` command has no `--warning-threshold` option.

### evaluate-escalations

Evaluate escalation rules against open tickets and trigger actions.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:evaluate-escalations` |
| Django | `python manage.py evaluate_escalations` |

### run-automations

Execute time-based automation rules.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:run-automations` |
| Django | `python manage.py run_automations` |

### close-resolved

Auto-close tickets that have been in "resolved" status for a configurable number of days.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:close-resolved` |
| Django | `python manage.py close_resolved` |

The Laravel command reads its age threshold from package configuration and has no `--days` or `--dry-run` option. Inspect Django command help for its options.

### poll-imap

Poll an IMAP mailbox for inbound emails and create/update tickets.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:poll-imap` |
| Django | `python manage.py poll_imap` |

## Maintenance

### purge-expired-data

Clean up expired tokens, old webhook deliveries, and stale import jobs.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:purge-expired` |
| Django | `python manage.py purge_expired_data` |

Laravel uses the configured retention policies and supports `--dry-run` and `--force`. It purges closed tickets, attachments, and audit logs, with the configured deletion/grace behavior. Django has its own cleanup command and options.

### purge-activities

Delete old ticket activity log entries beyond a retention period.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:purge-activities` |
| Django | `python manage.py purge_activities` |

Laravel accepts `--days` to override the configured retention period (default 90 days). It does not provide a dry-run option. Inspect the Django command help before running cleanup.

### seed-permissions

Initialize or refresh the default permission set and system roles. Safe to run multiple times (idempotent).

| Framework | Command |
|-----------|---------|
| Django | `python manage.py seed_permissions` |

## Data Import

### import

Import tickets and data from external platforms.

| Framework | Command |
|-----------|---------|
| Laravel | `php artisan escalated:import` |
| Django | `python manage.py escalated_import` |

Supported platforms: Zendesk, Freshdesk, Intercom, Help Scout. See [Importing Data](/docs/importing) for details.
