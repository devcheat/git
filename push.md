`git push`
===

## Introduction

`git push` uploads local commits, tags, and references from your local repository to a remote repository. It is the primary command used to share work with team members and synchronize local development with remote servers.

```bash
git push
```

Think of `git push` as the command that publishes your local history.

```text
Local Repository
       |
       | git push
       v
Remote Repository
```

---

# Syntax

```bash
git push [options]
git push <remote>
git push <remote> <branch>
```

Examples:

```bash
git push
git push origin main
git push --tags
git push -u origin feature-login
```

---

# How Git Push Works

When you run:

```bash
git push origin main
```

Git:

1. Checks remote state.
2. Transfers missing commits.
3. Updates the remote branch.

```text
Local main
    |
    | git push origin main
    v
origin/main
```

---

# Common Usage Scenarios

## Push Current Branch

```bash
git push
```

Pushes the current branch to its configured upstream.

---

## Push a Specific Branch

```bash
git push origin main
```

Uploads local commits to `origin/main`.

---

## Push New Feature Branch

```bash
git push -u origin feature-login
```

Creates the remote branch and configures tracking.

---

## Push All Tags

```bash
git push --tags
```

Uploads all local tags.

---

## Delete Remote Branch

```bash
git push origin --delete feature-old
```

Removes the branch from the remote repository.

---

# All Major Options

## `git push`

Default push command.

```bash
git push
```

---

## `git push origin main`

Push specific branch.

```bash
git push origin main
```

---

## `git push -u`

Equivalent:

```bash
git push --set-upstream
```

Example:

```bash
git push -u origin feature-auth
```

Future pushes can use simply:

```bash
git push
```

---

## `git push --set-upstream`

Creates upstream tracking relationship.

```bash
git push --set-upstream origin feature-auth
```

---

## `git push --all`

Push all branches.

```bash
git push --all origin
```

---

## `git push --tags`

Push all tags.

```bash
git push --tags
```

---

## `git push --follow-tags`

Push annotated tags related to pushed commits.

```bash
git push --follow-tags
```

---

## `git push --delete`

Delete remote branch.

```bash
git push origin --delete feature-old
```

---

## `git push -f`

Equivalent:

```bash
git push --force
```

Force updates remote history.

```bash
git push -f origin main
```

Use carefully.

---

## `git push --force`

Overwrites remote history.

Useful after rebasing.

---

## `git push --force-with-lease`

Safer alternative to force push.

```bash
git push --force-with-lease
```

Prevents overwriting others' work accidentally.

---

## `git push --dry-run`

Preview push.

```bash
git push --dry-run
```

---

## `git push --atomic`

All references update together.

```bash
git push --atomic origin main release
```

---

## `git push --mirror`

Mirror all references.

```bash
git push --mirror backup
```

Useful for repository backups.

---

## `git push --prune`

Remove remote branches missing locally.

```bash
git push --prune origin
```

---

## `git push --porcelain`

Machine-readable output.

```bash
git push --porcelain
```

Useful for automation.

---

## `git push --quiet`

Reduce output.

```bash
git push --quiet
```

---

## `git push --verbose`

Detailed output.

```bash
git push --verbose
```

---

## `git push --recurse-submodules`

Push relevant submodule commits.

```bash
git push --recurse-submodules=on-demand
```

---

# Pushing Tags

## Push Single Tag

```bash
git push origin v1.0
```

---

## Push All Tags

```bash
git push --tags
```

---

## Push Annotated Release Tags

```bash
git push --follow-tags
```

---

# Real-World Scenarios

## Scenario 1: Publish New Feature

```bash
git checkout -b feature-payment
git push -u origin feature-payment
```

---

## Scenario 2: Push Release Branch

```bash
git push origin release-2.0
```

---

## Scenario 3: Publish Release Tags

```bash
git tag -a v2.0 -m "Release"
git push --tags
```

---

## Scenario 4: Safe Rebase Update

```bash
git rebase main
git push --force-with-lease
```

---

## Scenario 5: Remove Obsolete Branch

```bash
git push origin --delete feature-legacy
```

---

## Scenario 6: Repository Backup

```bash
git push --mirror backup
```

---

# Difference Between Common Variants

## `git push` vs `git pull`

`git push`

- Uploads commits
- Local → Remote

`git pull`

- Downloads commits
- Remote → Local

---

## `--force` vs `--force-with-lease`

`--force`

- Overwrites remote state
- Higher risk

`--force-with-lease`

- Verifies remote state first
- Safer collaboration

---

## `--tags` vs `--follow-tags`

`--tags`

- Push all tags

`--follow-tags`

- Push relevant annotated tags only

---

# Common Errors and Troubleshooting

## Non Fast Forward Rejected

```text
! [rejected] main -> main (non-fast-forward)
```

Solution:

```bash
git pull --rebase
git push
```

---

## Upstream Branch Missing

```text
fatal: no upstream branch
```

Solution:

```bash
git push -u origin branch-name
```

---

## Authentication Failed

Verify credentials, token, or SSH configuration.

---

## Force Push Risks

Prefer:

```bash
git push --force-with-lease
```

instead of:

```bash
git push --force
```

---

# Best Practices

1. Pull before pushing shared branches.
2. Prefer `--force-with-lease` over `--force`.
3. Use meaningful branch names.
4. Push frequently.
5. Push release tags immediately after creation.
6. Review commits before publishing.
7. Protect important branches.

---

# Useful Workflow

```bash
# Review changes
git status

# Commit changes
git commit -m "Implement feature"

# Publish branch
git push -u origin feature-auth

# Continue pushing normally
git push
```

---

# Quick Reference

```bash
git push                              # Default push
git push origin main                  # Push branch
git push -u origin feature            # Set upstream
git push --tags                       # Push tags
git push --follow-tags                # Push annotated tags
git push --force-with-lease           # Safe force push
git push --force                      # Force push
git push origin --delete branch       # Delete branch
git push --all origin                 # Push all branches
git push --dry-run                    # Preview push
```

---

# Conclusion

`git push` is the command that publishes local work to shared repositories. By understanding upstream tracking, branch publishing, tag distribution, safe force pushes, remote branch management, and collaboration workflows, developers can confidently share code while maintaining repository integrity.
