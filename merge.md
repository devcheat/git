# `git merge`

## Introduction

`git merge` is used to combine changes from one branch into another. It is one of Git's core collaboration features and enables teams to integrate feature development, bug fixes, hotfixes, and release work.

```bash
git merge <branch>
```

---

# What Is a Merge?

A merge combines the histories of two branches.

```text
A---B---C  main
     \
      D---E  feature
```

After merge:

```text
A---B---C---------M  main
     \         /
      D---E----/   feature
```

`M` is the merge commit.

---

# Basic Syntax

```bash
git merge [options] <branch>
```

Examples:

```bash
git merge feature-login
git merge release-v1
git merge --no-ff feature-payment
```

---

# Common Merge Types

## Fast-Forward Merge

```bash
git merge feature-login
```

When no divergence exists, Git simply moves the branch pointer forward.

```text
A---B---C main
         \
          D feature
```

Becomes:

```text
A---B---C---D main
```

---

## Three-Way Merge

Occurs when both branches contain unique commits.

Creates a merge commit.

---

# Basic Workflow

```bash
# Switch to target branch
git switch main

# Merge feature branch
git merge feature-login
```

---

# Major Options

## `git merge --no-ff`

Always create a merge commit.

```bash
git merge --no-ff feature-login
```

Useful for preserving branch history.

---

## `git merge --ff`

Allow fast-forward merge.

```bash
git merge --ff feature-login
```

Default behavior.

---

## `git merge --ff-only`

Refuse non-fast-forward merges.

```bash
git merge --ff-only feature-login
```

---

## `git merge --squash`

Combine branch changes into a single commit.

```bash
git merge --squash feature-login
```

No merge commit is created automatically.

---

## `git merge --commit`

Perform merge and create commit.

```bash
git merge --commit feature-login
```

---

## `git merge --no-commit`

Perform merge without creating commit.

```bash
git merge --no-commit feature-login
```

Allows review before final commit.

---

## `git merge -m`

Specify merge commit message.

```bash
git merge -m "Merge authentication feature" feature-auth
```

---

## `git merge --abort`

Cancel an in-progress merge.

```bash
git merge --abort
```

---

## `git merge --continue`

Continue after resolving conflicts.

```bash
git merge --continue
```

---

## `git merge --quit`

Stop merge process without changing files.

```bash
git merge --quit
```

---

## `git merge --strategy`

Specify merge strategy.

```bash
git merge -s ort feature-login
```

Common strategies:

- ort
- recursive
- ours
- subtree
- octopus

---

## `git merge -X ours`

Favor current branch changes.

```bash
git merge -X ours feature-login
```

---

## `git merge -X theirs`

Favor incoming branch changes.

```bash
git merge -X theirs feature-login
```

---

# Merge Conflicts

## Example Conflict

```text
CONFLICT (content): Merge conflict in app.py
```

Git marks conflicts:

```text
<<<<<<< HEAD
Current branch
=======
Incoming branch
>>>>>>> feature
```

---

## Resolve Conflict

1. Edit file.
2. Remove markers.
3. Stage file.

```bash
git add app.py
```

4. Continue merge.

```bash
git merge --continue
```

---

# Merge Strategies

## ORT Strategy

Default modern strategy.

```bash
git merge -s ort feature
```

---

## Ours Strategy

```bash
git merge -s ours feature
```

Keeps current branch content.

---

## Octopus Strategy

Merge multiple branches.

```bash
git merge feature1 feature2 feature3
```

---

## Subtree Strategy

Useful for repository integration.

```bash
git merge -s subtree branch
```

---

# Real-World Scenarios

## Scenario 1: Merge Feature Branch

```bash
git switch main
git merge feature-login
```

---

## Scenario 2: Preserve Feature History

```bash
git merge --no-ff feature-payment
```

---

## Scenario 3: Single Commit Integration

```bash
git merge --squash feature-payment
```

---

## Scenario 4: Resolve Conflict

```bash
git merge feature-login
```

Fix conflicts and continue.

---

## Scenario 5: Abort Failed Merge

```bash
git merge --abort
```

---

## Scenario 6: Enterprise Release Merge

```bash
git merge release/v2.0
```

Integrate release branch changes.

---

# Common Mistakes

## Merging Wrong Branch

Always verify:

```bash
git branch --show-current
```

---

## Forgetting Pull Before Merge

```bash
git pull
```

before merging.

---

## Losing Context With Squash Merges

```bash
git merge --squash
```

Removes detailed branch history.

---

## Force Conflict Resolution Without Review

Always inspect conflicting files before accepting changes.

---

# Comparison with Related Commands

## `git merge` vs `git rebase`

`git merge`

- Preserves history
- Creates merge commits

`git rebase`

- Rewrites history
- Creates linear timeline

---

## `git merge` vs `git cherry-pick`

`git merge`

- Integrates entire branch

`git cherry-pick`

- Integrates selected commits

---

# Best Practices

1. Pull latest changes before merging.
2. Use feature branches.
3. Resolve conflicts carefully.
4. Use `--no-ff` when branch history matters.
5. Use squash merges for small feature branches.
6. Review code before merge.
7. Delete merged branches after integration.
8. Keep branches short-lived.

---

# Useful Workflow

```bash
# Update branch
git pull

# Switch to main
git switch main

# Merge feature branch
git merge feature-login

# Push merged result
git push
```

---

# Quick Reference

```bash
git merge branch-name                 # Merge branch
git merge --no-ff branch-name         # Force merge commit
git merge --ff-only branch-name       # Fast-forward only
git merge --squash branch-name        # Squash merge
git merge --no-commit branch-name     # Merge without commit
git merge --abort                     # Abort merge
git merge --continue                  # Continue merge
git merge -m "message" branch-name   # Custom message
git merge -X ours branch-name         # Prefer current changes
git merge -X theirs branch-name       # Prefer incoming changes
```

---

# Conclusion

`git merge` is one of Git's most important collaboration commands. Understanding merge strategies, conflict resolution, fast-forward behavior, squash merges, and branch integration workflows enables teams to integrate code safely and maintain a healthy repository history.
