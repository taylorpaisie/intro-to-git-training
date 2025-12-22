---
layout: default
title: Lesson 2 — Local Commits
parent: Lessons
nav_order: 2
---

# 📸 Lesson 2 — Local Commits

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

| Component | Description | Example |
|-----------|-------------|---------|
| **Changes** | What files were modified, added, or deleted | `README.md` modified |
| **Author** | Who made the changes | `Taylor Paisie <taylor@example.com>` |
| **Timestamp** | When the changes were made | `Dec 17, 2024 10:30 AM` |
| **Message** | A description of what changed | `Add Taylor to attendees list` |
| **Hash** | A unique identifier (SHA-1) | `a1b2c3d` |

{: .note }
> Commits are **permanent** and **immutable**. Once created, a commit's content never changes. This is what makes Git so reliable for tracking history.

---

## 🎭 The Three Areas of Git

Before diving into commits, it's essential to understand Git's three main areas:

```
┌─────────────────┐    git add     ┌─────────────────┐   git commit   ┌─────────────────┐
│                 │  ──────────▶   │                 │  ──────────▶   │                 │
│  Working        │                │    Staging      │                │   Repository    │
│  Directory      │                │    Area         │                │   (History)     │
│                 │  ◀──────────   │                 │                │                 │
│  (your files)   │  git restore   │  (index)        │                │  (.git folder)  │
└─────────────────┘                └─────────────────┘                └─────────────────┘
```

| Area | What It Is | Analogy |
|------|------------|---------|
| **Working Directory** | Your actual project files that you edit | Your desk where you work |
| **Staging Area** | Changes selected for the next commit | A box of items ready to ship |
| **Repository** | The complete history of commits | The warehouse of shipped packages |

{: .important }
> The staging area gives you **control**. You decide exactly which changes go into each commit, allowing you to create focused, logical commits even when you've changed many files.

---

## 📝 Step-by-Step: Making Your First Commit

{: .important }
This lesson assumes you created the `training-notes` repository in Lesson 1. If not, go back and complete Lesson 1 first.

### Step 1: Make Changes to Your Project

First, let's modify a file:

1. Open `README.md` in VS Code
2. Add a short section like this:

```markdown
## Notes

- Today I learned what a commit is.
```

3. Save the file

### Step 2: Check Your Status

See what Git knows about your changes:

```bash
git status
```

{: .highlight }
> **Expected output:**
> ```
> On branch main
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>         modified:   README.md
> ```

The output tells you:
- 🔴 **Red text** = Changes not yet staged
- 🟢 **Green text** = Changes staged and ready to commit

### Step 3: Stage Your Changes

Add your changes to the staging area:

```bash
git add README.md
```

Now check the status again:

```bash
git status
```

{: .highlight }
> **Expected output:**
> ```
> On branch main
> Changes to be committed:
>   (use "git restore --staged <file>..." to unstage)
>         modified:   README.md
> ```

The file is now **green** — it's staged and ready to commit!

### Step 4: Create the Commit

Save your staged changes to the repository:

```bash
git commit -m "Update README with notes"
```

{: .highlight }
> **Expected output:**
> ```
> [main a1b2c3d] Add your-name to attendees list
>  1 file changed, 1 insertion(+)
> ```

🎉 **Congratulations!** You've made your first commit!

{: .warning }
> **Oops! I forgot to `git add`!** If you commit and realize you forgot to stage files, no problem:
> ```bash
> # Check what was committed
> git log --oneline -1
> 
> # Only some files were committed? Stage the missing ones and do:
> git add <forgotten-file>
> git commit --amend --no-edit
> ```

---

## 🔧 Staging Commands Reference

| Command | What It Does |
|---------|--------------|
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changes in current directory |
| `git add -A` | Stage all changes in entire repository |
| `git add -p` | Interactively stage parts of files |
| `git restore --staged <file>` | Unstage a file (keep changes) |
| `git restore <file>` | Discard changes to a file ⚠️ |

{: .warning }
> `git restore <file>` will **permanently discard** your uncommitted changes. Use with caution!

---

## 🔍 Review changes before you commit (`git diff`)

`git status` tells you *what* changed. `git diff` shows you *exactly what lines* changed.

```bash
# Changes not staged yet (in working directory)
git diff

# Changes staged for the next commit
git diff --staged
```

### Understanding `git diff` Output

When you run `git diff`, you'll see output like this:

