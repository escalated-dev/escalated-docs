# Route

Escalated registra tre gruppi di route sotto il prefisso configurato (predefinito: `/support`).

## Route clienti

| Metodo | URL | Descrizione |
| ------ | --- | ----------- |
| GET | /support | Lista ticket del cliente |
| GET | /support/create | Form di creazione nuovo ticket |
| POST | /support | Creazione ticket |
| GET | /support/kb | Home della knowledge base |
| GET | /support/kb/{slug} | Articolo della knowledge base |
| POST | /support/kb/{slug}/feedback | Feedback sull'articolo |
| GET | /support/{reference} | Dettaglio del ticket |
| POST | /support/{reference}/reply | Risposta al ticket |
| POST | /support/{reference}/close | Chiusura del ticket |
| POST | /support/{reference}/reopen | Riapertura del ticket |
| POST | /support/{reference}/rate | Invio valutazione di soddisfazione |

## Route agenti

Richiede il gate `escalated-agent`.

| Metodo | URL | Descrizione |
| ------ | --- | ----------- |
| GET | /support/agent | Dashboard agente |
| GET | /support/agent/tickets | Coda dei ticket |
| GET | /support/agent/tickets/{reference} | Dettaglio del ticket |
| POST | /support/agent/tickets/{reference}/reply | Risposta pubblica |
| POST | /support/agent/tickets/{reference}/note | Nota interna |
| POST | /support/agent/tickets/{reference}/assign | Assegnazione agente |
| POST | /support/agent/tickets/{reference}/status | Cambio stato |
| POST | /support/agent/tickets/{reference}/priority | Cambio priorità |
| POST | /support/agent/tickets/bulk | Azioni in blocco sui ticket |
| POST | /support/agent/tickets/{reference}/follow | Toggle segui/non seguire |
| POST | /support/agent/tickets/{reference}/macro | Applicazione macro |
| POST | /support/agent/tickets/{reference}/presence | Segnalazione presenza |
| POST | /support/agent/tickets/{reference}/typing | Segnalazione stato digitazione |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Toggle fissa/libera nota |

## Route amministrative

Richiede il gate `escalated-admin`. Gli amministratori hanno accesso a tutte le route agente più le pagine di gestione.

| Metodo | URL | Descrizione |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Dashboard analitica |
| GET | /support/admin/departments | Gestione dipartimenti |
| GET | /support/admin/sla-policies | Gestione policy SLA |
| GET | /support/admin/escalation-rules | Creazione regole di escalation |
| GET | /support/admin/tags | Gestione tag |
| GET | /support/admin/canned-responses | Template di risposte predefinite |
| GET | /support/admin/macros | Gestione macro |
| GET | /support/admin/custom-fields | Campi personalizzati e form |
| GET | /support/admin/statuses | Stati personalizzati |
| GET | /support/admin/business-hours | Pianificazione orari lavorativi |
| GET | /support/admin/roles | Ruoli e permessi degli agenti |
| GET | /support/admin/audit-log | Traccia di audit |
| GET | /support/admin/skills | Gestione competenze |
| GET | /support/admin/capacity | Controlli capacità degli agenti |
| GET | /support/admin/automations | Automazioni basate sul tempo |
| GET | /support/admin/webhooks | Webhook in uscita |
| GET | /support/admin/webhooks/{webhook}/deliveries | Log di consegna dei webhook |
| GET | /support/admin/kb-articles | Articoli della knowledge base |
| GET | /support/admin/kb-categories | Categorie della knowledge base |
| GET | /support/admin/reports/dashboard | Dashboard dei report |
| GET | /support/admin/reports/agents | Report produttività agenti |
| GET | /support/admin/reports/sla | Report conformità SLA |
| GET | /support/admin/reports/csat | Report CSAT |
| GET | /support/admin/settings/csat | Impostazioni sondaggio CSAT |
| GET | /support/admin/settings/sso | Impostazioni SSO |
| GET | /support/admin/settings/two-factor | Impostazioni autenticazione a due fattori |
| GET | /support/admin/settings/data-retention | Impostazioni conservazione dati |
| GET | /support/admin/settings/email | Impostazioni canale email |
| GET | /support/admin/custom-objects | Oggetti personalizzati |
| GET | /support/admin/custom-objects/{customObject}/records | Record degli oggetti personalizzati |
| GET | /support/admin/tickets/merge-search | Ricerca obiettivi di unione |
| POST | /support/admin/tickets/{reference}/merge | Unione del ticket nell'obiettivo |
| GET | /support/admin/tickets/{reference}/links | Lista ticket collegati |
| POST | /support/admin/tickets/{reference}/links | Collegamento ticket correlato |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Rimozione collegamento ticket |
| GET | /support/admin/tickets/{reference}/side-conversations | Lista conversazioni laterali |
| POST | /support/admin/tickets/{reference}/side-conversations | Avvio conversazione laterale |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Risposta in conversazione laterale |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Chiusura conversazione laterale |
| POST | /support/admin/macros | Creazione macro |
| PUT | /support/admin/macros/{macro} | Aggiornamento macro |
| DELETE | /support/admin/macros/{macro} | Eliminazione macro |

## Route guest

Nessuna autenticazione richiesta. Accesso tramite token univoco.

| Metodo | URL | Descrizione |
| ------ | --- | ----------- |
| GET | /support/guest/create | Form ticket guest |
| POST | /support/guest | Creazione ticket guest |
| GET | /support/guest/{token} | Visualizzazione ticket guest |
| POST | /support/guest/{token}/reply | Risposta al ticket guest |
| POST | /support/guest/{token}/rate | Invio valutazione di soddisfazione |
