# `git diff`

## Introduction

`git diff` is one of the most important Git commands for inspecting changes. It shows differences between:

- Working directory and staging area
- Staging area and repository
- Commits
- Branches
- Tags
- Files

It helps developers review code before staging, committing, merging, or deploying.

```bash
git diff
```

---

# Understanding Git Areas

```text
Repository (HEAD)
       |
       v
Staging Area (Index)
       |
       v
Working Directory
```

`git diff` compares content between these locations.

---

# Basic Syntax

```bash
git diff [options]
```

General syntax:

```bash
git diff <source> <target>
```

Examples:

```bash
git diff
git diff --staged
git diff HEAD
git diff main feature-branch
```

---

# Common Usage Scenarios

## Show Unstaged Changes

```bash
git diff
```

Compares:

```text
Working Directory
vs
Staging Area
```

Use before running `git add`.

---

## Show Staged Changes

```bash
git diff --staged
```

or

```bash
git diff --cached
```

Compares:

```text
Staging Area
vs
HEAD
```

Useful before committing.

---

## Show All Changes Since Last Commit

```bash
git diff HEAD
```

Displays:

- Staged changes
- Unstaged changes

---

## Compare Two Files

```bash
git diff file1.txt file2.txt
```

Useful outside normal Git workflows.

---

# Understanding Diff Output

Example:

```diff
- console.log("old")
+ console.log("new")
```

Legend:

```text
- Removed line
+ Added line
```

Metadata example:

```diff
@@ -10,3 +10,4 @@
```

Meaning:

```text
Old file line range
New file line range
```

---

# Comparing Commits

## Compare Two Commits

```bash
git diff commit1 commit2
```

Example:

```bash
git diff a1b2c3 d4e5f6
```

---

## Compare Commit With HEAD

```bash
git diff a1b2c3 HEAD
```

---

## Compare Previous Commit

```bash
git diff HEAD~1 HEAD
```

Compare latest commit with its parent.

---

## Compare Several Commits Back

```bash
git diff HEAD~5 HEAD
```

---

# Comparing Branches

## Compare Branches

```bash
git diff main feature
```

Shows differences between branch tips.

---

## Compare Current Branch Against Main

```bash
git diff main
```

Common during pull request preparation.

---

## Show Changes Introduced by Feature Branch

```bash
git diff main...feature
```

Triple dot compares from merge base.

---

## Two Dots vs Three Dots

### Two Dots

```bash
git diff main..feature
```

Compare branch endpoints.

### Three Dots

```bash
git diff main...feature
```

Compare feature changes since divergence.

Common for code reviews.

---

# Comparing Tags

```bash
git diff v1.0 v2.0
```

Useful for release notes and audits.

---

# Comparing Specific Files

## Single File

```bash
git diff app.py
```

---

## File Across Branches

```bash
git diff main feature -- app.py
```

---

## Multiple Files

```bash
git diff -- app.py config.yml
```

---

# Major Options

## `git diff --staged`

Show staged changes.

```bash
git diff --staged
```

---

## `git diff --cached`

Alias for:

```bash
git diff --staged
```

---

## `git diff --name-only`

Display changed file names only.

```bash
git diff --name-only
```

Output:

```text
app.py
config.yml
```

---

## `git diff --name-status`

Show file names and statuses.

```bash
git diff --name-status
```

Example:

```text
M app.py
A test.py
D old.py
```

---

## `git diff --stat`

Summary statistics.

```bash
git diff --stat
```

Example:

```text
app.py | 10 +++++++---
```

---

## `git diff --shortstat`

Compact statistics.

```bash
git diff --shortstat
```

---

## `git diff --numstat`

Machine-readable statistics.

```bash
git diff --numstat
```

Useful for automation.

---

## `git diff --word-diff`

Highlight word changes.

```bash
git diff --word-diff
```

Useful for documentation changes.

---

## `git diff --color-words`

Colored word-level differences.

