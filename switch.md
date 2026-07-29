# `git switch`

## Introduction

`git switch` is the modern Git command used to move between branches. It was introduced to simplify branch-related operations that were historically handled by `git checkout`.

```bash
git switch <branch>
```

Unlike `git checkout`, `git switch` focuses only on branch switching and branch creation.

```text
Current Branch
      |
      | git switch develop
      v
Target Branch
```

---

# Syntax

```bash
git switch <branch>
git switch -c <new-branch>
git switch -C <branch>
git switch --detach <commit>
git switch --orphan <branch>
```

Examples:

```bash
git switch main
git switch develop
git switch -c feature-login
git switch --detach HEAD~2
```

---

# Common Usage Scenarios

## Switch to an Existing Branch

```bash
git switch main
```

Moves your working directory to the `main` branch.

---

## Create and Switch to a New Branch

```bash
git switch -c feature-payment
```

Creates the branch and immediately switches to it.

---

## Return to the Previous Branch

```bash
git switch -
```

Useful when moving between two active branches.

---

## Switch to a Remote Tracking Branch

```bash
git switch feature-api
```

Git can automatically create a local tracking branch if a matching remote branch exists.

---

## Review Older Commits

```bash
git switch --detach HEAD~5
```

Used to inspect historical commits without affecting branches.

---

# Understanding Branch Switching

Example:

```text
main
 |
 +---- feature-login
 |
 +---- develop
```

Switching branches changes:

- Working directory files
- Current branch reference
- Future commit destination

---

# All Major Options

## `git switch <branch>`

Switch to an existing branch.

```bash
git switch develop
```

---

## `git switch -`

Switch back to previously checked-out branch.

```bash
git switch -
```

---

## `git switch @{-1}`

Equivalent to previous branch.

```bash
git switch @{-1}
```

---

## `git switch -c`

Equivalent:

```bash
git switch --create
```

Example:

```bash
git switch -c feature-auth
```

---

## `git switch --create`

Create and switch.

```bash
git switch --create bugfix-login
```

---

## `git switch -C`

Equivalent:

```bash
git switch --force-create
```

Creates or resets existing branch.

```bash
git switch -C testing
```

---

## `git switch --force-create`

Force branch recreation.

```bash
git switch --force-create testing
```

---

## `git switch --detach`

Detach HEAD.

```bash
git switch --detach HEAD~3
```

Allows temporary exploration.

---

## `git switch --orphan`

Create orphan branch.

```bash
git switch --orphan gh-pages
```

Branch starts with no history.

---

## `git switch --track`

Track remote branch.

```bash
git switch --track origin/release
```

---

## `git switch --guess`

Allow Git to infer remote tracking branch.

```bash
git switch --guess feature-api
```

---

## `git switch --no-guess`

Disable automatic guessing.

```bash
git switch --no-guess feature-api
```

---

## `git switch --discard-changes`

Discard working tree changes during switch.

```bash
git switch --discard-changes main
```

Use carefully.

---

## `git switch -f`

Force switch.

```bash
git switch -f main
```

---

## `git switch --merge`

Attempt branch switch while preserving local modifications.

```bash
git switch --merge main
```

---

## `git switch --conflict=merge`

Use merge-style conflict markers.

```bash
git switch --conflict=merge main
```

---

## `git switch --conflict=diff3`

Use diff3 format.

```bash
git switch --conflict=diff3 main
```

---

## `git switch --recurse-submodules`

Update submodules when switching.

```bash
git switch --recurse-submodules develop
```

---

## `git switch --quiet`

Reduce output.

```bash
git switch --quiet main
```

---

# Detached HEAD Scenarios

## Inspect Previous Release

```bash
git switch --detach v1.0
```

---

## Test Historical Commit

```bash
git switch --detach a1b2c3d
```

---

## Temporary Experimentation

```bash
git switch --detach HEAD
```

Create experimental commits without affecting branches.

---

# Real-World Scenarios

## Scenario 1: Start New Feature

```bash
git switch main
git switch -c feature-profile
```

---

## Scenario 2: Hotfix Production Issue

```bash
git switch main
git switch -c hotfix-login
```

---

## Scenario 3: Jump Between Branches

```bash
git switch main
git switch develop
git switch -
```

---

## Scenario 4: Review Previous Release

```bash
git switch --detach v2.0
```

---

## Scenario 5: Create Documentation Site Branch

```bash
git switch --orphan gh-pages
```

---

## Scenario 6: Work with Remote Branch

```bash
git switch --track origin/feature-payment
```

## Scenario 7: Enterprise Monorepo Workflow (PR-Based)
```bash
#1. Feature integration happens through PR, not local merge.
#2. You still rebase feature branch on origin/main to reduce conflicts.

# Update local view of remotes
git fetch --all --prune

# Start from an up-to-date main
git switch main
git pull --ff-only origin main

# Create feature branch
git switch -c feature/payments-api-rate-limit

# Work and commit
git add .
git commit -m "feat(payments): add rate limit config"

# Keep branch current while working
git fetch origin
git rebase origin/main

# Resolve rebase conflicts if needed
git status
git add <resolved-files>
git rebase --continue

# Publish branch for PR
git push -u origin feature/payments-api-rate-limit

# Open Pull Request: feature/payments-api-rate-limit -> main
# Do NOT merge locally when team policy is PR merge only.

# After PR is merged, sync local main
git switch main
git pull --ff-only origin main

# Optional: create release tag from updated main and publish
git tag -a v1.2.0 -m "release: payments api rate limit"
git push origin v1.2.0
```
---

# Difference Between Common Variants

## `git switch` vs `git checkout`

`git switch`

- Branch focused
- Easier to learn
- Safer workflow

`git checkout`

- Multiple responsibilities
- More complex

---

## `git switch -c` vs `git branch + git switch`

```bash
git switch -c feature-api
```

Equivalent to:

```bash
git branch feature-api
git switch feature-api
```

---

## `git switch` vs `git restore`

`git switch`

- Branch operations

`git restore`

- File restoration

---

# Common Errors and Troubleshooting

## Local Changes Would Be Overwritten

```text
Your local changes would be overwritten
```

Solution:

```bash
git stash
git switch main
```

---

## Branch Does Not Exist

```text
fatal: invalid reference
```

Verify branch name.

---

## Detached HEAD Confusion

Return to a branch:

```bash
git switch main
```

---

# Best Practices

1. Prefer `git switch` over `git checkout` for branch operations.
2. Create feature branches using `-c`.
3. Use detached HEAD mode only for temporary work.
4. Commit or stash changes before switching.
5. Use tracking branches for team collaboration.
6. Keep branch names descriptive.
7. Avoid force options unless necessary.

---

# Useful Workflow

```bash
# Update main branch
git switch main
git pull

# Create feature branch
git switch -c feature-reporting

# Work and commit
git commit -m "Add reporting"

# Return to main
git switch main
```

---

# Quick Reference

```bash
git switch main                     # Switch branch
git switch -                        # Previous branch
git switch -c feature               # Create branch
git switch -C feature               # Recreate branch
git switch --detach HEAD~2          # Detached HEAD
git switch --orphan gh-pages        # Orphan branch
git switch --track origin/main      # Track branch
git switch --merge main             # Preserve changes
git switch --discard-changes main   # Discard changes
git switch --quiet main             # Quiet mode
```

---

# Conclusion

`git switch` provides a cleaner and safer way to work with branches. By mastering branch creation, remote tracking, detached HEAD workflows, orphan branches, and branch navigation techniques, developers can work more efficiently and avoid many of the common mistakes associated with older branch-switching workflows.
