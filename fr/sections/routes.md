# Routes

Escalated enregistre trois groupes de routes sous le prefixe configure (par defaut : `/support`).

## Routes client

| Methode | URL | Description |
| ------ | --- | ----------- |
| GET | /support | Liste des tickets du client |
| GET | /support/create | Formulaire de nouveau ticket |
| POST | /support | Creer un ticket |
| GET | /support/kb | Accueil de la base de connaissances |
| GET | /support/kb/{slug} | Article de la base de connaissances |
| POST | /support/kb/{slug}/feedback | Retour sur l'article |
| GET | /support/{reference} | Detail du ticket |
| POST | /support/{reference}/reply | Repondre au ticket |
| POST | /support/{reference}/close | Cloturer le ticket |
| POST | /support/{reference}/reopen | Rouvrir le ticket |
| POST | /support/{reference}/rate | Soumettre une evaluation de satisfaction |

## Routes agent

Necessite le gate `escalated-agent`.

| Methode | URL | Description |
| ------ | --- | ----------- |
| GET | /support/agent | Tableau de bord des agents |
| GET | /support/agent/tickets | File d'attente des tickets |
| GET | /support/agent/tickets/{reference} | Detail du ticket |
| POST | /support/agent/tickets/{reference}/reply | Reponse publique |
| POST | /support/agent/tickets/{reference}/note | Note interne |
| POST | /support/agent/tickets/{reference}/assign | Assigner un agent |
| POST | /support/agent/tickets/{reference}/status | Changer le statut |
| POST | /support/agent/tickets/{reference}/priority | Changer la priorite |
| POST | /support/agent/tickets/bulk | Actions groupees sur les tickets |
| POST | /support/agent/tickets/{reference}/follow | Activer/desactiver le suivi |
| POST | /support/agent/tickets/{reference}/macro | Appliquer une macro |
| POST | /support/agent/tickets/{reference}/presence | Signaler la presence |
| POST | /support/agent/tickets/{reference}/typing | Signaler l'etat de saisie |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Epingler/desepingler une note |

## Routes d'administration

Necessite le gate `escalated-admin`. Les administrateurs ont toutes les routes agent plus les pages de gestion.

| Methode | URL | Description |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Tableau de bord analytique |
| GET | /support/admin/departments | Gestion des departements |
| GET | /support/admin/sla-policies | Gestion des politiques SLA |
| GET | /support/admin/escalation-rules | Constructeur de regles d'escalade |
| GET | /support/admin/tags | Gestion des etiquettes |
| GET | /support/admin/canned-responses | Modeles de reponses predefinies |
| GET | /support/admin/macros | Gestion des macros |
| GET | /support/admin/custom-fields | Champs personnalises et formulaires |
| GET | /support/admin/statuses | Statuts personnalises |
| GET | /support/admin/business-hours | Horaires de travail |
| GET | /support/admin/roles | Roles et permissions des agents |
| GET | /support/admin/audit-log | Journal d'audit |
| GET | /support/admin/skills | Gestion des competences |
| GET | /support/admin/capacity | Controles de capacite des agents |
| GET | /support/admin/automations | Automatisations basees sur le temps |
| GET | /support/admin/webhooks | Webhooks sortants |
| GET | /support/admin/webhooks/{webhook}/deliveries | Journal des livraisons de webhooks |
| GET | /support/admin/kb-articles | Articles de la base de connaissances |
| GET | /support/admin/kb-categories | Categories de la base de connaissances |
| GET | /support/admin/reports/dashboard | Tableau de bord des rapports |
| GET | /support/admin/reports/agents | Rapport de productivite des agents |
| GET | /support/admin/reports/sla | Rapport de performance SLA |
| GET | /support/admin/reports/csat | Rapport CSAT |
| GET | /support/admin/settings/csat | Parametres d'enquete CSAT |
| GET | /support/admin/settings/sso | Parametres SSO |
| GET | /support/admin/settings/two-factor | Parametres d'authentification a deux facteurs |
| GET | /support/admin/settings/data-retention | Parametres de retention des donnees |
| GET | /support/admin/settings/email | Parametres du canal de messagerie |
| GET | /support/admin/custom-objects | Objets personnalises |
| GET | /support/admin/custom-objects/{customObject}/records | Enregistrements d'objets personnalises |
| GET | /support/admin/tickets/merge-search | Rechercher des cibles de fusion |
| POST | /support/admin/tickets/{reference}/merge | Fusionner le ticket dans la cible |
| GET | /support/admin/tickets/{reference}/links | Lister les tickets lies |
| POST | /support/admin/tickets/{reference}/links | Lier un ticket associe |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Delier un ticket associe |
| GET | /support/admin/tickets/{reference}/side-conversations | Liste des conversations paralleles |
| POST | /support/admin/tickets/{reference}/side-conversations | Demarrer une conversation parallele |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Repondre dans une conversation parallele |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Cloturer une conversation parallele |
| POST | /support/admin/macros | Creer une macro |
| PUT | /support/admin/macros/{macro} | Mettre a jour une macro |
| DELETE | /support/admin/macros/{macro} | Supprimer une macro |

## Routes invites

Aucune authentification requise. Acces via un jeton unique.

| Methode | URL | Description |
| ------ | --- | ----------- |
| GET | /support/guest/create | Formulaire de ticket invite |
| POST | /support/guest | Creer un ticket invite |
| GET | /support/guest/{token} | Voir le ticket invite |
| POST | /support/guest/{token}/reply | Repondre au ticket invite |
| POST | /support/guest/{token}/rate | Soumettre une evaluation de satisfaction |
