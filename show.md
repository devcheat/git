# `git show`

## Introduction

`git show` is a powerful Git command used to display detailed information about Git objects, most commonly commits.

It can show:

- Commit metadata
- Author information
- Commit messages
- File modifications
- Line-by-line code changes (patches)
- Tags
- Branch references
- Blobs and other Git objects

```bash
git show
```

Unlike `git log`, which displays multiple commits, `git show` focuses on a single Git object and provides detailed information about it.

## Basic Syntax

```bash
git show [options] [object]
```

## Common Examples

```bash
git show
git show HEAD
git show HEAD~1
git show a1b2c3d
git show v1.0
git show HEAD:file.txt
```

## Major Options

### Show Statistics

```bash
git show --stat
```

### Show Only File Names

```bash
git show --name-only
```

### Show File Statuses

```bash
git show --name-status
```

### Show Metadata Only

```bash
git show --no-patch
```

or

```bash
git show -s
```

### Custom Format

```bash
git show --format="%h %an %s"
```

### Word-Level Diff

```bash
git show --word-diff
```

## File Content Retrieval

```bash
git show HEAD:app.py
git show HEAD~3:app.py
git show main:app.py
git show v2.0:config.yml
```

## Real-World Scenarios

### Review Latest Commit

```bash
git show
```

### Inspect Production Hotfix

```bash
git show <commit-hash>
```

### Recover Older Version of File

```bash
git show HEAD~10:application.yml
```

### Audit Release Tag

```bash
git show v3.2
```

## Best Practices

1. Review every important commit with `git show`.
2. Use `--stat` for quick summaries.
3. Use `--no-patch` when only metadata is needed.
4. Retrieve old file contents using `commit:file` syntax.
5. Combine with `git log` for historical investigations.

## Quick Reference

```bash
git show                          # Latest commit
git show HEAD                     # Current commit
git show HEAD~1                   # Previous commit
git show COMMIT_HASH              # Specific commit
git show v1.0                     # Show tag
git show main                     # Show branch HEAD
git show --stat                   # Statistics
git show --name-only              # File names
git show --name-status            # File statuses
git show --no-patch               # Metadata only
git show HEAD:file.txt            # File contents
git show HEAD~3:file.txt          # Historical file
```

## Conclusion

`git show` is an essential Git inspection tool for reviewing commits, examining historical file contents, auditing releases, and understanding repository changes in detail.
