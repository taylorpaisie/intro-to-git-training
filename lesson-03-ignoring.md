---
layout: post
title: Ignoring Things
description: Keep temporary and build files out of your repository
image: /images/phd101212s.png
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

Some files are not part of the "source of truth" for a project:
- Build outputs (e.g., `dist/`, `build/`)
- Dependency folders (e.g., `node_modules/`)
- OS/editor noise (e.g., `.DS_Store`, `Thumbs.db`)
- Secrets / local config (API keys, `.env`)

Git lets you ignore these via a `.gitignore` file.

{: .warning }
> `.gitignore` is not a security feature. Do not rely on it to protect secrets. If something sensitive is committed, treat it as leaked.

---

## Create a `.gitignore`

In your repository, create a `.gitignore` file:

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

Create a test file that matches your `.gitignore`:

```bash
touch debug.log
git status
```

You should **not** see `debug.log` in the output. Git is ignoring it!

---

## Common Patterns

| Pattern | Matches |
|---------|---------|
| `*.log` | All `.log` files anywhere |
| `build/` | The `build/` directory and all contents |
| `.env` | Only `.env` files in the root |
| `**/*.tmp` | All `.tmp` files at any depth |
| `!important.log` | Negation: stop ignoring `important.log` |

---

## Important: Already-Tracked Files

If a file was already committed before adding it to `.gitignore`, Git **will still track it**!

To fix this:

```bash
git rm --cached filename.log
git commit -m "Stop tracking filename.log"
```

This removes it from Git but keeps it on your disk.
