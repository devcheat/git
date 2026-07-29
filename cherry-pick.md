# `git cherry-pick`

## Introduction

`git cherry-pick` applies one or more commits from one branch onto another branch. It is commonly used to transfer bug fixes, hotfixes, specific features, and selected changes without merging an entire branch.

```bash
git cherry-pick <commit>
```

Unlike a merge, cherry-pick copies selected commits instead of combining complete branch histories.

```text
main
 |
 +---- feature
         |
         +---- Commit A
         +---- Commit B

Cherry-pick Commit A
         |
         v
main receives only Commit A
```

---

# Syntax

```bash
git cherry-pick <commit>
git cherry-pick <commit1> <commit2>
git cherry-pick <start>..<end>
git cherry-pick [options] <commit>
```

Examples:

```bash
git cherry-pick a1b2c3d
git cherry-pick a1b2c3d b2c3d4e
git cherry-pick main~3..main
```

---

# Understanding Cherry-Pick

Cherry-pick creates a new commit on the current branch using changes from an existing commit.

```text
Before:

main
A---B

feature
A---B---C

After Cherry-Pick(C):

main
A---B---D

feature
A---B---C
```

Commit `D` contains the same changes as `C` but has a different commit ID.

---

# Common Usage Scenarios

## Apply a Single Commit

```bash
git cherry-pick a1b2c3d
```

Apply one specific commit.

---

## Apply Multiple Commits

```bash
git cherry-pick a1b2c3d b2c3d4e
```

Apply selected commits sequentially.

---

## Move Hotfix to Production

```bash
git cherry-pick fix_commit_hash
```

Useful when only the bug fix is needed.

---

## Apply Commit Range

```bash
git cherry-pick release~3..release
```

Transfer multiple commits at once.

---

# All Major Options

## `git cherry-pick <commit>`

Apply a single commit.

```bash
git cherry-pick a1b2c3d
```

---

## `git cherry-pick -e`

Equivalent:

```bash
git cherry-pick --edit
```

Edit commit message before commit.

```bash
git cherry-pick -e a1b2c3d
```

---

## `git cherry-pick --edit`

Open editor before creating commit.

---

## `git cherry-pick -n`

Equivalent:

```bash
git cherry-pick --no-commit
```

Apply changes without creating a commit.

```bash
git cherry-pick -n a1b2c3d
```

---

## `git cherry-pick --no-commit`

Useful when combining multiple commits.

---

## `git cherry-pick -m`

Select parent of a merge commit.

```bash
git cherry-pick -m 1 merge_commit
```

---

## `git cherry-pick --mainline`

Used with merge commits.

```bash
git cherry-pick --mainline 1 merge_commit
```

---

## `git cherry-pick -x`

Append source commit information.

```bash
git cherry-pick -x a1b2c3d
```

Adds reference to original commit.

---

## `git cherry-pick --ff`

Allow fast-forward optimization.

```bash
git cherry-pick --ff commit_hash
```

---

## `git cherry-pick --allow-empty`

Preserve empty commits.

```bash
git cherry-pick --allow-empty hash
```

---

## `git cherry-pick --allow-empty-message`

Permit empty commit messages.

```bash
git cherry-pick --allow-empty-message hash
```

---

## `git cherry-pick --signoff`

Add Signed-off-by line.

```bash
git cherry-pick --signoff hash
```

---

## `git cherry-pick --strategy`

Select merge strategy.

```bash
git cherry-pick --strategy=recursive hash
```

---

## `git cherry-pick --strategy-option`

Pass merge strategy options.

```bash
git cherry-pick -X theirs hash
```

---

## `git cherry-pick --continue`

Continue after conflict resolution.

```bash
git cherry-pick --continue
```

---

## `git cherry-pick --skip`

Skip problematic commit.

```bash
git cherry-pick --skip
```

---

## `git cherry-pick --abort`

Cancel cherry-pick.

```bash
git cherry-pick --abort
```

---

## `git cherry-pick --quit`

Stop operation state without rollback.

```bash
git cherry-pick --quit
```

---

# Handling Conflicts

## Conflict Example

```text
CONFLICT (content): Merge conflict in app.py
```

Resolve conflicts and continue:

```bash
git add app.py
git cherry-pick --continue
```

---

# Real-World Scenarios

## Scenario 1: Production Hotfix

```bash
git switch production
git cherry-pick fix_commit
```

---

## Scenario 2: Selective Feature Migration

```bash
git cherry-pick feature_commit
```

Only required functionality is copied.

---

## Scenario 3: Backport Fix to Older Release

```bash
git switch release-1.0
git cherry-pick fix_commit
```

---

## Scenario 4: Apply Multiple Bug Fixes

```bash
git cherry-pick hash1 hash2 hash3
```

---

## Scenario 5: Copy Changes Without Commit

```bash
git cherry-pick -n hash
```

Review before committing.

---

## Scenario 6: Recover Commit From Another Branch

```bash
git cherry-pick old_commit
```

---

# Difference Between Common Variants

## `git cherry-pick` vs `git merge`

`git cherry-pick`

- Selected commits only
- No branch merge

`git merge`

- Entire branch history
- Broader integration

---

## `git cherry-pick` vs `git rebase`

`git cherry-pick`

- Copies commits

`git rebase`

- Replays branch history

---

## `git cherry-pick -n` vs Normal Cherry-Pick

Normal

- Creates commit immediately

`-n`

- Applies changes only

---

# Common Errors and Troubleshooting

## Merge Commit Requires Mainline

```text
error: commit is a merge but no -m option was given
```

Solution:

```bash
git cherry-pick -m 1 HASH
```

---

## Conflict During Cherry-Pick

Resolve conflicts then:

```bash
git cherry-pick --continue
```

---

## Wrong Commit Selected

Abort operation:

```bash
git cherry-pick --abort
```

---

## Empty Cherry Pick

Use:

```bash
git cherry-pick --allow-empty HASH
```

---

# Best Practices

1. Prefer cherry-pick for hotfixes.
2. Avoid excessive cherry-picking between long-lived branches.
3. Use `-x` for traceability.
4. Review commits before applying.
5. Test after cherry-picking.
6. Resolve conflicts carefully.
7. Consider merge or rebase for larger integrations.

---

# Useful Workflow

```bash
# Find commit
git log --oneline

# Switch branch
git switch release

# Apply commit
git cherry-pick -x COMMIT_HASH

# Test changes
# Push changes
```

---

# Quick Reference

```bash
git cherry-pick HASH                 # Single commit
git cherry-pick HASH1 HASH2          # Multiple commits
git cherry-pick A..B                 # Commit range
git cherry-pick -x HASH              # Track source commit
git cherry-pick -n HASH              # No commit
git cherry-pick -m 1 HASH            # Merge commit
git cherry-pick --continue           # Continue
git cherry-pick --skip               # Skip
git cherry-pick --abort              # Cancel
git cherry-pick --signoff HASH       # Add signoff
```

---

# Conclusion

`git cherry-pick` provides precise control over moving changes between branches. By mastering commit selection, conflict resolution, merge-commit handling, traceability options, and recovery workflows, developers can safely transfer fixes and features without merging entire branches.
