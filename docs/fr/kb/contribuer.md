---
title: Contribuer
description: Proposer une correction ou un nouveau guide par pull request sur le dépôt de ce site.
---

# Contribuer

La base de connaissances est ouverte : toute équipe FTC peut proposer une correction, une précision ou un nouveau guide. Tout passe par une **pull request** sur le dépôt [BladesRunners25022/website](https://github.com/BladesRunners25022/website).

## Signaler un problème

Pas le temps de rédiger la correction ? Ouvrez une [issue](https://github.com/BladesRunners25022/website/issues/new) en indiquant la page, ce qui ne va pas, et vos versions (SDK, Android Studio, système) si c'est un problème technique.

Les retours de terrain nous intéressent particulièrement, par exemple sur les points marqués **« à confirmer »**.

## Corriger une page

Chaque page a un bouton :material-file-edit-outline: **Modifier** en haut à droite.

1. Cliquez le bouton : GitHub ouvre le fichier Markdown de la page.
2. GitHub vous propose de *forker* le dépôt : acceptez.
3. Faites votre modification, puis `Commit changes…` → `Propose changes`.
4. Ouvrez la pull request en expliquant ce qui change et pourquoi.

Un membre de l'équipe relit, éventuellement pose des questions, puis merge. Le site est republié automatiquement.

## Proposer un nouveau guide

Pour un ajout plus important, travaillez en local :

```bash
git clone https://github.com/<votre-compte>/website.git
cd website
python -m venv .venv
# Windows : .venv\Scripts\activate    macOS/Linux : source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Le site s'affiche sur <http://127.0.0.1:8000> et se recharge à chaque modification.

### Organisation des fichiers

```text
docs/
  fr/                     version française (langue par défaut)
    index.md              accueil du site
    equipe.md, robot.md, soutenir.md
    kb/                   base de connaissances
      index.md
      contribuer.md
      build/              une rubrique = un dossier avec son index.md
      code/…
      outreach/
  en/                     version anglaise, mêmes noms de fichiers
  assets/                 logo, images, feuille de style (communs aux deux langues)
overrides/                gabarits du thème (accueil, pied de page)
mkdocs.yml                navigation, thème, version du SDK de référence
```

- Une page = un fichier Markdown dans `docs/fr/kb/`, avec **le même nom** dans `docs/en/kb/`. Si la traduction manque, la page française est affichée à la place.
- Ajoutez la page dans `nav` de `mkdocs.yml`, et son titre anglais dans `nav_translations`.
- Le build en CI utilise `mkdocs build --strict` : un lien cassé fait échouer la pull request. Vérifiez avec la même commande en local.

## Règles de rédaction

- **Générique.** Le contenu doit servir à n'importe quelle équipe : pas de nom d'organisation, de serveur de discussion ou de procédure interne propres à une équipe. Utilisez des exemples neutres (`mon-equipe-ftc`).
- **Aucune donnée personnelle d'élève** : ni nom, ni photo, ni pseudo, ni capture d'écran où ils apparaissent.
- **Versions explicites.** Indiquez à quelle version du SDK et des outils une instruction s'applique. Ce qui n'est pas vérifié est marqué « à confirmer ».
- **Ne pas recopier ce qui existe.** Si [gm0](https://gm0.org/) ou [FTC Docs](https://ftc-docs.firstinspires.org/) l'expliquent bien, faites un lien.
- Phrases courtes, deuxième personne du pluriel, noms des menus et boutons en `code`, tels qu'ils s'affichent dans l'interface (en anglais).

## Nouvelle version du SDK

La version de référence affichée en pied de page est définie une seule fois, dans `mkdocs.yml` :

```yaml
extra:
  sdk:
    version: "12.0"
    season: "2026-27"
    gradle: "9.1"
    agp: "8.13.2"
```

À chaque nouveau SDK, mettez-la à jour dans la même pull request que les pages concernées (recherchez les numéros de version dans `docs/`).
