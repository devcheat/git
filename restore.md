# `git restore`

## Introduction

`git restore` is a modern Git command introduced to make undoing changes safer and easier to understand. It is primarily used to:

- Restore files in the working directory
- Unstage files from the staging area
- Restore files from a specific commit, branch, or tag

Before Git 2.23, developers commonly used `git checkout` and `git reset` for these operations. Git introduced `restore` to provide a clearer and less error-prone workflow.

```bash
git restore [options] <pathspec>
```

---

# Understanding What `git restore` Affects

Git has three important areas:

```text
Repository (Commit History)
          |
          |
          v
     Staging Area
          |
          |
          v
   Working Directory
```

`git restore` can operate on:

- Working Directory
- Staging Area
- Both simultaneously

---

# Syntax

```bash
git restore [options] <file>
```

General form:

```bash
git restore [--source=<tree>] [--staged] [--worktree] <pathspec>
```

---

# Common Usage Scenarios

## Restore a Modified File

Suppose:

```bash
vim app.py
```

You made changes but want to discard them.

```bash
git restore app.py
```

Result:

```text
Working directory changes removed.
```

---

## Restore Multiple Files

```bash
git restore app.py config.yml README.md
```

---

## Restore All Files

```bash
git restore .
```

Restores all tracked files in the current directory tree.

---

# Unstage Files

A common use case.

Current state:

```bash
git add app.py
git status
```

Output:

```text
Changes to be committed
```

Remove from staging:

```bash
git restore --staged app.py
```

File remains modified but is no longer staged.

---

# Restore Working Tree and Staging Area

## Restore Both

```bash
git restore --staged --worktree app.py
```

Equivalent to returning the file to the version in HEAD.

---

# Restore from Specific Commit

## Using `--source`

Restore a file from another commit.

```bash
git restore --source=HEAD~1 app.py
```

Restore version from previous commit.

---

## Restore from Branch

```bash
git restore --source=main app.py
```

Copy file content from branch `main`.

---

## Restore from Tag

```bash
git restore --source=v1.0 app.py
```

Restore file from release tag.

---

# Major Options

## `git restore --staged`

Restore the index (staging area).

```bash
git restore --staged app.py
```

Equivalent purpose to:

```bash
git reset HEAD app.py
```

but easier to understand.

---

## `git restore --worktree`

Restore working directory only.

```bash
git restore --worktree app.py
```

Normally implied by default.

---

## `git restore --staged --worktree`

Restore both staging area and working directory.

```bash
git restore --staged --worktree app.py
```

---

## `git restore --source`

Choose the source tree.

```bash
git restore --source=HEAD~2 app.py
```

Examples:

```bash
git restore --source=main file.txt
git restore --source=feature1 file.txt
git restore --source=v2.0 file.txt
```

---

## `git restore -p`

Patch mode.

```bash
git restore -p app.py
```

Interactively select chunks to restore.

Options:

```text
y = restore hunk
n = keep hunk
q = quit
s = split hunk
e = edit hunk
```

---

## `git restore --patch`

Long form of:

```bash
git restore -p
```

Useful for partial rollback.

---

## `git restore --quiet`

Suppress output.

```bash
git restore --quiet file.txt
```

Useful in automation scripts.

---

## `git restore --progress`

Force progress reporting.

```bash
git restore --progress .
```

---

## `git restore --ignore-unmerged`

Ignore unmerged paths.

```bash
git restore --ignore-unmerged .
```

Useful during conflict resolution workflows.

---

## `git restore --ours`

Restore your side of a merge conflict.

```bash
git restore --ours app.py
```

---

## `git restore --theirs`

Restore incoming side of merge conflict.

```bash
git restore --theirs app.py
```

---

## `git restore --merge`

Recreate merge conflict.

```bash
git restore --merge app.py
```

Useful when conflict markers were accidentally modified.

---

## `git restore --ignore-skip-worktree-bits`

Restore files regardless of sparse checkout settings.

```bash
git restore --ignore-skip-worktree-bits file.txt
```

Useful in monorepos.

---

# Real-World Scenarios

## Scenario 1: Accidental File Modification

```bash
git restore app.py
```

Return file to last committed state.

---

## Scenario 2: Undo `git add`

```bash
git restore --staged app.py
```

Keep modifications while removing from staging.

---

## Scenario 3: Roll Back Only Part of a File

```bash
git restore -p app.py
```

Choose individual hunks.

---

## Scenario 4: Restore Earlier Version

```bash
git restore --source=HEAD~3 config.yml
```

Recover content from an older commit.

---

## Scenario 5: Merge Conflict Resolution

Keep your version:

```bash
git restore --ours app.py
```

Keep incoming version:

```bash
git restore --theirs app.py
```

---

## Scenario 6: Recover After Experimental Changes

```bash
git restore .
```

Discard all tracked modifications.

---

# Common Mistakes

## Trying to Restore Untracked Files

Untracked files are not affected.

```text
newfile.txt
```

To remove them:

```bash
git clean -fd
```

---

## Restoring Wrong File

Always review status first.

```bash
git status
```

---

## Data Loss

```bash
git restore app.py
```

Discarded changes cannot be recovered unless stored elsewhere.

---

# Comparison with Other Commands

## `git restore` vs `git checkout`

`git restore`

- Focused on restoring files
- Safer and clearer

`git checkout`

- Switch branches
- Restore files
- Multiple responsibilities

---

## `git restore` vs `git reset`

`git restore --staged`

```bash
git restore --staged app.py
```

`git reset`

```bash
git reset HEAD app.py
```

Both unstage files, but `restore` is more explicit.

---

## `git restore` vs `git revert`

`git restore`

- Affects local changes
- Does not create commits

`git revert`

- Creates new commit
- Reverses existing commit history

---

# Best Practices

1. Run `git status` before restoring.
2. Use `-p` for selective rollback.
3. Verify with `git diff` before discarding changes.
4. Avoid restoring files unless certain changes are no longer needed.
5. Prefer `git restore --staged` over older reset patterns when teaching beginners.
6. Understand whether you are affecting the worktree, index, or both.
7. Commit frequently to reduce accidental data loss.

---

# Useful Workflow

```bash
# Check current status
git status

# Review changes
git diff

# Unstage file
git restore --staged app.py

# Discard working changes
git restore app.py

# Verify result
git status
```

---

# Quick Reference

```bash
git restore file.txt                          # Discard local changes
git restore .                                 # Restore all files
git restore --staged file.txt                 # Unstage file
git restore --staged --worktree file.txt      # Restore both areas
git restore --source=HEAD~1 file.txt          # Restore from commit
git restore --source=main file.txt            # Restore from branch
git restore -p file.txt                       # Interactive restore
git restore --ours file.txt                   # Keep local version
git restore --theirs file.txt                 # Keep incoming version
git restore --merge file.txt                  # Recreate conflict
```

---

# Conclusion

`git restore` is the modern Git command for undoing file-level changes safely and clearly. Whether you need to discard local modifications, unstage files, recover content from another commit, or resolve merge conflicts, `git restore` provides a focused and predictable workflow that is easier to understand than older combinations of `git checkout` and `git reset`.
