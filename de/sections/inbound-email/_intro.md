# Eingehende E-Mails

Erstellen und beantworten Sie Tickets direkt aus eingehenden E-Mails. Escalated unterstützt **Mailgun**-, **Postmark**-, **AWS SES**-Webhooks und **IMAP**-Polling als Fallback.

## Funktionsweise

1. Ihr E-Mail-Anbieter empfängt eine Nachricht an Ihrer Support-Adresse (z. B. `support@yourapp.com`)
2. Der Anbieter leitet sie per Webhook an Ihre App weiter (oder IMAP-Polling ruft sie ab)
3. Escalated normalisiert die Nutzdaten und prüft auf Thread-Übereinstimmungen anhand der Betreff-Referenz (z. B. `[ESC-00001]`) oder `In-Reply-To`-Headers
4. Übereinstimmende E-Mails fügen eine Antwort hinzu; nicht übereinstimmende E-Mails erstellen ein neues Ticket (oder Gast-Ticket für unbekannte Absender)

## Konfiguration

Aktivieren Sie eingehende E-Mails und konfigurieren Sie Ihren Adapter in den Admin-Einstellungen oder über Umgebungsvariablen. Admin-Einstellungen haben Vorrang vor Umgebungs-/Konfigurationswerten.

## Webhook-URLs

Richten Sie den Inbound-Webhook Ihres E-Mail-Anbieters auf diese URLs. Diese Routen erfordern keine Authentifizierung (sie verwenden stattdessen Signaturverifikation).

| Anbieter | Webhook-URL |
| -------- | ----------- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## IMAP-Polling

Für E-Mail-Anbieter ohne Webhook-Unterstützung verwenden Sie den IMAP-Polling-Befehl nach Zeitplan.

## Funktionen

- **Thread-Erkennung** über Betreff-Referenz und In-Reply-To / References-Headers
- **Gast-Tickets** für unbekannte Absender mit automatisch abgeleitetem Anzeigenamen
- **Automatisches Wiedereröffnen** gelöster oder geschlossener Tickets bei eingehender E-Mail-Antwort
- **Duplikaterkennung** über Message-ID-Headers zur Vermeidung doppelter Verarbeitung
- **Anhangverarbeitung** mit konfigurierbaren Größen- und Anzahlbegrenzungen
- **Audit-Protokollierung** -- jede eingehende E-Mail wird für Debugging und Compliance aufgezeichnet
- **Admin-konfigurierbar** -- alle Einstellungen über das Admin-Panel verwaltbar mit Umgebungs-/Konfigurations-Fallback
