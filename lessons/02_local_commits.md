---
layout: default
title: Lesson 2 — Local Commits
parent: Lessons
nav_order: 2
---

# Lesson 2 — Local Commits

## Understanding Commits

A commit in Git is like taking a snapshot of your project at a specific point in time. Each commit records the changes you've made to your files, along with:
- Who made the changes (author)
- When the changes were made (timestamp)
- A message describing what changes were made (commit message)
- A unique identifier (commit hash)

## The Staging Area

Before you can commit changes in Git, you need to stage them first. The staging area (also called the "index") is like a preparation area for your commit. This two-step process gives you control over exactly which changes go into each commit.

1. First, let's make a change to your project:
   - Open `attendees.md`
   - Add your name to the list of attendees

2. Check the status of your changes:
```bash
git status
```
This command shows you which files are:
- Modified but not staged
- Staged and ready to commit
- Untracked (new files)

## Staging Your Changes

3. Stage your changes using:
```bash
git add attendees.md
```

You can also:
- Stage all changes with `git add .`
- Stage parts of a file with `git add -p`
- Remove files from staging with `git restore --staged <file>`

## Creating a Commit

4. Commit your staged changes:
```bash
git commit -m "Add <your-name> to attendees"
```

### Writing Good Commit Messages
- Keep messages clear and concise
- Use the imperative mood ("Add feature" not "Added feature")
- Start with a capital letter
- Keep the first line under 50 characters
- Add more details in the body if needed (separated by a blank line)

Example of a detailed commit:
```bash
git commit -m "Add Taylor to attendees list

- Added name and GitHub username
- Updated alphabetical order
- Fixed formatting"
```

## Viewing History

5. View your commit history:
```bash
git log --oneline                 # Compact view
git log                           # Detailed view
git log --patch                   # Show changes in each commit
git log --graph --oneline --all   # Show branch history
```

6. View specific commit details:
```bash
git show <commit-hash>            # Show changes in a specific commit
```

## Practice Exercise

1. Create a new file called `bio.md`
2. Add a brief bio about yourself
3. Stage the file
4. Check the status
5. Commit with a meaningful message
6. View the commit in the history

## Tips and Best Practices

- Make atomic commits (one logical change per commit)
- Commit frequently
- Always review your changes before committing
- Use meaningful commit messages
- Don't commit temporary files or build artifacts


