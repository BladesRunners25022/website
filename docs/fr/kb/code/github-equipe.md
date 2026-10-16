---
title: Mettre en place GitHub pour une équipe FTC
description: Organisation GitHub, fork du SDK FTC, branche main par défaut, équipe Code, jetons d'accès et rulesets.
---

# Mettre en place GitHub pour une équipe FTC

**Pour qui :** les coachs ou mentors qui administrent le code de l'équipe.
**Quand :** une fois, au lancement de l'équipe. **Durée :** environ 20 minutes.
**Prérequis :** un compte GitHub personnel par coach.

À la fin de ce guide, l'équipe dispose d'un dépôt de code qui lui appartient, à jour du SDK officiel, où les élèves peuvent proposer leurs modifications sans risquer de casser la version qui va sur le robot.

Dans les exemples, l'organisation s'appelle `mon-equipe-ftc` et le dépôt `FtcRobotController` : remplacez-les par vos propres noms.

## 1. Créer l'organisation GitHub

L'organisation possède le code de l'équipe. Il survit ainsi aux départs de coachs et d'élèves : personne n'a à « transférer » son dépôt personnel en fin d'année.

1. Connecté à votre compte, ouvrez [github.com/account/organizations/new](https://github.com/account/organizations/new?plan=free) et choisissez le plan `Free`.
2. Nom de l'organisation : par exemple `mon-equipe-ftc` (minuscules, sans espace). Le numéro d'équipe FTC dans le nom aide les autres équipes à vous trouver.
3. Contact email : une adresse de coach. `This organization belongs to` : `My personal account`.
4. Ajoutez au moins un deuxième adulte comme propriétaire : `People` → `Invite member` → rôle `Owner`.

!!! tip "Toujours deux propriétaires"
    Si l'unique propriétaire perd l'accès à son compte, l'organisation devient ingérable. Deux `Owner` minimum.

## 2. Forker le SDK officiel dans l'organisation

Le SDK FTC est publié par *FIRST* sur GitHub. On en fait une copie (un *fork*) dans l'organisation : ce sera le dépôt de l'équipe.

1. Ouvrez [github.com/FIRST-Tech-Challenge/FtcRobotController](https://github.com/FIRST-Tech-Challenge/FtcRobotController).
2. Cliquez `Fork`. `Owner` : choisissez l'organisation.
3. Gardez le nom `FtcRobotController` ou renommez-le. Laissez cochée `Copy the master branch only` : seule `master` nous intéresse. Cliquez `Create fork`.

!!! warning "Un fork est public"
    C'est la pratique courante en FTC : le code des équipes est visible de tous, comme le SDK. Si vous tenez à un dépôt privé, utilisez plutôt `Import repository` avec la même URL. Vous perdez alors le bouton `Sync fork` qui permet de récupérer les mises à jour du SDK en un clic.

!!! note "Un seul fork par organisation"
    GitHub n'autorise qu'**un seul fork d'un même dépôt par organisation**. On garde donc le même dépôt d'une saison à l'autre : voir [Nouvelle saison](gestion-de-configuration.md#nouvelle-saison).

## 3. Créer la branche `main` et en faire la branche par défaut

Le fork contient la branche `master` de *FIRST*. Nous la gardons comme **copie exacte du SDK** et créons à côté la branche de travail de l'équipe, `main`. Le pourquoi est détaillé dans [Gestion de configuration](gestion-de-configuration.md).

1. Sur la page **du dépôt de l'équipe** (`mon-equipe-ftc/FtcRobotController`, pas celui de *FIRST*) : `Branches` → `New branch` → nom `main`.
2. Dans `Source`, vérifiez le dépôt **et** la branche : `mon-equipe-ftc/FtcRobotController` · `master`.
3. `Create new branch`.
4. `Settings` → `General` → `Default branch` → choisissez `main` → `Update`.

!!! warning "Le `master` de l'équipe, pas celui de *FIRST*"
    Dans un fork, la liste `Source` propose aussi le dépôt d'origine, `FIRST-Tech-Challenge/FtcRobotController`, avec sa propre branche `master`. Les deux portent le même nom : vérifiez que c'est bien **le dépôt de votre organisation** qui est sélectionné. De même, si vous passez par la page des branches, assurez-vous d'être sur `github.com/mon-equipe-ftc/…` et non sur `github.com/FIRST-Tech-Challenge/…`.

Désormais, les clones partent de `main` et les pull requests visent `main` par défaut.

## 4. Créer l'équipe « Code » et inviter les élèves

Plutôt que de donner des droits élève par élève, on les donne à une équipe GitHub.

1. Dans l'organisation : `Teams` → `New team` → nom `code`.
2. Dans le dépôt : `Settings` → `Collaborators and teams` → `Add teams` → `code`, rôle `Write`.
3. Quand un élève a créé son compte GitHub, invitez-le : `People` → `Invite member` → rôle `Member`, équipe `code`.

!!! tip "Pseudos GitHub"
    Conseillez aux élèves un pseudo sobre et l'activation de la double authentification : le pseudo apparaît dans l'historique public du code.

## 5. Autoriser les jetons d'accès *classic*

Pour envoyer leur code sur GitHub depuis Android Studio, les élèves utilisent un **jeton d'accès personnel *classic*** : c'est le type de jeton qu'attend la connexion GitHub d'Android Studio (`Log In with Token…`). L'organisation doit l'accepter.

1. Organisation → `Settings` → `Personal access tokens` → `Settings`.
2. Section *Personal access tokens (classic)* : choisissez `Allow access via personal access tokens (classic)`. **Ne les bloquez pas**, sinon les élèves ne pourront pas pousser depuis Android Studio.
3. Section *Fine-grained personal access tokens* : réglage libre, ils ne sont pas utilisés dans ce guide.

!!! note "Pas de validation pour les jetons *classic*"
    Les jetons *classic* ne passent pas par une approbation de l'organisation. Sur le dépôt, ils ne donnent que les droits de l'élève, c'est-à-dire ceux de l'équipe `code` : retirer un élève de l'équipe ou de l'organisation suffit à couper son accès.

La création du jeton côté élève est décrite dans [Poste de travail et premier build](poste-et-premier-build.md#6-creer-son-jeton-dacces-github).

## 6. Protéger les branches avec des *rulesets* (conseillé)

Objectif : personne ne pousse directement sur `main`. Chacun travaille sur sa branche et ouvre une pull request, relue par une autre personne. Et personne ne modifie `master`, réservée aux mises à jour du SDK.

Dépôt → `Settings` → `Rules` → `Rulesets` → `New ruleset` → `New branch ruleset`. Créez deux rulesets, avec `Enforcement status` : `Active`.

| Ruleset | Cible (`Target branches`) | Règles à cocher | `Bypass list` |
|---|---|---|---|
| `main` | `Include default branch` | `Require a pull request before merging`, `Block force pushes`, `Restrict deletions` | rôle `Organization admin` (pour les urgences) |
| `master` | `Include by pattern` → `master` | `Restrict updates`, `Block force pushes`, `Restrict deletions` | rôle `Organization admin` (pour faire le `Sync fork`) |

!!! tip "Nombre d'approbations"
    Dans `Require a pull request before merging`, vous pouvez exiger une approbation (`Required approvals` : 1). C'est utile quand plusieurs élèves sont autonomes ; avec une petite équipe débutante, une relecture informelle par un coach suffit souvent. À adapter à votre équipe.

## Récapitulatif

- [x] Organisation créée, au moins deux propriétaires
- [x] SDK forké dans l'organisation
- [x] Branche `main` créée depuis `master`, branche par défaut
- [x] Équipe `code` avec le rôle `Write` sur le dépôt
- [x] Jetons *classic* autorisés
- [x] Rulesets sur `main` et `master`

Étape suivante pour les élèves : [Poste de travail et premier build](poste-et-premier-build.md).
