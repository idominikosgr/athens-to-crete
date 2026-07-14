---
name: athens-to-crete
description: Integration-first engineering methodology. Use before implementing any feature or significant change, when reviewing an implementation approach, when code feels disconnected or over-engineered, or when checking for dead/orphaned code, silent failures, type-safety violations, or incomplete implementations.
---

# Athens to Crete

You're in Athens and need to reach Crete. The naive approach: build a road - impossible, there's sea in the way. The over-engineered approach: invent a "shipcopter" - wastes time on fantasy. The wise approach: recognize boats and planes exist, and use them.

**Don't build roads across seas. Don't invent shipcopters. Use boats.**

## Before Implementing

1. Understand the actual problem, not the stated request
2. Map real constraints and terrain
3. Identify existing solutions in the codebase
4. Verify the path is complete end-to-end

## Method

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

## Quality Bar

Check every implementation against [references/anti-patterns.md](references/anti-patterns.md) - error handling, type safety, implementation integrity, language-specific rules, framework and database pitfalls.

Strip needless indirection using [references/anti-indirection.md](references/anti-indirection.md) - forwarding wrappers, fallback chains, compatibility adapters, single-implementation abstractions. Every layer must justify its existence with actual work.

For tooling and stack choices, follow [references/tooling.md](references/tooling.md) - bleeding-edge-first, with the preferred toolchain per ecosystem.

## Escalation Paths

When installed as the `crete` plugin, deeper workflows are available:

- `/crete:think-first` - problem analysis before any code
- `/crete:build-connected` - full architecture → strategy → build → validate pipeline
- `/crete:validate-coherence` - post-implementation completeness check
- `/crete:find-orphans` - dead/disconnected code scan
- `/crete:project-synthesis` - whole-project reconciliation of docs, code, and vision

## Remember

- Code that "compiles" ≠ code that "solves the problem"
- Semantic coherence > syntactic correctness
- Every feature must be a bridge, not an island
