# `git clean`

## Introduction

`git clean` removes untracked files and directories from a Git repository. It is commonly used to clean build artifacts, temporary files, generated content, and other files that are not tracked by Git.

```bash
git clean
```

Unlike `git reset`, which affects tracked files, `git clean` focuses on untracked content.

```text
Repository
   |
   +-- Tracked Files
   |
   +-- Untracked Files
             |
             | git clean
             v
         Removed
```

---

# Syntax

```bash
git clean [options]
git clean -f
git clean -fd
git clean -n
```

Examples:

```bash
git clean -n
git clean -f
git clean -fd
git clean -fx
```

---

# Understanding Git Clean

Before cleaning:

```text
project
├── src/
├── build/
├── temp.log
└── test-output/
```

After:

```bash
git clean -fd
```

Only untracked files and directories are removed.

---

# Common Usage Scenarios

## Preview Cleanup

```bash
git clean -n
```

Shows files that would be removed.

---

## Remove Untracked Files

```bash
git clean -f
```

Deletes untracked files.

---

## Remove Untracked Directories

```bash
git clean -fd
```

Removes files and folders.

---

## Clean Build Outputs

```bash
git clean -fx
```

Removes ignored build artifacts.

---

# All Major Options

## `git clean -n`

Dry run mode.

```bash
git clean -n
```

Displays what will be deleted.

---

## `git clean --dry-run`

Equivalent to `-n`.

```bash
git clean --dry-run
```

---

## `git clean -f`

Force deletion.

```bash
git clean -f
```

Required because Git protects files by default.

---

## `git clean --force`

Equivalent to `-f`.

```bash
git clean --force
```

---

## `git clean -d`

Include directories.

```bash
git clean -d
```

Typically combined with `-f`.

---

## `git clean -fd`

Remove files and directories.

```bash
git clean -fd
```

---

## `git clean -x`

Remove ignored files too.

```bash
git clean -fx
```

Deletes files listed in `.gitignore`.

---

## `git clean -X`

Remove only ignored files.

```bash
git clean -fX
```

Leaves other untracked files untouched.

---

## `git clean -e`

Exclude specific files.

```bash
git clean -f -e '*.log'
```

---

## `git clean -i`

Interactive mode.

```bash
git clean -i
```

Allows selective cleanup.

---

## `git clean -q`

Quiet mode.

```bash
git clean -fq
```

Suppresses output.

---

# Interactive Clean Mode

```bash
git clean -i
```

Provides options such as:

- Clean selected files
- Filter files
- View candidates
- Confirm removals

Useful when repositories contain many untracked files.

---

# Real-World Scenarios

## Scenario 1: Clean Build Directory

```bash
git clean -fd
```

Remove generated build outputs.

---

## Scenario 2: Reset Development Environment

```bash
git reset --hard
git clean -fd
```

Return repository to a clean state.

---

## Scenario 3: Remove Ignored Build Artifacts

```bash
git clean -fx
```

Useful for Maven, Gradle, npm, and .NET projects.

---

## Scenario 4: Delete Only Ignored Files

```bash
git clean -fX
```

Preserves manually created files.

---

## Scenario 5: Interactive Cleanup

```bash
git clean -i
```

Review files before deleting.

---

## Scenario 6: Preserve Logs While Cleaning

```bash
git clean -f -e '*.log'
```

---

# Difference Between Common Variants

## `git clean -f` vs `git clean -fd`

`-f`

- Removes files only

`-fd`

- Removes files and directories

---

## `git clean -x` vs `git clean -X`

`-x`

- Removes ignored and untracked files

`-X`

- Removes ignored files only

---

## `git clean` vs `git reset`

`git clean`

- Untracked files
- No commit history change

`git reset`

- Tracked changes
- Moves references depending on mode

---

# Common Errors and Troubleshooting

## Nothing Happens

```text
fatal: clean.requireForce defaults to true
```

Solution:

```bash
git clean -f
```

---

## Important Files Deleted

Git cannot automatically recover removed untracked files.

Always run:

```bash
git clean -n
```

first.

---

## Directories Not Removed

Use:

```bash
git clean -fd
```

---

## Ignored Files Remain

Use:

```bash
git clean -fx
```

---

# Best Practices

1. Always preview with `-n` before cleaning.
2. Be careful when using `-x`.
3. Do not run clean blindly in production repositories.
4. Use interactive mode for large repositories.
5. Keep backups of important generated files.
6. Combine with `git reset --hard` for a full cleanup.
7. Understand the difference between ignored and untracked files.

---

# Useful Workflow

```bash
# Review repository state
git status

# Preview cleanup
git clean -n

# Remove files and directories
git clean -fd

# Verify clean state
git status
```

---

# Quick Reference

```bash
git clean -n                 # Preview cleanup
git clean -f                 # Remove files
git clean -fd                # Remove files and folders
git clean -fx                # Remove ignored files too
git clean -fX                # Remove ignored files only
git clean -i                 # Interactive mode
git clean -q                 # Quiet mode
git clean -f -e '*.log'      # Exclude files
git reset --hard && git clean -fd  # Full cleanup
```

---

# Conclusion

`git clean` is a powerful repository cleanup tool that removes untracked content and helps maintain a predictable working environment. By understanding dry runs, force operations, ignored-file cleanup, interactive mode, and recovery risks, developers can safely clean repositories without affecting tracked source code.
