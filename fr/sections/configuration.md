# Configuration

Escalated fonctionne immediatement avec des valeurs par defaut sensees. La configuration est optionnelle mais disponible pour la personnalisation.

> **Options de configuration**
>
> - `routes.prefix` -- Le prefixe d'URL pour toutes les routes Escalated (par defaut : `support`)
> - `routes.middleware` -- Middleware applique aux routes client (par defaut : `['web', 'auth']`)
> - `user_model` -- La classe du modele utilisateur (par defaut : `App\Models\User`)
> - `table_prefix` -- Prefixe pour les tables de base de donnees (par defaut : `escalated_`)
> - `tickets.allow_customer_close` -- Si les clients peuvent cloturer leurs propres tickets (par defaut : `true`)
> - `tickets.auto_close_resolved_after_days` -- Cloture automatique des tickets resolus apres N jours (par defaut : `7`)
> - `sla.business_hours_only` -- Ne compter que les heures ouvrables pour les objectifs SLA (par defaut : `false`)
> - `notifications.channels` -- Canaux de notification (par defaut : `['mail', 'database']`)

## Parametres et modules d'administration

Les mises a jour recentes de la plateforme ajoutent des ecrans de configuration et de gestion pour :

- Champs personnalises avec regles de visibilite conditionnelle
- Statuts personnalises et horaires de travail
- Roles (RBAC), routage par competences et capacite des agents
- Consultation du journal d'audit
- Automatisations et webhooks sortants
- Comportement des enquetes CSAT
- SSO et authentification a deux facteurs
- Politiques de retention des donnees et comportement de purge
- Parametres des canaux de messagerie
- Objets et enregistrements personnalises

## Publication des ressources

```bash
# Publier le fichier de configuration
$ php artisan vendor:publish --tag=escalated-config

# Publier les modeles d'e-mail pour personnalisation
$ php artisan vendor:publish --tag=escalated-views

# Publier les migrations (si vous devez les personnaliser)
$ php artisan vendor:publish --tag=escalated-migrations
```
