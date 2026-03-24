# Agent Ready by Sero

Scan any project for AI agent readiness, fix what's broken, and level up — not just report. 20 criteria across 5 pillars, maturity levels L1-L5, prioritized improvement plans, and auto-fixing.

Most agent failures aren't agent failures — they're environment failures. Missing tests, no linter, undocumented setup, 800-line files. This skill measures what actually matters and fixes it.

---

## What It Does

1. **Scans** — detects language, framework, structure (mono vs single app)
2. **Evaluates** — 20 criteria across 5 pillars (feedback loops, structure, docs, testing, safety)
3. **Scores** — assigns a maturity level (L1 Functional → L5 Exemplary)
4. **Plans** — generates a prioritized improvement plan, auto-fixable items separated from human-input items
5. **Fixes** — implements improvements one level at a time, commits after each level, re-scans to confirm

## The 5 Pillars

| Pillar | What It Checks | Why It Matters |
|--------|---------------|----------------|
| **Feedback Loops** | Build command, test command, linter, formatter, type checking, pre-commit hooks | Can the agent verify its own work? |
| **Structure** | File sizes, directory sizes, lock file, type safety violations | Can the agent navigate without drowning in context? |
| **Documentation** | CLAUDE.md/AGENTS.md, subdirectory context, README setup, .env.example, .gitignore | Can the agent understand the project without guessing? |
| **Testing** | Tests exist, test-to-source ratio, test patterns | Can the agent prove its changes work? |
| **Safety** | No hardcoded secrets, dependency update automation | Will the agent introduce vulnerabilities? |

## Maturity Levels

| Level | Name | What It Means |
|-------|------|---------------|
| **L1** | Functional | Can build, has basics (linter, lock file, README, .gitignore, tests exist) |
| **L2** | Documented | Agent can understand the project (CLAUDE.md, type checking, pre-commit hooks, env docs) |
| **L3** | Agent-Ready | Agent can work effectively (tests runnable, small files, subdir context, good test ratio) |
| **L4** | Optimized | Agent works with confidence (formatter, test patterns, no secrets, dep updates) |
| **L5** | Exemplary | Everything dialed |

**L3 is the target for most projects.** At L3, agents can handle routine work — bug fixes, features, tests, docs — without constant human intervention.

## First-Run Integration

On first run, the skill appends **Agent Readiness Standards** to your global `~/.claude/CLAUDE.md`. These rules are then enforced automatically in every project you work on — file size limits, CLAUDE.md requirements, type safety, test minimums, linting.

This only happens once. After that, it just scans and fixes.

## Installation

Copy `SKILL.md` to `~/.claude/skills/agent-ready/SKILL.md`:

```bash
mkdir -p ~/.claude/skills/agent-ready
curl -o ~/.claude/skills/agent-ready/SKILL.md \
  https://raw.githubusercontent.com/peth-eth/agent-ready-by-sero/main/SKILL.md
```

Then run `/agent-ready` in any project.

## What It Fixes (auto, no confirmation needed)

- Missing CLAUDE.md files (root + subdirectories) — actually reads the directory and writes useful context
- Missing .env.example (scans code for env var usage)
- Missing/sparse .gitignore
- Missing lint/format scripts in package.json
- PR/issue templates
- Pre-commit hooks (husky/lint-staged for JS, pre-commit for Python)
- Basic test scaffolds when zero tests exist

## What It Asks Before Fixing

- Adding/modifying linter rules
- Enabling TypeScript strict mode
- Setting up Dependabot/Renovate
- Splitting oversized files
- Fixing type safety violations

## Impact

For a medium project (50-100 source files), going from unstructured to agent-ready typically means:

- **40-60% fewer tokens per task** (smaller files, faster orientation)
- **2-3x faster task completion** (fewer search cycles, less backtracking)
- **3-5x more parallelizable** (independent files instead of monoliths)
