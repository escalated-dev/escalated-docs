# Routes

Escalated registreert drie groepen routes onder het geconfigureerde voorvoegsel (standaard: `/support`).

## Klantroutes

| Methode | URL | Beschrijving |
| ------ | --- | ----------- |
| GET | /support | Ticketlijst van de klant |
| GET | /support/create | Nieuw ticketformulier |
| POST | /support | Ticket aanmaken |
| GET | /support/kb | Startpagina kennisbank |
| GET | /support/kb/{slug} | Kennisbankartikel |
| POST | /support/kb/{slug}/feedback | Artikelfeedback |
| GET | /support/{reference} | Ticketdetails |
| POST | /support/{reference}/reply | Ticket beantwoorden |
| POST | /support/{reference}/close | Ticket sluiten |
| POST | /support/{reference}/reopen | Ticket heropenen |
| POST | /support/{reference}/rate | Tevredenheidsbeoordeling indienen |

## Agentroutes

Vereist de `escalated-agent`-gate.

| Methode | URL | Beschrijving |
| ------ | --- | ----------- |
| GET | /support/agent | Agentdashboard |
| GET | /support/agent/tickets | Ticketwachtrij |
| GET | /support/agent/tickets/{reference} | Ticketdetails |
| POST | /support/agent/tickets/{reference}/reply | Openbaar antwoord |
| POST | /support/agent/tickets/{reference}/note | Interne notitie |
| POST | /support/agent/tickets/{reference}/assign | Agent toewijzen |
| POST | /support/agent/tickets/{reference}/status | Status wijzigen |
| POST | /support/agent/tickets/{reference}/priority | Prioriteit wijzigen |
| POST | /support/agent/tickets/bulk | Bulkticketacties |
| POST | /support/agent/tickets/{reference}/follow | Volgen aan/uit |
| POST | /support/agent/tickets/{reference}/macro | Macro toepassen |
| POST | /support/agent/tickets/{reference}/presence | Aanwezigheid melden |
| POST | /support/agent/tickets/{reference}/typing | Typstatus melden |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Notitie vastpinnen aan/uit |

## Beheerroutes

Vereist de `escalated-admin`-gate. Beheerders hebben alle agentroutes plus beheerpagina's.

| Methode | URL | Beschrijving |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Analysedashboard |
| GET | /support/admin/departments | Afdelingsbeheer |
| GET | /support/admin/sla-policies | SLA-beleidsbeheer |
| GET | /support/admin/escalation-rules | Escalatieregel-bouwer |
| GET | /support/admin/tags | Tagbeheer |
| GET | /support/admin/canned-responses | Standaardantwoordtemplates |
| GET | /support/admin/macros | Macrobeheer |
| GET | /support/admin/custom-fields | Aangepaste velden en formulieren |
| GET | /support/admin/statuses | Aangepaste statussen |
| GET | /support/admin/business-hours | Kantoorurenroosters |
| GET | /support/admin/roles | Agentrollen en machtigingen |
| GET | /support/admin/audit-log | Auditlogboek |
| GET | /support/admin/skills | Vaardigheidsbeheer |
| GET | /support/admin/capacity | Agentcapaciteitsinstellingen |
| GET | /support/admin/automations | Tijdgebaseerde automatiseringen |
| GET | /support/admin/webhooks | Uitgaande webhooks |
| GET | /support/admin/webhooks/{webhook}/deliveries | Webhook-afleveringslogboek |
| GET | /support/admin/kb-articles | Kennisbankartikelen |
| GET | /support/admin/kb-categories | Kennisbankcategorieen |
| GET | /support/admin/reports/dashboard | Rapportagedashboard |
| GET | /support/admin/reports/agents | Agentproductiviteitsrapport |
| GET | /support/admin/reports/sla | SLA-prestatierapport |
| GET | /support/admin/reports/csat | CSAT-rapport |
| GET | /support/admin/settings/csat | CSAT-enquete-instellingen |
| GET | /support/admin/settings/sso | SSO-instellingen |
| GET | /support/admin/settings/two-factor | Tweefactorinstellingen |
| GET | /support/admin/settings/data-retention | Gegevensbewaringsinstellingen |
| GET | /support/admin/settings/email | E-mailkanaalinstellingen |
| GET | /support/admin/custom-objects | Aangepaste objecten |
| GET | /support/admin/custom-objects/{customObject}/records | Records van aangepaste objecten |
| GET | /support/admin/tickets/merge-search | Samenvoegdoelen zoeken |
| POST | /support/admin/tickets/{reference}/merge | Ticket samenvoegen met doel |
| GET | /support/admin/tickets/{reference}/links | Gekoppelde tickets weergeven |
| POST | /support/admin/tickets/{reference}/links | Gerelateerd ticket koppelen |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Gerelateerd ticket ontkoppelen |
| GET | /support/admin/tickets/{reference}/side-conversations | Lijst van zijgesprekken |
| POST | /support/admin/tickets/{reference}/side-conversations | Zijgesprek starten |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Antwoorden in zijgesprek |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Zijgesprek sluiten |
| POST | /support/admin/macros | Macro aanmaken |
| PUT | /support/admin/macros/{macro} | Macro bijwerken |
| DELETE | /support/admin/macros/{macro} | Macro verwijderen |

## Gastroutes

Geen authenticatie vereist. Toegang via uniek token.

| Methode | URL | Beschrijving |
| ------ | --- | ----------- |
| GET | /support/guest/create | Gastticketformulier |
| POST | /support/guest | Gastticket aanmaken |
| GET | /support/guest/{token} | Gastticket bekijken |
| POST | /support/guest/{token}/reply | Gastticket beantwoorden |
| POST | /support/guest/{token}/rate | Tevredenheidsbeoordeling indienen |
