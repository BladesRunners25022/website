---
title: Contributing
description: Suggest a fix or a new guide through a pull request on this site's repository.
---

# Contributing

The knowledge base is open: any FTC team can suggest a fix, a clarification or a new guide. Everything goes through a **pull request** on the [BladesRunners25022/website](https://github.com/BladesRunners25022/website) repository.

## Report a problem

No time to write the fix? Open an [issue](https://github.com/BladesRunners25022/website/issues/new) with the page, what is wrong, and your versions (SDK, Android Studio, operating system) for technical issues.

Field reports are especially welcome, for example on points marked **"to be confirmed"**.

## Fix a page

Every page has an :material-file-edit-outline: **Edit** button at the top right.

1. Click it: GitHub opens the page's Markdown file.
2. GitHub offers to *fork* the repository: accept.
3. Make your change, then `Commit changes…` → `Propose changes`.
4. Open the pull request, explaining what changes and why.

A team member reviews, may ask questions, then merges. The site is republished automatically.

## Suggest a new guide

For a larger addition, work locally:

```bash
git clone https://github.com/<your-account>/website.git
cd website
python -m venv .venv
# Windows: .venv\Scripts\activate    macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

The site is served at <http://127.0.0.1:8000> and reloads on every change.

### File layout

```text
docs/
  fr/                     French version (default language)
    index.md              site home page
    equipe.md, robot.md, soutenir.md
    kb/                   knowledge base
      index.md
      contribuer.md
      build/              one section = one folder with its index.md
      code/…
      outreach/
  en/                     English version, same file names
  assets/                 logo, images, stylesheet (shared by both languages)
overrides/                theme templates (home page, footer)
mkdocs.yml                navigation, theme, reference SDK version
```

- One page = one Markdown file in `docs/fr/kb/`, with **the same name** in `docs/en/kb/`. If a translation is missing, the French page is shown instead.
- Add the page to `nav` in `mkdocs.yml`, and its English title to `nav_translations`.
- CI builds with `mkdocs build --strict`: a broken link fails the pull request. Check with the same command locally.

## Writing rules

- **Generic.** Content must work for any team: no organization names, chat servers or internal procedures specific to one team. Use neutral examples (`my-ftc-team`).
- **No students' personal data**: no names, photos, usernames, or screenshots where they appear.
- **Explicit versions.** State which SDK and tool versions an instruction applies to. Anything unverified is marked "to be confirmed".
- **Don't copy what exists.** If [gm0](https://gm0.org/) or [FTC Docs](https://ftc-docs.firstinspires.org/) explain it well, link to it.
- Short sentences; menu and button names in `code`, exactly as they appear in the interface.

## New SDK release

The reference version shown in the footer is defined once, in `mkdocs.yml`:

```yaml
extra:
  sdk:
    version: "12.0"
    season: "2026-27"
    gradle: "9.1"
    agp: "8.13.2"
```

For each new SDK, update it in the same pull request as the affected pages (search `docs/` for version numbers).
