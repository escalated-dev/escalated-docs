# Benachrichtigungen

Escalated nutzt das native Benachrichtigungssystem Ihres Frameworks. E-Mail- und Datenbankbenachrichtigungen werden automatisch für wichtige Ereignisse wie neue Tickets, Antworten, Zuweisungen, Statusänderungen und SLA-Verletzungen gesendet.

- Ticket-Zugewiesener wird bei neuen Antworten benachrichtigt
- Anfragender wird bei Agentenantworten und Statusänderungen benachrichtigt
- **Ticket-Follower** erhalten dieselben Benachrichtigungen wie der Zugewiesene -- Antworten und Statusänderungen
- SLA-Verletzungswarnungen werden an den Zugewiesenen und Abteilungsmitglieder gesendet

E-Mail-Vorlagen anpassen durch Veröffentlichung der Views: `php artisan vendor:publish --tag=escalated-views`
