# `git bisect`

## Introduction

`git bisect` is Git's built-in binary search tool for finding the exact commit that introduced a bug, regression, performance issue, or unwanted behavior.

Instead of manually checking hundreds or thousands of commits, Git uses a binary search algorithm to drastically reduce the number of commits you need to test.

```bash
git bisect
```

Typical use cases:

- Finding when a bug was introduced
- Identifying performance regressions
- Locating breaking changes
- Tracking configuration issues
- Debugging production incidents

---

# Why Git Bisect Is Powerful

Imagine a repository with:

```text
1,024 commits
```

Without `git bisect`:

```text
Potentially 1,024 manual checks
```

With binary search:

```text
Only about 10 checks
```

This makes `git bisect` one of the most valuable debugging tools in Git.

---

# How Git Bisect Works

Binary search repeatedly divides the commit range in half.

```text
Bad Commit (Current)
        |
        |
        v
 [A]-[B]-[C]-[D]-[E]-[F]-[G]-[H]
  Good                     Bad
```

You tell Git:

- A known good commit
- A known bad commit

Git chooses a midpoint and asks whether it is:

```text
good
bad
skip
```

The search continues until the first bad commit is identified.

---

# Basic Workflow

## Step 1: Start Bisect

```bash
git bisect start
```

---

## Step 2: Mark Current Commit as Bad

```bash
git bisect bad
```

or

```bash
git bisect bad <commit>
```

---

## Step 3: Mark Known Good Commit

```bash
git bisect good <commit>
```

Example:

```bash
git bisect good a1b2c3d
```

Git automatically checks out a midpoint commit.

---

## Step 4: Test the Commit

Run your application:

```bash
npm test
```

or

```bash
mvn test
```

or

```bash
pytest
```

---

## Step 5: Tell Git the Result

If bug exists:

```bash
git bisect bad
```

If bug does not exist:

```bash
git bisect good
```

Git moves to another midpoint.

---

## Step 6: Finish

Eventually Git shows:

```text
<commit> is the first bad commit
```

Reset repository:

```bash
git bisect reset
```

---

# Core Commands

## `git bisect start`

Start a bisect session.

```bash
git bisect start
```

---

## `git bisect good`

Mark commit as good.

```bash
git bisect good <commit>
```

Example:

```bash
git bisect good v1.2
```

---

## `git bisect bad`

Mark commit as bad.

```bash
git bisect bad
```

or

```bash
git bisect bad HEAD
```

---

## `git bisect reset`

End session and return to original branch.

```bash
git bisect reset
```

---

## `git bisect skip`

Skip commits that cannot be tested.

```bash
git bisect skip
```

Examples:

```text
Build failures
Missing dependencies
Corrupt commit state
```

---

## `git bisect log`

Show bisect history.

```bash
git bisect log
```

Useful for documenting investigations.

---

## `git bisect replay`

Replay previous bisect session.

```bash
git bisect replay bisect-log.txt
```

---

## `git bisect visualize`

View candidate commits.

```bash
git bisect visualize
```

Equivalent:

```bash
gitk
```

or configured visual tools.

---

## `git bisect view`

Alias for visualize.

```bash
git bisect view
```

---

# Automated Bisect

One of the most powerful features.

## `git bisect run`

Automatically execute a test script.

```bash
git bisect run ./test.sh
```

Git uses exit codes.

```text
0 = good
1-127 = bad
125 = skip
```

---

## Example Test Script

```bash
#!/bin/bash
npm test
```

Run:

```bash
git bisect run ./test.sh
```

Git automatically finds the bad commit.

---

# Advanced Options

## Start With Good and Bad Commits

```bash
git bisect start HEAD v1.0
```

Equivalent to:

```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0
```

---

## Multiple Good Commits

```bash
git bisect good v1.0 v1.1 v1.2
```

Useful for narrowing large histories.

---

## Bisect Only Specific Paths

