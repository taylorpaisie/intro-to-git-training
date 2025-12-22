---
layout: default
title: Lesson 4 — Remotes (GitLab)
parent: Lessons
nav_order: 4
---

# Lesson 4 — Remotes (GitLab)

{: .highlight }
> **⏱️ Estimated Time:** 20-25 minutes

**Goal:** Understand what a remote is, connect your local repository to GitLab, and practice `push`, `pull`, and `fetch`.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain what a “remote” is
- Add a GitLab remote called `origin`
- Push your commits to GitLab
- Pull changes from GitLab back to your laptop

---

## Key idea: local vs remote

- Your **local repository** is on your computer.
- A **remote repository** is a copy hosted somewhere else (e.g., GitLab).

Most workflows name the primary remote `origin` by convention.

{: .note }
> **`origin` is just a local name.** The real remote is the URL. You can have multiple remotes (`origin`, `upstream`, etc.), each with different URLs.

---

## HTTPS vs SSH

Both work, but they differ in setup and workflow:

| Method | Auth | Setup | Each Push/Pull |
|--------|------|-------|---------------|
| **HTTPS** | Username + Password (or token) | No extra setup needed | May prompt for password/token |
| **SSH** | SSH key pair | One-time SSH key setup | No prompts (automatic with agent) |

**Recommendation for most users:** Start with HTTPS if you're new (simpler), switch to SSH later when you're comfortable.

**If you set up SSH in Lesson 1**, you can use the SSH URLs. Otherwise, use HTTPS.

---

## Option A (recommended): Create a new GitLab repo and push

1. In GitLab (`gitlab.technomics.net`), create a new repository named `training-notes`.
   - Do **not** initialize with a README (you already have one locally).

2. In your local `training-notes` folder, add the remote URL GitLab shows you:

```bash
# HTTPS example (Technomics GitLab)
# git remote add origin https://gitlab.technomics.net/<group>/<project>.git

# SSH example (Technomics GitLab)
# git remote add origin git@gitlab.technomics.net:<group>/<project>.git

# If you ever work with GitLab.com too, the format is the same:
# https://gitlab.com/<group-or-user>/training-notes.git
# git@gitlab.com:<group-or-user>/training-notes.git
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

## Practice: make a change on GitLab, then pull

1. On GitLab, edit `README.md` directly in the browser and commit the change.
2. Back on your computer:

```bash
git pull
```

---

## Troubleshooting Authentication & Common Errors

### Authentication Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `fatal: Authentication failed` | Password is wrong, token expired, or key not loaded | For HTTPS: Use GitLab personal access token (not password). For SSH: Ensure SSH key is added to GitLab and `ssh-add` has loaded it. |
| `error: the username/password you supplied is incorrect` | Credentials don't match GitLab account | Use `git config --unset credential.helper` to clear cached credentials, then try again with correct email/token. |
| `Permission denied (publickey)` | SSH key not found or not authorized | Run `ssh -T git@gitlab.technomics.net` to test. Check that your SSH key is added to GitLab. |

### Empty Remote Issues

If you create an empty repository on GitLab without a README:

```bash
# First push may need to explicitly set upstream
git push -u origin main

# After that, git push alone works
git push
```

If GitLab complains "repository is empty," it's expected. After you push, this message goes away.

### Checking Remote Details

```bash
# See what remote is configured and its URL
git remote -v

# See more details about a remote
git remote show origin

# If you made a mistake with the URL:
git remote set-url origin <new-url>
```

---

## ✅ Lesson Checklist

- [ ] You can explain what a remote is
- [ ] `git remote -v` shows `origin`
- [ ] You successfully pushed `main` to GitLab
- [ ] You successfully pulled a change from GitLab

---

## 🎯 Next Steps

Continue to Lesson 5 to learn branching and merge requests.
