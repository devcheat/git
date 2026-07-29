# `git status`

## Introduction

`git status` provides a snapshot of the current state of your repository. It shows:

- Current branch
- Staged changes
- Unstaged changes
- Untracked files
- Merge conflicts
- Remote tracking status

```bash
git status
```

---

# Why Use `git status`

It helps developers:

- Verify changes before committing
- Detect forgotten files
- Review merge conflicts
- Check synchronization with remotes
- Understand repository state quickly

---

# Git Areas Explained

```text
Repository (HEAD)
       |
       v
Staging Area
       |
       v
Working Directory
```

`git status` reports differences between these areas.

---

# Basic Syntax

```bash
git status [options]
```

Examples:

```bash
git status
git status -s
git status -b
git status --porcelain
```

---

# Common Usage

## Check Repository Status

```bash
git status
```

Example Output:

```text
On branch main
Changes not staged for commit:
  modified: app.py

Untracked files:
  notes.txt
```

---

## Clean Working Tree

```bash
git status
```

Output:

```text
nothing to commit, working tree clean
```

---

# Understanding Status Sections

## Changes to Be Committed

```text
Changes to be committed:
```

Files already staged.

## Changes Not Staged

```text
Changes not staged for commit:
```

Modified files not yet staged.

## Untracked Files

```text
Untracked files:
```

Files Git does not currently track.

---

# Short Status Format

## `git status -s`

```bash
git status -s
```

Example:

```text
M  app.py
 M config.yml
?? notes.txt
```

---

# Status Codes

```text
M  Modified
A  Added
D  Deleted
R  Renamed
C  Copied
?? Untracked
!! Ignored
```

---

# Two-Column Status Format

```text
XY filename
```

Where:

- X = staging area status
- Y = working tree status

Example:

```text
MM app.py
```

Meaning:

- Staged modification exists
- Additional unstaged modification exists

---

# Major Options

## `git status -s`

Short format.

```bash
git status -s
```

---

## `git status --short`

Equivalent to:

```bash
git status --short
```

---

## `git status -b`

Show branch tracking details.

```bash
git status -b
```

---

## `git status --branch`

Long form:

```bash
git status --branch
```

---

## `git status --show-stash`

Show stash information.

```bash
git status --show-stash
```

---

## `git status --ignored`

Display ignored files.

```bash
git status --ignored
```

---

## `git status --untracked-files`

```bash
git status --untracked-files=no
git status --untracked-files=normal
git status --untracked-files=all
```

---

## `git status --porcelain`

Machine-readable output.

```bash
git status --porcelain
```

Useful for scripts and CI/CD.

---

## `git status --porcelain=v2`

Enhanced machine-readable format.

```bash
git status --porcelain=v2
```

---

## `git status -v`

Verbose output.

```bash
git status -v
```

---

## `git status --verbose`

Equivalent to:

```bash
git status --verbose
```

---

# Branch Tracking Status

## Ahead of Remote

```text
Your branch is ahead of 'origin/main' by 2 commits.
```

Need:

```bash
git push
```

---

## Behind Remote

```text
Your branch is behind 'origin/main' by 3 commits.
```

Need:

```bash
git pull
```

---

## Diverged Branches

```text
Your branch and 'origin/main' have diverged.
```

Requires merge or rebase.

---

# Merge Conflict Status

Example:

```text
both modified: app.py
```

Common conflict codes:

```text
UU Both Modified
AA Both Added
DD Both Deleted
```

---

# Real-World Scenarios

## Scenario 1: Verify Before Commit

```bash
git status
```

Ensure expected files are staged.

---

## Scenario 2: Find Forgotten Files

```text
?? test.py
```

Add:

```bash
git add test.py
```

---

## Scenario 3: Verify Push Readiness

```text
Your branch is ahead of origin/main by 2 commits.
```

Push changes.

---

## Scenario 4: Resolve Merge Conflicts

```bash
git status
```

Quickly identifies conflicted files.

---

## Scenario 5: Automation Scripts

```bash
git status --porcelain
```

Reliable machine-readable output.

---

# Common Mistakes

## Forgetting Untracked Files

```text
?? newfile.py
```

These files won't be committed until staged.

---

## Committing Unexpected Changes

Always review:

```bash
git status
```

before committing.

---

## Working on the Wrong Branch

Use:

```bash
git status -b
```

---

# Comparison with Related Commands

## `git status` vs `git diff`

`git status`

- Summary of changes

`git diff`

- Exact content changes

---

## `git status` vs `git log`

`git status`

- Current repository state

`git log`

- Historical repository state

---

# Best Practices

1. Run `git status` frequently.
2. Run it before commits.
3. Run it before pushes.
4. Review untracked files.
5. Keep working trees clean.
6. Use short mode during development.
7. Use porcelain output in automation.
8. Review branch tracking information regularly.

---

# Useful Workflow

```bash
# Check status
git status

# Stage changes
git add .

# Verify staging
git status

# Commit
git commit -m "Implement feature"

# Verify push status
git status
```

---

# Quick Reference

```bash
git status                          # Full status
git status -s                       # Short format
git status --short                  # Short format
git status -b                       # Branch details
git status --branch                 # Branch info
git status --show-stash             # Display stash info
git status --ignored                # Show ignored files
git status --porcelain              # Machine-readable output
git status --porcelain=v2           # Enhanced machine output
git status -v                       # Verbose mode
```

---

# Conclusion

`git status` is the command developers use most frequently because it provides instant visibility into repository state. Mastering its output and options helps prevent mistakes, improves commit quality, and enables safer Git workflows.
