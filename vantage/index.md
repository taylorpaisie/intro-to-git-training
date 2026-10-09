---
layout: default
title: Git in Army Vantage
nav_order: 3
has_children: true
permalink: /vantage/
---

# Git Version Control in Army Vantage

**A separate training track for analysts using Palantir Foundry Code Repositories.**

Use the core Git lessons for general concepts, then use this track to apply them inside Vantage. The browser workflow does not require installing Git or connecting to GitHub/GitLab.

{: .note }
> This guide uses public Palantir Foundry documentation. Army Vantage menus, available applications, permissions, and release procedures may differ. Follow your team's configured workflow and in-platform documentation; this is not an official Army operating procedure.

## Learning path

| Module | What you will practice | Time |
|--------|-----------------------|------|
| [1 — Concepts & Browser Workflow]({{ '/vantage/workflow/' | relative_url }}) | Connect Git concepts to Code Repositories; branch, commit, build, review, and merge | 20–25 min |
| [2 — Hands-on Lab]({{ '/vantage/lab/' | relative_url }}) | Change a synthetic vehicle fielding rule and document validation | 25–35 min |
| [3 — Team Practices & Quick Reference]({{ '/vantage/reference/' | relative_url }}) | Review changes, handle conflicts, recover safely, and record releases | Reference |

## Before you begin

- Access to a designated training Code Repository and its training datasets.
- Permission to create branches, edit code, and run training builds.
- A partner or instructor who can review your pull request.
- The approved base branch, output locations, and merge procedure from the repository owner.

Use synthetic examples in this public training repository. Keep operational code, Army data, credentials, and internal resource identifiers in their approved environment.

## What Git tracks here

Foundry Code Repositories provides a browser interface over a Git repository. It supports versioning source files and collaborating through pull requests. Python, Java, and SQL transforms are common repository types. See [Palantir: Code Repositories overview](https://www.palantir.com/docs/foundry/code-repositories/overview).

A pipeline has several records of change:

| Record | What it tells you |
|--------|-------------------|
| Git commit | Which source files changed, who committed them, and the explanation |
| Pull request | What was reviewed and approved for merging |
| Dataset transaction | A version of dataset contents maintained by Foundry |
| Build record | Which execution produced outputs and whether it succeeded |

Git is the history of your logic; Foundry also manages the history of your data. A Git tag alone does not freeze a complete analytical result.

[Start Module 1 →]({{ '/vantage/workflow/' | relative_url }})
