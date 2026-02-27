# Agent Collaboration

Keep your support team in sync with real-time presence indicators and pinned internal notes. No external tools needed.

## Collision detection

When multiple agents open the same ticket, each agent sees an avatar indicator showing who else is currently viewing. This prevents duplicate replies and wasted effort.

- Avatar stack with initials of other viewers
- "Also viewing" tooltip on hover
- Polls every 30 seconds -- lightweight, cache-based (no database table required)

## Typing indicators

Agents can broadcast active typing state while composing replies so teammates can avoid overlapping responses.

- Real-time typing state per ticket
- Complements collision detection for faster handoffs

## Pinned internal notes

Important internal notes can be pinned to the top of the ticket detail view. Pinned notes are highlighted in an amber card above the conversation thread, so agents don't miss critical context.

- Pin or unpin any internal note with one click
- Pinned notes display at the top of the ticket, always visible
- Only internal notes can be pinned -- public replies cannot

## Knowledge panel

The ticket sidebar includes a contextual knowledge panel so agents can reference related help content without leaving the ticket view.
