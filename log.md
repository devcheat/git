# `git log`

## Introduction

`git log` is one of the most important Git commands for exploring repository history. It allows developers to inspect commits, trace changes, identify contributors, investigate bugs, review releases, and analyze project evolution.

```bash
git log
```

`git log` reads commit history from the repository and displays information such as:

- Commit hash
- Author
- Date
- Commit message
- Branch history
- Merge history

---

# Why `git log` Matters

Common use cases:

- Understanding project history
- Tracking feature development
- Reviewing releases
- Debugging regressions
- Finding breaking changes
- Identifying contributors
- Preparing audits and reports

---

# Basic Syntax

```bash
git log [options]
```

Examples:

```bash
git log
git log --oneline
git log --graph
git log --stat
```

---

# Basic Usage

## Show Complete Commit History

```bash
git log
```

Sample output:

```text
commit f8d12ab
Author: John Doe
Date: Tue Jul 15 10:00:00 2026

    Add payment validation
```

---

## Limit Number of Commits

```bash
git log -5
```

Show the five most recent commits.

---

## One-Line Output

```bash
git log --oneline
```

Output:

```text
f8d12ab Add payment validation
9c21def Fix login issue
```

Useful for quick reviews.

---

# Commit Formatting Options

## `git log --oneline`

Compressed commit view.

```bash
git log --oneline
```

---

## `git log --decorate`

Display branch and tag references.

```bash
git log --decorate
```

Example:

```text
HEAD -> main
origin/main
v2.0
```

---

## `git log --graph`

Display branch structure.

```bash
git log --graph
```

Example:

```text
* Commit A
|\
| * Commit B
* Commit C
```

---

## `git log --graph --oneline --all`

Popular visualization command.

```bash
git log --graph --oneline --all
```

---

## `git log --pretty`

Customize output format.

```bash
git log --pretty=oneline
```

---

## `git log --pretty=format`

Custom fields.

```bash
git log --pretty=format:"%h %an %s"
```

Placeholders:

```text
%H Full hash
%h Short hash
%an Author name
%ae Author email
%ad Author date
%s Subject
```

---

# Filtering Commit History

## By Author

```bash
git log --author="Vinod"
```

---

## By Commit Message

```bash
git log --grep="security"
```

Search commit messages.

---

## Case-Insensitive Search

```bash
git log --grep="fix" -i
```

---

## Multiple Message Searches

```bash
git log --grep="bug" --grep="security"
```

---

## By Date Range

### Since Date

```bash
git log --since="2026-01-01"
```

### Until Date

```bash
git log --until="2026-06-30"
```

### Relative Time

```bash
git log --since="2 weeks ago"
```

---

## Find Commits by File

```bash
git log app.py
```

Show commits affecting a file.

---

## Find Commits by Directory

```bash
git log src/
```

---

# Comparing History

## View Branch History

```bash
git log main..feature
```

Commits in feature not in main.

---

## View Unique Branch Changes

```bash
git log main...feature
```

Uses merge base comparison.

---

## All Branches

```bash
git log --all
```

Show commits from all refs.

---

# Statistics and File Changes

## Show Modified Files

```bash
git log --name-only
```

---

## Show File Statuses

```bash
git log --name-status
```

Output:

```text
A newfile.py
M app.py
D old.py
```

---

## Show Statistics

```bash
git log --stat
```

Output:

```text
app.py | 10 ++++++----
```

---

## Show Patch Content

```bash
git log -p
```

Displays actual code changes.

---

## Show Summary

```bash
git log --summary
```

---

# Advanced Search Options

## Search for Added or Removed Text

```bash
git log -S "CustomerService"
```

Useful for tracking when text appeared.

---

## Search by Regex

```bash
git log -G "Customer.*Service"
```

---

## Follow Renamed Files

```bash
git log --follow app.py
```

Tracks file history across renames.

---

# Working with Merges

## Show Merge Commits

```bash
git log --merges
```

---

## Exclude Merge Commits

```bash
git log --no-merges
```

---

## First Parent History

```bash
git log --first-parent
```

Useful for release tracking.

---

# Reflog vs Log

## Standard History

```bash
git log
```

Shows repository history.

---

## Reflog History

```bash
git reflog
```

Shows local reference movement.

Useful for recovery operations.

---

# Real-World Scenarios

## Scenario 1: Review Recent Work

```bash
git log --oneline -20
```

---

## Scenario 2: Find Who Added Feature

```bash
git log --grep="payment"
```

---

## Scenario 3: Audit Security Fixes

```bash
git log --grep="security" --since="1 year ago"
```

---

## Scenario 4: Review Release History

```bash
git log --first-parent --oneline
```

---

## Scenario 5: Investigate File Issues

```bash
git log --follow app.py
```

---

## Scenario 6: Visualize Team Branches

```bash
git log --graph --decorate --all --oneline
```

---

# Common Mistakes

## Using Full Log in Large Repositories

```bash
git log
```

Can produce enormous output.

Prefer:

```bash
git log -20
```

---

## Confusing Two Dots and Three Dots

```bash
git log main..feature
```

is different from

```bash
git log main...feature
```

---

## Forgetting `--follow`

File rename history may appear incomplete.

---

# Comparison with Related Commands

## `git log` vs `git show`

`git log`

- Multiple commits
- Historical timeline

`git show`

- Detailed view of a specific commit

---

## `git log` vs `git diff`

`git log`

- Commit history

`git diff`

- Content differences

---

## `git log` vs `git reflog`

`git log`

- Repository history

`git reflog`

- Local reference history

---

# Best Practices

1. Use `--oneline` for quick reviews.
2. Use `--graph` to understand branch topology.
3. Use `--stat` before releases.
4. Use `--grep` for targeted investigations.
5. Use `--follow` for renamed files.
6. Use `-S` and `-G` during debugging.
7. Use `--first-parent` for release analysis.
8. Combine filters to narrow large histories.

---

# Useful Workflow

```bash
# Quick history
git log --oneline -10

# Visualize branches
git log --graph --decorate --all --oneline

# Find commits touching a file
git log --follow app.py

# Inspect changes
git log -p -5
```

---

# Quick Reference

```bash
git log                                 # Full history
git log -10                             # Last 10 commits
git log --oneline                       # Compact view
git log --graph --oneline --all         # Visual graph
git log --author="John"                # Filter by author
git log --grep="security"              # Search message
git log --since="30 days ago"          # Date filter
git log --stat                          # Statistics
git log -p                              # Show patches
git log --follow file.txt               # Track file history
git log -S "text"                      # Search added/removed text
git log --merges                        # Merge commits
```

---

# Conclusion

`git log` is the primary command for understanding repository history. From simple commit reviews to advanced forensic investigations, contributor analysis, release audits, and debugging sessions, mastering `git log` enables developers to navigate project history efficiently and make better engineering decisions.
