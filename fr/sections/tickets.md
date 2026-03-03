# Tickets

Les tickets sont au coeur d'Escalated. Chaque ticket est une machine a etats a longue duree de vie avec un historique complet de conversation, des niveaux de priorite, un suivi d'assignation et une surveillance SLA.

> **Remarque :** Chaque ticket recoit une reference unique (par exemple, `ESC-00001`) et prend en charge les statuts personnalises, les niveaux de priorite, l'assignation de departement, les etiquettes, le suivi SLA et les conversations enrichies avec pieces jointes. Toutes les donnees sont stockees dans votre base de donnees.

## Flux de travail avances pour les tickets

- Flux de fusion de tickets pour combiner les doublons tout en preservant l'historique
- Tickets lies pour les flux de travail incidents/problemes associes
- Conversations paralleles pour la coordination interne/externe en parallele
- Support d'agent limite pour les roles operationnels a acces restreint
- Formulaires de champs personnalises avec regles conditionnelles basees sur le contexte du ticket
