---
layout: post
title: Branching & Merge Requests
description: Isolate work and collaborate using branches and merge requests
image: /images/phd101212s.png
---

# Lesson 5 — Branching & Merge Requests

{: .highlight }
> **⏱️ Estimated Time:** 25-30 minutes

**Goal:** Use branches to isolate work, push a branch to GitLab, and open a merge request (MR).

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Create and switch branches
- Make commits on a feature branch
- Push a branch to GitLab
- Open a merge request and understand the review/merge flow

---

## Why branches?

Branches let you:
- Keep `main` stable
- Work on a change without affecting others
- Collaborate via MRs and code review

---

## Create a branch

From your `training-notes` repository:

```bash
git status
```

Make sure you're clean (no uncommitted changes), then:

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

Push your branch to GitLab:

```bash
git push -u origin add-agenda
```

The `-u` sets the upstream branch.

---

## Open a Merge Request

1. Go to GitLab (`gitlab.technomics.net`)
2. Navigate to your `training-notes` repository
3. Click the **Merge Requests** tab
4. Click **New Merge Request**
5. Select:
   - **Source branch:** `add-agenda`
   - **Target branch:** `main`
6. Add a title and description
7. Click **Create Merge Request**

---

## Review and Merge

Your merge request is now open for review:

- Teammates can review your changes
- Discuss feedback in comments
- Make additional commits to address feedback
- Once approved, **merge** the MR

Then delete the branch to keep things clean.

---

## Viewing Branches

List all branches:

```bash
git branch
git branch -a  # includes remote branches
```

Switch between branches:

```bash
git switch main
git switch add-agenda
```
