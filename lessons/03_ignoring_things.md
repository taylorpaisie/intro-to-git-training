---
layout: default
title: Lesson 3 — Ignoring Things
parent: Lessons
nav_order: 3
---

# Lesson 3 — Ignoring Things

{: .highlight }
> **⏱️ Estimated Time:** 10-15 minutes

**Goal:** Learn how to keep temporary/build/local files out of your repository using `.gitignore`.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain why some files should not be committed
- Add ignore patterns to a `.gitignore`
- Understand why a file might *still* be tracked after adding it to `.gitignore`

---

## Why ignore files?

Some files are not part of the “source of truth” for a project:
- Build outputs (e.g., `dist/`, `build/`)
- Dependency folders (e.g., `node_modules/`)
- OS/editor noise (e.g., `.DS_Store`, `Thumbs.db`)
- Secrets / local config (API keys, `.env`)

Git lets you ignore these via a `.gitignore` file.

{: .warning }
> `.gitignore` is not a security feature. Do not rely on it to protect secrets. If something sensitive is committed, treat it as leaked.

---

## Create a `.gitignore`

In your `training-notes` repository, create a `.gitignore` file:

```bash
code .gitignore
```

Add a few common entries:

```gitignore
# macOS
.DS_Store

# Windows
Thumbs.db

# Logs
*.log

# Environment files (often contain secrets)
.env
```

Save the file, then check what Git sees:

```bash
git status
```

Commit it:

```bash
git add .gitignore
git commit -m "Add .gitignore"
```

---

## Test that ignoring works

Create a file that matches an ignore pattern:

```bash
echo "temporary" > debug.log
git status
```

You should *not* see `debug.log` show up as an untracked file.

If you want to confirm whether Git is ignoring something:

```bash
git status --ignored
```

---

## Common gotcha: “I ignored it, but Git still tracks it”

If a file was already committed, adding it to `.gitignore` won’t automatically stop tracking it.

High-level fix:
- Keep the file on disk
- Remove it from Git tracking
- Commit the change

Example (be careful with file paths):

```bash
git rm --cached path/to/file
```

---

## ✅ Lesson Checklist

- [ ] You can explain why `.gitignore` exists
- [ ] You created and committed a `.gitignore`
- [ ] You verified ignored files do not appear in `git status`

---

## 🎯 Next Steps

Continue to Lesson 4 to connect your local repo to GitLab and start using remotes.
