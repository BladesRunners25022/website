---
title: Installer son poste et faire le premier build
description: Git, Android Studio, jeton d'accès, clonage du dépôt de l'équipe et premier build Gradle du SDK FTC v12.0.
---

# Installer son poste et faire le premier build

**Pour qui :** chaque élève qui code, sur son propre ordinateur.
**Durée :** environ 1 h 30, surtout à cause des téléchargements.
**Prérequis :** l'équipe a déjà [mis en place GitHub](github-equipe.md) ; environ 15 Go d'espace libre et 8 Go de RAM minimum.

!!! info "Nouveau sur Git ?"
    Lisez d'abord [Pourquoi Git et GitHub ?](pourquoi-github.md) : 5 minutes pour comprendre à quoi sert tout ce qu'on installe ici.

!!! tip "Faites les téléchargements chez vous"
    Les réseaux des établissements scolaires bloquent souvent les téléchargements d'Android Studio et de Gradle. Faites les étapes 2 à 6 sur une connexion personnelle : ensuite, tout est en cache.

Ce guide reprend les points propres à la saison et à notre organisation GitHub. Pour le pas-à-pas illustré de l'interface d'Android Studio, **[gm0 l'explique très bien](https://gm0.org/en/latest/docs/software/getting-started/using-android-studio.html)** : nous y renvoyons plutôt que de le recopier.

## Versions de la saison 2026-27

| Élément | Version |
|---|---|
| SDK FTC | v12.0 |
| Gradle | 9.1 |
| Android Gradle Plugin (AGP) | 8.13.2 |
| Android Studio **conseillé** | Rabbit 1 (2026.2.1), stable depuis le 1er octobre 2026 |
| Android Studio **minimum** | Narwhal 3 Feature Drop (2025.1.3) |
| JDK supplémentaire | Liberica JDK 17 *Full* (simulateur, secours) |

Rabbit prend en charge les AGP 7.1 à 9.4 : il est compatible avec le SDK v12.0.

!!! warning "La page FTC Docs « Installing Android Studio » est obsolète"
    Elle décrit encore Android Studio Ladybug et un JDK 17 à installer pour le build. Ici, le build utilise le JDK fourni avec Android Studio ; Liberica 17 (étape 4) sert au simulateur et en secours.

## 1. Créer son compte GitHub et rejoindre l'équipe

1. Créez un compte sur [github.com/signup](https://github.com/signup). Choisissez un pseudo sobre : il apparaîtra dans l'historique public du code.
2. Activez la double authentification : `Settings` → `Password and authentication`.
3. Transmettez votre pseudo à la personne qui administre l'organisation de l'équipe.
4. Acceptez l'invitation reçue par e-mail (ou sur [github.com/notifications](https://github.com/notifications)).

## 2. Installer Git

- **Windows :** téléchargez [Git for Windows](https://git-scm.com/download/win) et gardez les options par défaut.
- **macOS :** dans le Terminal, lancez la commande ci-dessous et acceptez l'installation des outils de développement proposée.

```bash
git --version
```

Puis indiquez votre nom et l'adresse e-mail de votre compte GitHub :

```bash
git config --global user.name "Prénom Nom"
git config --global user.email "adresse-du-compte-github@exemple.fr"
```

!!! tip "Garder son adresse privée"
    GitHub fournit une adresse `…@users.noreply.github.com` (`Settings` → `Emails`) que vous pouvez utiliser ici pour ne pas publier votre vraie adresse dans l'historique.

## 3. Installer Android Studio

1. Téléchargez la dernière version stable sur [developer.android.com/studio](https://developer.android.com/studio) : **Rabbit** (2026.2) au moment où nous écrivons.
2. Lancez l'installation **en tant qu'administrateur** : sous Windows, clic droit sur le fichier téléchargé → `Exécuter en tant qu'administrateur` ; sous macOS, glissez Android Studio dans `Applications` avec un compte administrateur. Choisissez `Standard` et acceptez les licences.

    !!! warning "Ordinateur sans droits administrateur"
        Sur un ordinateur géré par l'établissement ou par un parent, demandez à la personne qui a les droits administrateur de lancer l'installation. Sans ces droits, l'installation échoue ou s'arrête en cours de route.
3. Laissez finir le téléchargement des composants Android : c'est l'étape la plus longue.
4. Android Studio déjà installé ? Vérifiez sa version dans `Help` → `About` (macOS : `Android Studio` → `About`). En dessous de Narwhal 3 Feature Drop (2025.1.3), le SDK v12.0 ne se synchronise pas : mettez à jour.

Détails et captures d'écran : [gm0, *Using Android Studio*](https://gm0.org/en/latest/docs/software/getting-started/using-android-studio.html).

## 4. Installer Liberica JDK 17 *Full*

Android Studio fournit déjà son propre JDK (le Java qui compile le code), et il suffit pour le projet de l'équipe. On installe en plus **Liberica JDK 17, version *Full*** :

- pour [s'entraîner chez soi avec virtual_robot](sentrainer-virtual-robot.md) : le simulateur a besoin de JavaFX, inclus seulement dans cette version ;
- comme JDK de secours si le build du projet échoue avec le JDK d'Android Studio (voir le dépannage).

1. Ouvrez [bell-sw.com/pages/downloads](https://bell-sw.com/pages/downloads/#jdk-17-lts) et sélectionnez **JDK 17 LTS**.
2. **Ne cliquez pas** sur les gros boutons de téléchargement : ils donnent la version standard, sans JavaFX.
3. Descendez jusqu'à votre système (Windows 64 bits ou macOS), choisissez votre processeur, puis dans `Package`, sélectionnez **`Full JDK`**.
4. Téléchargez l'installeur (`.msi` sous Windows, `.dmg` sous macOS) et lancez-le. Les options `Add to PATH`, `Set JAVA_HOME` et les associations de fichiers ne sont pas nécessaires : vous pouvez les décocher.

!!! warning "La version 17, pas une autre"
    L'auteur de virtual_robot indique que Liberica 21 ne fonctionne pas avec le simulateur. Restez sur la 17.

## 5. Cloner le dépôt de l'équipe

Le dépôt de l'équipe est public : pas besoin de jeton ni de connexion à GitHub pour le cloner.

1. Écran d'accueil : `Clone Repository` (ou `File` → `New` → `Project from Version Control`).
2. URL : celle du dépôt de l'équipe, de la forme `https://github.com/mon-equipe-ftc/FtcRobotController.git`.
3. `Directory` : un dossier court, **sans espace ni accent**, par exemple `C:\ftc\FtcRobotController` ou `~/ftc/FtcRobotController`.
4. `Clone`, puis `Trust Project`.

## 6. Lancer le premier build

!!! danger "Refusez toute mise à jour de Gradle ou de l'AGP"
    À l'ouverture du projet, Android Studio peut proposer « Upgrade Gradle » ou l'**AGP Upgrade Assistant** : Rabbit propose de passer en AGP 9.x. **Refusez.** Le projet FTC doit garder les versions fournies par *FIRST* (Gradle 9.1, AGP 8.13.2).

1. Vérifiez le Java utilisé par Gradle : `Settings` → `Build, Execution, Deployment` → `Build Tools` → `Gradle` → `Gradle JDK`. Sélectionnez le JDK fourni avec Android Studio (`jbr-…`, JetBrains Runtime).
2. Cliquez l'icône éléphant `Sync Project with Gradle Files`. La première synchronisation télécharge beaucoup de dépendances : patience.
3. `Build` → `Make Project`.

C'est réussi quand l'onglet `Build`, en bas, affiche **`BUILD SUCCESSFUL`**.

!!! question "JDK : à confirmer"
    Avec Gradle 9.1, le JDK fourni avec Android Studio **devrait suffire**, sans passer par Liberica. Nous ne l'avons **pas encore testé** sur toutes les configurations. Si vous le confirmez (ou l'infirmez), dites-le-nous : voir [Contribuer](../contribuer.md). En cas d'échec, voir le dépannage ci-dessous.

## 7. Créer son jeton d'accès GitHub

Pour **envoyer** du code sur GitHub (*push*) et travailler avec les pull requests, il faut s'authentifier. Le jeton remplace votre mot de passe : c'est lui qu'Android Studio présente à GitHub. **Traitez-le comme un mot de passe** : ne le collez jamais dans une messagerie ni dans le code.

1. Ouvrez [github.com/settings/tokens/new](https://github.com/settings/tokens/new) (*Personal access token (classic)*).
2. `Note` : `android-studio`. `Expiration` : `Custom`, jusqu'à la fin de la saison.
3. `Select scopes` : cochez exactement ces permissions, demandées par Android Studio :

    | Permission | Où la trouver | À quoi elle sert |
    |---|---|---|
    | `repo` | en haut de la liste | pousser son code sur le dépôt de l'équipe, travailler avec les pull requests |
    | `workflow` | juste sous `repo` | pousser des modifications des fichiers `.github/workflows` du SDK |
    | `gist` | milieu de la liste | partager des extraits de code depuis Android Studio |
    | `read:org` | sous `admin:org` (ne cochez **que** `read:org`) | voir les dépôts de l'organisation de l'équipe |
    | `read:user` | sous `user` | lire son profil GitHub |
    | `user:email` | sous `user` | lire son adresse e-mail GitHub |

4. `Generate token`, puis copiez-le tout de suite : GitHub ne l'affiche qu'une fois.

!!! tip "Jeton pas copié ou perdu ?"
    Pas de panique : GitHub ne peut pas vous le réafficher, mais vous pouvez en refaire un. Dans `Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)`, supprimez l'ancien jeton (`Delete`), puis recréez-en un en reprenant cette étape depuis le début. Si le jeton était déjà enregistré dans Android Studio, remplacez-le à l'étape 8.

!!! warning "Un jeton *classic* ouvre tous vos dépôts"
    Avec `repo`, le jeton donne accès à **tous** les dépôts auxquels votre compte a accès, pas seulement à celui de l'équipe. Gardez une date d'expiration et supprimez le jeton (`Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)`) si vous pensez qu'il a fuité.

## 8. Utiliser le jeton dans Android Studio

On enregistre le jeton une fois dans Android Studio, qui s'en sert ensuite automatiquement à chaque *push* vers GitHub et pour afficher les pull requests.

1. `Settings` (macOS : `Android Studio` → `Settings`).
2. `Version Control` → `GitHub` → `+` → `Log In with Token…`
3. Collez le jeton → `Add Account`. Votre pseudo GitHub apparaît dans la liste des comptes.
4. Sous Windows, vérifiez aussi `Version Control` → `Git` → `Test` : Android Studio doit trouver Git.

!!! tip "Une fenêtre de connexion s'ouvre quand même au premier push ?"
    Selon la configuration, Git peut demander lui-même des identifiants au moment du *push* :

    - fenêtre **Git Credential Manager** (*Connect to GitHub*, Windows) : choisissez `Token` et collez le jeton, plutôt que `Sign in with your browser` ;
    - fenêtre **identifiant / mot de passe** : identifiant = votre pseudo GitHub, mot de passe = **le jeton** (pas votre mot de passe GitHub).

    Les identifiants sont ensuite mémorisés : la question ne revient qu'à l'expiration du jeton.

## 9. Premier OpMode, première branche

Tout le code de l'équipe va dans le module `TeamCode`. Les exemples de *FIRST* sont dans le module `FtcRobotController` et ne se modifient pas.

1. Partez de `main` à jour : en bas à droite, cliquez le nom de la branche → `main` → `Update`. Puis `New Branch` → `prenom/premier-opmode`.
2. Ouvrez les exemples : `FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples`.
3. Copiez `BasicOpMode_Linear.java` dans `TeamCode/src/main/java/org/firstinspires/ftc/teamcode`.
4. Dans le fichier copié, supprimez la ligne `@Disabled` et changez le nom dans `@TeleOp(name = "…")`.
5. `Build` → `Make Project` : toujours `BUILD SUCCESSFUL` ?
6. `Git` → `Commit` : cochez le fichier, écrivez un message clair (« Ajout premier OpMode TeleOp »), puis `Commit and Push`. C'est ce *push* qui utilise votre jeton (étape 8).
7. Sur GitHub, ouvrez la pull request proposée vers `main`.

Les règles de branches et de pull requests sont expliquées dans [Gestion de configuration](gestion-de-configuration.md).

## Dépannage

??? failure "Android Studio propose « Upgrade Gradle » ou l'« AGP Upgrade Assistant »"
    Refusez et fermez la fenêtre. Si vous avez déjà accepté : `Git` → `Rollback` sur les fichiers modifiés, ou reclonez le dépôt.

??? failure "« Sync failed » dès l'ouverture, ou message sur la version de l'Android Gradle Plugin"
    Android Studio trop ancien. Installez Rabbit (ou au minimum Narwhal 3 Feature Drop, 2025.1.3) : étape 3.

??? failure "« Unsupported class file major version » ou « Incompatible Gradle JVM »"
    Mauvais Java. Dans `Gradle JDK` (étape 6), sélectionnez le JDK fourni avec Android Studio (`jbr-…`). Si l'erreur persiste, sélectionnez Liberica 17 (installé à l'étape 4), et signalez-nous le cas (voir l'encadré « à confirmer » ci-dessus).

??? failure "La synchronisation Gradle tourne sans fin ou échoue sur un téléchargement"
    Réseau filtré, typiquement en établissement scolaire. Faites la première synchronisation sur une autre connexion ; ensuite tout est en cache.

??? failure "« Authentication failed » ou « Permission denied » au push"
    Jeton expiré ou permissions manquantes (vérifiez `repo` et `workflow`), ou invitation dans l'organisation pas encore acceptée (étape 1). Revoyez les étapes 7 et 8.

??? failure "Erreurs de chemin ou fichiers introuvables sous Windows"
    Le dossier du projet contient un espace, un accent, ou est trop profond. Reclonez dans `C:\ftc\`.

??? info "Toujours bloqué ?"
    Gardez une capture de l'onglet `Build` avec le message d'erreur complet : c'est la première chose qu'on vous demandera. Ressources : [FTC Docs](https://ftc-docs.firstinspires.org/), [gm0](https://gm0.org/), et le forum [FTC Community](https://ftc-community.firstinspires.org/).
