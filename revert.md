# `git revert`

## Introduction

`git revert` safely undoes changes introduced by an existing commit by creating a new commit that reverses the changes. Unlike `git reset`, revert does not rewrite history, making it the preferred option for shared and collaborative branches.

```bash
git revert <commit>
```

```text
Original Commit
       |
       v
Commit A ---- Commit B ---- Commit C
                                |
                                | git revert
                                v
Commit D (reverses Commit C)
```

---

# Syntax

```bash
git revert <commit>
git revert <commit1> <commit2>
git revert <range>
git revert [options] <commit>
```

Examples:

```bash
git revert a1b2c3d
git revert HEAD
git revert HEAD~1
git revert main~3..main
```

---

# Understanding Git Revert

Instead of deleting a commit, Git generates another commit that applies the opposite changes.

Before:

```text
A --- B --- C
```

After reverting C:

```text
A --- B --- C --- D
```

Where commit D undoes the changes from commit C.

---

# Common Usage Scenarios

## Revert Latest Commit

```bash
git revert HEAD
```

---

## Revert Specific Commit

```bash
git revert a1b2c3d
```

---

## Undo Production Bug

```bash
git revert bug_commit_hash
```

---

## Revert Multiple Commits

```bash
git revert hash1 hash2
```

---

# All Major Options

## `git revert <commit>`

Revert a commit.

```bash
git revert HASH
```

---

## `git revert HEAD`

Undo latest commit.

```bash
git revert HEAD
```

---

## `git revert -n`

Equivalent:

```bash
git revert --no-commit
```

Apply changes without creating a commit.

```bash
git revert -n HASH
```

---

## `git revert --no-commit`

Useful when reverting multiple commits together.

```bash
git revert --no-commit HASH
```

---

## `git revert -m`

Equivalent to:

```bash
git revert --mainline
```

Used for merge commits.

```bash
git revert -m 1 MERGE_HASH
```

---

## `git revert --mainline`

Specify parent number while reverting merge commits.

```bash
git revert --mainline 1 HASH
```

---

## `git revert --edit`

Edit commit message.

```bash
git revert --edit HASH
```

---

## `git revert --no-edit`

Accept generated message.

```bash
git revert --no-edit HASH
```

---

## `git revert --signoff`

Add Signed-off-by line.

```bash
git revert --signoff HASH
```

---

## `git revert --strategy`

Specify merge strategy.

```bash
git revert --strategy=recursive HASH
```

---

## `git revert -X`

Pass strategy option.

```bash
git revert -X theirs HASH
```

---

## `git revert --continue`

Continue after conflict resolution.

```bash
git revert --continue
```

---

## `git revert --abort`

Cancel revert process.

```bash
git revert --abort
```

---

## `git revert --quit`

Stop revert state.

```bash
git revert --quit
```

---

## `git revert --skip`

Skip problematic commit.

```bash
git revert --skip
```

---

# Reverting Merge Commits

Merge commits require specifying a parent.

```bash
git revert -m 1 MERGE_COMMIT
```

Parent values:

- 1 = first parent
- 2 = second parent

---

# Handling Revert Conflicts

Example:

```text
CONFLICT (content): Merge conflict
```

Resolve conflicts:

```bash
git add .
git revert --continue
```

Abort operation:

```bash
git revert --abort
```

---

# Real-World Scenarios

## Scenario 1: Undo Faulty Production Deployment

```bash
git revert release_commit
```

Safely removes bad code.

---

## Scenario 2: Revert a Security Change

```bash
git revert security_commit
```

---

## Scenario 3: Revert Multiple Buggy Commits

```bash
git revert hash1 hash2 hash3
```

---

## Scenario 4: Revert Without Automatic Commit

```bash
git revert -n hash1
git revert -n hash2
```

Create a single combined commit afterward.

---

## Scenario 5: Undo a Merge

```bash
git revert -m 1 merge_hash
```

---

## Scenario 6: Shared Branch Recovery

```bash
git revert bad_commit
git push
```

Safe for collaboration.

---

# Difference Between Common Variants

## `git revert` vs `git reset`

`git revert`

- Creates new commit
- Preserves history
- Safe for shared branches

`git reset`

- Rewrites history
- Changes branch pointer
- Risky on shared branches

---

## `git revert` vs `git checkout`

`git revert`

- Creates undo commit

`git checkout` / `git restore`

- Restores files only

---

## `git revert` vs `git cherry-pick`

`git revert`

- Reverses changes

`git cherry-pick`

- Copies changes

---

# Common Errors and Troubleshooting

## Merge Commit Requires Mainline

```text
error: commit is a merge but no -m option was given
```

Solution:

```bash
git revert -m 1 HASH
```

---

## Conflict During Revert

Resolve conflicts then:

```bash
git revert --continue
```

---

## Wrong Commit Reverted

Revert the revert:

```bash
git revert REVERT_COMMIT
```

---

## Revert Already Applied

Git may report there is nothing to revert.

---

# Best Practices

1. Use revert on shared branches.
2. Prefer revert over reset for published commits.
3. Test after reverting critical changes.
4. Use meaningful revert messages.
5. Review affected files before pushing.
6. Understand merge-parent selection.
7. Revert small units of change when possible.

---

# Useful Workflow

```bash
# Identify commit
git log --oneline

# Revert commit
git revert COMMIT_HASH

# Review changes
git status

# Push safely
git push
```

---

# Quick Reference

```bash
git revert HASH                    # Revert commit
git revert HEAD                    # Revert latest commit
git revert -n HASH                 # No commit
git revert --continue              # Continue
.git revert --abort                # Abort
git revert --skip                  # Skip
git revert -m 1 MERGE_HASH         # Revert merge
git revert --no-edit HASH          # Default message
git revert --edit HASH             # Edit message
git revert --signoff HASH          # Signoff
```

---

# Conclusion

`git revert` is the safest method for undoing changes in shared repositories. By creating inverse commits instead of rewriting history, it enables teams to recover from mistakes while preserving a complete audit trail of what happened and why.
