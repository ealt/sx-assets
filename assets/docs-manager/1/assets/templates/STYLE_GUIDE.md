# Style Guide

This document defines the code formatting and style conventions for {{PROJECT_NAME}}.

## Code Formatting

### General

- Indentation: {{INDENT_SIZE}} spaces
- Maximum line length: {{LINE_LENGTH}} characters
- Use trailing commas in multiline structures
- End files with a single newline

### {{LANGUAGE}}

<!-- Language-specific formatting rules -->

{{LANGUAGE_FORMATTING_RULES}}

## Naming Conventions

### Files

<!-- File naming conventions -->

| Type | Convention | Example |
|------|------------|---------|
| {{FILE_TYPE_1}} | {{CONVENTION_1}} | `{{EXAMPLE_1}}` |
| {{FILE_TYPE_2}} | {{CONVENTION_2}} | `{{EXAMPLE_2}}` |

### Variables and Functions

<!-- Variable and function naming rules -->

- Variables: {{VARIABLE_CONVENTION}}
- Functions: {{FUNCTION_CONVENTION}}
- Constants: {{CONSTANT_CONVENTION}}
- Boolean variables: prefix with `is`, `has`, `should`, `can`

### {{TYPE_SPECIFIC}} (if applicable)

<!-- Type-specific naming conventions (classes, interfaces, etc.) -->

{{TYPE_NAMING_RULES}}

## Documentation

### Comments

- Use comments to explain "why", not "what"
- Keep comments close to the code they describe
- Update comments when code changes

### {{DOC_STYLE}} (if applicable)

<!-- Documentation style (JSDoc, docstrings, etc.) -->

{{DOC_STYLE_RULES}}

## Patterns

### Preferred Patterns

<!-- Document preferred patterns -->

**{{PATTERN_NAME}}**
```{{LANGUAGE}}
{{GOOD_EXAMPLE}}
```

### Patterns to Avoid

<!-- Document anti-patterns -->

**{{ANTI_PATTERN_NAME}}**
```{{LANGUAGE}}
// Avoid this:
{{BAD_EXAMPLE}}

// Prefer this:
{{GOOD_ALTERNATIVE}}
```

## Linting Configuration

Configuration files:
- `{{LINTER_CONFIG}}` - {{LINTER_NAME}} rules
- `{{FORMATTER_CONFIG}}` - {{FORMATTER_NAME}} settings

<!-- Add additional config files -->

### Key Rules

<!-- Explain non-obvious or important lint rules -->

- **{{RULE_NAME}}**: {{RULE_EXPLANATION}}

## Editor Setup

<!-- Optional: editor-specific configuration -->

For consistent formatting, configure your editor:

**VS Code:**
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "{{FORMATTER_EXTENSION}}"
}
```

## Running Linters

For commands to run linting and formatting, see [AGENTS.md](AGENTS.md#commands).
