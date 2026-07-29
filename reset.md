# `git reset`

## Introduction

`git reset` is one of Git's most powerful commands for moving HEAD, unstaging changes, and undoing commits.

It allows developers to modify repository history, staging area contents, and working directory state depending on the reset mode used.

```bash
git reset
```

---

# What Is Git Reset?

`git reset` moves the current branch reference and optionally updates the index (staging area) and working tree.

```text
HEAD -> C

A --- B --- C
```

After resetting:

```text
HEAD -> B

A --- B
```

---

# Understanding HEAD, Index, and Working Tree

## HEAD

Current commit reference.

## Index

Staging area.

## Working Tree

Your local files.

---

# Basic Syntax

```bash
git reset [options] <commit>
git reset [file>
git reset --hard HEAD~1
```

---

# Reset Modes

## Soft Reset

```bash
git reset --soft HEAD~1
```

Moves HEAD only.

---

## Mixed Reset (Default)

```bash
git reset --mixed HEAD~1
```

Moves HEAD and resets index.

---

## Hard Reset

```bash
git reset --hard HEAD~1
```

Moves HEAD, index, and working tree.

---

# Major Options

## `git reset --soft`

Preserve index and working files.

```bash
git reset --soft HEAD~3
```

---

## `git reset --mixed`

Default reset mode.

```bash
git reset --mixed HEAD~1
```

---

## `git reset --hard`

Discard local changes.

```bash
git reset --hard HEAD~1
```

---

## `git reset --merge`

Preserve unmerged local work where possible.

```bash
git reset --merge HEAD~1
```

---

## `git reset --keep`

Keep working tree changes.

```bash
git reset --keep HEAD~1
```

---

## `git reset --pathspec-from-file`

Read paths from file.

```bash
git reset --pathspec-from-file=files.txt
```

---

## `git reset --pathspec-file-nul`

Use NUL-separated path list.

```bash
git reset --pathspec-file-nul
```

---

## `git reset -q`

Quiet mode.

```bash
git reset -q HEAD~1
```

---

## `git reset --refresh`

Refresh index after reset.

```bash
git reset --refresh
```

---

# Reset Files

## Unstage Single File

```bash
git reset app.js
```

---

## Unstage Multiple Files

```bash
git reset file1.txt file2.txt
```

---

## Reset Specific Paths

```bash
git reset HEAD src/
```

---

# Resetting to Commits

## Previous Commit

```bash
git reset --soft HEAD~1
```

---

## Specific Commit

```bash
git reset --hard abc1234
```

---

## Reset to Remote State

```bash
git reset --hard origin/main
```

---

# Reset vs Restore

## Reset

- History manipulation
- Index management

## Restore

- File restoration

---

# Reset vs Revert

## Reset

- Rewrites history

## Revert

- Creates new commit

---

# Real-World Scenarios

## Scenario 1: Undo Last Commit Keep Changes

```bash
git reset --soft HEAD~1
```

---

## Scenario 2: Unstage Accidentally Added Files

```bash
git reset
```

---

## Scenario 3: Remove Bad Local Commit

```bash
git reset --hard HEAD~1
```

---

## Scenario 4: Start Again From Remote

```bash
git reset --hard origin/main
```

---

## Scenario 5: Clean Feature Branch Before PR

```bash
git reset --soft HEAD~3
```

---

## Scenario 6: Recover During Merge Problems

```bash
git reset --merge
```

---

## Scenario 7: Remove Staged Secrets

```bash
git reset secrets.txt
```

---

# Recovering After Reset

## Using Reflog

```bash
git reflog
```

```bash
git reset --hard HEAD@{1}
```

---

# Common Mistakes

## Using Hard Reset Without Backup

Can permanently discard local changes.

---

## Resetting Shared History

Avoid rewriting published commits.

---

## Confusing Reset and Revert

Understand history implications before use.

---

# Enterprise Best Practices

1. Prefer revert for shared branches.
2. Use soft reset for commit cleanup.
3. Verify before hard reset.
4. Know how to use reflog.
5. Avoid history rewrites on protected branches.
6. Communicate before force pushes.
7. Use backup branches for risky operations.

---

# Quick Reference

```bash
git reset
git reset file.txt
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
git reset --merge
git reset --keep
git reset --hard origin/main
git reset abc1234
```

---

# Conclusion

`git reset` is a powerful command for undoing commits, unstaging changes, moving branch pointers, and recovering from mistakes. Understanding reset modes and recovery techniques is essential for effective Git usage.
