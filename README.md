# Blades Runners 92 · site d'équipe FTC

Site de l'équipe FIRST Tech Challenge Blades Runners 92 (Levallois-Perret, accueillie par le lycée Léonard de Vinci), avec sa base de connaissances FTC ouverte à toutes les équipes. Français et anglais.

Site publié : https://bladesrunners25022.github.io/website/

```bash
pip install -r requirements.txt
mkdocs serve          # aperçu local sur http://127.0.0.1:8000/website/
mkdocs build --strict # même vérification que la CI
```

- Pages : `docs/fr/` et `docs/en/` (mêmes noms de fichiers).
- Identité visuelle : `docs/assets/stylesheets/blades.css` (couleurs du logo en haut du fichier), logo dans `docs/assets/images/`.
- Accueil : textes du bandeau dans le front matter de `docs/*/index.md`, gabarit `overrides/home.html`.
- Pour contribuer à la base de connaissances : page « Contribuer » du site (`docs/fr/kb/contribuer.md`).
