# AGENTS.md

This file provides guidance to AI agents working with this repository.

## Commands

<!-- List all development commands in a table format -->
<!-- Commands should be copy-paste ready -->

| Command | Purpose |
|---------|---------|
| `{{BUILD_COMMAND}}` | {{BUILD_DESCRIPTION}} |
| `{{TEST_COMMAND}}` | {{TEST_DESCRIPTION}} |
| `{{LINT_COMMAND}}` | {{LINT_DESCRIPTION}} |
| `{{FORMAT_COMMAND}}` | {{FORMAT_DESCRIPTION}} |

<!-- Add additional commands as needed -->

## Architecture Overview

<!-- Brief, high-level overview of project structure -->
<!-- For detailed architecture, create docs/architecture.md -->

{{ARCHITECTURE_OVERVIEW}}

### Directory Structure

```
{{PROJECT_DIRECTORY}}/
├── {{SOURCE_DIR}}/          # {{SOURCE_DESCRIPTION}}
├── {{TEST_DIR}}/            # {{TEST_DESCRIPTION}}
└── ...
```

<!-- Link to detailed docs if they exist -->
<!-- For detailed architecture, see [docs/architecture.md](docs/architecture.md). -->

## Key Files

<!-- List important files and their purposes -->

- `{{ENTRY_POINT}}` - {{ENTRY_DESCRIPTION}}
- `{{CONFIG_FILE}}` - {{CONFIG_DESCRIPTION}}

## Patterns

<!-- Document non-obvious patterns used in the codebase -->

### {{PATTERN_NAME}}

{{PATTERN_DESCRIPTION}}

## Gotchas

<!-- Document things that aren't obvious from the code -->
<!-- Include common mistakes and how to avoid them -->

- {{GOTCHA_1}}
- {{GOTCHA_2}}

## Tool Usage Patterns

### When Reading Files

<!-- Guidance on how to explore the codebase -->

- Start with `{{ENTRY_POINT}}` to understand the application entry point
- Check `{{TEST_DIR}}/` for usage examples of public APIs

### When Editing Files

<!-- Guidance on making changes -->

- Run `{{LINT_FIX_COMMAND}}` after editing to auto-fix formatting
- Verify tests pass with `{{TEST_COMMAND}}` before committing

## Multi-Step Workflows

### Adding a New Feature

1. {{FEATURE_STEP_1}}
2. {{FEATURE_STEP_2}}
3. {{FEATURE_STEP_3}}
4. Run tests to verify
5. Update documentation if user-facing

### Fixing a Bug

1. Write a failing test that reproduces the bug
2. Implement the fix
3. Verify the test passes
4. Check for similar issues elsewhere

## Style Reference

For detailed formatting rules, see [STYLE_GUIDE.md](STYLE_GUIDE.md).
