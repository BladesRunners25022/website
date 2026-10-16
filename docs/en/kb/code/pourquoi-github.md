---
title: Why Git and GitHub?
description: An introduction for high-school students on an FTC team - what Git and GitHub are for, and the words to know.
---

# Why Git and GitHub?

**Who:** students who are going to code, before installing anything. **Time:** a 5-minute read.

## The problem

The night before a competition. Someone improves the arm code, and suddenly the robot no longer runs its autonomous. What changed? Who changed it? How do you get back to yesterday's version that worked?

Or: the "official" code is on the laptop of a student who is absent on match day. Or there are three versions on three USB sticks, one of them called `final_code_v3_REAL.zip`.

As soon as several people code the same robot, you need a tool to stay organized. That is what Git and GitHub are for.

## Git: the history of the code

Git records the **history** of your project. At each important step, you make a **commit**: a snapshot of all the code, with a message saying what changed and why.

- You know **who** changed **what**, **when**, and **why**.
- You can **go back** to any earlier version.
- You can **compare** two versions line by line to find the mistake.

It is a bit like the version history of a shared document, but for a whole project, and you decide when to take the snapshot.

## Branches: working without stepping on each other

A **branch** is a working copy of the code. Everyone develops their topic on their own branch (driving, autonomous, the arm…) without getting in others' way. The team's main branch, `main`, **always** stays in a working state: it is what goes on the robot for a match.

When your work is ready, you **merge** it into `main`.

## GitHub: the team's code online

Git runs on your computer. **GitHub** is the website that hosts the shared version of the code, the team **repository**:

- **Reachable from anywhere**: at school, at home, at a competition. A lost or broken laptop loses nothing.
- **Review before merging**: to bring your branch into `main`, you open a **pull request**. Someone else reviews your changes before they go in, like having a presentation proofread before handing it in.
- **SDK updates**: the FTC SDK itself is published by *FIRST* on GitHub. Our repository is a copy of it (a *fork*), so each new release can be pulled in with a few clicks.

## What's in it for you?

- Git and GitHub are used in most software companies and projects. You are learning a professional tool.
- Your work is **visible and credited**: every commit carries your name, which also helps tell the project's story in the engineering portfolio.

## The vocabulary in one minute

| Word | What it means |
|---|---|
| **Repository** (repo) | The project and its whole history. The team's lives on GitHub. |
| **Clone** | Download a copy of the repository to your computer. |
| **Commit** | A saved snapshot of the code, with a message. |
| **Branch** | A separate line of work, to develop a topic without getting in others' way. |
| **Push** | Send your commits from your computer to GitHub. |
| **Pull** | Bring other people's commits onto your computer. |
| **Pull request** (PR) | A request to bring your branch into `main`, with a review. |
| **Merge** | Bring the changes of one branch into another. |
| **Fork** | A copy of a repository under another owner, here our copy of *FIRST*'s SDK. |

## What next?

1. [Set up your workstation and run the first build](poste-et-premier-build.md): Git, Android Studio and your first branch.
2. [Configuration management](gestion-de-configuration.md): the team's rules for branches and pull requests.
