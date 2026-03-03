# Meldingen

Escalated maakt gebruik van het eigen meldingssysteem van je framework. E-mail- en databasemeldingen worden automatisch verzonden voor belangrijke gebeurtenissen zoals nieuwe tickets, antwoorden, toewijzingen, statuswijzigingen en SLA-schendingen.

- De toegewezen agent wordt op de hoogte gesteld van nieuwe antwoorden
- De aanvrager wordt op de hoogte gesteld van agentantwoorden en statuswijzigingen
- **Ticketvolgers** ontvangen dezelfde meldingen als de toegewezen agent -- antwoorden en statuswijzigingen
- SLA-schendingswaarschuwingen worden verzonden naar de toegewezen agent en afdelingsleden

Pas e-mailtemplates aan door views te publiceren: `php artisan vendor:publish --tag=escalated-views`
