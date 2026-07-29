# `git tag`

## Introduction

`git tag` is used to create permanent references to specific commits. Tags are commonly used for software releases, production deployments, milestones, rollback points, and version management.

```bash
git tag <tagname>
```

Think of tags as bookmarks that point to important commits.

```text
Commit History
      |
      | tag v1.0
      v
A --- B --- C --- D
            ^
            v1.0
```

---

# Syntax

```bash
git tag [options] <tagname>
git tag [options] <tagname> <commit>
git tag [options] -d <tagname>
git tag [options] -l
```

---

# Types of Git Tags

## Lightweight Tag

```bash
git tag v1.0
```

Stores only a reference to a commit.

### Best For

- Temporary markers
- Local development
- Quick checkpoints

---

## Annotated Tag

```bash
git tag -a v1.0 -m "Version 1.0 Release"
```

Stores:

- Tag name
- Creator
- Date
- Message
- Commit reference

Recommended for releases.

---

## Signed Tag

```bash
git tag -s v1.0 -m "Signed Release"
```

Uses GPG signatures to verify authenticity.

---

# Common Usage Scenarios

## Create Release Tag

```bash
git tag -a v1.0.0 -m "Production Release"
```

---

## Tag Current Commit

```bash
git tag v2.0
```

---

## Tag Older Commit

```bash
git tag -a v1.5 abcd123
```

---

## List Existing Tags

```bash
git tag
```

---

## Show Tag Details

```bash
git show v1.0
```

---

# All Major Options

## `git tag -a`

Equivalent:

```bash
git tag --annotate
```

Creates annotated tags.

Example:

```bash
git tag -a v1.0 -m "Release"
```

---

## `git tag --annotate`

```bash
git tag --annotate v1.0
```

---

## `git tag -m`

Equivalent:

```bash
git tag --message
```

Adds tag message.

```bash
git tag -a v1.0 -m "First release"
```

---

## `git tag --message`

```bash
git tag -a v1.0 --message "Release"
```

---

## `git tag -F`

Equivalent:

```bash
git tag --file
```

Read message from file.

```bash
git tag -a v1.0 -F release-notes.txt
```

---

## `git tag --file`

```bash
git tag --file notes.txt -a v1.0
```

---

## `git tag -s`

Equivalent:

```bash
git tag --sign
```

Create signed tag.

---

## `git tag --sign`

```bash
git tag --sign v1.0
```

---

## `git tag -u`

Specify signing key.

```bash
git tag -s -u ABC123 v1.0
```

---

## `git tag --local-user`

```bash
git tag --local-user ABC123 -s v1.0
```

---

## `git tag -f`

Equivalent:

```bash
git tag --force
```

Replace existing tag.

```bash
git tag -f v1.0
```

---

## `git tag --force`

Use carefully because existing references change.

---

## `git tag -d`

Equivalent:

```bash
git tag --delete
```

Delete local tag.

```bash
git tag -d v1.0
```

---

## `git tag --delete`

```bash
git tag --delete v1.0
```

---

## `git tag -l`

Equivalent:

```bash
git tag --list
```

List tags.

```bash
git tag -l
```

---

## `git tag --list`

```bash
git tag --list "v2.*"
```

---

## `git tag -n`

Show annotation lines.

```bash
git tag -n
```

---

## `git tag --contains`

Display tags containing a commit.

```bash
git tag --contains abcd123
```

---

## `git tag --no-contains`

Show tags that do not contain commit.

```bash
git tag --no-contains abcd123
```

---

## `git tag --points-at`

```bash
git tag --points-at HEAD
```

---

## `git tag --merged`

```bash
git tag --merged main
```

---

## `git tag --no-merged`

```bash
git tag --no-merged main
```

---

## `git tag --sort`

```bash
git tag --sort=-version:refname
```

---

## `git tag -i`

Ignore case when filtering.

```bash
git tag -l -i "release*"
```

---

## `git tag --create-reflog`

Create reflog entry.

```bash
git tag --create-reflog v1.0
```

---

## `git tag --cleanup`

Control message cleanup.

```bash
git tag --cleanup=strip -a v1.0
```

---

## `git tag -v`

Equivalent:

```bash
git tag --verify
```

Verify signature.

```bash
git tag -v v1.0
```

---

# Remote Tag Operations

## Push Single Tag

```bash
git push origin v1.0
```

## Push All Tags

```bash
git push --tags
```

## Delete Remote Tag

```bash
git push origin --delete v1.0
```

## Fetch Tags

```bash
git fetch --tags
```

---

# Real-World Scenarios

## Scenario 1: First Production Release

```bash
git tag -a v1.0.0 -m "Production Release"
git push origin v1.0.0
```

## Scenario 2: Emergency Hotfix

```bash
git tag -a v1.0.1 -m "Hotfix"
```

## Scenario 3: Mark Deployment

```bash
git tag production-2026-07
```

## Scenario 4: Rollback Point

```bash
git tag pre-upgrade-backup
```

## Scenario 5: Signed Enterprise Release

```bash
git tag -s v3.0 -m "Signed Release"
```

---

# Difference Between Common Variants

## Lightweight vs Annotated Tags

Lightweight Tags

- Simple reference
- No metadata
- Quick creation

Annotated Tags

- Metadata stored
- Recommended for releases
- Auditable

---

## Annotated vs Signed Tags

Annotated Tags

- Author information
- Release notes

Signed Tags

- Cryptographic verification
- Enterprise distribution

---

# Best Practices

1. Use annotated tags for releases.
2. Follow semantic versioning.
3. Sign production releases.
4. Push tags after creation.
5. Verify important tags.
6. Keep release notes meaningful.
7. Avoid force-updating published tags.

---

# Useful Workflow

```bash
# Create release tag
git tag -a v2.0.0 -m "Release 2.0"

# Verify
git show v2.0.0

# Push tag
git push origin v2.0.0
```

---

# Quick Reference

```bash
git tag                         # List tags
git tag v1.0                    # Lightweight tag
git tag -a v1.0 -m "Release"   # Annotated tag
git tag -s v1.0                 # Signed tag
git tag -d v1.0                 # Delete local tag
git push --tags                 # Push all tags
git fetch --tags                # Fetch tags
git tag --contains HEAD         # Containing tags
git tag --points-at HEAD        # Tags at commit
git tag -v v1.0                 # Verify signature
```

---

# Conclusion

`git tag` is the foundation of Git-based release management. By mastering lightweight, annotated, signed, and remote tag workflows, teams can manage releases, deployments, version history, auditing, rollback strategies, and CI/CD automation with confidence.
