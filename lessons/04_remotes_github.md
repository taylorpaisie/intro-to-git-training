---
layout: default
title: Lesson 4 — Remotes (GitHub)
parent: Lessons
nav_order: 4
---

# Lesson 4 — Remotes (GitHub)

{: .highlight }
> **⏱️ Estimated Time:** 20-25 minutes

**Goal:** Understand what a remote is, connect your local repository to GitHub, and practice `push`, `pull`, and `fetch`.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain what a “remote” is
- Add a GitHub remote called `origin`
- Push your commits to GitHub
- Pull changes from GitHub back to your laptop

---

## Key idea: local vs remote

- Your **local repository** is on your computer.
- A **remote repository** is a copy hosted somewhere else (e.g., GitHub).

Most workflows name the primary remote `origin` by convention.

---

## Option A (recommended): Create a new GitHub repo and push

1. On GitHub, create a new repository named `training-notes`.
   - Do **not** initialize with a README (you already have one locally).

2. In your local `training-notes` folder, add the remote URL GitHub shows you:

```bash
# HTTPS example
# git remote add origin https://github.com/<org-or-user>/training-notes.git

# SSH example
# git remote add origin git@github.com:<org-or-user>/training-notes.git
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

If the repository already exists on GitHub, clone it:

```bash
git clone <repo-url>
cd <repo-name>
```

---

## Fetch vs pull

- `git fetch` downloads remote history/branches but doesn’t change your working files.
- `git pull` is roughly: **fetch + merge** (or fetch + rebase, depending on config).

Try:

```bash
git fetch origin
```

Then inspect what you have locally:

```bash
git log --oneline --graph --all
```

---

## Practice: make a change on GitHub, then pull

1. On GitHub, edit `README.md` directly in the browser and commit the change.
2. Back on your computer:

```bash
git pull
```

---

## ✅ Lesson Checklist

- [ ] You can explain what a remote is
- [ ] `git remote -v` shows `origin`
- [ ] You successfully pushed `main` to GitHub
- [ ] You successfully pulled a change from GitHub

---

## 🎯 Next Steps

Continue to Lesson 5 to learn branching and pull requests.
