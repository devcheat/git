# `git config`

## Introduction

`git config` is the command used to view, create, modify, and manage Git configuration settings. These settings control Git behavior, user identity, aliases, editors, merge tools, credential handling, default branches, and many other aspects of Git.

```bash
git config
```

Every Git user should understand `git config` because it affects how Git behaves across repositories and systems.

```text
System Configuration
        |
Global Configuration
        |
Local Repository Configuration
```

---

# Syntax

```bash
git config [options]
git config <name>
git config <name> <value>
```

Examples:

```bash
git config user.name
git config user.email
git config user.name "Vinod"
git config --global user.email "user@example.com"
```

---

# Understanding Configuration Levels

## System Configuration

Applies to all users on the machine.

```bash
git config --system user.name
```

---

## Global Configuration

Applies to the current user.

```bash
git config --global user.name "Vinod"
```

Stored in:

```text
~/.gitconfig
```

---

## Local Configuration

Applies only to the current repository.

```bash
git config --local user.email "project@example.com"
```

Stored in:

```text
.git/config
```

---

# Common Usage Scenarios

## Configure Username

```bash
git config --global user.name "John Doe"
```

---

## Configure Email Address

```bash
git config --global user.email "john@example.com"
```

---

## View Current Configuration

```bash
git config --list
```

---

## Configure Default Editor

```bash
git config --global core.editor "code --wait"
```

---

## Create Git Alias

```bash
git config --global alias.st status
```

Usage:

```bash
git st
```

---

# All Major Options

## `git config --list`

Display all configuration values.

```bash
git config --list
```

---

## `git config -l`

Short form of list.

```bash
git config -l
```

---

## `git config --get`

Get a specific value.

```bash
git config --get user.name
```

---

## `git config --get-all`

Display all matching entries.

```bash
git config --get-all remote.origin.fetch
```

---

## `git config --global`

Update user-level configuration.

```bash
git config --global user.name "John"
```

---

## `git config --local`

Update repository configuration.

```bash
git config --local core.editor vim
```

---

## `git config --system`

Update system configuration.

```bash
git config --system advice.statusHints false
```

---

## `git config --unset`

Remove configuration value.

```bash
git config --unset user.name
```

---

## `git config --unset-all`

Remove all matching values.

```bash
git config --unset-all alias.st
```

---

## `git config --replace-all`

Replace matching entries.

```bash
git config --replace-all user.name "New Name"
```

---

## `git config --add`

Add an additional value.

```bash
git config --add remote.origin.fetch pattern
```

---

## `git config --edit`

Edit configuration file directly.

```bash
git config --global --edit
```

---

## `git config --show-origin`

Display value source.

```bash
git config --show-origin --list
```

---

## `git config --show-scope`

Show configuration scope.

```bash
git config --show-scope --list
```

---

## `git config --file`

Use a specific configuration file.

```bash
git config --file custom.conf user.name
```

---

## `git config --remove-section`

Delete section.

```bash
git config --remove-section alias
```

---

## `git config --rename-section`

Rename configuration section.

```bash
git config --rename-section alias shortcuts
```

---

# Frequently Configured Settings

## User Identity

```bash
git config --global user.name "John Doe"
git config --global user.email "john@example.com"
```

---

## Default Branch Name

```bash
git config --global init.defaultBranch main
```

---

## Default Editor

```bash
git config --global core.editor "code --wait"
```

---

## Enable Color Output

```bash
git config --global color.ui auto
```

---

## Configure Credential Storage

```bash
git config --global credential.helper manager
```

---

## Create Useful Aliases

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
```

---

# Real-World Scenarios

## Scenario 1: First Git Setup

```bash
git config --global user.name "John Doe"
git config --global user.email "john@example.com"
```

---

## Scenario 2: Company-Specific Repository Identity

```bash
git config --local user.email "work@company.com"
```

---

## Scenario 3: Visual Studio Code Integration

```bash
git config --global core.editor "code --wait"
```

---

## Scenario 4: Productivity Aliases

```bash
git config --global alias.lg "log --oneline --graph"
```

---

## Scenario 5: Determine Configuration Source

```bash
git config --show-origin --list
```

---

## Scenario 6: Troubleshoot Configuration Conflicts

```bash
git config --show-scope --list
```

---

# Difference Between Common Variants

## Global vs Local Configuration

Global

- User-wide
- Applies to all repositories

Local

- Repository-specific
- Overrides global values

---

## `--get` vs `--get-all`

`--get`

- Single value

`--get-all`

- Multiple matching values

---

## `--unset` vs `--unset-all`

`--unset`

- Remove one value

`--unset-all`

- Remove every matching value

---

# Common Errors and Troubleshooting

## Missing User Identity

```text
Please tell me who you are
```

Solution:

```bash
git config --global user.name "Name"
git config --global user.email "mail@example.com"
```

---

## Incorrect Email Address

Verify:

```bash
git config user.email
```

---

## Conflicting Settings

Review configuration origins.

```bash
git config --show-origin --list
```

---

## Alias Not Working

Verify alias configuration.

```bash
git config --get alias.st
```

---

# Best Practices

1. Configure username and email immediately after installation.
2. Use global settings for personal preferences.
3. Use local settings for project-specific identities.
4. Create aliases for frequently used commands.
5. Review configuration origins during troubleshooting.
6. Keep credential settings secure.
7. Standardize configurations across development teams.

---

# Useful Workflow

```bash
# Verify identity
git config --global user.name
git config --global user.email

# Configure editor
git config --global core.editor "code --wait"

# Create aliases
git config --global alias.st status

# Verify configuration
git config --list
```

---

# Quick Reference

```bash
git config --list                       # Show all settings
git config --get user.name             # Get value
git config --global user.name NAME     # Set username
git config --global user.email EMAIL   # Set email
git config --unset user.name           # Remove value
git config --global --edit             # Edit config
git config --show-origin --list        # Show sources
git config --show-scope --list         # Show scopes
git config --global alias.st status    # Create alias
git config --global core.editor vim    # Configure editor
```

---

# Conclusion

`git config` is the central command for customizing Git behavior. By understanding configuration scopes, user identity settings, aliases, credential management, editors, and troubleshooting techniques, developers can create a consistent and efficient Git environment tailored to their workflow.
