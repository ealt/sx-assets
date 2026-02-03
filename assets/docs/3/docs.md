---
name: docs
description: Generate or regenerate repository documentation
argument-hint: [--files=FILE1,FILE2] [--dry-run]
---

Generate well-structured repository documentation for this project.

**Arguments:**
- `--files=README,AGENTS,CLAUDE,...` - Generate only specific files (comma-separated, default: all)
- `--dry-run` - Show what would be generated without writing files

$ARGUMENTS

Use the docs-manager skill to:

1. **Analyze the project:**
   - Read package.json, pyproject.toml, Makefile, or other config files
   - Identify available commands (build, test, lint, format)
   - Detect the technology stack
   - Read any existing documentation files

2. **Ask for confirmation:**
   - Confirm the project description
   - Ask about patterns or gotchas to document
   - Confirm which files to generate

3. **Generate documentation:**
   - Each file has clear content ownership (no duplication)
   - Cross-references between files instead of repeating content
   - Commands are copy-paste ready
   - Preserve valuable content from existing docs

**Available files:**
- `README.md` - Project overview, quick start
- `AGENTS.md` - Commands, architecture overview, patterns, gotchas (single source of truth for AI)
- `CLAUDE.md` - Redirect to AGENTS.md
- `CONTRIBUTING.md` - Setup instructions, PR workflow
- `STYLE_GUIDE.md` - Formatting rules, naming conventions
- `LICENSE` - Full license text
- `CODE_OF_CONDUCT.md` - Community guidelines
- `SECURITY.md` - Security policy, vulnerability reporting
- `CHANGELOG.md` - Version history
- `docs/` - Full architecture, detailed documentation
- `walkthroughs/` - Interactive code walkthroughs (use **virgil** skill)
