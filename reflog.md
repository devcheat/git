# `git reflog`

## Introduction

`git reflog` records updates to branch tips and HEAD references in your local repository. It acts as a safety net, allowing you to recover commits, branches, and work that may appear lost after operations such as reset, rebase, checkout, switch, merge, or branch deletion.

```bash
git reflog
```

Unlike `git log`, which shows commit history, `git reflog` shows reference history.

```text
HEAD
 |
 | commit
 | reset
 | rebase
 | switch
 v
Reflog History
```

---

# Syntax

```bash
git reflog
git reflog show
git reflog expire
git reflog delete
git reflog exists
```

Examples:

```bash
git reflog
git reflog show main
git reflog delete HEAD@{2}
git reflog expire --expire=30.days refs/heads/main
```

---

# Understanding Reflog Entries

Example:

```text
a1b2c3d HEAD@{0}: commit: Fix login issue
b4c5d6e HEAD@{1}: pull origin main
c7d8e9f HEAD@{2}: checkout: moving from main to feature
```

Each entry contains:

- Commit hash
- Reflog index
- Action performed
- Description

---

# Common Usage Scenarios

## View Reference History

```bash
git reflog
```

Displays recent HEAD movements.

---

## Recover Lost Commit

```bash
git reflog
git checkout HEAD@{3}
```

Useful after accidental resets.

---

## Recover Deleted Branch

```bash
git reflog
```

Locate the last commit and recreate the branch.

---

## Undo Hard Reset

```bash
git reset --hard HEAD@{1}
```

Return repository state to a previous reference.

---

# All Major Commands and Options

## `git reflog`

Show reflog entries.

```bash
git reflog
```

---

## `git reflog show`

Display reflog for a specific reference.

```bash
git reflog show main
```

---

## `git reflog list`

List references that have reflogs.

```bash
git reflog list
```

---

## `git reflog exists`

Check whether a reflog exists.

```bash
git reflog exists refs/heads/main
```

---

## `git reflog delete`

Delete a reflog entry.

```bash
git reflog delete HEAD@{2}
```

---

## `git reflog drop`

Delete an entire reflog.

```bash
git reflog drop refs/heads/temp
```

---

## `git reflog expire`

Expire old entries.

```bash
git reflog expire --expire=30.days --all
```

---

## `git reflog expire --expire`

Remove entries older than a specified age.

```bash
git reflog expire --expire=90.days --all
```

---

## `git reflog expire --expire-unreachable`

Expire unreachable entries.

```bash
git reflog expire --expire-unreachable=30.days --all
```

---

## `git reflog expire --all`

Apply operation to all reflogs.

```bash
git reflog expire --all
```

---

## `git reflog expire --rewrite`

Rewrite reflog indexes.

```bash
git reflog expire --rewrite --all
```

---

## `git reflog expire --updateref`

Update references when expiring entries.

```bash
git reflog expire --updateref --all
```

---

## `git reflog expire --dry-run`

Preview expiration.

```bash
git reflog expire --dry-run --all
```

---

## `git reflog expire --verbose`

Display detailed output.

```bash
git reflog expire --verbose --all
```

---

# Recovering Lost Work

## Recover After Hard Reset

```bash
git reflog
git reset --hard HEAD@{1}
```

---

## Recover After Rebase

```bash
git reflog
git reset --hard HEAD@{5}
```

---

## Recover Deleted Branch

```bash
git branch recovered-branch COMMIT_HASH
```

---

## Recover Detached HEAD Work

```bash
git branch rescue HEAD
```

---

# Real-World Scenarios

## Scenario 1: Accidental Hard Reset

```bash
git reflog
git reset --hard HEAD@{1}
```

---

## Scenario 2: Bad Rebase Recovery

```bash
git reflog
git reset --hard HEAD@{4}
```

---

## Scenario 3: Restore Deleted Branch

```bash
git reflog
git branch restore-feature HASH
```

---

## Scenario 4: Recover Lost Commit

```bash
git cherry-pick HASH
```

---

## Scenario 5: Recover From Detached HEAD

```bash
git branch rescue-work HEAD
```

---

## Scenario 6: Investigate Branch Movement

```bash
git reflog show main
```

---

# Difference Between Common Variants

## `git reflog` vs `git log`

`git reflog`

- Reference history
- Local only
- Recovery focused

`git log`

- Commit history
- Repository history
- Audit focused

---

## `git reflog` vs `git status`

`git reflog`

- Historical actions

`git status`

- Current repository state

---

## `git reflog` vs `git fsck`

`git reflog`

- Find previous references

`git fsck`

- Find dangling objects

---

# Common Errors and Troubleshooting

## Entry No Longer Available

Old reflog entries may have expired.

---

## Repository Garbage Collection

Git cleanup may remove unreachable objects.

---

## Wrong Reference Selected

Verify entry:

```bash
git show HEAD@{3}
```

before recovery.

---

## Branch Recovery Failure

Verify commit still exists using:

```bash
git fsck --lost-found
```

---

# Best Practices

1. Check reflog before assuming work is lost.
2. Use reflog before aggressive recovery tools.
3. Verify entries with `git show`.
4. Create recovery branches instead of resetting immediately.
5. Keep garbage collection settings appropriate.
6. Learn reflog indexes such as `HEAD@{1}`.
7. Use reflog after failed rebases and resets.

---

# Useful Workflow

```bash
# View reference history
git reflog

# Inspect candidate commit
git show HEAD@{3}

# Create recovery branch
git branch recovered-work HEAD@{3}

# Continue work safely
git switch recovered-work
```

---

# Quick Reference

```bash
git reflog                              # View reflog
git reflog show main                    # Reflog for branch
git reflog list                         # List reflogs
git reflog exists refs/heads/main       # Check reflog
git reflog delete HEAD@{2}              # Delete entry
git reflog drop refs/heads/test         # Drop reflog
git reflog expire --all                 # Expire entries
git reset --hard HEAD@{1}               # Recover state
git show HEAD@{3}                       # Inspect entry
git branch recovery HEAD@{3}            # Create recovery branch
```

---

# Conclusion

`git reflog` is one of Git's most valuable recovery tools. By understanding reflog entries, recovery workflows, expiration policies, and reference history, developers can restore lost work, reverse mistakes, recover deleted branches, and confidently experiment knowing that important repository states can often be recovered.
