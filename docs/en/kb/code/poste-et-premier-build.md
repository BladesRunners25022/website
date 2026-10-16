---
title: Set up your workstation and run the first build
description: Git, Android Studio, access token, cloning the team repository and a first Gradle build of FTC SDK v12.0.
---

# Set up your workstation and run the first build

**Who:** every student who codes, on their own computer.
**Time:** about 1 h 30, mostly downloads.
**Prerequisites:** the team has already [set up GitHub](github-equipe.md); about 15 GB of free disk space and at least 8 GB of RAM.

!!! info "New to Git?"
    Read [Why Git and GitHub?](pourquoi-github.md) first: 5 minutes to understand what everything you install here is for.

!!! tip "Download at home"
    School networks often block Android Studio and Gradle downloads. Do steps 2 to 5 on a home connection: after that, everything is cached.

This guide covers what is specific to this season and to our GitHub setup. For an illustrated walkthrough of the Android Studio interface, **[gm0 explains it very well](https://gm0.org/en/latest/docs/software/getting-started/using-android-studio.html)**: we link to it rather than copy it.

## 2026-27 season versions

| Item | Version |
|---|---|
| FTC SDK | v12.0 |
| Gradle | 9.1 |
| Android Gradle Plugin (AGP) | 8.13.2 |
| Android Studio **recommended** | Rabbit 1 (2026.2.1), stable since October 1, 2026 |
| Android Studio **minimum** | Narwhal 3 Feature Drop (2025.1.3) |

Rabbit supports AGP 7.1 to 9.4, so it is compatible with SDK v12.0.

!!! warning "The FTC Docs “Installing Android Studio” page is out of date"
    It still describes Android Studio Ladybug and installing a separate JDK 17. For the 2026-27 season, follow the versions above instead.

## 1. Create your GitHub account and join the team

1. Create an account at [github.com/signup](https://github.com/signup). Pick a sober username: it will appear in the public code history.
2. Turn on two-factor authentication: `Settings` → `Password and authentication`.
3. Send your username to whoever manages the team's organization.
4. Accept the invitation you receive by email (or at [github.com/notifications](https://github.com/notifications)).

## 2. Install Git

- **Windows:** download [Git for Windows](https://git-scm.com/download/win) and keep the default options.
- **macOS:** run the command below in Terminal and accept the developer tools installation it offers.

```bash
git --version
```

Then set your name and your GitHub account's email address:

```bash
git config --global user.name "First Last"
git config --global user.email "github-account-address@example.com"
```

!!! tip "Keep your address private"
    GitHub provides a `…@users.noreply.github.com` address (`Settings` → `Emails`) you can use here so your real address does not end up in the history.

## 3. Install Android Studio

1. Download the latest stable release from [developer.android.com/studio](https://developer.android.com/studio): **Rabbit** (2026.2) at the time of writing.
2. Run the installer **as administrator**: on Windows, right-click the downloaded file → `Run as administrator`; on macOS, drag Android Studio into `Applications` from an administrator account. Choose `Standard` and accept the licenses.

    !!! warning "Computer without administrator rights"
        On a computer managed by the school or a parent, ask whoever has administrator rights to run the installation. Without them, the installation fails or stops partway.
3. Let it finish downloading the Android components: this is the longest step.
4. Android Studio already installed? Check its version under `Help` → `About` (macOS: `Android Studio` → `About`). Below Narwhal 3 Feature Drop (2025.1.3), SDK v12.0 will not sync: update.

Details and screenshots: [gm0, *Using Android Studio*](https://gm0.org/en/latest/docs/software/getting-started/using-android-studio.html).

## 4. Clone the team repository

The team repository is public: no token or GitHub login is needed to clone it.

1. Welcome screen: `Clone Repository` (or `File` → `New` → `Project from Version Control`).
2. URL: the team repository's, of the form `https://github.com/my-ftc-team/FtcRobotController.git`.
3. `Directory`: a short folder path **with no spaces or accented characters**, for example `C:\ftc\FtcRobotController` or `~/ftc/FtcRobotController`.
4. `Clone`, then `Trust Project`.

## 5. Run the first build

!!! danger "Decline any Gradle or AGP upgrade"
    When the project opens, Android Studio may offer "Upgrade Gradle" or the **AGP Upgrade Assistant**: Rabbit suggests moving to AGP 9.x. **Decline.** The FTC project must keep the versions shipped by *FIRST* (Gradle 9.1, AGP 8.13.2).

1. Check which Java Gradle uses: `Settings` → `Build, Execution, Deployment` → `Build Tools` → `Gradle` → `Gradle JDK`. Select the JDK bundled with Android Studio (`jbr-…`, JetBrains Runtime).
2. Click the elephant icon `Sync Project with Gradle Files`. The first sync downloads a lot of dependencies: be patient.
3. `Build` → `Make Project`.

It worked when the `Build` tab at the bottom shows **`BUILD SUCCESSFUL`**.

!!! question "JDK: to be confirmed"
    With Gradle 9.1, the JDK bundled with Android Studio **should be enough**, with no separate JDK install. We have **not yet tested** this on every setup. If you can confirm it (or not), please tell us: see [Contributing](../contribuer.md). If it fails, see troubleshooting below.

## 6. Create your GitHub access token

To **send** code to GitHub (*push*) and work with pull requests, you need to authenticate. The token replaces your password: it is what Android Studio presents to GitHub. **Treat it like a password**: never paste it into a chat or into the code.

1. Open [github.com/settings/tokens/new](https://github.com/settings/tokens/new) (*Personal access token (classic)*).
2. `Note`: `android-studio`. `Expiration`: `Custom`, until the end of the season.
3. `Select scopes`: check exactly these scopes, required by Android Studio:

    | Scope | Where to find it | What it is for |
    |---|---|---|
    | `repo` | top of the list | push your code to the team repository, work with pull requests |
    | `workflow` | right below `repo` | push changes to the SDK's `.github/workflows` files |
    | `gist` | middle of the list | share code snippets from Android Studio |
    | `read:org` | under `admin:org` (check **only** `read:org`) | see the team organization's repositories |
    | `read:user` | under `user` | read your GitHub profile |
    | `user:email` | under `user` | read your GitHub email address |

4. `Generate token`, then copy it right away: GitHub only shows it once.

!!! tip "Didn't copy the token, or lost it?"
    No need to panic: GitHub can't show it again, but you can make a new one. In `Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)`, delete the old token (`Delete`), then create a new one by going through this step again from the start. If the token was already registered in Android Studio, replace it in step 7.

!!! warning "A classic token opens all your repositories"
    With `repo`, the token gives access to **every** repository your account can reach, not just the team's. Keep an expiration date and delete the token (`Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)`) if you think it leaked.

## 7. Use the token in Android Studio

You register the token once in Android Studio, which then uses it automatically for every *push* to GitHub and to show pull requests.

1. `Settings` (macOS: `Android Studio` → `Settings`).
2. `Version Control` → `GitHub` → `+` → `Log In with Token…`
3. Paste the token → `Add Account`. Your GitHub username shows up in the account list.
4. On Windows, also check `Version Control` → `Git` → `Test`: Android Studio must find Git.

!!! tip "A login window still opens on the first push?"
    Depending on the setup, Git itself may ask for credentials when you *push*:

    - **Git Credential Manager** window (*Connect to GitHub*, Windows): choose `Token` and paste the token, rather than `Sign in with your browser`;
    - **username / password** window: username = your GitHub username, password = **the token** (not your GitHub password).

    The credentials are then remembered: you will only be asked again when the token expires.

## 8. First OpMode, first branch

All team code goes in the `TeamCode` module. *FIRST*'s samples live in the `FtcRobotController` module and are not modified.

1. Start from an up-to-date `main`: bottom right, click the branch name → `main` → `Update`. Then `New Branch` → `firstname/first-opmode`.
2. Open the samples: `FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples`.
3. Copy `BasicOpMode_Linear.java` into `TeamCode/src/main/java/org/firstinspires/ftc/teamcode`.
4. In the copied file, delete the `@Disabled` line and change the name in `@TeleOp(name = "…")`.
5. `Build` → `Make Project`: still `BUILD SUCCESSFUL`?
6. `Git` → `Commit`: check the file, write a clear message ("Add first TeleOp OpMode"), then `Commit and Push`. This *push* is what uses your token (step 7).
7. On GitHub, open the suggested pull request to `main`.

Branch and pull request rules are explained in [Configuration management](gestion-de-configuration.md).

## Troubleshooting

??? failure "Android Studio offers “Upgrade Gradle” or the “AGP Upgrade Assistant”"
    Decline and close the window. If you already accepted: `Git` → `Rollback` on the modified files, or clone the repository again.

??? failure "“Sync failed” right after opening, or a message about the Android Gradle Plugin version"
    Android Studio is too old. Install Rabbit (or at least Narwhal 3 Feature Drop, 2025.1.3): step 3.

??? failure "“Unsupported class file major version” or “Incompatible Gradle JVM”"
    Wrong Java. In `Gradle JDK` (step 5), select the JDK bundled with Android Studio (`jbr-…`). If the error persists, install JDK 21 from [adoptium.net](https://adoptium.net/temurin/releases/?version=21), select it, and report your case to us (see the "to be confirmed" box above).

??? failure "Gradle sync never ends or fails on a download"
    Filtered network, typically at school. Do the first sync on another connection; after that, everything is cached.

??? failure "“Authentication failed” or “Permission denied” on push"
    Token expired or missing scopes (check `repo` and `workflow`), or organization invitation not accepted yet (step 1). Go back to steps 6 and 7.

??? failure "Path errors or files not found on Windows"
    The project folder contains a space or an accented character, or is nested too deep. Clone again into `C:\ftc\`.

??? info "Still stuck?"
    Keep a screenshot of the `Build` tab with the full error message: it is the first thing you will be asked for. Resources: [FTC Docs](https://ftc-docs.firstinspires.org/), [gm0](https://gm0.org/), and the [FTC Community](https://ftc-community.firstinspires.org/) forum.
