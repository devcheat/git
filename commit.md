# `git commit`

## Introduction

`git commit` records changes from the staging area into the repository history.

It is one of the most important Git commands and is used to create snapshots of your work, document changes, enable collaboration, and maintain a traceable project history.

```bash
git commit
```

---

# What Is a Commit?

A commit is a permanent snapshot of your project at a specific point in time.

```text
A --- B --- C
            ^
            |
         HEAD
```

Each commit contains:

- Snapshot of tracked files
- Commit message
- Author information
- Committer information
- Timestamp
- Parent commit reference
- Unique SHA hash

---

# Basic Syntax

```bash
git commit [options]
```

Examples:

```bash
git commit
git commit -m "Add login feature"
git commit -am "Fix login bug"
git commit --amend
```

---

# Commit Workflow

## Stage Files

```bash
git add .
```

## Create Commit

```bash
git commit -m "Implement user authentication"
```

## Push Commit

```bash
git push origin main
```

---

# Major Options

## `git commit -m`

Specify commit message directly.

```bash
git commit -m "Add payment API"
```

---

## `git commit -a`

Automatically stage modified tracked files.

```bash
git commit -am "Fix timeout issue"
```

---

## `git commit --amend`

Modify the latest commit.

```bash
git commit --amend
```

Scenario:

Forgot to include a file in the previous commit.

---

## `git commit --amend --no-edit`

Update last commit without changing message.

```bash
git commit --amend --no-edit
```

---

## `git commit --reset-author`

Reset commit author information.

```bash
git commit --amend --reset-author
```

---

## `git commit -C COMMIT`

Reuse message from another commit.

```bash
git commit -C abc1234
```

---

## `git commit -c COMMIT`

Reuse and edit message from another commit.

```bash
git commit -c abc1234
```

---

## `git commit --fixup COMMIT`

Create fixup commit.

```bash
git commit --fixup abc1234
```

---

## `git commit --squash COMMIT`

Create squash commit.

```bash
git commit --squash abc1234
```

---

## `git commit --interactive`

Interactive commit creation.

```bash
git commit --interactive
```

---

## `git commit -v`

Verbose commit editor.

```bash
git commit -v
```

---

## `git commit -q`

Quiet mode.

```bash
git commit -q
```

---

## `git commit --dry-run`

Preview commit result.

```bash
git commit --dry-run
```

---

## `git commit --allow-empty`

Create empty commit.

```bash
git commit --allow-empty -m "Trigger deployment"
```

---

## `git commit --allow-empty-message`

Allow blank commit message.

```bash
git commit --allow-empty-message
```

---

## `git commit --cleanup`

Control commit message cleanup.

```bash
git commit --cleanup=strip
```

Supported modes:

- strip
- whitespace
- verbatim
- scissors
- default

---

## `git commit --author`

Override author.

```bash
git commit --author="John Doe <john@example.com>"
```

---

## `git commit --date`

Override commit date.

```bash
git commit --date="2026-01-01 10:00:00"
```

---

## `git commit --signoff`

Add Signed-off-by trailer.

```bash
git commit --signoff
```

---

## `git commit -S`

Create signed commit.

```bash
git commit -S -m "Release candidate"
```

---

## `git commit --no-gpg-sign`

Disable commit signing.

```bash
git commit --no-gpg-sign
```

---

## `git commit --trailer`

Add metadata trailer.

```bash
git commit --trailer "Reviewed-by: Team Lead"
```

---

## `git commit --pathspec-from-file`

Read paths from external file.

```bash
git commit --pathspec-from-file=files.txt
```

---

## `git commit --pathspec-file-nul`

Expect NUL-separated paths.

```bash
git commit --pathspec-file-nul
```

---

# Commit Message Best Practices

- Use imperative mood
- Keep subject under 50 characters when practical
- Explain why, not only what
- Keep commits focused
- Reference issue IDs when needed

---

# Conventional Commits

```text
feat: add user registration
fix: resolve login failure
docs: update README
refactor: simplify service layer
test: add unit tests
chore: update dependencies
```

---

# Real-World Scenarios

## Scenario 1: Feature Development

```bash
git commit -m "feat: add shopping cart"
```

---

## Scenario 2: Production Hotfix

```bash
git commit -m "fix: resolve payment failure"
```

---

## Scenario 3: Documentation Update

```bash
git commit -m "docs: update API examples"
```

---

## Scenario 4: Trigger CI Pipeline

```bash
git commit --allow-empty -m "Trigger CI"
```

---

## Scenario 5: Clean History Before Merge

```bash
git commit --fixup abc1234
```

---

## Scenario 6: Open Source Contribution

```bash
git commit --signoff
```

---

## Scenario 7: Security Sensitive Release

```bash
git commit -S
```

---

# Common Mistakes

## Large Mixed Commits

Avoid combining unrelated changes.

---

## Poor Commit Messages

Bad:

```text
update
```

Good:

```text
fix: prevent duplicate invoice creation
```

---

## Rewriting Shared History

Use caution with amended commits that were already pushed.

---

# Git Commit vs Related Commands

## `git add` vs `git commit`

`git add`

- Stages changes

`git commit`

- Records staged changes

---

## `git commit` vs `git push`

`git commit`

- Local action

`git push`

- Sends commits to remote repository

---

# Enterprise Best Practices

1. Use signed commits.
2. Enforce commit message standards.
3. Keep commits atomic.
4. Use issue identifiers.
5. Review commit history regularly.
6. Automate validation with hooks.
7. Document contribution standards.

---

# Quick Reference

```bash
git commit -m "message"
git commit -am "message"
git commit --amend
git commit --amend --no-edit
git commit --fixup COMMIT
git commit --squash COMMIT
git commit --signoff
git commit -S
git commit --allow-empty
git commit --dry-run
git commit --author="NAME <EMAIL>"
git commit --date="DATE"
```

---

# Conclusion

`git commit` is the core command used to create project history, enable collaboration, support auditing, and maintain reliable software delivery workflows.
