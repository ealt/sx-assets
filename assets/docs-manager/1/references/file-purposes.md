# Documentation File Purposes

This reference provides detailed guidance on each documentation file's canonical purpose, structure, and boundaries.

## README.md

### Purpose

The README is the front door of your project. It serves humans who are discovering the project for the first time and need to quickly understand what it does and how to get started.

### Audience

- New users discovering the project
- Potential contributors evaluating the project
- Users looking for quick reference

### Canonical Structure

```markdown
# Project Name

<!-- Optional: badges -->

One-paragraph description of what the project does and why it exists.

## Quick Start

1. Clone: `git clone <url>`
2. Install: `<install command>`
3. Run: `<run command>`

## Documentation

- [Contributing](CONTRIBUTING.md) - Development setup and workflow
- [Style Guide](STYLE_GUIDE.md) - Code formatting rules

## License

[MIT License](LICENSE)
```

### Content Boundaries

**INCLUDE:**
- Project name (as H1 heading)
- Badges (CI status, version, license)
- One-paragraph description
- Quick start (3-5 steps maximum)
- Links to other documentation
- Link to LICENSE
- Links to external resources (docs site, Discord, etc.)

**EXCLUDE (link instead):**
- Detailed setup instructions → CONTRIBUTING.md
- Full architecture documentation → docs/
- Style/formatting rules → STYLE_GUIDE.md
- Command reference tables → AGENTS.md
- Long-form tutorials
- Full license text → LICENSE

### Guidelines

- Keep the quick start genuinely quick
- Use numbered steps, not paragraphs
- Prefer `inline code` for commands
- Don't explain every option, just the happy path

---

## CONTRIBUTING.md

### Purpose

The contributing guide helps developers set up their environment and understand the workflow for making contributions. It's the detailed counterpart to README's quick start.

### Audience

- Developers setting up local development
- First-time contributors
- Team members following established processes

### Canonical Structure

```markdown
# Contributing to Project Name

## Prerequisites

- Node.js 20+
- pnpm 8+

## Setup

1. Fork and clone the repository
2. Install dependencies: `pnpm install`
3. Copy environment file: `cp .env.example .env`
4. Start development server: `pnpm dev`

## Development Workflow

### Running Tests

```bash
pnpm test
```

### Code Style

Follow our [Style Guide](STYLE_GUIDE.md) for formatting rules.

## Pull Request Process

1. Create a feature branch
2. Make your changes
3. Run tests and linting
4. Submit PR against `main`

## Code of Conduct

[Link to CODE_OF_CONDUCT.md if applicable]
```

### Content Boundaries

**INCLUDE:**
- Prerequisites (runtime versions, tools)
- Detailed setup instructions
- Environment configuration
- How to run tests
- PR submission process
- Branch naming conventions
- Commit message format
- Code review expectations

**EXCLUDE (link instead):**
- Style rules themselves → STYLE_GUIDE.md
- Command reference tables → AGENTS.md
- Project overview → README.md

### Guidelines

- Be specific about versions ("Node.js 20+", not "recent Node")
- Include environment variable setup if applicable
- Document the complete setup, not just the happy path
- Link to style guide for formatting, don't duplicate rules

---

## STYLE_GUIDE.md

### Purpose

The style guide documents all code formatting, naming conventions, and documentation standards. It's the authoritative source for "how should this be written?"

### Audience

- Developers writing code
- Documentation authors
- Code reviewers checking style compliance

### Canonical Structure

```markdown
# Style Guide

## Code Formatting

### General

- Use 2-space indentation
- Maximum line length: 100 characters
- Use trailing commas in multiline structures

### TypeScript

- Prefer `interface` over `type` for object shapes
- Use explicit return types on exported functions
- Prefer `const` over `let`

## Naming Conventions

### Files

- Components: `PascalCase.tsx`
- Utilities: `camelCase.ts`
- Tests: `*.test.ts`

### Variables

- Boolean: prefix with `is`, `has`, `should`
- Arrays: use plural nouns

## Documentation

- Use JSDoc for public APIs
- Keep comments close to code they describe

## Linting

Configuration lives in:
- `.eslintrc.js` - ESLint rules
- `.prettierrc` - Prettier formatting
- `tsconfig.json` - TypeScript settings

To run linting: see [AGENTS.md](AGENTS.md#commands)
```

### Content Boundaries

**INCLUDE:**
- Code formatting rules
- Indentation and whitespace standards
- Naming conventions (files, variables, functions)
- Comment and documentation standards
- Examples of correct/incorrect patterns
- Linting configuration file locations
- Explanation of non-obvious lint rules

