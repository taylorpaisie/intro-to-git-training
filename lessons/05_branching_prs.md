---
layout: default
title: Lesson 5 — Branching & Pull Requests
parent: Lessons
nav_order: 5
---

# Lesson 5 — Branching & Pull Requests

{: .highlight }
> **⏱️ Estimated Time:** 25-30 minutes

**Goal:** Use branches to isolate work, push a branch to GitHub, and open a pull request (PR).

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Create and switch branches
- Make commits on a feature branch
- Push a branch to GitHub
- Open a pull request and understand the review/merge flow

---

## Why branches?

Branches let you:
- keep `main` stable
- work on a change without affecting others
- collaborate via PRs and code review

---

## Create a branch

From your `training-notes` repository:

```bash
git status
```

Make sure you’re clean (no uncommitted changes), then:

```bash
git switch -c add-agenda
```

(`git checkout -b add-agenda` is the older equivalent.)

---

## Make a change and commit it

Edit `README.md` and add an agenda section:

```markdown
## Agenda

- Setup
- Commits
- Remotes
- Branches
- Conflicts
```

Then:

```bash
git status
git diff

git add README.md
git commit -m "Add agenda to README"
```

---

## Push the branch

```bash
git push -u origin add-agenda
```

---

## Open a Pull Request (PR)

On GitHub:
- You should see a prompt to “Compare & pull request”
- Open a PR from `add-agenda` → `main`
- Add a short description: what changed and why

Review checklist (lightweight but effective):
- Does this change do what it says?
- Are commit messages readable?
- Is the scope small enough?

Merge the PR (choose the merge strategy your team uses).

---

## Sync back to main

After merging the PR on GitHub:

```bash
git switch main
git pull
```

Optional cleanup:

```bash
# Delete the local branch
git branch -d add-agenda

# Delete the remote branch
git push origin --delete add-agenda
```

---

## ✅ Lesson Checklist

- [ ] You created a branch and made a commit on it
- [ ] You pushed the branch to GitHub
- [ ] You opened and merged a PR
- [ ] Your local `main` is up to date after `git pull`

---

## 🎯 Next Steps

Continue to Lesson 6 to intentionally create and resolve a merge conflict.
