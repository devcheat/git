# `git grep`

## Introduction

`git grep` is Git's built-in search tool for finding text patterns inside files tracked by Git. It is significantly faster than many general-purpose search tools when working inside repositories because it operates directly on Git-managed content.

Typical use cases:

- Finding function definitions
- Locating API usage
- Searching configuration values
- Auditing secrets
- Investigating bugs
- Refactoring code

```bash
git grep <pattern>
```

---

# Why Use Git Grep?

Compared to standard tools:

```text
grep        -> Searches files on disk
git grep    -> Optimized for Git repositories
```

Benefits:

- Fast search performance
- Repository-aware
- Supports revisions and branches
- Supports regular expressions
- Searches tracked files only by default

---

# Basic Syntax

```bash
git grep [options] <pattern>
```

Examples:

```bash
git grep "TODO"
git grep "getUser"
git grep "password"
```

---

# Basic Searches

## Search for Text

```bash
git grep "TODO"
```

Output:

```text
src/app.py:TODO: Refactor this method
```

---

## Search in Specific File

```bash
git grep "UserService" app.py
```

---

## Search in Multiple Files

```bash
git grep "database" *.yml
```

---

## Search in Directory

```bash
git grep "Exception" src/
```

---

# Major Options

## `git grep -n`

Show line numbers.

```bash
git grep -n "TODO"
```

Output:

```text
app.py:42:TODO: Remove hardcoded value
```

---

## `git grep --line-number`

Equivalent to:

```bash
git grep -n
```

---

## `git grep -i`

Case-insensitive search.

```bash
git grep -i "error"
```

Matches:

```text
ERROR
Error
error
```

---

## `git grep --ignore-case`

Long form of:

```bash
git grep -i
```

---

## `git grep -w`

Match whole words.

```bash
git grep -w "user"
```

Matches:

```text
user
```

Not:

```text
username
userId
```

---

## `git grep -v`

Invert match.

```bash
git grep -v "DEBUG"
```

Show lines not containing pattern.

---

## `git grep -l`

Show file names only.

```bash
git grep -l "TODO"
```

Output:

```text
app.py
service.py
```

---

## `git grep -L`

Show files without matches.

```bash
git grep -L "Copyright"
```

---

## `git grep -c`

Count matches per file.

```bash
git grep -c "Exception"
```

---

## `git grep -o`

Show only matched text.

```bash
git grep -o "ERROR"
```

---

## `git grep -h`

Suppress file names.

```bash
git grep -h "TODO"
```

---

## `git grep -H`

Always show file names.

```bash
git grep -H "TODO"
```

---

## `git grep --full-name`

Show paths relative to repository root.

```bash
git grep --full-name "Config"
```

---

## `git grep --break`

Insert blank line between file outputs.

```bash
git grep --break "TODO"
```

---

## `git grep --heading`

Group matches under filename heading.

```bash
git grep --heading "TODO"
```

---

# Regular Expression Searches

## Extended Regular Expressions

```bash
git grep -E "error|warning"
```

Matches either pattern.

---

## Basic Regular Expressions

```bash
git grep -G "error"
```

Default regex engine.

---

## Perl Compatible Regex

```bash
git grep -P "\bUser\d+\b"
```

Advanced pattern matching.

---

## Fixed String Search

```bash
git grep -F "user.name"
```

Treats pattern literally.

---

# Multiple Patterns

## Using Multiple Expressions

```bash
git grep -e "error" -e "warning"
```

---

## Boolean AND Search

```bash
git grep -e "login" --and -e "failed"
```

---

## Boolean OR Search

```bash
git grep -e "error" --or -e "warning"
```

---

## Boolean NOT Search

```bash
git grep -e "error" --not -e "ignored"
```

---

# Searching Commit History

## Search in Specific Revision

```bash
git grep "API_KEY" HEAD~5
```

---

## Search in Branch

```bash
git grep "UserService" main
```

---

## Search in Tag

```bash
git grep "deprecated" v1.0
```

---

## Search Across Multiple Revisions

```bash
git grep "password" main feature
```

---

# Function Context Searches

## Show Function Names

```bash
git grep -p "TODO"
```

Displays surrounding function context.

---

## Function Matching

```bash
git grep -W "getUser"
```

Shows entire function body.

---

# Real-World Scenarios

## Scenario 1: Find Hardcoded Passwords

```bash
git grep -i "password"
```

Security audits.

---

## Scenario 2: Find TODO Items

```bash
git grep -n "TODO"
```

Track technical debt.

---

## Scenario 3: Locate API Usage

```bash
git grep "CustomerService"
```

Useful before refactoring.

---

## Scenario 4: Identify Deprecated Methods

```bash
git grep -n "deprecated"
```

Migration planning.

---

## Scenario 5: Search Release Branch

```bash
git grep "FeatureFlag" release/v2
```

Audit old behavior.

---

## Scenario 6: Compliance Review

```bash
git grep -E "token|secret|password"
```

Find sensitive information.

---

# Common Mistakes

## Forgetting Quotes

Incorrect:

```bash
git grep TODO item
```

Correct:

```bash
git grep "TODO item"
```

---

## Using Grep Instead of Git Grep

```bash
grep -r "TODO" .
```

May search build artifacts and generated files.

`git grep` generally focuses on repository content.

---

## Searching Wrong Revision

Always verify branch:

```bash
git branch
```

---

# Comparison with Related Commands

## `git grep` vs `grep`

`grep`

- General-purpose search
- Searches any file

`git grep`

- Repository-aware
- Faster in large repositories

---

## `git grep` vs `git log -S`

`git grep`

- Finds current occurrences

`git log -S`

- Finds commits that introduced or removed text

---

## `git grep` vs IDE Search

IDE Search:

- Visual interface

Git Grep:

- Scriptable
- Fast
- Works remotely and in terminals

---

# Best Practices

1. Use `-n` to display line numbers.
2. Use `-i` when casing is uncertain.
3. Use regex patterns for audits.
4. Use `-l` during large refactoring efforts.
5. Search release branches before production fixes.
6. Automate compliance scans using `git grep`.
7. Use fixed-string search (`-F`) when special characters exist.
8. Combine with shell scripting for reporting.

---

# Useful Workflow

```bash
# Find TODO comments
git grep -n "TODO"

# Find API usage
git grep -n "CustomerService"

# Review secrets
git grep -iE "password|token|secret"

# List impacted files
git grep -l "CustomerService"
```

---

# Quick Reference

```bash
git grep "TODO"                       # Basic search
git grep -n "TODO"                    # Line numbers
git grep -i "error"                   # Ignore case
git grep -w "user"                    # Whole word
git grep -l "TODO"                    # Files only
git grep -L "TODO"                    # Files without match
git grep -c "ERROR"                   # Count matches
git grep -E "error|warning"           # Extended regex
git grep -F "user.name"               # Fixed string
git grep -P "\\d+"                  # Perl regex
git grep main "Service"               # Search branch
git grep HEAD~5 "password"            # Search revision
```

---

# Conclusion

`git grep` is one of the fastest and most effective tools for searching code within a Git repository. Whether you are debugging, auditing, refactoring, tracking technical debt, or performing security reviews, mastering `git grep` can dramatically improve developer productivity and repository analysis workflows.
