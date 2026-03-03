# Email in Entrata

Crea e rispondi ai ticket direttamente dalle email in arrivo. Escalated supporta i webhook di **Mailgun**, **Postmark**, **AWS SES** e il polling **IMAP** come fallback.

## Come Funziona

1. Il tuo provider email riceve un messaggio al tuo indirizzo di supporto (es. `support@yourapp.com`)
2. Il provider lo inoltra alla tua app tramite webhook (oppure il polling IMAP lo recupera)
3. Escalated normalizza il payload e verifica la corrispondenza dei thread tramite il riferimento nell'oggetto (es. `[ESC-00001]`) o gli header `In-Reply-To`
4. Le email corrispondenti aggiungono una risposta; le email senza corrispondenza creano un nuovo ticket (o un ticket guest per mittenti sconosciuti)

## Configurazione

Abilita le email in entrata e configura il tuo adattatore nelle impostazioni di amministrazione, o tramite variabili d'ambiente. Le impostazioni di amministrazione hanno la precedenza sui valori env/config.

## URL dei Webhook

Punta il webhook in entrata del tuo provider email a questi URL. Queste route non richiedono autenticazione (utilizzano la verifica della firma).

| Provider | URL del Webhook |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## Polling IMAP

Per i provider email senza supporto webhook, usa il comando di polling IMAP in modo programmato.

## Funzionalità

- **Rilevamento dei thread** tramite riferimento nell'oggetto e header In-Reply-To / References
- **Ticket guest** per mittenti sconosciuti con nomi visualizzati derivati automaticamente
- **Riapertura automatica** dei ticket risolti o chiusi quando arriva una risposta via email
- **Rilevamento duplicati** tramite header Message-ID per prevenire l'elaborazione duplicata
- **Gestione allegati** con limiti configurabili di dimensione e numero
- **Log di audit** -- ogni email in entrata viene registrata per debug e conformità
- **Configurabile dall'amministratore** -- tutte le impostazioni gestibili dal pannello di amministrazione con fallback su env/config
