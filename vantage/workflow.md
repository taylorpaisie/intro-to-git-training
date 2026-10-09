---
layout: default
title: 1 — Concepts & Browser Workflow
parent: Git in Army Vantage
nav_order: 1
permalink: /vantage/workflow/
---

# Concepts & Browser Workflow

**Goal:** Explain the separate steps between editing a transform and delivering updated data.

## Translate what you already know

| General Git concept | Foundry Code Repositories |
|---------------------|---------------------------|
| Repository | Versioned source files behind the browser editor |
| Feature branch | A named line of development for a change |
| Commit | A recorded source-code change |
| GitLab merge request | Foundry pull request (PR) |
| Merge | Incorporate reviewed source changes into a target branch |
| Tag | A named reference to a significant code version |

GitHub, GitLab, and Foundry are different interfaces and services. A Foundry repository does not automatically synchronize with this public GitHub repo.

## Three steps that answer different questions

| Step | Question it answers | What it does not establish |
|------|---------------------|----------------------------|
| Commit | Which code version am I recording? | That the output data is correct |
| Build | What happens when the pipeline executes? | That reviewers approved the change |
| Merge | Which source changes enter the target branch? | That production datasets have been rebuilt |

For transform repositories, successful publishing checks make job specifications available to the build system. A build executes logic on a selected branch and writes output dataset transactions there. Inputs can fall back to another configured branch when unavailable on the build branch. Inspect input resolution before comparing results; a feature branch need not contain separate copies of every input. [Palantir: Branching](https://www.palantir.com/docs/foundry/data-integration/branching/).

## Browser workflow

1. **Open the training Code Repository.** Confirm its current branch and your team's base branch.
2. **Create a branch.** Use the branch selector or **Branches** tab; name it for one change.
3. **Edit and review.** Inspect the diff; automatic saving is separate from committing.
4. **Commit.** Record a meaningful message and wait for repository checks.
5. **Validate.** Use an available preview for fast feedback, then build the training output on your branch. Inspect logs and results.
6. **Propose changes.** Open a PR; verify source and target branches.
7. **Review.** Address comments and rerun validation after changes.
8. **Merge.** An authorized team member merges when the configured requirements are satisfied.

Menu labels may vary. See [Palantir: Navigation](https://www.palantir.com/docs/foundry/code-repositories/navigation) for the documented interface.

## After the merge

Follow the team's release process to build the approved target branch and validate its outputs. A schedule may trigger that build; confirm the actual result rather than assuming the merge refreshed a dashboard.

Identify downstream dependencies before changing an output schema or a business rule. A reviewer should understand which consumer needs the change and what might be affected.

Your base branch may be `master`, `main`, or a development branch. Do not rename it to match this guide. Protected branches can require successful publishing checks and designated approvals. [Palantir: Branch settings](https://www.palantir.com/docs/foundry/code-repositories/branch-settings).

## Check your understanding

- Can a build succeed while the business rule is wrong? **Yes. Execution success is not business validation.**
- Does a commit refresh every dashboard? **No. Outputs must be built and consumers must read the relevant data.**
- Why check fallback inputs? **To know which data your branch actually used.**

[Next: Hands-on Lab →]({{ '/vantage/lab/' | relative_url }})
