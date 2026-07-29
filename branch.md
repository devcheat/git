# `git branch`

## Introduction

`git branch` is the primary command used to create, list, rename, delete, and manage branches in Git repositories.

Branches allow developers to work on features, bug fixes, experiments, and releases independently without affecting the main codebase.

```bash
git branch
```

---

# What Is a Branch?

A branch is a movable pointer to a commit.

```text
main
  |
  v
A---B---C
```

Creating a branch:

```bash
git branch feature-login
```

Results in:

```text
main
  |
  v
A---B---C
         ^
         |
 feature-login
```

---

# Basic Syntax

```bash
git branch [options]
```

Examples:

```bash
git branch
git branch feature-login
git branch -d feature-login
git branch -m new-name
```

---

# Listing Branches

## List Local Branches

```bash
git branch
```

Current branch is marked with:

```text
*
```

Example:

```text
* main
  develop
  feature-login
```

---

## List Remote Branches

```bash
git branch -r
```

---

## List All Branches

```bash
git branch -a
```

Includes:

- Local branches
- Remote branches

---

# Creating Branches

## Create a Branch

```bash
git branch feature-login
```

Creates a branch but does not switch to it.

---

## Create Branch From Specific Commit

```bash
git branch hotfix abc1234
```

---

## Create Branch From Tag

```bash
git branch release-v1 v1.0
```

---

# Switching Branches

Create and switch:

```bash
git switch -c feature-login
```

Legacy alternative:

```bash
git checkout -b feature-login
```

---

# Branch Information

## Verbose Branch List

```bash
git branch -v
```

Shows:

- Last commit
- Commit message

---

## Very Verbose Output

```bash
git branch -vv
```

Shows:

- Tracking branches
- Ahead/behind status

---

# Major Options

## `git branch -a`

List all local and remote branches.

```bash
git branch -a
```

---

## `git branch -r`

List remote branches.

```bash
git branch -r
```

---

## `git branch -v`

Verbose output.

```bash
git branch -v
```

---

## `git branch -vv`

Very verbose output.

```bash
git branch -vv
```

---

## `git branch --show-current`

Display current branch.

```bash
git branch --show-current
```

---

## `git branch --merged`

Show branches already merged.

```bash
git branch --merged
```

Useful for cleanup.

---

## `git branch --no-merged`

Show unmerged branches.

```bash
git branch --no-merged
```

---

# Renaming Branches

## Rename Current Branch

```bash
git branch -m new-name
```

---

## Rename Another Branch

```bash
git branch -m old-name new-name
```

---

## Force Rename

```bash
git branch -M old-name new-name
```

---

# Deleting Branches

## Safe Delete

```bash
git branch -d feature-login
```

Deletes only if merged.

---

## Force Delete

```bash
git branch -D feature-login
```

Deletes regardless of merge status.

---

# Branch Tracking

## Set Upstream Branch

```bash
git branch --set-upstream-to=origin/main
```

---

## Remove Upstream

```bash
git branch --unset-upstream
```

---

# Filtering Branches

## Branches Containing Commit

```bash
git branch --contains abc1234
```

---

## Branches Not Containing Commit

```bash
git branch --no-contains abc1234
```

---

## Sort Branches

```bash
git branch --sort=-committerdate
```

---

# Real-World Scenarios

## Scenario 1: Create Feature Branch

```bash
git branch feature-payment
```

---

## Scenario 2: Remove Completed Branches

```bash
git branch --merged
```

Then:

```bash
git branch -d feature-payment
```

---

## Scenario 3: Rename Default Branch

```bash
git branch -m master main
```

---

## Scenario 4: Audit Active Development

```bash
git branch -vv
```

---

## Scenario 5: Find Branches With Specific Fix

```bash
git branch --contains abc1234
```

---

# Common Mistakes

## Assuming Branch Creation Switches Branch

```bash
git branch feature-x
```

Only creates the branch.

---

## Force Deleting Valuable Work

```bash
git branch -D feature-x
```

Use carefully.

---

## Forgetting Remote Cleanup

Deleting a local branch does not delete its remote counterpart.

---

# Comparison With Related Commands

## `git branch` vs `git switch`

`git branch`

- Manage branch references

`git switch`

- Move between branches

---

## `git branch` vs `git checkout`

`git checkout`

- Multiple responsibilities

`git branch`

- Branch management only

---

# Best Practices

1. Use descriptive branch names.
2. Delete merged branches regularly.
3. Use `-vv` to monitor tracking status.
4. Keep feature branches focused.
5. Avoid long-lived branches when possible.
6. Establish naming conventions.
7. Review merged branches periodically.

---

# Quick Reference

```bash
git branch                           # List local branches
git branch -a                        # List all branches
git branch -r                        # Remote branches
git branch feature-login             # Create branch
git branch -m old new                # Rename branch
git branch -d feature-login          # Delete merged branch
git branch -D feature-login          # Force delete branch
git branch -vv                       # Verbose details
git branch --merged                  # Merged branches
git branch --no-merged               # Unmerged branches
git branch --show-current            # Current branch
git branch --contains COMMIT         # Branches containing commit
```

---

# Conclusion

`git branch` is a foundational Git command for managing parallel development workflows. Understanding how to create, inspect, rename, track, and delete branches enables teams to collaborate effectively and maintain clean repository structures.