**EXCLUDE (link instead):**
- Commands to run linters → AGENTS.md
- Setup instructions → CONTRIBUTING.md
- Project overview → README.md

### Guidelines

- Show examples, not just rules
- Include both correct and incorrect examples when helpful
- Explain the "why" for non-obvious conventions
- Keep rules actionable and verifiable

---

## AGENTS.md

### Purpose

AGENTS.md is the single source of truth for AI agent guidance. It provides all AI agents with the information needed to work effectively in the codebase: commands, architecture overview, patterns, and gotchas.

### Audience

- All AI coding assistants (Claude, Cursor, Copilot, Codex, etc.)
- Multi-agent systems
- Developers looking for command reference

### Canonical Structure

```markdown
# AGENTS.md

This file provides guidance to AI agents working with this repository.

## Commands

| Command | Purpose |
|---------|---------|
| `npm run dev` | Start development server |
| `npm test` | Run test suite |
| `npm run lint` | Run ESLint |
| `npm run build` | Production build |

## Architecture Overview

Brief overview of project structure:
- `src/` - Application source code
- `src/components/` - React components
- `src/lib/` - Utility functions
- `tests/` - Test files

For detailed architecture, see [docs/](docs/).

## Key Files

- `src/index.ts` - Application entry point
- `src/config.ts` - Configuration loading

## Patterns

### Error Handling

This project uses Result types instead of exceptions.

### State Management

State is managed via React Context in `src/context/`.

## Gotchas

- Always run `npm run generate` after modifying GraphQL schemas
- The `config.ts` file is generated, don't edit directly

## Tool Usage Patterns

### When Reading Files

- Start with `src/index.ts` to understand entry points
- Check `tests/` for usage examples

### When Editing Files

- Run `npm run lint -- --fix` after editing
- Verify tests pass before committing

## Multi-Step Workflows

### Adding a New Feature

1. Create component in `src/components/`
2. Add tests in `tests/components/`
3. Export from `src/index.ts` if public
4. Update documentation if user-facing

## Style Reference

For detailed formatting rules, see [STYLE_GUIDE.md](STYLE_GUIDE.md).
```

### Content Boundaries

**INCLUDE:**
- Build, test, lint, format commands (canonical location)
- Project architecture overview (high-level)
- Directory structure explanation
- Key files and entry points
- Non-obvious patterns and conventions
- Gotchas and common pitfalls
- Tool usage patterns specific to this codebase
- Multi-step workflow documentation
- Context that helps AI agents work effectively

**EXCLUDE (link instead):**
- Detailed style rules → STYLE_GUIDE.md
- Human-oriented prose and tutorials
- Contribution workflow → CONTRIBUTING.md
- Full architecture documentation → docs/

### Guidelines

- Commands should be copy-paste ready
- Use tables for command reference
- Keep architecture section high-level (detailed docs go in docs/)
- Focus on what an AI needs to be productive
- Document things that aren't obvious from the code
- Include context that helps agents make good decisions

---

## CLAUDE.md

### Purpose

CLAUDE.md exists only because Claude Code looks for this file specifically, while other AI agents look for AGENTS.md. To maintain a single source of truth, CLAUDE.md simply redirects Claude to read AGENTS.md.

### Audience

- Claude Code only

### Canonical Structure

```markdown
# CLAUDE.md

Read [AGENTS.md](AGENTS.md) for all guidance on working with this repository.
```

That's it. The entire file should be just a redirect.

### Content Boundaries

**INCLUDE:**
- A single line redirecting to AGENTS.md

**EXCLUDE:**
- Any actual documentation (all content lives in AGENTS.md)

### Guidelines

- Keep it minimal - one line
- Don't duplicate any content from AGENTS.md

---

## LICENSE

### Purpose

LICENSE (no extension) contains the full license text for the project. README.md links here.

### Audience

- Anyone needing to understand licensing terms
- Legal review

### Canonical Structure

The full text of the chosen license (MIT, Apache 2.0, GPL, etc.).

### Content Boundaries

**INCLUDE:**
- Full license text
- Copyright holder and year

**EXCLUDE:**
- Project description
- Usage instructions

---

## CODE_OF_CONDUCT.md

### Purpose

CODE_OF_CONDUCT.md establishes community standards and expectations for behavior. It helps create a welcoming environment and provides a framework for handling violations.

### Audience

- Contributors and community members
- Project maintainers (enforcement)

### Canonical Structure

```markdown
# Code of Conduct

## Our Pledge

...

## Our Standards

**Positive behavior includes:**
- ...

**Unacceptable behavior includes:**
- ...

## Enforcement

...

## Reporting

...

## Attribution

Adapted from Contributor Covenant...
```

