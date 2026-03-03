# Inkomende E-mail

Maak tickets aan en beantwoord ze rechtstreeks vanuit inkomende e-mails. Escalated ondersteunt **Mailgun**-, **Postmark**-, **AWS SES**-webhooks en **IMAP**-polling als terugvaloptie.

## Hoe het werkt

1. Je e-mailprovider ontvangt een bericht op je supportadres (bijv. `support@yourapp.com`)
2. De provider stuurt het door naar je app via webhook (of IMAP-polling haalt het op)
3. Escalated normaliseert de payload en controleert op threadovereenkomsten via onderwerpreferentie (bijv. `[ESC-00001]`) of `In-Reply-To`-headers
4. Overeenkomende e-mails voegen een antwoord toe; niet-overeenkomende e-mails maken een nieuw ticket aan (of gastticket voor onbekende afzenders)

## Configuratie

Schakel inkomende e-mail in en configureer je adapter in de beheerinstellingen, of via omgevingsvariabelen. Beheerinstellingen hebben voorrang op env-/configwaarden.

## Webhook-URL's

Wijs de inkomende webhook van je e-mailprovider naar deze URL's. Deze routes vereisen geen authenticatie (ze gebruiken handtekeningverificatie).

| Provider | Webhook-URL |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## IMAP-polling

Voor e-mailproviders zonder webhookondersteuning, gebruik het IMAP-pollingcommando op een schema.

## Functies

- **Threaddetectie** via onderwerpreferentie en In-Reply-To / References headers
- **Gasttickets** voor onbekende afzenders met automatisch afgeleide weergavenamen
- **Automatisch heropenen** van opgeloste of gesloten tickets wanneer een antwoord binnenkomt via e-mail
- **Duplicaatdetectie** via Message-ID headers om dubbele verwerking te voorkomen
- **Bijlageverwerking** met configureerbare limieten voor grootte en aantal
- **Auditlogging** -- elke inkomende e-mail wordt vastgelegd voor foutopsporing en compliance
- **Configureerbaar door beheerder** -- alle instellingen beheerbaar vanuit het beheerpaneel met terugval naar env/config
