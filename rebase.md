# `git rebase`

## Introduction

`git rebase` is one of Git's most powerful history-management commands.

It is used to move, replay, combine, clean up, and reorganize commits onto a new base commit.

Rebasing helps create a cleaner and more linear project history.

```bash
git rebase
```

---

# What Is Rebase?

Rebase reapplies commits from one branch onto another base.

Before:

```text
A---B---C main
     \
      D---E feature
```

After:

```text
A---B---C main
         \
          D'---E' feature
```

The commits are replayed and receive new commit IDs.

---

# Rebase vs Merge

## Merge

```text
A---B---C
     \   \
      D---E---M
```

Preserves complete history.

## Rebase

```text
A---B---C---D'---E'
```

Creates linear history.

---

# Basic Syntax

```bash
git rebase <branch>
git rebase <upstream>
git rebase --interactive
git rebase --continue
```

---

# Standard Rebase Workflow

```bash
git checkout feature-login
git rebase main
```

---

# Major Options

## `git rebase --interactive`

Interactive commit editing.

```bash
git rebase -i HEAD~5
```

Use for:

- Squashing commits
- Reordering commits
- Editing messages
- Splitting commits

---

## `git rebase --continue`

Continue after conflict resolution.

```bash
git rebase --continue
```

---

## `git rebase --abort`

Cancel rebase operation.

```bash
git rebase --abort
```

---

## `git rebase --skip`

Skip problematic commit.

```bash
git rebase --skip
```

---

## `git rebase --quit`

Quit rebase without resetting worktree.

```bash
git rebase --quit
```

---

## `git rebase --onto`

Rebase onto specific branch or commit.

```bash
git rebase --onto main develop feature
```

---

## `git rebase --root`

Rebase from repository root.

```bash
git rebase --root
```

---

## `git rebase --autosquash`

Automatically apply fixup and squash commits.

```bash
git rebase -i --autosquash main
```

---

## `git rebase --autostash`

Automatically stash local changes.

```bash
git rebase --autostash main
```

---

## `git rebase --reapply-cherry-picks`

Reapply commits previously detected as cherry-picks.

```bash
git rebase --reapply-cherry-picks main
```

---

## `git rebase --empty`

Control handling of empty commits.

```bash
git rebase --empty=keep
```

Options:

- drop
- keep
- stop

---

## `git rebase --keep-base`

Keep original merge base.

```bash
git rebase --keep-base main
```

---

## `git rebase --fork-point`

Use fork point analysis.

```bash
git rebase --fork-point main
```

---

## `git rebase --no-fork-point`

Disable fork point detection.

```bash
git rebase --no-fork-point main
```

---

## `git rebase --merge`

Use merge strategy backend.

```bash
git rebase --merge main
```

---

## `git rebase --apply`

Use patch application backend.

```bash
git rebase --apply main
```

---

## `git rebase --strategy`

Specify merge strategy.

```bash
git rebase --strategy=ort main
```

---

## `git rebase -X`

Pass strategy options.

```bash
git rebase -X theirs main
```

---

## `git rebase --exec`

Execute command after each commit.

```bash
git rebase -i --exec "npm test"
```

---

## `git rebase --signoff`

Add signoff line.

```bash
git rebase --signoff main
```

---

## `git rebase --gpg-sign`

GPG sign rewritten commits.

```bash
git rebase --gpg-sign main
```

---

## `git rebase --no-gpg-sign`

Disable commit signing.

```bash
git rebase --no-gpg-sign main
```

---

## `git rebase --committer-date-is-author-date`

Synchronize dates.

```bash
git rebase --committer-date-is-author-date
```

---

## `git rebase --ignore-date`

Rewrite date metadata.

```bash
git rebase --ignore-date
```

---

# Interactive Rebase Commands

```text
pick
reword
edit
squash
fixup
drop
exec
break
label
reset
merge
```

---

# Conflict Resolution

## Step 1

```bash
git status
```

## Step 2

Resolve files.

## Step 3

```bash
git add .
```

## Step 4

```bash
git rebase --continue
```

---

# Real-World Scenarios

## Scenario 1: Update Feature Branch

```bash
git rebase main
```

---

## Scenario 2: Clean Commit History Before PR

```bash
git rebase -i HEAD~10
```

---

## Scenario 3: Squash Fix Commits

```bash
git rebase -i --autosquash
```

---

## Scenario 4: Move Feature to Different Base

```bash
git rebase --onto release-branch main feature
```

---

## Scenario 5: Resolve Long-Lived Branch Divergence

```bash
git rebase main
```

---

## Scenario 6: Enterprise Pull Request Cleanup

```bash
git rebase -i HEAD~20
```

---

## Scenario 7: Automated Validation During Rebase

```bash
git rebase -i --exec "mvn test"
```

---

# Common Mistakes

## Rebasing Shared History

Avoid rebasing commits already consumed by other developers.

---

## Force Pushing Without Review

Validate rewritten history before push.

---

## Ignoring Conflicts

Always inspect conflict resolution carefully.

---

# Rebase vs Related Commands

## `git rebase` vs `git merge`

Rebase:

- Linear history
- Rewrites commits

Merge:

- Preserves history
- Creates merge commits

---

## `git rebase` vs `git cherry-pick`

Rebase:

- Replays a series of commits

Cherry-pick:

- Copies selected commits

---

# Best Practices

1. Rebase local feature branches regularly.
2. Avoid rebasing public shared history.
3. Use interactive rebase before pull requests.
4. Squash unnecessary commits.
5. Resolve conflicts carefully.
6. Validate builds after rebasing.
7. Communicate before force pushes.
8. Keep commit history meaningful.

---

# Quick Reference

```bash
git rebase main
git rebase -i HEAD~5
git rebase --continue
git rebase --abort
git rebase --skip
git rebase --onto main old-base feature
git rebase --autosquash
git rebase --autostash
git rebase --root
git rebase --merge
git rebase --signoff
```

---

# Conclusion

`git rebase` is an advanced Git command used to maintain clean, linear, and professional commit histories. Understanding rebasing, conflict resolution, interactive rebase workflows, and history rewriting techniques enables teams to produce maintainable repositories and high-quality pull requests.