```diff
diff --git a/README.md b/README.md
index abc1234..def5678 100644
--- a/README.md
+++ b/README.md
@@ -5,3 +5,8 @@ My Project
 Some description here.
 
-Old line that was deleted
+New line that was added
+Another new line
```

| Line Prefix | Meaning |
|-------------|---------|
| `-` (red) | Line was removed |
| `+` (green) | Line was added |
| (no prefix) | Line unchanged (context) |
| `@@` | Section header showing line numbers |

**Tip:** Always review `git diff` before staging. It catches mistakes early.

---

## ✍️ Writing Good Commit Messages

Commit messages are **documentation for your future self** (and your team). A good message explains *what* changed and *why*.

### The Anatomy of a Commit Message

```
<type>: <subject line - what changed>
                                        ← blank line
<body - why it changed, additional context>
                                        ← blank line
<footer - references to issues, breaking changes>
```

### Quick Commits (Subject Only)

For simple changes, a single line is fine:

```bash
git commit -m "Add Taylor to attendees list"
```

### Detailed Commits (Subject + Body)

For complex changes, add more context:

```bash
git commit -m "Fix attendee sorting bug

The attendees list was not sorted alphabetically
after the last merge. This commit:
- Reorders attendees A-Z by last name
- Adds a comment explaining the sort order
- Fixes #42"
```

### Commit Message Best Practices

| ✅ Do | ❌ Don't |
|-------|---------|
| Use imperative mood: "Add feature" | Use past tense: "Added feature" |
| Keep subject under 50 characters | Write long, rambling subjects |
| Capitalize the first word | Start with lowercase |
| Explain *why*, not just *what* | Only describe the obvious |
| Reference related issues | Leave context out |

### Good vs. Bad Examples

| ❌ Bad | ✅ Good |
|--------|--------|
| `fix` | `Fix login button not responding on mobile` |
| `updates` | `Update dependencies to patch security vulnerability` |
| `WIP` | `Add user authentication - password validation` |
| `asdfasdf` | `Refactor database queries for better performance` |

{: .note }
> **Pro tip:** If you can't describe your commit in 50 characters, you might be committing too many changes at once. Consider splitting it into smaller commits.

---

## 🔍 Viewing Your Commit History

Git keeps a complete history of every commit. Here's how to explore it:

### Basic History Commands

```bash
# Compact one-line view (most useful for quick overview)
git log --oneline
```

{: .highlight }
> **Example output:**
> ```
> a1b2c3d (HEAD -> main) Update README with notes
> e4f5g6h Initial commit with project structure
> i7j8k9l Add README with project description
> ```

{: .note }
> Use `git log --oneline` by default — it's fast and readable. Use full `git log` when you need more detail about specific commits.

### Common Shortcuts for Commit Messages & Staging

| Shortcut | What It Does | When to Use |
|----------|--------------|------------|
| `git commit -a -m "msg"` | Stage **tracked** files + commit in one step | Simple, single-file changes |
| `git commit -am "msg"` | Same as above (shorthand) | Small, obvious changes only |
| `git log --oneline -n 5` | Show last 5 commits | Quick history check |
| `git show HEAD` | Show details of last commit | Verify what you just committed |

{: .warning }
> `git commit -a` only stages files Git already knows about. **New files won't be included**. Always use `git status` first to check.

### Detailed History

```bash
# Full details for each commit
git log

# Show what changed in each commit
git log --patch

# Limit to last 5 commits
git log -5
```

### Visual History (Great for Branches)

```bash
# ASCII graph of branch history
git log --oneline --graph --all
```

{: .highlight }
> **Example output:**
> ```
> * a1b2c3d (HEAD -> main) Add Taylor to attendees list
> * e4f5g6h Merge feature branch
> |\
> | * x1y2z3a Add new feature
> |/
> * i7j8k9l Initial commit
> ```

### Viewing a Specific Commit

```bash
# Show details and changes for one commit
git show a1b2c3d

# Show just the files that changed
git show --stat a1b2c3d
```

### Searching History

```bash
# Find commits by message
git log --grep="attendees"

# Find commits by author
git log --author="Taylor"

# Find commits that changed a specific file
git log -- README.md
```

---

## 🔄 Undoing Mistakes

Made an error? Git has you covered:

### Before Committing

| Situation | Command |
|-----------|---------|
| Unstage a file | `git restore --staged <file>` |
| Discard changes to a file | `git restore <file>` |
| Discard all changes | `git restore .` |

