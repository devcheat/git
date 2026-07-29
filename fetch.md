# `git fetch`

## Introduction

`git fetch` downloads commits, branches, tags, and references from a remote repository without modifying your current branch. It is one of the safest synchronization commands in Git because it updates remote-tracking references while leaving your working directory unchanged.

```bash
git fetch
```

Think of `git fetch` as a way to check what changed on the remote before deciding whether to merge or rebase those changes.

```text
Remote Repository
       |
       | git fetch
       v
Remote Tracking Branches
       |
       | review changes
       v
Local Branch
```

---

# Syntax

```bash
git fetch [options]
git fetch <remote>
git fetch <remote> <branch>
```

Examples:

```bash
git fetch
git fetch origin
git fetch origin main
git fetch --all
```

---

# Common Usage Scenarios

## Fetch Latest Changes

```bash
git fetch origin
```

Downloads latest information from the remote without changing local code.

---

## Fetch a Specific Branch

```bash
git fetch origin main
```

Useful when only one branch matters.

---

## Fetch All Remotes

```bash
git fetch --all
```

Fetches updates from every configured remote.

---

## Fetch Tags

```bash
git fetch --tags
```

Downloads tags from the remote repository.

---

## Preview a Fetch

```bash
git fetch --dry-run
```

Shows what would be fetched.

---

# Understanding Remote Tracking Branches

After fetching:

```text
Local Branch          main
Remote Branch         origin/main
```

Compare them:

```bash
git log main..origin/main
```

View incoming commits before merging.

---

# All Major Options

## `git fetch`

Default fetch operation.

```bash
git fetch
```

---

## `git fetch origin`

Fetch from a specific remote.

```bash
git fetch origin
```

---

## `git fetch origin main`

Fetch only one branch.

```bash
git fetch origin main
```

---

## `git fetch --all`

Fetch from every remote.

```bash
git fetch --all
```

Useful when repository contains:

```text
origin
upstream
backup
```

---

## `git fetch --append`

Append fetched references to fetch history.

```bash
git fetch --append
```

---

## `git fetch --atomic`

Apply updates atomically.

```bash
git fetch --atomic
```

Either all reference updates succeed or none do.

---

## `git fetch --depth`

Perform shallow fetch.

```bash
git fetch --depth=10
```

Downloads limited history.

---

## `git fetch --deepen`

Extend shallow history.

```bash
git fetch --deepen=50
```

---

## `git fetch --shallow-since`

Fetch history after a date.

```bash
git fetch --shallow-since="2026-01-01"
```

---

## `git fetch --shallow-exclude`

Exclude commits reachable from a reference.

```bash
git fetch --shallow-exclude=release
```

---

## `git fetch --unshallow`

Convert shallow repository to full repository.

```bash
git fetch --unshallow
```

---

## `git fetch --update-shallow`

Allow shallow boundary updates.

```bash
git fetch --update-shallow
```

---

## `git fetch --dry-run`

Preview operation.

```bash
git fetch --dry-run
```

---

## `git fetch --tags`

Fetch all tags.

```bash
git fetch --tags
```

---

## `git fetch --no-tags`

Skip tag download.

```bash
git fetch --no-tags
```

---

## `git fetch --prune`

Remove obsolete remote-tracking branches.

```bash
git fetch --prune
```

---

## `git fetch --prune-tags`

Remove stale tags.

```bash
git fetch --prune-tags
```

---

## `git fetch --force`

Force reference updates.

```bash
git fetch --force
```

---

## `git fetch --recurse-submodules`

Fetch submodule content.

```bash
git fetch --recurse-submodules
```

---

## `git fetch --no-recurse-submodules`

Skip submodule downloads.

```bash
git fetch --no-recurse-submodules
```

---

## `git fetch --jobs`

Parallel fetch operations.

```bash
git fetch --jobs=4
```

---

## `git fetch --multiple`

Fetch multiple remotes.

```bash
git fetch --multiple origin upstream
```

---

## `git fetch --ipv4`

Force IPv4.

```bash
git fetch --ipv4
```

---

## `git fetch --ipv6`

Force IPv6.

```bash
git fetch --ipv6
```

---

## `git fetch --verbose`

Verbose output.

```bash
git fetch --verbose
```

---

## `git fetch --quiet`

Minimal output.

```bash
git fetch --quiet
```

---

# Real-World Scenarios

## Scenario 1: Start Your Workday

```bash
git fetch origin
git log HEAD..origin/main --oneline
```

Review incoming work before pulling.

---

## Scenario 2: Check Changes Before Merge

```bash
git fetch origin
git diff main origin/main
```

---

## Scenario 3: Clean Stale Branches

```bash
git fetch --prune
```

Removes deleted remote references.

---

## Scenario 4: Release Validation

```bash
git fetch --tags
git tag
```

---

## Scenario 5: CI/CD Pipeline

```bash
git fetch --depth=1
```

Reduces download time.

---

# Difference Between Common Variants

## `git fetch` vs `git pull`

`git fetch`

- Downloads changes
- Does not merge
- Safe inspection

`git pull`

- Downloads changes
- Merges or rebases
- Modifies current branch

---

## `git fetch` vs `git fetch --all`

`git fetch`

- Current remote only

`git fetch --all`

- Every configured remote

---

## `git fetch --tags` vs `git fetch --no-tags`

`--tags`

- Download tags

`--no-tags`

- Skip tags

---

# Best Practices

1. Fetch before starting work.
2. Review incoming commits before merging.
3. Use `--prune` regularly.
4. Keep remote branches clean.
5. Use shallow fetches in CI pipelines.
6. Fetch tags before releases.
7. Prefer fetch over blind pull operations.

---

# Useful Workflow

```bash
# Synchronize metadata
git fetch origin

# Review incoming commits
git log HEAD..origin/main --oneline

# Review differences
git diff main origin/main

# Merge when ready
git merge origin/main
```

---

# Quick Reference

```bash
git fetch                       # Default fetch
git fetch origin                # Fetch remote
git fetch origin main           # Fetch branch
git fetch --all                 # All remotes
git fetch --tags                # Tags
git fetch --prune               # Cleanup stale refs
git fetch --dry-run             # Preview
git fetch --depth=1             # Shallow fetch
git fetch --unshallow           # Full history
git fetch --verbose             # Detailed output
```

---

# Conclusion

`git fetch` is the safest way to synchronize with remote repositories. By understanding remote-tracking branches, fetch options, pruning, shallow repositories, tags, and comparison workflows, developers can review incoming changes confidently before integrating them into local development branches.
