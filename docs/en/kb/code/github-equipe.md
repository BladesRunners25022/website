---
title: Set up GitHub for an FTC team
description: GitHub organization, FTC SDK fork, main as default branch, Code team, access tokens and rulesets.
---

# Set up GitHub for an FTC team

**Who:** the coaches or mentors who manage the team's code.
**When:** once, when the team starts. **Time:** about 20 minutes.
**Prerequisites:** a personal GitHub account for each coach.

By the end of this guide, the team owns a code repository, up to date with the official SDK, where students can propose changes without risking the version that runs on the robot.

In the examples, the organization is called `my-ftc-team` and the repository `FtcRobotController`: replace them with your own names.

## 1. Create the GitHub organization

The organization owns the team's code. It outlives coaches and students leaving: nobody has to "hand over" a personal repository at the end of the year.

1. Signed in to your account, open [github.com/account/organizations/new](https://github.com/account/organizations/new?plan=free) and pick the `Free` plan.
2. Organization name: for example `my-ftc-team` (lowercase, no spaces). Putting your FTC team number in the name helps other teams find you.
3. Contact email: a coach's address. `This organization belongs to`: `My personal account`.
4. Add at least one more adult as an owner: `People` → `Invite member` → role `Owner`.

!!! tip "Always two owners"
    If the only owner loses access to their account, the organization can no longer be managed. Keep at least two `Owner`s.

## 2. Fork the official SDK into the organization

The FTC SDK is published by *FIRST* on GitHub. We make a copy of it (a *fork*) in the organization: this becomes the team repository.

1. Open [github.com/FIRST-Tech-Challenge/FtcRobotController](https://github.com/FIRST-Tech-Challenge/FtcRobotController).
2. Click `Fork`. `Owner`: pick the organization.
3. Keep the name `FtcRobotController` or rename it. Leave `Copy the master branch only` checked: `master` is all we need. Click `Create fork`.

!!! warning "A fork is public"
    This is common practice in FTC: team code is visible to everyone, like the SDK. If you want a private repository, use `Import repository` with the same URL instead. You then lose the `Sync fork` button that pulls SDK updates in one click.

!!! note "One fork per organization"
    GitHub allows **only one fork of a given repository per organization**. So the same repository is kept from one season to the next: see [New season](gestion-de-configuration.md#new-season).

## 3. Create the `main` branch and make it the default

The fork contains *FIRST*'s `master` branch. We keep it as an **exact copy of the SDK** and create the team's working branch, `main`, next to it. The reasoning is in [Configuration management](gestion-de-configuration.md).

1. On **the team repository** page (`my-ftc-team/FtcRobotController`, not *FIRST*'s): `Branches` → `New branch` → name `main`.
2. Under `Source`, check both the repository **and** the branch: `my-ftc-team/FtcRobotController` · `master`.
3. `Create new branch`.
4. `Settings` → `General` → `Default branch` → pick `main` → `Update`.

!!! warning "The team's `master`, not *FIRST*'s"
    In a fork, the `Source` list also offers the original repository, `FIRST-Tech-Challenge/FtcRobotController`, with its own `master` branch. Both have the same name: make sure **your organization's repository** is selected. Likewise, if you go through the branches page, make sure you are on `github.com/my-ftc-team/…` and not on `github.com/FIRST-Tech-Challenge/…`.

From now on, clones start from `main` and pull requests target `main` by default.

## 4. Create the "Code" team and invite students

Rather than granting access student by student, grant it to a GitHub team.

1. In the organization: `Teams` → `New team` → name `code`.
2. In the repository: `Settings` → `Collaborators and teams` → `Add teams` → `code`, role `Write`.
3. When a student has created their GitHub account, invite them: `People` → `Invite member` → role `Member`, team `code`.

!!! tip "GitHub usernames"
    Suggest that students pick a sober username and turn on two-factor authentication: the username shows up in the public code history.

## 5. Allow classic access tokens

To push their code to GitHub from Android Studio, students use a **classic personal access token**: it is the type of token Android Studio's GitHub login (`Log In with Token…`) expects. The organization has to accept it.

1. Organization → `Settings` → `Personal access tokens` → `Settings`.
2. *Personal access tokens (classic)* section: choose `Allow access via personal access tokens (classic)`. **Don't block them**, or students won't be able to push from Android Studio.
3. *Fine-grained personal access tokens* section: your choice, they are not used in this guide.

!!! note "No approval for classic tokens"
    Classic tokens don't go through an organization approval. On the repository, they only carry the student's rights, i.e. those of the `code` team: removing a student from the team or the organization is enough to cut their access.

Creating the token on the student side is covered in [Workstation and first build](poste-et-premier-build.md#6-create-your-github-access-token).

## 6. Protect branches with rulesets (recommended)

Goal: nobody pushes directly to `main`. Everyone works on their own branch and opens a pull request, reviewed by someone else. And nobody changes `master`, which is reserved for SDK updates.

Repository → `Settings` → `Rules` → `Rulesets` → `New ruleset` → `New branch ruleset`. Create two rulesets, with `Enforcement status`: `Active`.

| Ruleset | Target (`Target branches`) | Rules to check | `Bypass list` |
|---|---|---|---|
| `main` | `Include default branch` | `Require a pull request before merging`, `Block force pushes`, `Restrict deletions` | `Organization admin` role (for emergencies) |
| `master` | `Include by pattern` → `master` | `Restrict updates`, `Block force pushes`, `Restrict deletions` | `Organization admin` role (to run `Sync fork`) |

!!! tip "Number of approvals"
    Under `Require a pull request before merging`, you can require one approval (`Required approvals`: 1). That helps when several students work independently; with a small beginner team, an informal review by a coach is often enough. Adapt to your team.

## Checklist

- [x] Organization created, at least two owners
- [x] SDK forked into the organization
- [x] `main` branch created from `master`, set as default
- [x] `code` team with `Write` role on the repository
- [x] Classic tokens allowed
- [x] Rulesets on `main` and `master`

Next step for students: [Workstation and first build](poste-et-premier-build.md).
