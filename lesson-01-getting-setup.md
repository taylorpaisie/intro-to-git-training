---
layout: post
title: Getting Set Up
description: Confirm Git installation, set your identity, and create your first repository
image: /images/phd101212s.png
---

# Lesson 1 — Getting Set Up

{: .highlight }
> **⏱️ Estimated Time:** 20 minutes

**Goal:** Confirm Git is installed, set your identity, learn how to get help, and create your first local repository.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain (at a high level) what Git is and why teams use it
- Configure your Git identity
- Create your first local repository
- Understand how Git stores history

---

## What is Git?

Git is a **version control system** (VCS) that tracks changes to files over time. Think of it as a save-game system for your code.

**Why use Git?**
- **History:** See every change ever made to a file
- **Collaboration:** Multiple people can work on the same project without stepping on each other's toes
- **Backup:** Your code is safely stored in multiple places
- **Branching:** Work on new features without affecting the main codebase

---

## Configure Your Identity

Before making commits, tell Git who you are:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

{: .note }
> Use the `--global` flag to apply this configuration to all repositories on your computer. Omit it to configure just the current repository.

Verify it worked:

```bash
git config --global user.name
git config --global user.email
```

---

## Create Your First Repository

Let's create a simple project to practice with. Pick a location on your computer (like your Documents folder):

```bash
mkdir training-notes
cd training-notes
```

Now initialize a Git repository:

```bash
git init
```

You've just created your first Git repository! A hidden `.git` folder now exists inside `training-notes`. This is where Git stores all the history.

Verify:

```bash
ls -la
```

You should see a `.git` directory.

---

## Get Help

Git has built-in help:

```bash
git help <command>
git help commit
```

Or for a quick summary:

```bash
git <command> --help
```
