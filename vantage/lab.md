---
layout: default
title: 2 — Hands-on Lab
parent: Git in Army Vantage
nav_order: 2
permalink: /vantage/lab/
---

# Hands-on Lab: Version a Vehicle Fielding Rule

**Time:** 25–35 minutes  
**Goal:** Deliver one explainable, reviewed change using synthetic data.

## Scenario

A training pipeline calculates vehicles still needed by fictional units. Its original rule subtracts assigned vehicles from authorized vehicles. When assignments exceed authorizations, it produces a negative requirement.

The requested change is to floor the requirement at zero while preserving every unit.

## Instructor preparation

In an approved training project:

1. Prepare a Python transforms Code Repository and a synthetic input dataset with the rows below.
2. Configure a training output and a transform that computes `vehicles_needed`.
3. Build the initial version on the team's training base branch.
4. Confirm learners can branch and build without writing to operational outputs.

The snippets below belong inside the existing transform where `df` is the input PySpark DataFrame. They are not complete Foundry transforms. Keep the repository's generated decorators, input/output bindings, and write logic.

| unit_id | authorized | assigned | Original vehicles_needed |
|---------|-----------:|---------:|-------------------------:|
| TRAIN-001 | 10 | 7 | 3 |
| TRAIN-002 | 8 | 8 | 0 |
| TRAIN-003 | 5 | 7 | -2 |

## 1. Create a feature branch

Create `training/<your-name>-nonnegative-requirements` from the instructor's base branch. Confirm the selector shows your branch before editing.

In the training README, state the requested behavior and expected rows. Make this your first commit:

```text
Document expected nonnegative vehicle requirements
```

## 2. Change one rule

Original logic:

```python
from pyspark.sql import functions as F

df = df.withColumn(
    "vehicles_needed",
    F.col("authorized") - F.col("assigned"),
)
```

Updated logic:

```python
from pyspark.sql import functions as F

df = df.withColumn(
    "vehicles_needed",
    F.greatest(
        F.col("authorized") - F.col("assigned"),
        F.lit(0),
    ),
)
```

For this exercise, both numeric input columns are non-null integers. Define a separate missing-data rule before adapting this logic to nullable inputs; this expression alone is not a missing-data policy.

Review the diff and commit:

```text
Floor training vehicle requirements at zero
```

## 3. Validate on your branch

Wait for checks, build the training output on your feature branch, and inspect that branch's dataset results.

| Check | Expected result |
|-------|-----------------|
| Output rows | 3 |
| Unique unit IDs | 3 |
| TRAIN-001 requirement | 3 |
| TRAIN-002 requirement | 0 |
| TRAIN-003 requirement | 0 |
| Negative requirements | 0 |
| Total vehicles needed | 3 |
| Original input columns | Preserved |

Record the actual values, branch name, commit, build identifier, and input dataset transaction/version available in your environment. Also confirm the base-branch output still contains the original `-2` value before merging.

A successful build with the wrong total is a failed exercise. The green check is helpful; it does not do arithmetic supervision.

## 4. Open a pull request

Use **Propose changes** and verify the target is the instructor's training base branch.

Suggested title:

```text
Prevent negative requirements in the training fielding output
```

Suggested description:

```text
Problem: Over-assigned units produced negative vehicles_needed values.
Change: Floor the difference at zero while retaining all units.
Validation: Three synthetic rows; requirements 3, 0, 0; total 3.
Impact: TRAIN-003 changes from -2 to 0; schema is unchanged.
Evidence: [Record training branch, commit, build, and input version here.]
```

Have a partner compare the diff with the validation table. If they request changes, commit the correction on the same branch and validate again.

## 5. Merge and verify

With instructor authorization, merge into the training base branch. Follow the training release procedure to build that branch and confirm the expected output values there.

Keep the PR and validation evidence as the explanation for the changed result.

## Completion checklist

- [ ] I created a branch from the approved training base.
- [ ] I made two focused commits and inspected their differences.
- [ ] I built and validated the feature-branch output.
- [ ] My partner reviewed the PR.
- [ ] I verified the target-branch result after its build.
- [ ] I can explain why committing, building, and merging are separate.

**Discussion:** If the source assignments change tomorrow, will the same code commit necessarily give the same total? What additional records would you need?

[Next: Team Practices & Quick Reference →]({{ '/vantage/reference/' | relative_url }})