```bash
git diff --color-words
```

---

## `git diff -U`

Control context lines.

```bash
git diff -U5
```

Show five surrounding lines.

---

## `git diff --unified`

Equivalent to:

```bash
git diff --unified=5
```

---

## `git diff -w`

Ignore whitespace changes.

```bash
git diff -w
```

Useful for formatting-only updates.

---

## `git diff --ignore-space-change`

Ignore amount of whitespace changes.

```bash
git diff --ignore-space-change
```

---

## `git diff --ignore-all-space`

Ignore all whitespace differences.

```bash
git diff --ignore-all-space
```

---

## `git diff --check`

Check whitespace errors.

```bash
git diff --check
```

---

## `git diff --exit-code`

Return status code if differences exist.

```bash
git diff --exit-code
```

Common in CI/CD.

---

## `git diff --quiet`

Suppress output.

```bash
git diff --quiet
```

Useful in scripts.

---

## `git diff --binary`

Generate binary patch.

```bash
git diff --binary
```

---

## `git diff --submodule`

Show submodule differences.

```bash
git diff --submodule
```

---

# Real-World Scenarios

## Scenario 1: Review Before Staging

```bash
git diff
```

Verify local edits.

---

## Scenario 2: Review Before Commit

```bash
git diff --staged
```

Ensure only intended changes are committed.

---

## Scenario 3: Pull Request Review

```bash
git diff main...feature
```

See branch-specific changes.

---

## Scenario 4: Detect Formatting Changes

```bash
git diff -w
```

Ignore whitespace noise.

---

## Scenario 5: CI Validation

```bash
git diff --quiet
```

Fail pipeline when differences exist.

---

## Scenario 6: Release Comparison

```bash
git diff v1.0 v2.0
```

Review release delta.

---

# Common Mistakes

## Expecting Staged Changes From Plain Diff

```bash
git diff
```

Shows only unstaged changes.

Use:

```bash
git diff --staged
```

---

## Misunderstanding Two Dots and Three Dots

```bash
git diff main..feature
```

is different from

```bash
git diff main...feature
```

Understand merge-base behavior before reviews.

---

## Ignoring Renames

Large refactors can be confusing without additional rename analysis options.

---

# Comparison with Related Commands

## `git diff` vs `git show`

`git diff`

- Compare states
- Compare branches
- Compare commits

`git show`

- Display commit details

---

## `git diff` vs `git status`

`git status`

- High-level summary

`git diff`

- Exact content changes

---

## `git diff` vs `git log`

`git log`

- Commit history

`git diff`

- Content differences

---

# Best Practices

1. Run `git diff` frequently.
2. Review changes before staging.
3. Review staged content before committing.
4. Use `--stat` for quick summaries.
5. Use `main...feature` for pull request validation.
6. Use whitespace-ignore options during formatting changes.
7. Automate validations using `--exit-code`.
8. Check release differences using tags.

---

# Useful Workflow

```bash
# Review local changes
git diff

# Stage selected files
git add app.py

# Review staged content
git diff --staged

# Commit
git commit -m "Implement feature"

# Compare with main
git diff main...HEAD
```

---

# Quick Reference

```bash
git diff                              # Unstaged changes
git diff --staged                     # Staged changes
git diff HEAD                         # All changes since last commit
git diff commit1 commit2              # Compare commits
git diff main feature                 # Compare branches
git diff main...feature               # Feature branch changes
git diff --name-only                  # Changed files only
git diff --name-status                # Files and statuses
git diff --stat                       # Summary statistics
git diff --word-diff                  # Word-level changes
git diff -w                           # Ignore whitespace
git diff --exit-code                  # Script-friendly validation
```

---

# Conclusion

`git diff` is the primary tool for understanding what has changed in a repository. Whether reviewing local modifications, validating staged changes, comparing commits, analyzing releases, or reviewing feature branches, mastering `git diff` significantly improves code quality, review effectiveness, and overall Git productivity.
