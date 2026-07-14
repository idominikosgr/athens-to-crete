# Athens to Crete - Engineering Playbook

Agent-agnostic instructions (Codex, Claude Code, and any AGENTS.md-aware tool). Copy this file into a project root, or merge it into an existing AGENTS.md.

## Philosophy

You're in Athens and need to reach Crete. The naive approach: build a road - impossible, there's sea in the way. The over-engineered approach: invent a "shipcopter" - wastes time on fantasy. The wise approach: recognize boats and planes exist, and use them.

Before implementing:

1. Understand the actual problem, not the stated request
2. Map real constraints and terrain
3. Identify existing solutions in the codebase
4. Verify the path is complete end-to-end

Don't build roads across seas. Don't invent shipcopters. Use boats.

## Workflow

### Before Writing Code

- Read existing code and documentation - understand context first
- Search the codebase for similar functionality before creating new
- Understand how domains interconnect and where this work fits
- Verify assumptions by checking, not guessing

### When Implementing

- Refactor in place - no "enhanced", "improved", "new", "v2" file variants
- No internal compatibility layers or wrapper adapters
- Always hard refactor the case in hand and align all references
- Fix architecture problems, don't patch around them
- Remove duplicate implementations immediately
- Verify cross-domain integration before considering work complete

### Integration Requirements

- All functionality interconnects across the codebase
- Expose features across TUI, CLI, UI, and API where applicable
- Domains must be able to call each other's functionality
- No siloed components

## Anti-Patterns

### Error Handling

- Silent failures - operations that fail without surfacing errors
- Error swallowing - catch blocks that log-and-continue
- Missing error context - re-throws without wrapping
- Ignored errors - unchecked return values, unhandled rejections

### Type Safety

- `any` in TypeScript - use `unknown` with narrowing, unions, or generics
- `type: ignore` in Python - requires justification comment
- Implicit `any` - untyped function parameters and returns
- Non-exhaustive switches - all variants handled or explicitly unreachable
- Unsafe casts - assertions that bypass compiler checks
- Nullable access without guards

### Implementation Integrity

- Stubs/mocks outside tests - no placeholder logic in production
- Dead code - unreachable branches, unused functions, commented blocks
- Partial implementations - happy path only, missing error paths
- Orphaned code - no call sites, no integration
- Broken invariants - state that violates contracts

### Language-Specific

**TypeScript:** No `unknown` casts without narrowing; exhaustive switches required

**Rust:** No `.unwrap()`/`.expect()` outside tests - use `?`; `unsafe` requires justification

**Python:** No bare `except:`; no broad `except Exception` without re-raise

**Go:** No `_ = err` - handle or propagate

### Framework (Next.js/React)

- Server/client boundary leaks
- Misplaced `"use client"` directives
- Hydration mismatches

### Database

- Missing FK indexes
- Constraints enforced in app logic instead of schema
- Schema drift - type changes without migrations

## Tooling

Bleeding edge is a feature, not a bug - never downgrade languages, tools, or libraries; continuously evaluate more modern alternatives.

- **General:** mise for runtimes/packages, homebrew for system dependencies
- **Node/TS:** pnpm, vite (or Next.js for SSR React), oxlint/oxfmt, tsgo, Knip, Syncpack, tsdown, turborepo
- **Python:** uv, ruff (replaces black/isort/flake8/mypy), pytest, Python 3.13+
- **Go:** golangci-lint, goimports, go mod, go test with coverage
- **Docker:** latest base images, multi-stage builds, .dockerignore, env-based config

## Documentation

- README with setup instructions
- Document complex algorithms and business logic
- Keep docs adjacent to code they describe; update docs when code changes
- **JS/TS:** JSDoc | **Python:** Google/NumPy docstrings | **Rust:** `///` with examples | **Go:** Godoc for exports

## Communication Style

- Direct, factual - no marketing tone or consultant-speak
- No timelines, roadmaps, or projected outcomes
- Realistic assessments over aspirational statements
- Concrete and actionable, not speculative

## Structured Workflows (for agents without subagent support)

When a prompt references a named agent, run its phase inline instead:

- **solution-architect** → analyze problem, map solution, audit existing resources, produce blueprint before code
- **implementation-strategist** → decompose, order by dependency (foundation → logic → service → presentation → integration), exact build order
- **coherence-validator** → after building, check reachability, completeness, integration, orphans; report COHERENT/DISCONNECTED/INCOMPLETE/MISSING
- **flow-analyzer** → validate every journey end-to-end: START → STEPS → BRANCH → ERROR → END
