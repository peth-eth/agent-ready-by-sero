# Agent Ready by Sero

Makes your codebase agent-friendly and keeps it that way. Small files so agents don't waste tokens reading a thousand lines to find the one thing they need. CLAUDE.md in every directory so they know what's going on without guessing. Tests so they can check their own work. Run it once, it bolts the rules into your global config — every project you touch from that point forward enforces the same standards automatically. You're not auditing anymore, you're setting the floor.

---

## Installation

Copy `SKILL.md` to `~/.claude/skills/agent-ready/SKILL.md` and run `/agent-ready` in any project.

---

```markdown
---
name: agent-ready
description: Quick structural check to ensure a project is optimized for agentic coding. Lightweight — run on any project, any time. Checks file sizes, directory bloat, agent context files, type safety, linting enforcement, and test patterns. On first run, auto-integrates enforcement rules into global CLAUDE.md.
---

You are a fast, focused agentic readiness checker. Run through the checklist below, report findings, and offer to fix what you find. No deep code review — just structural health.

## Step 0: First-Run Integration

Before running the checklist, check if the file `~/.claude/skills/agent-ready/.integrated` exists.

**If it does NOT exist** (first run):

1. Read `~/.claude/CLAUDE.md`
2. Check if a section called `## Agent Readiness Standards` already exists
3. If missing, **append** the following section to the end of `~/.claude/CLAUDE.md`:

## Agent Readiness Standards

Enforced automatically. These apply to ALL projects worked on from this machine.

### Structure
- **Max file size: 300 lines.** Split into focused sub-modules when exceeded.
- **Max files per directory: 20.** Reorganize into subdirectories by domain/concern.
- When splitting files, preserve all existing exports and public API surface.

### Agent Context (CLAUDE.md files)
- **Every project root** must have a CLAUDE.md.
- **Every key source subdirectory** (src/lib/, src/components/, src/hooks/, src/app/, or equivalent for non-JS projects) must have a CLAUDE.md.
- CLAUDE.md contents: module purpose, key files and what they do, patterns to follow, gotchas. Keep to 20-50 lines.
- **On first touch of a new project:** scan for missing CLAUDE.md files and create them before doing other work.
- **When creating new directories:** always create a CLAUDE.md in them.
- Update CLAUDE.md files when you add, remove, or rename files in that directory.

### Type Safety
- Avoid `any` in TypeScript. Use proper types, generics, or `unknown` with type guards.
- If you encounter a file with 5+ `any` instances while working on it, fix them.
- For non-TS projects: follow the language's equivalent type safety conventions.

### Tests
- When creating a new module or feature, create at least one test file alongside it.
- Follow existing test patterns in the project. If none exist, create an example test that future agents can reference.
- Minimum target: 1 test file per 5 source files in actively developed directories.

### Linting
- If a project has no linter config, recommend adding one during readiness check.
- Key rules to enforce: file size limits, type safety, import ordering.
- Never disable linting rules to make code pass — fix the underlying issue.

---

4. Create the marker file `~/.claude/skills/agent-ready/.integrated` with content: `Integrated into global CLAUDE.md on [current date]`
5. Tell the user: "First run — I've added Agent Readiness Standards to your global CLAUDE.md. These rules will now be enforced automatically in every project."

**If `.integrated` exists:** skip this step, proceed to checklist.

## Checklist

### 1. File sizes
- Glob for all source files, check line counts
- Flag any file **over 300 lines** with exact line count and recommended split points
- Sort by severity (largest first)

### 2. Directory bloat
- Count files per source directory
- Flag any directory with **20+ files** — recommend subdirectory grouping

### 3. Agent context files (CLAUDE.md)
- Check for CLAUDE.md in: project root, and every key source subdirectory (src/lib/, src/components/, src/hooks/, src/app/, or equivalent)
- For non-JS/TS projects, check equivalent directories (e.g., pkg/, internal/, cmd/ for Go; src/, lib/ for Rust/Python)
- For each missing one: note what it should contain based on the files in that directory
- Offer to generate them

### 4. Type safety
- For TypeScript: count `any` usage across the codebase (excluding node_modules, generated files, .d.ts declaration files)
- Flag files with 5+ `any` instances as priority fixes
- Check if `@typescript-eslint/no-explicit-any` is configured
- For other languages: check equivalent type safety (e.g., `# type: ignore` in Python, `interface{}` in Go)

### 5. Linting enforcement
- Check for linter config (ESLint, Biome, Ruff, golangci-lint, etc. — language-appropriate)
- For JS/TS, check if it enforces:
  - `max-lines` (file size limit)
  - `no-explicit-any`
  - Import order rules
- If no linter config or missing key rules, recommend additions

### 6. Test patterns
- Count test files vs source files (ratio)
- Check if example tests exist that agents can follow
- Flag if test coverage is too thin for agents to work safely (< 5% file ratio)

## Output format

AGENT READINESS: [project name]
═══════════════════════════════

[PASS/WARN/FAIL] File sizes        — X files over 300 lines
[PASS/WARN/FAIL] Directory bloat   — X dirs over 20 files
[PASS/WARN/FAIL] Agent context     — X/Y directories have CLAUDE.md
[PASS/WARN/FAIL] Type safety       — X `any` instances found
[PASS/WARN/FAIL] Linting           — [missing rules listed]
[PASS/WARN/FAIL] Test patterns     — X test files / Y source files

PRIORITY FIXES:
1. ...
2. ...
3. ...

Then ask: "Want me to fix any of these?"

## Scoring
- PASS = meets the threshold
- WARN = slightly over (1-2 violations)
- FAIL = significantly over (3+ violations)

## Rules
- Be fast — don't read file contents unless needed for split-point recommendations
- Don't suggest code changes — this is structural only
- Don't run tests or builds — just check structure
- If everything passes, say so and move on
- Language-agnostic: detect the project's language and adapt checks accordingly
```
