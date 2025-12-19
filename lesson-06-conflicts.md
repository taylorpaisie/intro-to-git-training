---
layout: post
title: Merge Conflicts
description: Understand, resolve, and avoid merge conflicts
image: /images/phd101212s.png
---

# Lesson 6 — Merge Conflicts

{: .highlight }
> **⏱️ Estimated Time:** 20-25 minutes

**Goal:** Understand what a merge conflict is, how to resolve it safely, and how to avoid common conflict pain.

---

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain why merge conflicts happen
- Recognize conflict markers in files
- Resolve a simple conflict and complete the merge

---

## What is a merge conflict?

A conflict happens when Git can't automatically combine changes. Usually that means:
- Two branches changed the same lines of the same file
- Or one branch deleted a file that the other edited

Conflicts are normal in team work.

---

## Practice: create a conflict on purpose

In `training-notes`, start clean:

```bash
git status
```

### 1) Create branch A

```bash
git switch -c conflict-a
```

Edit `README.md` and add (or change) this line under `## Notes`:

```markdown
- Notes: written by Branch A
```

Commit it:

```bash
git add README.md
git commit -m "Edit notes line (A)"
```

### 2) Create branch B from main

```bash
git switch main

git switch -c conflict-b
```

Edit the same line in `README.md` to something different:

```markdown
- Notes: written by Branch B
```

Commit it:

```bash
git add README.md
git commit -m "Edit notes line (B)"
```

### 3) Merge A into main, then try to merge B

```bash
git switch main
git merge conflict-a
```

This should succeed with no conflict.

Now try to merge branch B:

```bash
git merge conflict-b
```

You should see a conflict!

---

## Resolving a Conflict

Look at the conflicted file:

```bash
git status
```

Open `README.md` and find the conflict markers:

```
<<<<<<< HEAD
- Notes: written by Branch A
=======
- Notes: written by Branch B
>>>>>>> conflict-b
```

| Marker | Means |
|--------|-------|
| `<<<<<<<` | Start of current branch (HEAD) |
| `=======` | Divider |
| `>>>>>>>` | End of incoming branch |

**To resolve:**
1. Choose which line to keep, or combine both
2. Delete the conflict markers
3. Stage and commit

```bash
git add README.md
git commit -m "Resolve conflict: merge conflict-b"
```

---

## Preventing Conflicts

- **Communicate** with teammates about what you're changing
- **Pull frequently** to catch conflicts early
- **Keep branches short-lived** (merge within a day or two)
- **Break work into smaller tasks**

---

## If You Get Stuck

Abort the merge and start over:

```bash
git merge --abort
```

Then discuss with your team!
