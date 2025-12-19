---
layout: post
title: Local Commits
description: Save your work using Git commits and the staging area
image: /images/phd101212s.png
---

# Lesson 2 — Local Commits

{: .highlight }
> **⏱️ Estimated Time:** 20-25 minutes

**Goal:** Learn how to save your work using Git commits. You'll understand the staging area, create commits with good messages, and view your project history.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain what a commit is and why it's important
- Use the staging area to prepare changes
- Review changes with `git diff` before committing
- Write clear, meaningful commit messages
- View and navigate your commit history

---

## 📖 Understanding Commits

A **commit** in Git is like taking a snapshot of your project at a specific point in time. Think of it as a save point in a video game — you can always go back to it.

Each commit records:

| Component | Description |
|-----------|-------------|
| **Changes** | What files were modified, added, or deleted |
| **Author** | Who made the changes |
| **Timestamp** | When the changes were made |
| **Message** | A description of what changed |
| **Hash** | A unique identifier (SHA-1) |

{: .note }
> Commits are **permanent** and **immutable**. Once created, a commit's content never changes.

---

## 🎭 The Three Areas of Git

Before diving into commits, understand Git's three main areas:

```
Working Directory → Staging Area → Repository
```

| Area | What It Is |
|------|-----------|
| **Working Directory** | Your actual project files that you edit |
| **Staging Area** | Changes selected for the next commit |
| **Repository** | The complete history of commits |

{: .important }
> The staging area gives you **control**. You decide exactly which changes go into each commit.

---

## 📝 Making Your First Commit

### Step 1: Make Changes

Create a README file:

```bash
echo "# Training Notes" > README.md
```

### Step 2: Check Status

```bash
git status
```

You should see `README.md` as "untracked".

### Step 3: Stage Changes

```bash
git add README.md
```

### Step 4: Review Staged Changes

```bash
git diff --cached
```

### Step 5: Commit

```bash
git commit -m "Add README"
```

The message should be clear and describe what changed.

### Step 6: View History

```bash
git log
git log --oneline
```

---

## 📝 Writing Good Commit Messages

A good commit message:
- Starts with a capital letter
- Is **imperative** ("Add feature" not "Added feature")
- Is **concise** (aim for <50 characters)
- Explains **what** and **why**, not how

**Examples:**
- ✅ `Add authentication to login form`
- ✅ `Fix typo in welcome message`
- ❌ `updated stuff`
- ❌ `Changed files`
