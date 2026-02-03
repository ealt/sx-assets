# Virgil Markdown Format Reference

Quick reference for the Virgil walkthrough format.

## Frontmatter

Required YAML frontmatter at the start of the file:

```yaml
---
remote: https://github.com/org/repo    # Git remote URL
commit: <full-sha>                      # Commit SHA to pin the walkthrough
---
```

### Diff Mode Frontmatter

For walkthroughs that compare changes, add one of:

```yaml
---
remote: https://github.com/org/repo
commit: <head-commit-sha>
baseBranch: main                        # Compare against branch
---
```

Or:

```yaml
---
remote: https://github.com/org/repo
commit: <head-commit-sha>
baseCommit: <base-commit-sha>           # Compare against specific commit
---
```

## Step Syntax

### Hierarchy

Steps are defined by markdown headers:

```markdown
## Main Step          <!-- Primary step -->
### Sub-step          <!-- Detail within main step -->
#### Deep detail      <!-- Further nesting -->
```

### Step Content

Each step contains:
1. **Header** - The step title
2. **Prose** - Explanation (markdown supported)
3. **Code location** - Link to the relevant code

```markdown
## Understanding the Parser

The parser converts raw input into an AST using a recursive descent approach.
This is the entry point that kicks off the parsing process.

[View code (45-78)](/src/parser/index.ts)
```

## Code Location Links

### Basic Format

```markdown
[View code (startLine-endLine)](/path/from/repo/root.ext)
```

- Lines are **1-based** and **inclusive**
- Path **must start with `/`**
- Path is relative to repository root

### Examples

Single range:
```markdown
[View code (10-25)](/src/utils/helper.ts)
```

Multiple ranges (comma-separated):
```markdown
[View code (10-25,45-60)](/src/utils/helper.ts)
```

### Diff Mode Links

In diff mode, include both current and base locations:

```markdown
[View code (10-25)](/src/file.ts) [Base (8-20)](/src/file.ts)
```

For code that only exists in base (deleted):
```markdown
[Base (100-150)](/src/removed-file.ts)
```

For new code (no base):
```markdown
[View code (1-50)](/src/new-file.ts)
```

## Best Practices

### Line Ranges

- Keep ranges focused: **10-50 lines** is typical
- Include enough context for understanding
- Don't include unrelated code

### Commit Pinning

Always include the commit SHA so the walkthrough remains accurate even as code changes.

### File Paths

- Always use leading `/`
- Use the path from repository root
- Match the actual file path exactly (case-sensitive)

### Narrative Flow

1. Start with context/overview
2. Progress from entry point through implementation
3. End with summary or next steps
4. Each step should build on previous understanding

## PR/Diff Coverage Requirements

Diff walkthroughs **must cover 100% of changed files**. Every file in the git diff must appear in the walkthrough with the appropriate link type.

### Coverage Rules by File Status

| Git Status | Required Links |
|------------|----------------|
| **A (Added)** | At least one `[View code ...]` link |
| **D (Deleted)** | At least one `[Base ...]` link |
| **M (Modified)** | Both `[View code ...]` AND `[Base ...]` links |
| **R (Renamed)** | `[Base ...]` for old path, `[View code ...]` for new path |

### Excluding Files

Some files don't need walkthrough coverage (lock files, generated code, etc.). Use a `.walkthrough-ignore` file or pass `--exclude` patterns to the verification script.

### Verification

After generating a diff walkthrough, validate coverage:

```bash
./scripts/verify-walkthrough-coverage.sh walkthrough.md
```

The script will:
1. Parse the frontmatter to determine the git range
2. Compare changed files against referenced files
3. Report any uncovered files

Exit codes:
- `0` - 100% coverage achieved
- `1` - Missing coverage (uncovered files listed)
- `2` - Usage or parse error

## Complete Example

```markdown
---
remote: https://github.com/example/project
commit: a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0
---

# How Authentication Works

## Overview

This walkthrough explains the authentication flow from login to session management.

## Login Handler

The login process starts when a user submits credentials.

[View code (25-45)](/src/auth/login.ts)

## Token Generation

### Creating the JWT

After validating credentials, we generate a signed token.

[View code (10-35)](/src/auth/tokens.ts)

### Token Claims

The token includes these standard claims plus custom user data.

[View code (37-52)](/src/auth/tokens.ts)

## Session Storage

Sessions are stored in Redis for fast lookup and automatic expiration.

[View code (15-40)](/src/auth/session.ts)

## Summary

The auth flow: credentials -> validation -> JWT -> session storage -> cookie.
```
