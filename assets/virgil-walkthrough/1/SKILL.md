---
name: virgil-walkthrough
description: Create interactive code walkthroughs in Virgil format. Use when the user asks to "create a walkthrough", "document the code flow", "explain how X works", "create an onboarding guide", "make a code tour", "create a PR walkthrough", or "document this feature".
version: 1.0.0
---

# Virgil Walkthrough Generator

Create interactive code walkthroughs in Virgil markdown format, compatible with the Virgil VS Code extension.

## Workflow

### Phase 1: Understand the Request

Before exploring code, clarify:

1. **Walkthrough type:**
   - **Standard** - Point-in-time explanation of how code works
   - **Diff** - Explains changes between commits/branches (for PRs)
   - **Onboarding** - Getting started guide for new contributors

2. **Scope:** What feature, flow, or concept should be covered?

3. **Audience:** Beginner, intermediate, or expert developers?

If the user hasn't specified, ask using AskUserQuestion:
- "What type of walkthrough?" with options: Standard (code explanation), Diff (PR/changes), Onboarding (new contributor guide)
- "What should the walkthrough cover?" if scope is unclear

### Phase 2: Gather Repository Context

1. **Get git information:**
   ```bash
   git remote get-url origin 2>/dev/null || echo "no-remote"
   git rev-parse HEAD
   git rev-parse --abbrev-ref HEAD
   ```

2. **For diff walkthroughs, also get:**
   ```bash
   git merge-base main HEAD  # or the appropriate base branch
   ```

3. **For diff walkthroughs, enumerate all changed files:**
   ```bash
   git diff --name-status <base>..<head>
   ```
   Categorize files by status:
   - **A (Added)** - New files that must have `[View code ...]` links
   - **D (Deleted)** - Removed files that must have `[Base ...]` links
   - **M (Modified)** - Changed files that must have both link types
   - **R (Renamed)** - Old path needs `[Base ...]`, new path needs `[View code ...]`

4. **Explore the codebase:**
   - Use Glob to find relevant files
   - Use Grep to locate key functions/patterns
   - Use Read to understand the code deeply
   - Map out the execution flow or architecture

### Phase 3: Design the Walkthrough Structure

Plan the narrative before writing:

1. **Identify 5-15 steps** that tell a coherent story
2. **Determine hierarchy:**
   - `##` for main steps (major concepts)
   - `###` for sub-steps (details within a concept)
   - `####`+ for deeply nested explanations
3. **For each step, note:**
   - File path and line range
   - Key insight to convey
   - Connection to next step

### Phase 4: Generate the Walkthrough

Create a markdown file in `walkthroughs/` directory.

**Frontmatter format:**
```yaml
---
remote: <git remote URL>
commit: <full commit SHA>
# For diff walkthroughs, add one of:
baseBranch: main
# or
baseCommit: <base commit SHA>
---
```

**Code location link format:**
```markdown
[View code (startLine-endLine)](/path/from/repo/root.ts)
```

- Lines are 1-based and inclusive
- Path must start with `/` and be relative to repo root
- For multiple ranges: `[View code (10-20,33-45)](/file.ts)`
- For diff mode, add base location after: `[View code (10-20)](/file.ts) [Base (8-18)](/file.ts)`

**Step structure:**
```markdown
## Step Title

Explanation of what this code does and why it matters.

[View code (startLine-endLine)](/path/to/file.ext)
```

**For diff walkthroughs, ensure 100% file coverage:**
- [ ] Every added file has at least one `[View code ...]` link
- [ ] Every deleted file has at least one `[Base ...]` link
- [ ] Every modified file has both `[View code ...]` AND `[Base ...]` links
- [ ] Renamed files: old path has `[Base ...]`, new path has `[View code ...]`

### Phase 5: Review and Refine

1. **Present the walkthrough** to the user
2. **Verify accuracy:**
   - All file paths exist
   - Line numbers point to the correct code
   - Narrative flows logically
3. **For diff walkthroughs, verify 100% coverage:**
   ```bash
   ./scripts/verify-walkthrough-coverage.sh walkthroughs/<name>.md
   ```
   Fix any uncovered files before finalizing.
4. **Iterate** based on user feedback

## Templates

Reference templates are available in `assets/templates/`:
- `standard.md` - Point-in-time code explanation
- `diff.md` - PR/change walkthrough
- `onboarding.md` - New contributor guide

## Virgil Format Reference

See `references/virgil-format.md` for complete format specification.

## Output Location

Save generated walkthroughs to:
```
walkthroughs/<descriptive-name>.md
```

Create the `walkthroughs/` directory if it doesn't exist.

## Best Practices

1. **Accurate line numbers** - Always read files to determine correct ranges; never guess
2. **Commit pinning** - Include commit SHA so the walkthrough remains valid
3. **Focused ranges** - Keep code selections to 10-50 lines; break up larger sections
4. **Narrative flow** - Start with context, build understanding progressively
5. **Explain "why"** - Don't just describe what code does; explain the reasoning
6. **Link concepts** - Show how pieces connect to form the whole
