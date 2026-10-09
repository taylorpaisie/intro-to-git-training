---
layout: default
title: 3 — Team Practices & Quick Reference
parent: Git in Army Vantage
nav_order: 3
permalink: /vantage/reference/
---

# Team Practices & Quick Reference

## Review an analytical change

Ask the author to connect the change to the decision it supports:

- What business rule changed, and who confirmed it?
- Which rows, totals, schemas, and downstream consumers are affected?
- Which inputs and versions were used for validation?
- Were joins checked for duplicate keys and unexpected row multiplication?
- Were nulls, units, date boundaries, and aggregation behavior considered?
- What evidence distinguishes an intentional change from a regression?

Prefer focused commits: `Fix duplicate training unit rows before aggregation` tells a reviewer more than `updates`.

## Release records

For a reproducible analytical delivery, record:

| Item | Example or purpose |
|------|--------------------|
| Commit or code tag | Identifies the source version |
| PR | Records review and approval |
| Input dataset versions | Identifies data used in the run |
| Build and output transactions | Connects execution to results |
| Parameters and environment | Captures settings and dependencies |
| Validation summary | Explains expected changes in the result |

Tags can name significant code versions through the **Tags** tab. They do not snapshot all input datasets or every downstream application. [Palantir: Navigation](https://www.palantir.com/docs/foundry/code-repositories/navigation).

For changes spanning repositories, agree on branch names and build order with the team. Palantir recommends consistent branch names across repositories belonging to one product, with testing before production release. This is a release strategy to adapt with the owner, not a required Army Vantage configuration. [Palantir: Branching and release process](https://www.palantir.com/docs/foundry/building-pipelines/branching-release-process).

## When something goes wrong

| Symptom | Next step |
|---------|-----------|
| Saved edit missing from history | Check whether you committed it |
| Publishing check failed | Read the failure details before expecting the updated logic to build |
| Build failed | Inspect job logs, inputs, and permissions on the selected branch |
| Build succeeded, totals are wrong | Compare business rules and row-level validation |
| Output appears unchanged | Confirm dataset branch, input versions, and actual build execution |
| PR cannot merge | Check conflicts, approvals, checks, and target branch requirements |
| Feature output used base inputs | Inspect fallback resolution; this can be expected behavior |

## Conflicts and recovery

When two people change the same rule, Git may require a conflict resolution. Coordinate with the other author, bring the target changes into the feature branch using your available merge tools, and resolve the intended logic together. Inspect the entire affected function, commit the resolution, and rerun validation before review.

For a bad shared change, prefer a reviewed corrective commit or revert through the team's available tools. Keep the audit trail. Reverting code does not automatically restore earlier dataset contents; the owner must decide whether to rebuild or use a dataset recovery procedure.

The editor's **Reset** action discards uncommitted edits. Preserve work you need before using it. [Palantir: Navigation](https://www.palantir.com/docs/foundry/code-repositories/navigation).

## Boundaries of this guide

- Code Repositories Git branches version source. Dataset branches version data through Foundry transactions and builds.
- Pipeline Builder proposals and Global Branching have their own workflows; do not assume these instructions apply to every Foundry application.
- Local cloning, credentials, VS Code integration, and external Git synchronization depend on your environment's approved setup. This browser track needs none of them.
- Training branch names do not grant permissions or change data access controls.

## Sources and maintenance

Public documentation checked **October 9, 2026**:

- [Code Repositories overview](https://www.palantir.com/docs/foundry/code-repositories/overview)
- [Navigation](https://www.palantir.com/docs/foundry/code-repositories/navigation)
- [Branch settings](https://www.palantir.com/docs/foundry/code-repositories/branch-settings)
- [Dataset and build branching](https://www.palantir.com/docs/foundry/data-integration/branching/)
- [Branching and release process](https://www.palantir.com/docs/foundry/building-pipelines/branching-release-process)

[Back to the Vantage training track]({{ '/vantage/' | relative_url }})
