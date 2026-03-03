# E-mail entrant

Creez et repondez aux tickets directement depuis les e-mails entrants. Escalated prend en charge les webhooks **Mailgun**, **Postmark**, **AWS SES** et le sondage **IMAP** comme solution de repli.

## Fonctionnement

1. Votre fournisseur de messagerie recoit un message a votre adresse de support (par exemple, `support@yourapp.com`)
2. Le fournisseur le transmet a votre application via webhook (ou le sondage IMAP le recupere)
3. Escalated normalise le payload et recherche des correspondances de fil via la reference du sujet (par exemple, `[ESC-00001]`) ou les en-tetes `In-Reply-To`
4. Les e-mails correspondants ajoutent une reponse ; les e-mails sans correspondance creent un nouveau ticket (ou un ticket invite pour les expediteurs inconnus)

## Configuration

Activez l'e-mail entrant et configurez votre adaptateur dans les parametres d'administration, ou via des variables d'environnement. Les parametres d'administration ont la priorite sur les valeurs d'environnement/configuration.

## URLs de webhooks

Pointez le webhook entrant de votre fournisseur de messagerie vers ces URLs. Ces routes ne necessitent aucune authentification (elles utilisent la verification de signature a la place).

| Fournisseur | URL du webhook |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## Sondage IMAP

Pour les fournisseurs de messagerie sans prise en charge de webhooks, utilisez la commande de sondage IMAP de maniere planifiee.

## Fonctionnalites

- **Detection de fil** via la reference du sujet et les en-tetes In-Reply-To / References
- **Tickets invites** pour les expediteurs inconnus avec noms d'affichage derives automatiquement
- **Reouverture automatique** des tickets resolus ou clotures lorsqu'une reponse arrive par e-mail
- **Detection de doublons** via les en-tetes Message-ID pour eviter le traitement en double
- **Gestion des pieces jointes** avec limites de taille et de nombre configurables
- **Journal d'audit** -- chaque e-mail entrant est enregistre pour le debogage et la conformite
- **Configurable par l'administration** -- tous les parametres sont gerables depuis le panneau d'administration avec repli sur les variables d'environnement/configuration
