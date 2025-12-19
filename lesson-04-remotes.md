---
layout: post
title: Remotes & GitLab
description: Connect your local repository to GitLab and collaborate
image: /images/phd101212s.png
---

# Lesson 4 — Remotes (GitLab)

{: .highlight }
> **⏱️ Estimated Time:** 20-25 minutes

**Goal:** Understand what a remote is, connect your local repository to GitLab, and practice `push`, `pull`, and `fetch`.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain what a "remote" is
- Add a GitLab remote called `origin`
- Push your commits to GitLab
- Pull changes from GitLab back to your laptop

---

## Key idea: local vs remote

- Your **local repository** is on your computer.
- A **remote repository** is a copy hosted somewhere else (e.g., GitLab).

Most workflows name the primary remote `origin` by convention.

---

## Option A (recommended): Create a new GitLab repo and push

1. In GitLab (`gitlab.technomics.net`), create a new repository named `training-notes`.
   - Do **not** initialize with a README (you already have one locally).

2. In your local `training-notes` folder, add the remote URL GitLab shows you:

```bash
# HTTPS example (Technomics GitLab)
git remote add origin https://gitlab.technomics.net/<group>/<project>.git

# SSH example (Technomics GitLab)
git remote add origin git@gitlab.technomics.net:<group>/<project>.git
```

3. Verify the remote:

```bash
git remote -v
```

4. Push your `main` branch:

```bash
git push -u origin main
```

The `-u` sets an upstream so future pushes can be just `git push`.

---

## Option B: Clone an existing repo

If the repository already exists on GitLab, clone it:

```bash
git clone <repo-url>
cd <repo-name>
```

---

## Understanding Push, Pull, and Fetch

| Command | What It Does | When to Use |
|---------|-------------|------------|
| `git push` | Send your local commits to the remote | After committing, to share your work |
| `git pull` | Fetch remote changes AND merge them | Get latest changes from teammates |
| `git fetch` | Download remote changes (no merge) | Preview changes before merging |

---

## Common Workflows

### Publish your commits:

```bash
git push
```

### Get the latest from your teammate:

```bash
git pull
```

### Preview changes before accepting them:

```bash
git fetch
git log main..origin/main
git merge origin/main
```
