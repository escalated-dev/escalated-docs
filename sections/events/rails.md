Events are dispatched via `ActiveSupport::Notifications`. Subscribe with `ActiveSupport::Notifications.subscribe("escalated.ticket_created")`.

> Events work in both UI-enabled and headless modes.
