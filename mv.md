# `git mv`

## Introduction

`git mv` is the Git command used to move or rename files and directories while automatically staging the change for the next commit.

```bash
git mv <source> <destination>
```

Instead of manually moving a file and then staging the rename, Git performs both actions in one operation.

```text
Old File Name
      |
      | git mv
      v
New File Name
```

---

# Syntax

```bash
git mv <source> <destination>
git mv [options] <source> <destination>
git mv <file1> <file2> <directory>
```

Examples:

```bash
git mv app.txt application.txt
git mv src/app.js src/main.js
git mv docs/ documentation/
```

---

# How Git MV Works

Traditional approach:

```bash
mv old.txt new.txt
git add new.txt
git rm old.txt
```

Simplified approach:

```bash
git mv old.txt new.txt
```

Git automatically stages the rename.

---

# Common Usage Scenarios

## Rename a File

```bash
git mv app.py main.py
```

---

## Move File to Another Directory

```bash
git mv config.yml config/config.yml
```

---

## Rename a Directory

```bash
git mv docs documentation
```

---

## Reorganize Project Structure

```bash
git mv services/* src/services/
```

---

# All Major Options

## `git mv`

Basic move or rename operation.

```bash
git mv old.txt new.txt
```

---

## `git mv -f`

Equivalent:

```bash
git mv --force
```

Overwrite destination if required.

```bash
git mv -f old.txt new.txt
```

---

## `git mv --force`

Force move operation.

```bash
git mv --force a.txt b.txt
```

---

## `git mv -k`

Equivalent:

```bash
git mv --skip-errors
```

Continue processing even if some moves fail.

```bash
git mv -k *.txt archive/
```

---

## `git mv --skip-errors`

Skip problematic files.

```bash
git mv --skip-errors *.log logs/
```

---

## `git mv -n`

Equivalent:

```bash
git mv --dry-run
```

Preview operations.

```bash
git mv -n old.txt new.txt
```

---

## `git mv --dry-run`

Simulate move without changes.

```bash
git mv --dry-run docs archive/
```

---

## `git mv -v`

Equivalent:

```bash
git mv --verbose
```

Display detailed output.

```bash
git mv -v old.txt new.txt
```

---

## `git mv --verbose`

Show files being moved.

```bash
git mv --verbose src/* backup/
```

---

# Understanding Rename Detection

Git does not store renames directly.

Instead, Git detects:

```text
Old File Removed
+
New File Added
=
Rename Detected
```

Using `git mv` helps stage this process correctly.

---

# Real-World Scenarios

## Scenario 1: Rename Source File

```bash
git mv LoginService.java AuthService.java
```

---

## Scenario 2: Project Refactoring

```bash
git mv controllers/ src/controllers/
```

---

## Scenario 3: Rename Configuration Files

```bash
git mv app.config production.config
```

---

## Scenario 4: Reorganize Documentation

```bash
git mv docs/ documentation/
```

---

## Scenario 5: Move Multiple Files

```bash
git mv *.md archive/
```

---

## Scenario 6: Monorepo Restructuring

```bash
git mv services/payment packages/payment
```

---

# Difference Between Common Variants

## `git mv` vs Operating System Move

`git mv`

- Moves file
- Stages change automatically

OS move command

- Moves file only
- Requires additional Git commands

---

## `git mv` vs `git rm` + `git add`

`git mv`

- Single command
- Easier workflow

Manual approach

- Multiple commands
- More error prone

---

## Directory Move vs File Move

File Move

```bash
git mv old.txt new.txt
```

Directory Move

```bash
git mv olddir newdir
```

---

# Common Errors and Troubleshooting

## Destination Already Exists

```text
fatal: destination exists
```

Solution:

```bash
git mv -f source destination
```

---

## Source File Missing

```text
fatal: bad source
```

Verify the file exists.

---

## File Not Tracked

Track file first:

```bash
git add filename
```

---

## Rename Not Reflected

Check staged changes:

```bash
git status
```

---

# Best Practices

1. Use `git mv` instead of operating system rename commands.
2. Verify changes with `git status`.
3. Commit large refactorings separately.
4. Use verbose mode for bulk reorganizations.
5. Preview large operations with `--dry-run`.
6. Keep renames focused and easy to review.
7. Test project references after moving files.

---

# Useful Workflow

```bash
# Rename file
git mv old-service.js new-service.js

# Verify change
git status

# Commit rename
git commit -m "Rename service file"
```

---

# Quick Reference

```bash
git mv old new                 # Move or rename
git mv file dir/               # Move file
git mv dir1 dir2               # Rename directory
git mv *.md archive/           # Move multiple files
git mv -f old new             # Force move
git mv -n old new             # Dry run
git mv -v old new             # Verbose output
git mv -k *.txt backup/       # Skip errors
```

---

# Conclusion

`git mv` simplifies file and directory renaming by combining filesystem operations with automatic staging. By understanding rename workflows, bulk moves, dry runs, force options, and repository restructuring techniques, developers can safely reorganize projects while maintaining clean and understandable version history.
