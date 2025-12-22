---
layout: default
title: Lesson 5 — Branching & Merge Requests
parent: Lessons
nav_order: 5
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
- keep `main` stable
- work on a change without affecting others
- collaborate via MRs and code review

---

## Branch Naming Conventions

Use descriptive names that explain the work. Your team's convention might look like:

```
feature/<feature-name>    — New features
bugfix/<bug-name>         — Bug fixes
docs/<topic>              — Documentation updates
refactor/<area>           — Code refactoring
experiment/<idea>         — Experimental/throwaway branches
```

Examples:
```bash
git switch -c feature/user-authentication
git switch -c bugfix/login-timeout
git switch -c docs/api-reference
```

{: .note }
> Use lowercase, hyphens (not underscores), and keep names short but descriptive. Avoid timestamps or issue numbers in the branch name (use GitLab issue links in the MR description instead).

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

The `-u` (upstream) flag tells Git to remember this branch is tracked to `origin/add-agenda`. Future pushes can be just `git push`.

{: .note }
> **Forgot the `-u`?** No problem. Git will tell you what to do. You can also manually set upstream with `git branch --set-upstream-to=origin/add-agenda`.

### Check upstream tracking

```bash
# See which local branches track which remotes
git branch -vv
```

{: .highlight }
> **Example output:**
> ```
> main                    a1b2c3d [origin/main] Initial commit
> add-agenda              e4f5g6h [origin/add-agenda] Add agenda to README
> ```

---

## Open a Merge Request (MR)

On GitLab:
- In your project, go to **Merge requests** → **New merge request** (or use the prompt GitLab shows after pushing a branch)
- Open an MR from `add-agenda` → `main`
- Add a short description: what changed and why

Review checklist (lightweight but effective):
- Does this change do what it says?
- Are commit messages readable?
- Is the scope small enough?

Merge the MR (choose the merge strategy your team uses).

---

## Sync back to main

After merging the MR on GitLab:

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
- [ ] You pushed the branch to GitLab
- [ ] You opened and merged an MR
- [ ] Your local `main` is up to date after `git pull`

---

## 🎯 Next Steps

Continue to Lesson 6 to intentionally create and resolve a merge conflict.
