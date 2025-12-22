---
layout: default
title: Glossary & Command Reference
nav_order: 8
has_children: false
---

# 📚 Glossary & Command Reference

Quick lookups for Git terms and commands used throughout the training.

---

## 🔤 Glossary

### Branch
A **branch** is an independent line of development. Branches let you work on features without affecting `main`. Branches are cheap in Git—create as many as you need.

**Related commands:** `git switch`, `git branch`, `git merge`

### Commit
A **commit** is a snapshot of your project at a specific point in time. It includes changes, an author, a timestamp, and a message describing what changed.

**Related commands:** `git commit`, `git log`, `git show`

### Merge
**Merging** combines two branches together. You merge a feature branch into `main` (or vice versa) to integrate changes.

**Related commands:** `git merge`, `git merge --abort`

### Merge Conflict
A **merge conflict** happens when Git can't automatically combine two branches because they changed the same lines. You must manually resolve it.

**Related commands:** `git merge`, `git status`, `git add` (after resolving)

### Merge Request (MR)
A **merge request** is a GitLab feature for proposing changes. You push a branch, open an MR on GitLab, and team members review before merging.

**Platform:** GitLab (GitHub calls it a "Pull Request" or "PR")

### Pull Request (PR)
Same as a merge request, but on GitHub. This training uses **GitLab MRs**, not GitHub PRs.

### Push
**Pushing** uploads your local commits to a remote repository (e.g., GitLab). Your teammates can then pull your changes.

**Related commands:** `git push`, `git push -u`

### Pull
**Pulling** downloads remote commits and merges them into your local branch. It's `git fetch + git merge`.

**Related commands:** `git pull`, `git fetch`

### Fetch
**Fetching** downloads remote history without changing your working files. Use `fetch` to check what's new without merging yet.

**Related commands:** `git fetch`, `git log --all`

### Staging Area (Index)
The **staging area** is where you prepare changes before committing. Think of it as a box of items ready to ship.

**Related commands:** `git add`, `git restore --staged`

### Remote
A **remote** is a copy of your repository hosted somewhere else (e.g., GitLab). The default remote is usually called `origin`.

**Related commands:** `git remote`, `git push`, `git pull`

### Origin
By convention, **`origin`** is the name of your primary remote (usually on GitLab). It's just a local nickname—the real remote is the URL.

### HEAD
**`HEAD`** is a pointer to your current commit. `HEAD~1` means "one commit before HEAD." `HEAD~3` means "three commits back."

**Related commands:** `git log`, `git reset HEAD~1`, `git revert HEAD`

### Stash
**Stashing** temporarily saves your uncommitted changes so you can switch branches or pull. You can reapply stashed changes later.

**Related commands:** `git stash`, `git stash pop`, `git stash list`

### Rebase
**Rebasing** is an alternative to merging. It replays your commits on top of another branch. Advanced feature—stick with `merge` for now.

**Related commands:** `git rebase`, `git rebase -i`

---

## 📋 Command Reference by Task

### Checking Status & Viewing History

| Task | Command |
|------|---------|
| What changed since last commit? | `git diff` |
| What staged changes are ready? | `git diff --staged` |
| Quick commit history | `git log --oneline` |
| Last 5 commits | `git log -5` |
| Visual branch history | `git log --oneline --graph --all` |
| Details of a specific commit | `git show <hash>` |
| Search commits by message | `git log --grep="keyword"` |
| Search commits by author | `git log --author="Name"` |
| Search commits that touched a file | `git log -- filename` |

### Creating & Switching Branches

| Task | Command |
|------|---------|
| List local branches | `git branch` |
| List all branches (including remote) | `git branch -a` |
| Show upstream tracking | `git branch -vv` |
| Create a new branch | `git switch -c branch-name` |
| Switch to existing branch | `git switch branch-name` |
| Delete a local branch | `git branch -d branch-name` |
| Delete a remote branch | `git push origin --delete branch-name` |

### Staging & Committing

| Task | Command |
|------|---------|
| Stage a specific file | `git add filename` |
| Stage all changes | `git add .` or `git add -A` |
| Unstage a file (keep changes) | `git restore --staged filename` |
| Discard changes to a file | `git restore filename` |
| Commit staged changes | `git commit -m "message"` |
| Commit with subject + body | `git commit -m "Subject"` (then editor opens for body) |
| Stage all tracked files + commit | `git commit -a -m "message"` |
| Fix the last commit message | `git commit --amend -m "new message"` |
| Add files to last commit | `git add file` then `git commit --amend --no-edit` |

### Working with Remotes

| Task | Command |
|------|---------|
| List configured remotes | `git remote -v` |
| Get details about a remote | `git remote show origin` |
| Add a remote | `git remote add origin <url>` |
| Change a remote URL | `git remote set-url origin <new-url>` |
| Fetch updates from remote | `git fetch origin` |
| Pull remote changes + merge | `git pull` |
| Push to remote | `git push` |
| Push and set upstream (first time) | `git push -u origin branch-name` |
| Delete remote branch | `git push origin --delete branch-name` |

### Undoing Changes

| Task | Command | Notes |
|------|---------|-------|
| Unstage before committing | `git restore --staged <file>` | Changes stay in working directory |
| Discard uncommitted changes | `git restore <file>` | **Permanent** — use with care |
| Undo last commit (keep changes) | `git reset --soft HEAD~1` | Only use if NOT yet pushed |
| Undo last commit (discard changes) | `git reset --hard HEAD~1` | **Permanent** — only local |
| Create new commit that undoes changes | `git revert <hash>` | Safe for shared branches |
| Recover a deleted branch | `git reflog` then `git switch -c branch <hash>` | Works for ~90 days |

### Handling Merge Conflicts

| Task | Command |
|------|---------|
| Start a merge | `git merge branch-name` |
| Check conflicted files | `git status` |
| Abort merge attempt | `git merge --abort` |
| Resolve and complete merge | (edit files) → `git add` → `git commit` |

---

## 🔑 Essential Git Aliases (Optional)

Make Git faster with shortcuts. Add these to your Git config:

```bash
git config --global alias.co "switch"
git config --global alias.br "branch"
git config --global alias.ci "commit"
git config --global alias.st "status"
git config --global alias.unstage "restore --staged"
git config --global alias.last "log -1"
git config --global alias.visual "log --oneline --graph --all"
git config --global alias.undo "reset --soft HEAD~1"
```

Then use them:

```bash
git co feature/my-feature    # same as git switch feature/my-feature
git st                        # same as git status
git visual                    # same as git log --oneline --graph --all
```

---

## 🆘 Emergency Commands

When something goes wrong, here's what to try (in order):

1. **Panic button:** `git merge --abort` or `git rebase --abort`
2. **See what happened:** `git reflog` (shows last 30 actions)
3. **Recover work:** `git reset --soft HEAD~1` (undo, keep changes)
4. **Ask for help:** Share your `git log --oneline -10` with a teammate

---

## 📖 Additional Resources

- [Official Git Book](https://git-scm.com/book) — Comprehensive reference
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials) — Great visual guides
- [Oh Shit, Git!?!](https://ohshitgit.com/) — Funny but practical error recovery guide
- [Your Team's Style Guide](../index.md) — Check with your team lead for conventions

---

## ✅ Using This Reference

- **Stuck on a command?** Search this page for the task you're trying to do
- **Unsure what a term means?** Check the glossary
- **Want to speed up?** Set up aliases (see above)
- **Forgot the syntax?** Copy/paste from the command reference

