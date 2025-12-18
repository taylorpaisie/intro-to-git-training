---
layout: default
title: Lesson 1 — Getting Set Up
nav_order: 1
parent: Lessons
---

# Lesson 1 — Getting Set Up

{: .highlight }
> **⏱️ Estimated Time:** 20 minutes

**Goal:** Confirm Git is installed, set your identity, learn how to get help, and create your first local repository.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain (at a high level) what Git is and why teams use it
- Configure your Git name/email
- Use built-in Git help to look up commands
- Create a repository and make an initial commit

---

## What is Git (and what is GitLab)?

- **Git** is a version control tool that records changes over time.
- **GitLab** is a hosting service for Git repositories (plus collaboration features like merge requests).

You can use Git entirely on your laptop. GitLab becomes relevant when you want to share, back up, or collaborate.

---

## 1. Verify your tools

If you haven’t installed Git yet on a Windows work computer, start with the [Windows Setup Guide](00_windows_setup.md).

Verify Git is available:

```bash
# Check Git version
git --version
```

If you’re using VS Code, you can also check:

```bash
code --version
```

---

## 2. First-time Git configuration

Configure your identity (required for commits):

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email (use the email you use in GitLab)
git config --global user.email "your.email@example.com"

# Set your default branch name
git config --global init.defaultBranch main

# Set your default editor (if using VS Code)
git config --global core.editor "code --wait"
```

Check what you set:

```bash
git config --global --list
```

### Optional (nice defaults)

```bash
# Enable colorful Git output
git config --global color.ui auto
```

---

## 3. Getting help (you’ll use this constantly)

Git ships with built-in documentation:

```bash
# General help
git help

# Help for a specific command
git help status

# Short help (flags/summary)
git status -h
```

---

## 4. Create your first repository

In a folder where you keep projects, create a new directory and initialize Git:

```bash
mkdir training-notes
cd training-notes
git init
```

Check the state:

```bash
git status
```

Create a file and make your first commit:

```bash
echo "# Training Notes" > README.md
git add README.md
git commit -m "Add README"
```

---

## ✅ Lesson Checklist

- [ ] `git --version` works
- [ ] `git config --global user.name` and `user.email` are set
- [ ] You can use `git help <command>` to look things up
- [ ] You created a repository and made a commit

---

## 🎯 Next Steps

Continue to [Lesson 2 — Local Commits](02_local_commits.md) to practice staging, reviewing changes, and reading history.

---