```bash
git bisect start -- src/
```

Or:

```bash
git bisect start HEAD v1.0 -- backend/
```

Limits search scope.

---

## Terms Other Than Good/Bad

### Old/New Terminology

Start:

```bash
git bisect start --term-old good --term-new bad
```

Example:

```bash
git bisect old
git bisect new
```

---

### Custom Terms

```bash
git bisect start --term-old working --term-new broken
```

Use:

```bash
git bisect working
git bisect broken
```

---

# Real-World Scenarios

## Scenario 1: Production Bug Investigation

Known:

```text
Version 2.1 works
Version 2.5 fails
```

Commands:

```bash
git bisect start
git bisect bad v2.5
git bisect good v2.1
```

Run tests until culprit commit is found.

---

## Scenario 2: Performance Regression

Application slowed down significantly.

```bash
git bisect start
git bisect bad HEAD
git bisect good v3.0
```

Measure response time at every candidate commit.

---

## Scenario 3: Failed CI Build

```bash
git bisect run ./build-validation.sh
```

Git performs investigation automatically.

---

## Scenario 4: Database Migration Failure

Find commit introducing schema issue.

```bash
git bisect good stable-release
git bisect bad current-release
```

---

## Scenario 5: Large Enterprise Repository

Restrict search:

```bash
git bisect start HEAD release-1.0 -- services/payment/
```

Focus only on relevant component.

---

# Example Complete Session

```bash
# Start investigation
git bisect start

# Mark current commit bad
git bisect bad

# Mark older commit good
git bisect good a1b2c3d

# Test checked-out revision
npm test

# If test passes
git bisect good

# If test fails
git bisect bad

# Continue until first bad commit found

# Restore repository
git bisect reset
```

---

# Common Mistakes

## Forgetting to Reset

After investigation:

```bash
git bisect reset
```

Otherwise repository may remain detached.

---

## Choosing Incorrect Good Commit

If the chosen good commit already contains the bug:

```text
Results become unreliable.
```

Verify carefully.

---

## Testing Inconsistently

Use identical validation criteria throughout the bisect session.

---

## Ignoring Build Dependencies

Older commits may require:

```text
Different libraries
Different runtimes
Different configurations
```

Consider using containers.

---

# Comparison with Other Git Commands

## `git bisect` vs `git log`

`git log`

- Shows history
- Manual investigation

`git bisect`

- Actively identifies culprit commit
- Automated binary search

---

## `git bisect` vs `git blame`

`git blame`

- Finds author of line

`git bisect`

- Finds commit introducing behavior

---

## `git bisect` vs Manual Checkout

Manual checkout:

```bash
git checkout commit
```

Requires sequential testing.

Bisect:

```bash
git bisect
```

Uses logarithmic search.

---

# Best Practices

1. Identify a verified good commit.
2. Automate tests whenever possible.
3. Use `git bisect run` for repeatable investigations.
4. Document results using `git bisect log`.
5. Skip untestable commits instead of guessing.
6. Reset after finishing.
7. Use path-limited bisecting in monorepos.
8. Ensure test results are deterministic.

---

# Quick Reference

```bash
git bisect start                        # Start session
git bisect bad                          # Mark bad commit
git bisect good COMMIT                  # Mark good commit
git bisect skip                         # Skip commit
git bisect reset                        # End session
git bisect log                          # Show log
git bisect replay log.txt               # Replay session
git bisect visualize                    # Visualize candidates
git bisect run ./test.sh                # Automated search
git bisect start HEAD v1.0              # Start with known range
git bisect start HEAD v1.0 -- src/      # Limit search path
```

---

# Conclusion

`git bisect` is one of the most powerful yet underutilized Git commands. By using binary search across commit history, it can quickly identify the exact commit that introduced a bug, regression, failure, or performance issue. Combined with automated testing through `git bisect run`, it becomes an essential tool for debugging complex applications and maintaining high-quality software delivery pipelines.
