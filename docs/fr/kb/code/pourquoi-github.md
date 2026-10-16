---
title: Pourquoi Git et GitHub ?
description: Une introduction pour les lycéens d'une équipe FTC - à quoi servent Git et GitHub, et le vocabulaire à connaître.
---

# Pourquoi Git et GitHub ?

**Pour qui :** les élèves qui vont coder, avant d'installer quoi que ce soit. **Durée :** 5 minutes de lecture.

## Le problème

Veille de compétition. Quelqu'un améliore le code du bras, et soudain le robot ne démarre plus son autonome. Qu'est-ce qui a changé ? Qui l'a changé ? Comment revenir à la version d'hier qui marchait ?

Ou bien : le code « officiel » est sur l'ordinateur d'un élève, absent le jour du match. Ou il en existe trois versions sur trois clés USB, dont un `code_final_v3_VRAI.zip`.

Dès qu'on est plusieurs à coder sur un même robot, il faut un outil pour s'organiser. C'est le rôle de Git et de GitHub.

## Git : l'historique du code

Git enregistre l'**histoire** de votre projet. À chaque étape importante, vous faites un **commit** : une photo de tout le code, avec un message qui dit ce qui a changé et pourquoi.

- On sait **qui** a changé **quoi**, **quand**, et **pourquoi**.
- On peut **revenir** à n'importe quelle version précédente.
- On peut **comparer** deux versions ligne par ligne pour trouver l'erreur.

C'est un peu l'historique des versions d'un document partagé, mais pour tout un projet, et c'est vous qui décidez quand prendre la photo.

## Les branches : travailler sans se marcher dessus

Une **branche** est une copie de travail du code. Chacun développe son sujet sur sa propre branche (le pilotage, l'autonome, le bras…) sans gêner les autres. La branche principale de l'équipe, `main`, reste **toujours** dans un état qui marche : c'est elle qui va sur le robot en match.

Quand votre travail est prêt, vous le **fusionnez** dans `main`.

## GitHub : le code de l'équipe en ligne

Git fonctionne sur votre ordinateur. **GitHub** est le site qui héberge la version commune du code, le **dépôt** de l'équipe :

- **Accessible de partout** : au lycée, chez vous, en compétition. Un ordinateur perdu ou en panne ne fait rien perdre.
- **Relecture avant fusion** : pour faire entrer votre branche dans `main`, vous ouvrez une **pull request**. Une autre personne relit vos modifications avant qu'elles soient intégrées, comme on fait relire un exposé avant de le rendre.
- **Mises à jour du SDK** : le SDK FTC est lui-même publié par *FIRST* sur GitHub. Notre dépôt en est une copie (un *fork*), ce qui permet de récupérer chaque nouvelle version en quelques clics.

## Et pour vous ?

- Git et GitHub sont utilisés dans la plupart des entreprises et des projets logiciels. Vous apprenez ici un outil de professionnel.
- Votre travail est **visible et attribué** : chaque commit porte votre nom, ce qui aide aussi à raconter le projet dans le portfolio d'ingénierie.

## Le vocabulaire en une minute

| Mot | Ce que ça veut dire |
|---|---|
| **Dépôt** (*repository*) | Le projet et tout son historique. Celui de l'équipe est sur GitHub. |
| **Cloner** (*clone*) | Télécharger une copie du dépôt sur son ordinateur. |
| **Commit** | Une photo enregistrée du code, avec un message. |
| **Branche** (*branch*) | Une ligne de travail séparée, pour développer un sujet sans gêner les autres. |
| **Pousser** (*push*) | Envoyer ses commits de son ordinateur vers GitHub. |
| **Tirer** (*pull*) | Récupérer sur son ordinateur les commits des autres. |
| **Pull request** (PR) | Une demande pour faire entrer sa branche dans `main`, avec relecture. |
| **Fusionner** (*merge*) | Intégrer les modifications d'une branche dans une autre. |
| **Fork** | Une copie d'un dépôt sous un autre propriétaire, ici notre copie du SDK de *FIRST*. |

## Et ensuite ?

1. [Installer son poste et faire le premier build](poste-et-premier-build.md) : Git, Android Studio et votre première branche.
2. [Gestion de configuration](gestion-de-configuration.md) : les règles de l'équipe pour les branches et les pull requests.
