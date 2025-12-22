---
layout: default
title: Lesson 7 — Common Mistakes & How to Fix Them
nav_order: 7
parent: Lessons
---

# 🚨 Lesson 7 — Common Mistakes & How to Fix Them

{: .highlight }
> **⏱️ Estimated Time:** 15-20 minutes

**Goal:** Learn what to do when something goes wrong. Everyone makes mistakes with Git—here's how to recover safely.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Recognize common Git mistakes
- Understand when to use `reset`, `revert`, and `amend`
- Safely recover from mistakes without data loss
- Know when to ask for help

---

## Mistake #1: Committed to `main` by accident

You realized your work belonged on a feature branch, not `main`.

### Scenario

```bash
git log --oneline -5
# a1b2c3d (HEAD -> main) My new feature (oops!)
# e4f5g6h Merge MR for other feature
# ...
```

### Fix (Safe — doesn't rewrite history)

Use `git revert` to create a **new commit** that undoes the changes:

```bash
# Create a commit that reverses the bad commit
git revert a1b2c3d

# Now create your feature branch with the work
git switch -c feature/my-feature

# Cherry-pick (reapply) the work on the feature branch
git cherry-pick a1b2c3d
```

Then delete the revert commit from main (if it was already pushed, let someone with permissions handle cleanup).

### Alternative (Use only if not yet pushed!)

If the commit is **only on your local machine** and not pushed:

```bash
# Undo the last commit, keeping your changes
git reset --soft HEAD~1

# Now you're back to before the commit, with changes ready to stage
# Create the feature branch
git switch -c feature/my-feature
git add .
git commit -m "My new feature"
```

{: .warning }
> **DO NOT use `git reset` on shared branches!** If others have pulled your commit, you'll cause problems. Use `git revert` instead.

---

## Mistake #2: Forgot to add a file before committing

You made a commit but forgot to include some files.

### Scenario

```bash
git status
# Changes not staged for commit:
#   modified:   utils/helpers.js
```

### Fix (One-liner)

```bash
# Add the forgotten file and amend the last commit
git add utils/helpers.js
git commit --amend --no-edit
```

The `--no-edit` flag keeps the old commit message. If you want to change the message too:

```bash
git add utils/helpers.js
git commit --amend -m "New message"
```

{: .note }
> `git commit --amend` rewrites the last commit. Only use on local work. If already pushed, don't amend.

---

## Mistake #3: Committed something sensitive (password, API key, secret)

You accidentally committed a secret file that should never be in the repo.

### Immediate Action

1. **Do NOT push yet** (if you haven't pushed, problem solved — just remove it and recommit).
2. **If already pushed:** Treat the secret as **compromised**. Rotate the key/password immediately.

### Remove the file from history

```bash
# Remove the file from Git history entirely
git filter-branch --tree-filter 'rm -f path/to/secret.env' HEAD

# Or (recommended for large repos):
git log --all --full-history -- secrets.txt | head -1
git rebase -i <commit-before-the-secret>
# Mark the commit with the secret as 'drop'
```

Then:

```bash
# Force-push to update the remote (careful with shared branches!)
git push -f origin main
```

{: .warning }
> **Secrets in Git are permanent.** Even after removing files, the history is cached. If you accidentally committed a real secret, **rotate it immediately** and inform your team. Prevention is easier: use `.gitignore` and `.env` files for secrets.

---

## Mistake #4: Wrong commit message

You want to fix a typo or improve the message of your last commit.

### Fix

```bash
# Amend the last commit with a new message
git commit --amend -m "Corrected message"
```

Or if you want to change an **older commit** message:

```bash
# Rebase interactively
git rebase -i HEAD~3  # Last 3 commits

# Change 'pick' to 'reword' for the commit you want to fix
# Save and edit the message in the editor that appears
```

{: .warning }
> Don't amend or rebase commits that are already pushed to a shared branch. Create a new commit instead: `git commit -m "Fix: corrected message in previous commit"`.

---

## Mistake #5: Merge conflict seems impossible to resolve

You're in the middle of a merge and the conflict is too complex.

### Abort and start over

```bash
# Cancel the merge entirely
git merge --abort

# You're back to before the merge attempt
git status  # Should say "On branch main" with no conflicts
```

Then:

```bash
# Try again, or ask for help
git merge <branch>
```

{: .note }
> Merge conflicts are normal. If a conflict seems impossible, slow down: look at both versions, talk to the person who made the other changes, or ask your team lead.

---

## Mistake #6: Deleted a branch by accident

You ran `git branch -d my-branch` and now it's gone.

### Recover (usually possible)

```bash
# See recently deleted branches
git reflog

# Find the branch in the output, note its commit hash (e.g., a1b2c3d)

# Recreate the branch pointing to that commit
git switch -c my-branch a1b2c3d
```

{: .note }
> Git keeps references for ~90 days. If you need to recover a branch older than that, ask your team or GitLab administrator.

---

## Mistake #7: `git push` rejected — need to pull first

You tried to push but got an error.

### Scenario

```bash
git push
# error: failed to push some refs to origin
# hint: Updates were rejected because the tip of your current branch is behind
```

### Fix

```bash
# Pull the remote changes first
git pull

# If there's a conflict, resolve it (see Lesson 6)

# Then push
git push
```

{: .highlight }
> This is **not** a mistake — it's Git protecting you from overwriting work. Always `pull` before pushing.

---

## Decision Tree: Which Fix Should I Use?

```
Did you already push?
├─ No  ──→ git reset --soft HEAD~1 (undo, keep changes)
└─ Yes ──→ Did you want to keep the changes?
           ├─ Yes ──→ git revert (undo with new commit)
           └─ No  ──→ git reset --hard HEAD~1 (undo, lose changes)
```

{: .warning }
> **The nuclear option:** If you're truly stuck, just create a new commit that fixes things. It's safer than rewriting history.

---

## When to Ask for Help

You should ask your team lead or a more experienced Git user if:

- You're about to use `--force` or `--hard` on a shared branch
- You deleted someone else's work and can't recover it
- You're in the middle of a long interactive rebase and confused
- A merge conflict involves files you don't understand
- You're not sure what a command will do

**Git is designed to be forgiving.** In most cases, your work isn't lost — you just need to know where to look.

---

## ✅ Lesson Checklist

- [ ] You understand `git revert` vs `git reset`
- [ ] You know how to recover a deleted branch
- [ ] You can fix a commit message with `--amend`
- [ ] You know to abort a merge with `git merge --abort` if stuck

---

## 🎯 Next Steps

At this point, you have a complete Git toolkit! Practice these commands by intentionally making mistakes in a test repository, then fixing them.

When you're confident, help your teammates get up to speed.

