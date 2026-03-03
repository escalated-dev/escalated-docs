# Notifications

Escalated utilise le systeme de notifications natif de votre framework. Les notifications par e-mail et base de donnees sont envoyees automatiquement pour les evenements cles tels que les nouveaux tickets, les reponses, les assignations, les changements de statut et les violations de SLA.

- L'assignataire du ticket est notifie des nouvelles reponses
- Le demandeur est notifie des reponses des agents et des changements de statut
- Les **abonnes du ticket** recoivent les memes notifications que l'assignataire -- reponses et changements de statut
- Les alertes de violation de SLA sont envoyees a l'assignataire et aux membres du departement

Personnalisez les modeles d'e-mail en publiant les vues : `php artisan vendor:publish --tag=escalated-views`
