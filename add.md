# Git `add` Command: The Complete Guide

## Introduction

`git add` is one of the most frequently used Git commands. It moves changes from your working directory into the **staging area** (also called the index), preparing them for the next commit.

```bash
git add <pathspec>
```

Think of Git as having three primary areas:

1. **Working Directory** – where you edit files.
2. **Staging Area (Index)** – where you prepare changes for commit.
3. **Repository** – where committed history resides.

```text
Working Directory
       |
       | git add
       v
 Staging Area
       |
       | git commit
       v
 Repository
```

---

# Syntax

```bash
git add [options] [--] <pathspec>
```

Examples:

```bash
git add file.txt
git add src/app.js
git add .
git add *.md
```

---

# Common Usage Scenarios

## Add a Single File

```bash
git add README.md
```

Use when only one file should be included in the next commit.

---

## Add Multiple Files

```bash
git add README.md LICENSE app.py
```

---

## Add All Changes in Current Directory

```bash
git add .
```

Stages:

- New files
- Modified files
- Deleted files

Only inside the current directory and subdirectories.

---

## Add Everything in Repository

```bash
git add -A
```

Stages:

- New files
- Modifications
- Deletions

Across the entire repository.

---

## Add Updated Files Only

```bash
git add -u
```

Stages:

- Modified files
- Deleted files

Does NOT stage newly created files.

Example:

```text
modified: app.py
deleted: old.py
new: test.py
```

Result:

```text
✓ app.py staged
✓ old.py staged
✗ test.py not staged
```

---

## Add New and Modified Files

```bash
git add .
```

Useful during regular development when working from the repository root.

---

# Interactive Staging

## Patch Mode

```bash
git add -p
```

Stages selected chunks (hunks) from a file.

Example:

```bash
git add -p app.py
```

Possible options:

```text
y - stage hunk
n - don't stage
q - quit
s - split hunk
e - edit hunk
```

Ideal when a file contains unrelated changes.

---

## Interactive Mode

```bash
git add -i
```

Menu-driven staging interface.

Possible actions include:

- status
- update
- revert
- add untracked
- patch
- diff

---

# All Major Options

## `git add -A`

Equivalent:

```bash
git add --all
```

Stages all changes across the repository.

Example:

```bash
git add --all
```

---

## `git add --all`

Stages:

- Added files
- Modified files
- Deleted files

Example:

```bash
git add --all
```

---

## `git add .`

Stages all changes beneath the current directory.

Example:

```bash
cd src
git add .
```

---

## `git add -u`

Equivalent:

```bash
git add --update
```

Stages modifications and deletions only.

---

## `git add --update`

```bash
git add --update
```

Common use:

```bash
git add -u
git commit -m "Update tracked files"
```

---

## `git add -N`

Equivalent:

```bash
git add --intent-to-add
```

Marks a file as intended for future addition.

Example:

```bash
git add -N newfile.txt
```

Useful for reviewing diffs before fully staging content.

---

## `git add --intent-to-add`

```bash
git add --intent-to-add report.md
```

---

## `git add -f`

Equivalent:

```bash
git add --force
```

Forces ignored files to be staged.

Example:

```bash
git add -f .env
```

Use carefully.

---

## `git add --force`

```bash
git add --force logs/debug.log
```

---

## `git add --ignore-removal`

Ignore removed files while staging.

Example:

```bash
git add --ignore-removal .
```

Primarily for compatibility with older workflows.

---

## `git add --no-all`

Similar behavior to `--ignore-removal`.

```bash
git add --no-all .
```

---

## `git add --refresh`

Refresh index without adding file content.

```bash
git add --refresh
```

Useful during troubleshooting.

---

## `git add --dry-run`

Preview what would be staged.

```bash
git add --dry-run .
```

or

```bash
git add -n .
```

---

## `git add -n`

Short form of:

```bash
git add --dry-run
```

---

## `git add -v`

Equivalent:

```bash
git add --verbose
```

Displays processed files.

```bash
git add -v .
```

---

## `git add --verbose`

Useful in automation and debugging.

---

## `git add --chmod`

Change executable bit.

Make executable:

```bash
git add --chmod=+x script.sh
```

Remove executable:

```bash
git add --chmod=-x script.sh
```

---

## `git add --renormalize`

Reapply clean filters.

Useful after changing:

```text
.gitattributes
line-ending rules
```

Example:

```bash
git add --renormalize .
```

---

## `git add --pathspec-from-file`

Read file paths from a file.

Example:

```bash
git add --pathspec-from-file=filelist.txt
```

Contents:

```text
src/app.py
README.md
config.yml
```

---

## `git add --pathspec-file-nul`

Used with NUL-separated path lists.

```bash
git add --pathspec-from-file=files.txt --pathspec-file-nul
```

Useful in scripts.

---

## `git add --ignore-errors`

Continue processing even when some files fail.

```bash
git add --ignore-errors .
```

---

## `git add --sparse`

Allows updating entries outside sparse-checkout cone.

```bash
git add --sparse src/module.py
```

Useful for large monorepos.

---

## `git add --edit`

Edit patch before staging.

```bash
git add --edit app.py
```

Advanced workflow.

---

# Real-World Scenarios

## Scenario 1: Commit Only Documentation

Files changed:

```text
README.md
app.py
config.yml
```

Stage only documentation:

```bash
git add README.md
```

---

## Scenario 2: Stage Everything

```bash
git add -A
git commit -m "Release changes"
```

---

## Scenario 3: Exclude Experimental Code

```bash
git add -p
```

Choose only stable hunks.

---

## Scenario 4: Force Add Ignored File

`.gitignore`

```text
.env
```

Need to commit it:

```bash
git add -f .env
```

---

## Scenario 5: Large Repository Automation

```bash
git add --pathspec-from-file=filelist.txt
```

Useful in deployment pipelines.

---

# Difference Between Common Variants

## `git add .` vs `git add -A`

`git add .`

- Current directory scope
- Stages changes under current path

`git add -A`

- Repository-wide scope
- Stages all changes everywhere

---

## `git add .` vs `git add -u`

`git add .`

- New files
- Modified files
- Deleted files

`git add -u`

- Modified files
- Deleted files
- Not new files

---

## `git add -p` vs `git add .`

`git add .`

- Stage entire files

`git add -p`

- Stage selected hunks

---

# Best Practices

1. Use `git add -p` for clean commits.
2. Verify staging with `git status`.
3. Review diffs using `git diff --staged`.
4. Avoid committing secrets.
5. Use `.gitignore` correctly.
6. Prefer small focused commits.
7. Use `--dry-run` before large staging operations.

---

# Useful Workflow

```bash
# Check changes
git status

# Stage selectively
git add -p

# Review staged changes
git diff --staged

# Commit
git commit -m "Implement feature"
```

---

# Quick Reference

```bash
git add file.txt                 # Single file
git add .                        # Current directory
git add -A                       # Entire repository
git add -u                       # Modified + deleted
git add -p                       # Patch mode
git add -i                       # Interactive mode
git add -f file                  # Force add ignored file
git add -N file                  # Intent to add
git add --chmod=+x script.sh     # Make executable
git add --dry-run .              # Preview staging
git add --renormalize .          # Reapply filters
```

---

# Conclusion

`git add` is the bridge between your working directory and commit history. Mastering its options allows you to create cleaner commits, improve code review quality, avoid accidental changes, and work efficiently in projects ranging from small repositories to enterprise-scale monorepos.
