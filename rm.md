# `git rm`

## Introduction

`git rm` is the Git command used to remove files and directories from both the working tree and the Git index (staging area). It is the recommended way to delete tracked files because Git records the deletion and stages it automatically.

```bash
git rm <file>
```

```text
Tracked File
      |
      | git rm
      v
File Deleted + Deletion Staged
```

---

# Syntax

```bash
git rm <file>
git rm [options] <file>
git rm -r <directory>
```

Examples:

```bash
git rm app.js
git rm README.md
git rm -r docs/
git rm --cached config.json
```

---

# Understanding Git RM

Traditional approach:

```bash
rm app.js
git add -A
```

Git approach:

```bash
git rm app.js
```

Git removes the file and stages the deletion.

---

# Common Usage Scenarios

## Delete a Tracked File

```bash
git rm app.js
```

---

## Delete Multiple Files

```bash
git rm file1.txt file2.txt
```

---

## Remove a Directory

```bash
git rm -r docs/
```

---

## Stop Tracking a File

```bash
git rm --cached config.json
```

File remains locally but is removed from Git tracking.

---

# All Major Options

## `git rm`

Remove tracked file.

```bash
git rm app.js
```

---

## `git rm -r`

Remove directories recursively.

```bash
git rm -r assets/
```

---

## `git rm --recursive`

Recursive removal.

```bash
git rm --recursive docs/
```

---

## `git rm -f`

Equivalent:

```bash
git rm --force
```

Force removal.

```bash
git rm -f app.js
```

---

## `git rm --force`

Remove file regardless of staged changes.

```bash
git rm --force file.txt
```

---

## `git rm --cached`

Remove from Git index only.

```bash
git rm --cached secrets.txt
```

---

## `git rm -n`

Equivalent:

```bash
git rm --dry-run
```

Preview operation.

```bash
git rm -n file.txt
```

---

## `git rm --dry-run`

Show what would be removed.

```bash
git rm --dry-run *.log
```

---

## `git rm -q`

Equivalent:

```bash
git rm --quiet
```

Suppress output.

```bash
git rm -q temp.txt
```

---

## `git rm --quiet`

Quiet execution mode.

```bash
git rm --quiet old.txt
```

---

## `git rm --ignore-unmatch`

Prevent errors if file is missing.

```bash
git rm --ignore-unmatch missing.txt
```

---

# Removing Files from Tracking Only

Common workflow:

```bash
git rm --cached .env
```

Then:

```bash
echo ".env" >> .gitignore
```

This keeps the file locally while preventing future tracking.

---

# Real-World Scenarios

## Scenario 1: Remove Obsolete Source File

```bash
git rm old-service.js
```

---

## Scenario 2: Delete Deprecated Directory

```bash
git rm -r legacy/
```

---

## Scenario 3: Remove Secrets from Tracking

```bash
git rm --cached .env
```

---

## Scenario 4: Clean Generated Files

```bash
git rm *.tmp
```

---

## Scenario 5: Remove Multiple Documents

```bash
git rm docs/*.md
```

---

## Scenario 6: Repository Cleanup

```bash
git rm -r unused-module/
```

---

# Difference Between Common Variants

## `git rm` vs Operating System Delete

`git rm`

- Deletes file
- Stages deletion

OS delete command

- Deletes file only
- Requires additional Git staging

---

## `git rm` vs `git rm --cached`

`git rm`

- Removes file completely

`git rm --cached`

- Keeps local file
- Stops tracking

---

## `git rm` vs `git clean`

`git rm`

- Removes tracked files

`git clean`

- Removes untracked files

---

# Common Errors and Troubleshooting

## File Has Local Modifications

```text
error: file has local modifications
```

Solution:

```bash
git rm -f filename
```

---

## Directory Removal Failed

Use:

```bash
git rm -r directory
```

---

## File Not Found

Verify path:

```bash
git status
```

---

## Accidentally Removed File

Restore before commit:

```bash
git restore filename
```

---

# Best Practices

1. Verify deletions with `git status`.
2. Use `--cached` for files that should remain locally.
3. Update `.gitignore` when removing tracked generated files.
4. Use `--dry-run` before bulk file removals.
5. Commit large deletions separately.
6. Be careful when using `-f`.
7. Review impacted dependencies before removing directories.

---

# Useful Workflow

```bash
# Remove file
git rm old-config.yml

# Review changes
git status

# Commit deletion
git commit -m "Remove obsolete configuration"
```

---

# Quick Reference

```bash
git rm file.txt                 # Remove file
git rm file1 file2              # Remove multiple files
git rm -r folder/               # Remove directory
git rm --cached file.txt        # Stop tracking file
git rm -f file.txt              # Force remove
git rm -n file.txt              # Dry run
git rm -q file.txt              # Quiet mode
git rm --ignore-unmatch file    # Ignore missing files
```

---

# Conclusion

`git rm` is the standard way to remove tracked files and directories from a Git repository. By understanding staged deletions, cached removals, recursive deletion, force options, and cleanup workflows, developers can safely manage repository contents while preserving a clear and accurate project history.
