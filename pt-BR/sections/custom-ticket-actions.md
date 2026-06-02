# Custom Ticket Actions

Custom ticket actions let your **host application add its own buttons to the agent ticket screen**. When an agent clicks one, Escalated dispatches an event your application handles however it likes — sync the ticket to a CRM, kick off a shipping label, post to Slack, anything.

Unlike [Macros](macros.md) (which bundle built-in actions) or [Workflows](workflows.md) (which react to events automatically), custom actions are an **extension point**: Escalated renders the button and fires the event; your code does the work.

## How it works

1. You register one or more actions in your application's Escalated configuration.
2. Visible actions appear as buttons on the agent ticket screen, and on the ticket detail API response under `custom_actions` (each with a `url` and HTTP `method`).
3. When an agent clicks a button, Escalated `POST`s to `/<prefix>/agent/tickets/{ticket}/actions/{action}`.
4. Escalated validates the action is **visible** (otherwise `404`) and **enabled** (otherwise `403`), records an internal note on the ticket for auditability, and dispatches the **custom action triggered** event.
5. Your application's listener handles the event.

## Defining an action

Every action has the same shape across frameworks:

| Field | Description |
|-------|-------------|
| `key` | Stable identifier, used in the action URL and the dispatched event. |
| `label` | Button text shown to the agent. |
| `variant` | Button style: `primary`, `secondary`, or `danger`. |
| `visible` | Whether the action appears for this ticket/agent. |
| `enabled` | Whether the button is clickable (vs. shown but disabled). |
| `confirmation` | Optional prompt shown before the action fires. |
| `metadata` | Arbitrary data passed through to the UI and the event (e.g. an `icon`). |

Each host framework registers actions using its own idiomatic mechanism — a config array (Laravel, Symfony, .NET, Spring, Phoenix, Django, AdonisJS, Rails, Go), a filter (WordPress), and/or a class/service for dynamic visibility. See your framework's plugin README for the exact syntax. For example, in Laravel:

```php
// config/escalated.php
'ticket_actions' => [
    'actions' => [
        [
            'key' => 'sync-crm',
            'label' => 'Sync CRM',
            'variant' => 'primary',
            'confirmation' => 'Sync this ticket to the CRM?',
            'metadata' => ['icon' => 'refresh-cw'],
        ],
    ],
],
```

For dynamic, per-ticket logic (visibility/enabled/label computed from the ticket and the current agent), provide an action **class** implementing your framework's `TicketAction` contract instead of a plain config entry.

## Handling the event

When the action fires, Escalated dispatches a **custom action triggered** event carrying the ticket, the action key, the triggering agent, an optional payload submitted by the UI, and the action's metadata. Subscribe to it the same way you subscribe to any other [Escalated event](events) — a listener (Laravel/NestJS), a signal receiver (Django), a notification subscriber (Rails), a `@EventListener` (Spring), a PubSub subscriber (Phoenix), a `do_action` hook (WordPress), the `IEscalatedEventDispatcher` (.NET), or the `OnCustomAction` callback (Go).

```php
use Escalated\Laravel\Events\TicketCustomActionTriggered;
use Illuminate\Support\Facades\Event;

Event::listen(TicketCustomActionTriggered::class, function (TicketCustomActionTriggered $event) {
    if ($event->action !== 'sync-crm') {
        return;
    }

    app(App\Services\CrmSync::class)->syncTicket($event->ticket, $event->user, $event->payload);
});
```

The event exposes the ticket, the action key, the triggering user, the payload, and the metadata. Escalated also records an internal note on the ticket each time an action is triggered, so there is always an audit trail of who ran what.

## Frontend

The agent ticket screen renders each visible action as a button (styled by `variant`, with a confirmation prompt when one is configured and a disabled state when `enabled` is false). This is built into the shared Escalated frontend — no per-application UI work is required. Custom frontends can read the ticket response's `customActions` / `custom_actions` collection and `POST` to each action's `url`.
