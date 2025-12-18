---
layout: default
title: Lesson 6 — Merge Conflicts
parent: Lessons
nav_order: 6
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

A conflict happens when Git can’t automatically combine changes. Usually that means:
- two branches changed the same lines of the same file
- or one branch deleted a file that the other edited

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

### 3) Merge and hit the conflict

Merge A into B (either direction is fine; we’ll choose this):

```bash
git merge conflict-a
```

Git will report a conflict.

---

## Resolve the conflict

Open `README.md`. You’ll see markers like:

```text
<<<<<<< HEAD
...your current branch version...
=======
...the other branch version...
>>>>>>> conflict-a
```

To resolve:
1. Decide what the final content should be
2. Edit the file so it contains only the final content (remove the markers)
3. Stage the resolution:

```bash
git add README.md
```

4. Complete the merge:

```bash
git commit
```

---

## Helpful commands while resolving

```bash
# Which files are conflicted?
git status

# Abort the merge attempt (returns you to pre-merge state)
git merge --abort
```

---

## ✅ Lesson Checklist

- [ ] You created a conflict and saw conflict markers
- [ ] You edited the file to the desired final version
- [ ] You staged the resolution and completed the merge

---

## 🎯 Next Steps

At this point you can do the full basic workflow: commits → ignore → remotes → branches/PRs → conflicts.

If you want, we can add an optional “collaboration workflow” lesson next (forks, reviews, and working with upstream).
