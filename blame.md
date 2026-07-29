# `git blame`

## Introduction

`git blame` helps identify who last modified each line of a file and when the modification occurred. It is widely used for debugging, auditing changes, understanding code ownership, investigating regressions, and reviewing project history.

```bash
git blame <file>
```

Rather than showing commit history chronologically, `git blame` annotates every line in a file with commit information.

```text
Source File
     |
     | git blame
     v
Line-by-Line History
```

---

# Syntax

```bash
git blame [options] <file>
git blame [options] <revision> -- <file>
```

Examples:

```bash
git blame app.py
git blame README.md
git blame HEAD~5 -- app.py
git blame -L 10,20 app.py
```

---

# Understanding Git Blame Output

Example:

```text
a1b2c3d4 (John 2026-06-10 10:15:23 +0530 1) import os
b5c6d7e8 (Mary 2026-06-15 09:12:00 +0530 2) import sys
```

Output contains:

- Commit hash
- Author name
- Timestamp
- Line number
- Source code line

---

# Common Usage Scenarios

## Identify Who Changed a Line

```bash
git blame app.py
```

Useful during debugging and code reviews.

---

## Investigate Production Issues

```bash
git blame config.yml
```

Find the developer responsible for a configuration change.

---

## Review Recent Modifications

```bash
git blame HEAD~10 -- app.py
```

Analyze code history before a regression occurred.

---

## Analyze Specific Lines

```bash
git blame -L 20,40 app.py
```

Review ownership of selected lines only.

---

# All Major Options

## `git blame`

Basic blame operation.

```bash
git blame app.py
```

---

## `git blame -L`

Blame a line range.

```bash
git blame -L 10,25 app.py
```

Useful for large files.

---

## `git blame --line-porcelain`

Machine-readable output.

```bash
git blame --line-porcelain app.py
```

Useful for automation and scripts.

---

## `git blame -p`

Short form of porcelain format.

```bash
git blame -p app.py
```

---

## `git blame -c`

Display commit information differently.

```bash
git blame -c app.py
```

Useful for commit-centric analysis.

---

## `git blame -e`

Show author email addresses.

```bash
git blame -e app.py
```

---

## `git blame -f`

Show source filename.

```bash
git blame -f app.py
```

Helpful after file renames.

---

## `git blame -l`

Show long commit hashes.

```bash
git blame -l app.py
```

---

## `git blame -n`

Show original line numbers.

```bash
git blame -n app.py
```

---

## `git blame -s`

Suppress author names.

```bash
git blame -s app.py
```

---

## `git blame -t`

Show raw timestamps.

```bash
git blame -t app.py
```

---

## `git blame -w`

Ignore whitespace-only changes.

```bash
git blame -w app.py
```

Very useful after formatting updates.

---

## `git blame -M`

Detect moved lines within a file.

```bash
git blame -M app.py
```

---

## `git blame -C`

Detect copied code between files.

```bash
git blame -C app.py
```

---

## `git blame --since`

Limit history by date.

```bash
git blame --since="2026-01-01" app.py
```

---

## `git blame --reverse`

Show earliest revision containing lines.

```bash
git blame --reverse HEAD~20..HEAD app.py
```

---

## `git blame --show-name`

Display original file names.

```bash
git blame --show-name app.py
```

---

## `git blame --show-number`

Display line numbers.

```bash
git blame --show-number app.py
```

---

# Real-World Scenarios

## Scenario 1: Debugging Production Failure

```bash
git blame payment.py
```

Identify the commit that introduced problematic code.

---

## Scenario 2: Find Owner of a Business Rule

```bash
git blame invoice.py
```

Locate the developer who implemented a specific rule.

---

## Scenario 3: Ignore Formatting Commits

```bash
git blame -w app.py
```

Avoid noise from indentation-only changes.

---

## Scenario 4: Review Code Movement

```bash
git blame -M service.py
```

Track moved code blocks.

---

## Scenario 5: Analyze Copied Code

```bash
git blame -C service.py
```

Determine source of copied logic.

---

## Scenario 6: Audit Sensitive Configuration

```bash
git blame security.yml
```

Review change ownership.

---

# Difference Between Common Variants

## `git blame` vs `git log`

`git blame`

- Line-level history
- Shows ownership

`git log`

- Commit-level history
- Shows chronological changes

---

## `git blame -M` vs `git blame -C`

`-M`

- Detect moved code
- Same file

`-C`

- Detect copied code
- Across files

---

## `git blame` vs `git annotate`

Both provide similar functionality.

Historically:

```bash
git annotate
```

is an older synonym for blame.

---

# Common Errors and Troubleshooting

## File Not Found

```text
fatal: no such path
```

Verify file path.

---

## Incorrect Revision

```text
fatal: bad revision
```

Check commit reference.

---

## Renamed File Issues

Use:

```bash
git blame -M filename
```

---

## Excessive Output

Limit lines:

```bash
git blame -L 1,50 app.py
```

---

# Best Practices

1. Use blame for investigation, not blame assignment.
2. Combine with `git log` for full context.
3. Use `-w` after formatting changes.
4. Use `-M` and `-C` when tracking refactored code.
5. Review commit messages after identifying changes.
6. Restrict analysis with `-L` on large files.
7. Verify historical context before drawing conclusions.

---

# Useful Workflow

```bash
# Identify change owner
git blame app.py

# View associated commit
git show COMMIT_HASH

# Review surrounding history
git log --follow app.py
```

---

# Quick Reference

```bash
git blame file.py                    # Basic blame
git blame -L 1,20 file.py            # Line range
git blame -w file.py                 # Ignore whitespace
git blame -M file.py                 # Detect moved code
git blame -C file.py                 # Detect copied code
git blame -e file.py                 # Show emails
git blame -l file.py                 # Long hashes
git blame -p file.py                 # Porcelain output
git blame --since="2026-01-01" file.py
git blame --reverse HEAD~10..HEAD file.py
```

---

# Conclusion

`git blame` is a powerful investigative tool that reveals line-by-line ownership and history. By mastering blame options, line filtering, rename tracking, copy detection, and history analysis techniques, developers can debug issues faster, understand project evolution, and maintain codebases more effectively.