### Content Boundaries

**INCLUDE:**
- Expected behavior standards
- Unacceptable behavior examples
- Enforcement procedures
- Contact information for reporting
- Attribution (if based on existing covenant)

**EXCLUDE:**
- Technical documentation
- Contribution workflow (→ CONTRIBUTING.md)

---

## SECURITY.md

### Purpose

SECURITY.md provides a security policy and instructions for reporting vulnerabilities. GitHub recognizes this file and displays it in the Security tab.

### Audience

- Security researchers
- Users who discover vulnerabilities

### Canonical Structure

```markdown
# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| x.x.x   | Yes       |

## Reporting a Vulnerability

...

## Response Timeline

...

## Disclosure Policy

...
```

### Content Boundaries

**INCLUDE:**
- Supported versions table
- How to report vulnerabilities
- What information to include in reports
- Response timeline expectations
- Disclosure policy

**EXCLUDE:**
- General bug reporting (→ CONTRIBUTING.md or issue templates)
- Technical documentation

---

## CHANGELOG.md

### Purpose

CHANGELOG.md documents all notable changes between releases. It helps users understand what changed and when.

### Audience

- Users upgrading between versions
- Contributors understanding project history

### Canonical Structure

```markdown
# Changelog

## [Unreleased]

## [1.0.0] - 2024-01-01

### Added
- New feature X

### Changed
- Updated behavior Y

### Fixed
- Bug fix Z
```

### Content Boundaries

**INCLUDE:**
- Version numbers and release dates
- Changes categorized (Added, Changed, Deprecated, Removed, Fixed, Security)
- Links to relevant issues/PRs

**EXCLUDE:**
- Detailed implementation notes
- Full commit history

### Guidelines

- Follow [Keep a Changelog](https://keepachangelog.com/) format
- Most recent version at top
- Use semantic versioning
- Link to compare views between versions

---

## docs/ Directory

### Purpose

The docs/ directory contains detailed documentation that goes beyond the scope of root-level files. This includes full architecture documentation, API references, design documents, and tutorials.

### Audience

- Developers needing deep technical understanding
- AI agents working on architectural changes
- Contributors understanding system design

### Common Structure

```
docs/
├── architecture.md      # Full system architecture
├── api/                 # API documentation
├── design/              # Design documents
└── guides/              # Tutorials and how-tos
```

### Content Boundaries

**INCLUDE:**
- Full architecture documentation
- Detailed technical documentation
- API reference
- Design documents and ADRs
- Tutorials and how-to guides

**EXCLUDE:**
- Quick start (→ README.md)
- Commands reference (→ AGENTS.md)
- Style rules (→ STYLE_GUIDE.md)

---

## walkthroughs/ Directory

### Purpose

The walkthroughs/ directory contains interactive code walkthroughs in virgil format. These provide step-by-step guided tours through code with highlighted locations.

### Audience

- New team members onboarding to the codebase
- Developers learning a new feature or subsystem
- Code reviewers understanding changes

### Creating Walkthroughs

Use the **virgil** skill to create and manage walkthroughs. It handles:
- Walkthrough file format (JSON and Markdown)
- Code location references and highlighting
- Hierarchical step organization
- Diff mode for code reviews
- Repository scoping

### Content Boundaries

**INCLUDE:**
- Step-by-step code explanations with location references
- Onboarding guides
- Feature documentation with code context
- Code review walkthroughs

**EXCLUDE:**
- Static documentation without code references (→ docs/)
- API reference (→ docs/)
- Style rules (→ STYLE_GUIDE.md)

---

## Summary: Content Routing

| Content Type | Canonical Location |
|--------------|-------------------|
| Project overview | README.md |
| Quick start | README.md |
| Detailed setup | CONTRIBUTING.md |
| PR process | CONTRIBUTING.md |
| Style rules | STYLE_GUIDE.md |
| Naming conventions | STYLE_GUIDE.md |
| Commands | AGENTS.md |
| Architecture overview | AGENTS.md |
| Gotchas | AGENTS.md |
| Tool usage patterns | AGENTS.md |
| Multi-step workflows | AGENTS.md |
| Claude redirect | CLAUDE.md |
| Full license text | LICENSE |
| Community guidelines | CODE_OF_CONDUCT.md |
| Vulnerability reporting | SECURITY.md |
| Version history | CHANGELOG.md |
| Full architecture | docs/ |
| API documentation | docs/ |
| Interactive code tours | walkthroughs/ |
| Onboarding guides (with code) | walkthroughs/ |
| Code review walkthroughs | walkthroughs/ |
