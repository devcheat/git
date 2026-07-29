# `git remote`

## Introduction

`git remote` is the Git command used to manage connections between a local repository and remote repositories. It allows you to add, remove, rename, inspect, and configure remote repositories.

```bash
git remote
```

A remote repository is typically hosted on GitHub, GitLab, Azure DevOps, Bitbucket, or an internal Git server.

```text
Local Repository
      |
      +---- origin
      |
      +---- upstream
      |
      +---- backup
```

---

# Syntax

```bash
git remote [options]
git remote add <name> <url>
git remote remove <name>
git remote rename <old> <new>
git remote show <name>
```

Examples:

```bash
git remote
git remote -v
git remote add origin https://github.com/user/repo.git
git remote remove origin
```

---

# Understanding Remotes

## What is a Remote?

A remote is a named reference to another Git repository.

Common names:

- origin
- upstream
- backup
- production

---

## Understanding origin

```bash
git remote add origin https://github.com/company/project.git
```

`origin` is simply a convention and can be renamed.

---

## Understanding upstream

```text
Forked Repository  -> origin
Original Repository -> upstream
```

Widely used in open-source development.

---

# Common Usage Scenarios

## View Configured Remotes

```bash
git remote
```

Lists remote names only.

---

## View Remote URLs

```bash
git remote -v
```

Displays fetch and push URLs.

---

## Add a Remote

```bash
git remote add origin https://github.com/user/app.git
```

---

## Rename Remote

```bash
git remote rename origin github
```

---

## Remove Remote

```bash
git remote remove backup
```

---

# All Major Options and Commands

## `git remote`

Show remote names.

```bash
git remote
```

---

## `git remote -v`

Equivalent to:

```bash
git remote --verbose
```

Displays remote URLs.

```text
origin  https://github.com/app.git (fetch)
origin  https://github.com/app.git (push)
```

---

## `git remote --verbose`

Verbose listing mode.

```bash
git remote --verbose
```

---

## `git remote add`

Add a new remote.

```bash
git remote add origin https://github.com/user/repo.git
```

---

## `git remote remove`

Equivalent:

```bash
git remote rm
```

Remove a remote.

```bash
git remote remove origin
```

---

## `git remote rm`

Short form of remove.

```bash
git remote rm origin
```

---

## `git remote rename`

Rename remote.

```bash
git remote rename origin github
```

---

## `git remote show`

Display detailed information.

```bash
git remote show origin
```

Displays:

- Fetch URL
- Push URL
- Tracking branches
- HEAD branch

---

## `git remote get-url`

Show specific URL.

```bash
git remote get-url origin
```

---

## `git remote set-url`

Update remote URL.

```bash
git remote set-url origin git@github.com:user/app.git
```

Useful when migrating from HTTPS to SSH.

---

## `git remote set-head`

Manage remote HEAD branch.

```bash
git remote set-head origin main
```

---

## `git remote prune`

Remove stale remote tracking references.

```bash
git remote prune origin
```

---

## `git remote update`

Update multiple remotes.

```bash
git remote update
```

Equivalent to fetching configured remotes.

---

# Remote URL Management

## HTTPS URL

```bash
https://github.com/user/project.git
```

Easy to configure.

---

## SSH URL

```bash
git@github.com:user/project.git
```

Preferred for frequent development.

---

## Switching HTTPS to SSH

```bash
git remote set-url origin git@github.com:user/project.git
```

---

# Real-World Scenarios

## Scenario 1: Clone and Verify Remotes

```bash
git remote -v
```

Verify repository configuration.

---

## Scenario 2: Add GitHub Remote

```bash
git remote add origin https://github.com/company/app.git
```

---

## Scenario 3: Open Source Fork Workflow

```bash
git remote add upstream https://github.com/original/project.git
```

Maintain synchronization with upstream.

---

## Scenario 4: Repository Migration

```bash
git remote set-url origin https://new-server/project.git
```

---

## Scenario 5: Remove Deprecated Remote

```bash
git remote remove oldserver
```

---

## Scenario 6: Cleanup Deleted Branches

```bash
git remote prune origin
```

---

## Scenario 7: Multi-Remote Development

```text
origin
upstream
backup
```

Useful in enterprise environments.

---

# Difference Between Common Variants

## `git remote` vs `git remote -v`

`git remote`

- Names only

`git remote -v`

- Names and URLs

---

## `git remote remove` vs `git remote prune`

`remove`

- Deletes remote configuration

`prune`

- Removes stale tracking branches

---

## HTTPS vs SSH URLs

HTTPS

- Easier setup
- Username/token based

SSH

- Key based authentication
- Common for developers

---

# Common Errors and Troubleshooting

## Remote Already Exists

```text
remote origin already exists
```

Solution:

```bash
git remote set-url origin NEW_URL
```

---

## Remote Not Found

```text
fatal: No such remote
```

Verify remote name.

---

## Authentication Problems

Verify:

- Access permissions
- SSH keys
- Credentials

---

## Invalid Remote URL

Check URL format.

```bash
git remote -v
```

---

# Best Practices

1. Use meaningful remote names.
2. Prefer SSH for active development.
3. Verify remotes after cloning.
4. Remove unused remotes.
5. Use upstream when contributing to forks.
6. Run prune periodically.
7. Keep URLs up to date.

---

# Useful Workflow

```bash
# View remotes
git remote -v

# Add upstream repository
git remote add upstream https://github.com/org/project.git

# Update remote references
git remote update

# Remove stale branches
git remote prune upstream
```

---

# Quick Reference

```bash
git remote                              # List remotes
git remote -v                           # List remotes with URLs
git remote add origin URL               # Add remote
git remote remove origin                # Remove remote
git remote rename old new               # Rename remote
git remote show origin                  # Detailed information
git remote get-url origin               # Show URL
git remote set-url origin URL           # Change URL
git remote prune origin                 # Remove stale refs
git remote update                       # Update remotes
```

---

# Conclusion

`git remote` is the foundation of repository connectivity in Git. By mastering remote creation, URL management, upstream configuration, pruning, synchronization, and multi-remote workflows, developers can efficiently collaborate across local and remote repositories while maintaining a clean and manageable Git environment.
