---
title: S'entraîner avec virtual_robot
description: Apprendre Java pour FTC chez soi, sans robot ni Control Hub - le livre Learn Java for FTC et le simulateur virtual_robot.
---

# S'entraîner avec virtual_robot

**Pour qui :** les élèves qui débutent en Java, ou qui veulent coder quand le robot n'est pas disponible.
**Durée :** environ 15 minutes d'installation.
**Prérequis :** Git, Android Studio et Liberica JDK 17 *Full* installés, comme dans [Poste de travail et premier build](poste-et-premier-build.md) (étapes 2 à 4).

Le robot n'est pas toujours là : il est au lycée, en démontage, ou un autre groupe s'en sert. Pour apprendre Java et le SDK FTC quand même, on combine deux outils gratuits :

- **[Learn Java for FTC](https://github.com/alan412/LearnJavaForFTC/blob/master/LearnJavaForFTC.pdf){ target="_blank" rel="noopener" }**, le livre d'Alan G. Smith (PDF gratuit, en anglais). Il apprend Java pas à pas avec une **planche de programmation** : un moteur, un servo, un potentiomètre, un capteur tactile et un capteur couleur-distance branchés sur un Control Hub. Le [dépôt GitHub de l'auteur](https://github.com/alan412/LearnJavaForFTC) contient aussi les solutions des exercices.
- **[virtual_robot](https://github.com/Beta8397/virtual_robot)**, un simulateur 2D de robot FTC. Il contient une configuration **Programming Board** qui reproduit la planche du livre : on fait les exercices sur son ordinateur, sans matériel.

## 1. Cloner virtual_robot

1. Dans Android Studio : `File` → `New` → `Project from Version Control` (ou `Clone Repository` sur l'écran d'accueil).
2. URL : `https://github.com/Beta8397/virtual_robot.git`.
3. `Directory` : un dossier **à côté** du projet de l'équipe, sans espace ni accent, par exemple `C:\ftc\virtual_robot` ou `~/ftc/virtual_robot`.
4. `Clone`, puis `Trust Project`.

Le simulateur est un projet séparé : n'y copiez pas le code de l'équipe, et ne copiez pas le simulateur dans le dépôt de l'équipe.

## 2. Choisir le JDK du simulateur

1. `File` → `Project Structure` → `Project`.
2. `SDK` : sélectionnez **Liberica 17**. S'il n'apparaît pas : `Add SDK` → `JDK…`, puis choisissez le dossier où Liberica s'est installé.
3. `Language level` : `17`.
4. `Apply`, puis `OK`.

## 3. Lancer le simulateur

Cliquez la flèche verte (configuration `Main`) dans la barre d'outils. Une fenêtre s'ouvre avec le terrain, les menus de configuration et une manette virtuelle.

1. Menu `Configuration` : choisissez **Programming Board**.
2. Menu `Op Mode` : choisissez un OpMode, par exemple `TestProgrammingBoard`.
3. Utilisez `INIT`, `START` et `STOP` comme sur la Driver Station.

La planche ne se déplace pas sur le terrain, mais vous pouvez la faire tourner à la souris pour tester l'IMU.

## 4. Faire les exercices du livre

- Écrivez vos classes et vos OpModes dans `TeamCode/src/org/firstinspires/ftc/teamcode`, avec l'annotation `@TeleOp` ou `@Autonomous`, en étendant `OpMode` ou `LinearOpMode`, comme sur le vrai robot.
- Les noms des périphériques du simulateur sont ceux du livre :

    | Périphérique | Nom dans `hardwareMap` |
    |---|---|
    | Moteur | `motor` |
    | Servo | `servo` |
    | Capteur tactile | `touch_sensor` |
    | Potentiomètre | `pot` |
    | Capteur couleur-distance | `sensor_color_distance` |
    | IMU | `imu` |

- Relancez le simulateur (flèche verte) après chaque modification de code pour qu'il la prenne en compte.

## Options utiles

??? tip "Utiliser une vraie manette"
    Ouvrez `Controller/src/virtual_robot/config/Config.java`, passez `USE_VIRTUAL_GAMEPAD` à `false`, branchez la manette et lancez le simulateur. Appuyez ensuite sur `Start` + `A` pour qu'elle devienne `gamepad1` (`Start` + `B` pour `gamepad2`).

??? tip "Fenêtre trop grande pour l'écran"
    Dans `Config.java`, réduisez `FIELD_WIDTH` (par exemple de `648` à `576`) et changez l'image de fond `BACKGROUND` pour la version de même taille (le nom de fichier finit par `576.bmp`, dans `Controller/src/virtual_robot/assets`).

## Limites

- Le simulateur fournit une **approximation du SDK FTC** : l'essentiel des exercices fonctionne, mais certaines API avancées peuvent manquer ou se comporter différemment.
- Ce n'est pas un projet Android : pas de Gradle, pas de déploiement. Ce qui marche dans le simulateur doit être **revérifié sur le vrai Control Hub**.

!!! success "Testé"
    Installation testée et fonctionnelle sous Windows avec Android Studio Rabbit et Liberica JDK 17 *Full*.

!!! question "À confirmer"
    Pas encore testé sur macOS (l'auteur pense que Liberica 17 *Full* y fonctionne). Retours bienvenus : voir [Contribuer](../contribuer.md).
