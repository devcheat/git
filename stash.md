# `git stash`

## Introduction

`git stash` temporarily saves uncommitted changes without creating a commit. It allows developers to switch branches, pull updates, investigate issues, or work on urgent tasks while preserving current work.

```bash
git stash
```

Think of stash as a temporary storage area for unfinished work.

```text
Working Directory
       |
       | git stash
       v
Stash Stack
       |
       | git stash apply
       v
Working Directory
```

---

# Syntax

```bash
git stash
git stash push
git stash pop
git stash apply
git stash list
```

Examples:

```bash
git stash
git stash push -m "login feature"
git stash list
git stash pop
```

---

# Understanding the Stash Stack

Git stores stashes in a stack structure.

```text
stash@{0} Latest
stash@{1}
stash@{2}
```

The most recent stash is always `stash@{0}`.

---

# Common Usage Scenarios

## Save Current Work

```bash
git stash
```

Temporarily removes changes from the working directory.

---

## Switch Branches Safely

```bash
git stash
git switch main
```

---

## Pull Changes Without Committing

```bash
git stash
git pull
git stash pop
```

---

## Save Work with a Description

```bash
git stash push -m "payment module"
```

---

# All Major Commands and Options

## `git stash`

Create a stash.

```bash
git stash
```

---

## `git stash push`

Modern stash command.

```bash
git stash push
```

---

## `git stash save`

Legacy syntax.

```bash
git stash save "message"
```

---

## `git stash push -m`

Add stash description.

```bash
git stash push -m "bugfix work"
```

---

## `git stash list`

View stash entries.

```bash
git stash list
```

---

## `git stash show`

View stash summary.

```bash
git stash show stash@{0}
```

---

## `git stash show -p`

View full patch.

```bash
git stash show -p stash@{0}
```

---

## `git stash apply`

Apply stash without removing it.

```bash
git stash apply stash@{0}
```

---

## `git stash pop`

Apply and remove stash.

```bash
git stash pop
```

---

## `git stash drop`

Delete specific stash.

```bash
git stash drop stash@{1}
```

---

## `git stash clear`

Delete all stashes.

```bash
git stash clear
```

---

## `git stash branch`

Create branch from stash.

```bash
git stash branch feature-recovery stash@{0}
```

---

## `git stash push -u`

Include untracked files.

```bash
git stash push -u
```

---

## `git stash push --include-untracked`

Include untracked files.

```bash
git stash push --include-untracked
```

---

## `git stash push -a`

Include ignored files.

```bash
git stash push -a
```

---

## `git stash push --all`

Include ignored and untracked files.

```bash
git stash push --all
```

---

## `git stash push --keep-index`

Keep staged changes.

```bash
git stash push --keep-index
```

---

## `git stash push --staged`

Stash staged changes only.

```bash
git stash push --staged
```

---

## `git stash push --patch`

Interactively select changes.

```bash
git stash push --patch
```

---

# Applying and Recovering Stashes

## Apply Specific Stash

```bash
git stash apply stash@{2}
```

---

## Restore Latest Stash

```bash
git stash pop
```

---

## Create Branch From Stash

```bash
git stash branch recovery stash@{0}
```

---

# Real-World Scenarios

## Scenario 1: Urgent Production Issue

```bash
git stash
git switch main
```

Save feature work and fix production issues.

---

## Scenario 2: Pull Latest Changes

```bash
git stash
git pull
git stash pop
```

---

## Scenario 3: Save Incomplete Feature

```bash
git stash push -m "half-complete login"
```

---

## Scenario 4: Test Alternative Solution

```bash
git stash
git switch -c experiment
```

---

## Scenario 5: Recover Work Weeks Later

```bash
git stash list
git stash apply stash@{3}
```

---

## Scenario 6: Stash Untracked Files

```bash
git stash push -u
```

---

# Difference Between Common Variants

## `git stash apply` vs `git stash pop`

`apply`

- Restores stash
- Keeps stash entry

`pop`

- Restores stash
- Removes stash entry

---

## `git stash` vs `git commit`

`git stash`

- Temporary storage
- Local only

`git commit`

- Permanent history
- Shareable via push

---

## `-u` vs `-a`

`-u`

- Includes untracked files

`-a`

- Includes untracked and ignored files

---

# Common Errors and Troubleshooting

## Merge Conflicts While Applying Stash

```text
CONFLICT (content)
```

Resolve conflicts and commit changes.

---

## Stash Not Found

```text
fatal: log for refs/stash is empty
```

Verify available stashes.

```bash
git stash list
```

---

## Lost Stash

Check reflog.

```bash
git reflog
```

---

## Wrong Stash Applied

Reset changes then apply correct stash.

---

# Best Practices

1. Use descriptive stash messages.
2. Prefer commits for long-term storage.
3. Review stashes regularly.
4. Remove obsolete stashes.
5. Use `apply` when you may need the stash again.
6. Use `branch` for large stash recoveries.
7. Include untracked files only when necessary.

---

# Useful Workflow

```bash
# Save work
git stash push -m "feature-api"

# Update repository
git pull

# Restore work
git stash pop

# Continue development
```

---

# Quick Reference

```bash
git stash                           # Create stash
git stash push -m "msg"            # Named stash
git stash list                      # View stashes
git stash show -p                   # View contents
git stash apply                     # Apply stash
git stash pop                       # Apply and remove
git stash drop stash@{0}            # Delete stash
git stash clear                     # Delete all stashes
git stash branch feature stash@{0}  # Create branch
git stash push -u                   # Include untracked files
```

---

# Conclusion

`git stash` is an essential productivity tool for temporarily saving unfinished work. By understanding stash creation, restoration, branch recovery, selective stashing, and stash management techniques, developers can safely switch contexts and maintain a smooth development workflow without losing changes.
