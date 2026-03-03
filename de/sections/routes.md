# Routen

Escalated registriert drei Gruppen von Routen unter dem konfigurierten Präfix (Standard: `/support`).

## Kundenrouten

| Methode | URL | Beschreibung |
| ------- | --- | ------------ |
| GET | /support | Kunden-Ticketliste |
| GET | /support/create | Neues-Ticket-Formular |
| POST | /support | Ticket erstellen |
| GET | /support/kb | Wissensdatenbank-Startseite |
| GET | /support/kb/{slug} | Wissensdatenbank-Artikel |
| POST | /support/kb/{slug}/feedback | Artikel-Feedback |
| GET | /support/{reference} | Ticket-Detailansicht |
| POST | /support/{reference}/reply | Auf Ticket antworten |
| POST | /support/{reference}/close | Ticket schließen |
| POST | /support/{reference}/reopen | Ticket wiedereröffnen |
| POST | /support/{reference}/rate | Zufriedenheitsbewertung abgeben |

## Agentenrouten

Erfordert das `escalated-agent`-Gate.

| Methode | URL | Beschreibung |
| ------- | --- | ------------ |
| GET | /support/agent | Agenten-Dashboard |
| GET | /support/agent/tickets | Ticket-Warteschlange |
| GET | /support/agent/tickets/{reference} | Ticket-Detailansicht |
| POST | /support/agent/tickets/{reference}/reply | Öffentliche Antwort |
| POST | /support/agent/tickets/{reference}/note | Interne Notiz |
| POST | /support/agent/tickets/{reference}/assign | Agent zuweisen |
| POST | /support/agent/tickets/{reference}/status | Status ändern |
| POST | /support/agent/tickets/{reference}/priority | Priorität ändern |
| POST | /support/agent/tickets/bulk | Massenaktionen für Tickets |
| POST | /support/agent/tickets/{reference}/follow | Folgen umschalten |
| POST | /support/agent/tickets/{reference}/macro | Makro anwenden |
| POST | /support/agent/tickets/{reference}/presence | Anwesenheit melden |
| POST | /support/agent/tickets/{reference}/typing | Tippstatus melden |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Notiz anheften/lösen |

## Admin-Routen

Erfordert das `escalated-admin`-Gate. Admins haben alle Agentenrouten plus Verwaltungsseiten.

| Methode | URL | Beschreibung |
| ------- | --- | ------------ |
| GET | /support/admin/reports | Analyse-Dashboard |
| GET | /support/admin/departments | Abteilungsverwaltung |
| GET | /support/admin/sla-policies | SLA-Richtlinienverwaltung |
| GET | /support/admin/escalation-rules | Eskalationsregel-Builder |
| GET | /support/admin/tags | Tag-Verwaltung |
| GET | /support/admin/canned-responses | Vorgefertigte Antwortvorlagen |
| GET | /support/admin/macros | Makroverwaltung |
| GET | /support/admin/custom-fields | Benutzerdefinierte Felder und Formulare |
| GET | /support/admin/statuses | Benutzerdefinierte Status |
| GET | /support/admin/business-hours | Geschäftszeiten-Zeitpläne |
| GET | /support/admin/roles | Agentenrollen und Berechtigungen |
| GET | /support/admin/audit-log | Audit-Protokoll |
| GET | /support/admin/skills | Fähigkeitenverwaltung |
| GET | /support/admin/capacity | Agentenkapazitäts-Steuerung |
| GET | /support/admin/automations | Zeitbasierte Automatisierungen |
| GET | /support/admin/webhooks | Ausgehende Webhooks |
| GET | /support/admin/webhooks/{webhook}/deliveries | Webhook-Zustellungsprotokoll |
| GET | /support/admin/kb-articles | Wissensdatenbank-Artikel |
| GET | /support/admin/kb-categories | Wissensdatenbank-Kategorien |
| GET | /support/admin/reports/dashboard | Berichts-Dashboard |
| GET | /support/admin/reports/agents | Agentenproduktivitäts-Bericht |
| GET | /support/admin/reports/sla | SLA-Erreichungs-Bericht |
| GET | /support/admin/reports/csat | CSAT-Bericht |
| GET | /support/admin/settings/csat | CSAT-Umfrageeinstellungen |
| GET | /support/admin/settings/sso | SSO-Einstellungen |
| GET | /support/admin/settings/two-factor | Zwei-Faktor-Einstellungen |
| GET | /support/admin/settings/data-retention | Datenaufbewahrungseinstellungen |
| GET | /support/admin/settings/email | E-Mail-Kanaleinstellungen |
| GET | /support/admin/custom-objects | Benutzerdefinierte Objekte |
| GET | /support/admin/custom-objects/{customObject}/records | Datensätze benutzerdefinierter Objekte |
| GET | /support/admin/tickets/merge-search | Zusammenführungsziele suchen |
| POST | /support/admin/tickets/{reference}/merge | Ticket zusammenführen |
| GET | /support/admin/tickets/{reference}/links | Verknüpfte Tickets auflisten |
| POST | /support/admin/tickets/{reference}/links | Verwandtes Ticket verknüpfen |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Verknüpfung aufheben |
| GET | /support/admin/tickets/{reference}/side-conversations | Seitenkonversationen auflisten |
| POST | /support/admin/tickets/{reference}/side-conversations | Seitenkonversation starten |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | In Seitenkonversation antworten |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Seitenkonversation schließen |
| POST | /support/admin/macros | Makro erstellen |
| PUT | /support/admin/macros/{macro} | Makro aktualisieren |
| DELETE | /support/admin/macros/{macro} | Makro löschen |

## Gastrouten

Keine Authentifizierung erforderlich. Zugriff über eindeutigen Token.

| Methode | URL | Beschreibung |
| ------- | --- | ------------ |
| GET | /support/guest/create | Gast-Ticket-Formular |
| POST | /support/guest | Gast-Ticket erstellen |
| GET | /support/guest/{token} | Gast-Ticket anzeigen |
| POST | /support/guest/{token}/reply | Auf Gast-Ticket antworten |
| POST | /support/guest/{token}/rate | Zufriedenheitsbewertung abgeben |