### After Committing

| Situation | Command |
|-----------|---------|
| Change the last commit message | `git commit --amend -m "New message"` |
| Add forgotten files to last commit | `git add <file>` then `git commit --amend --no-edit` |
| Undo last commit (keep changes) | `git reset --soft HEAD~1` |
| Undo last commit (discard changes) | `git reset --hard HEAD~1` ⚠️ |

{: .warning }
> If you already pushed a commit to a shared branch, prefer `git revert <hash>` instead of rewriting history.

{: .warning }
> `git reset --hard` **permanently deletes** uncommitted changes. Only use when you're sure you want to discard everything.

---

## 🏋️ Practice Exercise

Let's reinforce what you've learned with a hands-on exercise.

### Exercise: Create Your Bio File

**Objective:** Create a new file, stage it, commit it, and view the history.

<details>
<summary><strong>📋 Step-by-step instructions</strong></summary>

1. **Create a new file** called `bio.md`:
   ```bash
   code bio.md
   ```

2. **Add content** to the file:
   ```markdown
   # About Me
   
   **Name:** Your Name
   **Role:** Your Role
   **Fun Fact:** Something interesting about you!
   ```

3. **Save the file** (`Ctrl+S`)

4. **Check the status**:
   ```bash
   git status
   ```
   You should see `bio.md` as an untracked file (red).

5. **Stage the file**:
   ```bash
   git add bio.md
   ```

6. **Verify it's staged**:
   ```bash
   git status
   ```
   You should see `bio.md` as a new file (green).

7. **Commit with a message**:
   ```bash
   git commit -m "Add personal bio for Your Name"
   ```

8. **View your history**:
   ```bash
   git log --oneline -3
   ```

</details>

<details>
<summary><strong>✅ Check your work</strong></summary>

After completing the exercise, verify:

- [ ] `git status` shows "nothing to commit, working tree clean"
- [ ] `git log --oneline` shows your new commit at the top
- [ ] `bio.md` exists in your project folder

</details>

---

## 💡 Tips and Best Practices

### The Golden Rules of Commits

| Rule | Why It Matters |
|------|----------------|
| **Make atomic commits** | One logical change per commit makes history easy to understand and revert |
| **Commit frequently** | Small commits are easier to review and debug |
| **Review before committing** | Use `git diff` to check what you're about to commit |
| **Write meaningful messages** | Future you will thank present you |
| **Don't commit generated files** | Use `.gitignore` for build outputs, dependencies, etc. |

### Quick Workflow Summary

```bash
# 1. Make changes to files
# 2. Review what changed
git status
git diff

# 3. Stage changes
git add <files>

# 4. Commit with a message
git commit -m "Describe what you did"

# 5. Verify
git log --oneline -1
```

### VS Code Shortcuts

You can also use VS Code's built-in Git features:

| Action | How |
|--------|-----|
| View changes | Click the Source Control icon (or `Ctrl+Shift+G`) |
| Stage files | Click the `+` next to changed files |
| Commit | Type message in box, click ✓ checkmark |
| View history | Install GitLens extension for inline history |

---

## 📋 Quick Reference

| Command | Description |
|---------|-------------|
| `git status` | Show current state of working directory |
| `git add <file>` | Stage a file for commit |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Create a commit with message |
| `git commit --amend` | Modify the last commit |
| `git log --oneline` | View compact commit history |
| `git show <hash>` | View details of a specific commit |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |

---

## ✅ Lesson Checklist

Before moving on, make sure you can:

- [ ] Explain the difference between working directory, staging area, and repository
- [ ] Stage and unstage files
- [ ] Create commits with meaningful messages
- [ ] View commit history in different formats
- [ ] Amend the last commit if needed

---

## 🎯 Next Steps

Great work! You now understand the fundamentals of Git commits.

{: .highlight }
> **Coming up:** In the next lesson, you'll learn how to work with remote repositories and collaborate with others using GitLab!

---

## 📚 Additional Resources

| Resource | Link |
|----------|------|
| Git Commit Documentation | [git-scm.com/docs/git-commit](https://git-scm.com/docs/git-commit) |
| Conventional Commits | [conventionalcommits.org](https://www.conventionalcommits.org/) |
| How to Write a Good Commit Message | [cbea.ms/git-commit](https://cbea.ms/git-commit/) |