# Collaboration entre agents

Gardez votre equipe de support synchronisee avec des indicateurs de presence en temps reel et des notes internes epinglees. Aucun outil externe necessaire.

## Detection de collisions

Lorsque plusieurs agents ouvrent le meme ticket, chaque agent voit un indicateur d'avatar montrant qui d'autre consulte actuellement le ticket. Cela evite les reponses en double et le travail inutile.

- Pile d'avatars avec les initiales des autres observateurs
- Info-bulle "Consulte egalement par" au survol
- Actualisation toutes les 30 secondes -- leger, base sur le cache (aucune table de base de donnees requise)

## Indicateurs de saisie

Les agents peuvent diffuser leur etat de saisie active lors de la redaction de reponses afin que les collegues puissent eviter les reponses qui se chevauchent.

- Etat de saisie en temps reel par ticket
- Complete la detection de collisions pour des transferts plus rapides

## Notes internes epinglees

Les notes internes importantes peuvent etre epinglees en haut de la vue de detail du ticket. Les notes epinglees sont mises en evidence dans une carte de couleur ambre au-dessus du fil de conversation, afin que les agents ne manquent pas de contexte critique.

- Epingler ou desepingler n'importe quelle note interne en un clic
- Les notes epinglees s'affichent en haut du ticket, toujours visibles
- Seules les notes internes peuvent etre epinglees -- les reponses publiques ne le peuvent pas

## Panneau de connaissances

La barre laterale du ticket inclut un panneau de connaissances contextuel pour que les agents puissent consulter le contenu d'aide associe sans quitter la vue du ticket.
