# `git backfill`

## Introduction

`git backfill` is an experimental Git command designed for repositories that use partial clone capabilities, especially blobless clones created with:

```bash
git clone --filter=blob:none
```

It downloads missing blob objects in efficient batches instead of fetching them one at a time when commands need them.

---

# Why Git Backfill Exists

In a blobless partial clone:

- Commits are downloaded
- Trees are downloaded
- Blob contents are omitted initially

This makes cloning large repositories significantly faster.

However, commands such as:

```bash
git blame
git log -p
git show
git diff
```

may later require historical blobs.

Without backfill, Git may download them individually, causing poor performance.

---

# Basic Syntax

```bash
git backfill [options] [revision-range]
```

Examples:

```bash
git backfill
git backfill HEAD~100..HEAD
git backfill --sparse
git backfill --min-batch-size=100000
```

---

# How Backfill Works

```text
Partial Clone
      |
      v
Missing Blob Objects
      |
      v
 git backfill
      |
      v
Bulk Blob Download
```

The command groups missing objects into larger requests to reduce network overhead.

---

# Major Options

## `git backfill`

Download missing blobs reachable from HEAD.

```bash
git backfill
```

---

## `--min-batch-size`

Specify minimum batch size.

```bash
git backfill --min-batch-size=50000
```

Example:

```bash
git backfill --min-batch-size=100000
```

Useful for large repositories.

---

## `--sparse`

Download only objects within the sparse checkout definition.

```bash
git backfill --sparse
```

Ideal for monorepos.

---

## `--no-sparse`

Disable sparse restrictions.

```bash
git backfill --no-sparse
```

Downloads matching objects regardless of sparse-checkout settings.

---

## `--include-edges`

Include blobs from boundary commits.

```bash
git backfill --include-edges
```

Useful before:

```bash
git log -p A..B
```

---

## `--no-include-edges`

Exclude edge commits.

```bash
git backfill --no-include-edges
```

---

# Revision Ranges

## Backfill Current History

```bash
git backfill HEAD
```

---

## Backfill Recent Commits

```bash
git backfill HEAD~100..HEAD
```

---

## Backfill Specific Branch

```bash
git backfill main
```

---

## Backfill Release History

```bash
git backfill release/v2.0
```

---

# Common Workflows

## Workflow 1: Blobless Clone Optimization

```bash
git clone --filter=blob:none repository-url
cd repository

git backfill
```

Pre-download missing historical blobs.

---

## Workflow 2: Improve Blame Performance

```bash
git backfill

git blame src/app.py
```

Avoid repeated object fetches.

---

## Workflow 3: Large Monorepo

```bash
git sparse-checkout init

git backfill --sparse
```

Downloads only necessary blob content.

---

## Workflow 4: Release Investigation

```bash
git backfill release/v1.0..release/v2.0
```

Prepare for history analysis.

---

# Real-World Scenarios

## Scenario 1: Enterprise Monorepo

Developers clone using:

```bash
git clone --filter=blob:none
```

Then:

```bash
git backfill --sparse
```

for faster analysis.

---

## Scenario 2: Security Audit

Before reviewing years of history:

```bash
git backfill
```

Ensures required blob data is available.

---

## Scenario 3: CI/CD Investigation

```bash
git backfill HEAD~500..HEAD
```

Prepare repository for extensive diff analysis.

---

# Common Mistakes

## Using Backfill on Normal Clones

Regular clones already contain blob objects.

```text
git backfill often provides little benefit.
```

---

## Forgetting Partial Clone Context

The command is primarily intended for:

```bash
git clone --filter=blob:none
```

workflows.

---

## Downloading Excessive History

```bash
git backfill
```

can request a large amount of data in very large repositories.

Consider limiting scope using revision ranges.

---

# Comparison with Related Commands

## `git backfill` vs `git fetch`

`git fetch`

- Downloads refs and objects normally requested

`git backfill`

- Specifically downloads missing historical blobs

---

## `git backfill` vs `git clone --filter=blob:none`

Partial clone:

- Delays blob downloads

Backfill:

- Retrieves delayed blob data in optimized batches

---

## `git backfill` vs On-Demand Fetches

On-demand:

- Many small requests

Backfill:

- Fewer large requests
- Better efficiency

---

# Best Practices

1. Use with blobless partial clones.
2. Use sparse checkout where possible.
3. Backfill only required revision ranges.
4. Use larger batch sizes in large repositories.
5. Perform backfill before extensive historical analysis.
6. Validate network and storage impact.
7. Combine with monorepo optimization strategies.

---

# Quick Reference

```bash
git backfill                                   # Backfill HEAD history
git backfill HEAD~100..HEAD                    # Specific range
git backfill --sparse                          # Sparse checkout only
git backfill --no-sparse                       # Ignore sparse rules
git backfill --include-edges                   # Include boundary commits
git backfill --no-include-edges                # Exclude boundary commits
git backfill --min-batch-size=100000           # Larger batches
git backfill main                              # Branch history
```

---

# Conclusion

`git backfill` is an advanced Git command aimed at improving the usability of blobless partial clones. By downloading missing blob objects in optimized batches, it improves performance for historical analysis, code archaeology, blame operations, release investigations, and large enterprise monorepo workflows.
