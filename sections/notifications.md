# Notifications

The configuration keys, routes, gates, and commands shown here describe the Laravel adapter unless a framework is named. Use your adapter source for its corresponding API and defaults.

Escalated uses your framework's native notification system. Email and database notifications are sent automatically for key events like new tickets, replies, assignments, status changes, and SLA breaches.

- Ticket assignee notified on new replies
- Requester notified on agent replies and status changes
- **Ticket followers** receive the same notifications as the assignee -- replies and status changes
- SLA breach alerts sent to assignee and department members

Customize email templates by publishing views: `php artisan vendor:publish --tag=escalated-views`
