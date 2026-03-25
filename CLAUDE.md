## Philosophy: Athens to Crete

You're in Athens and need to reach Crete. The naive approach: build a road—impossible, there's sea in the way. The over-engineered approach: invent a "shipcopter"—wastes time on fantasy. The wise approach: recognize boats and planes exist, and use them.

Before implementing:
1. Understand the actual problem, not the stated request
2. Map real constraints and terrain
3. Identify existing solutions in the codebase
4. Verify the path is complete end-to-end

Don't build roads across seas. Don't invent shipcopters. Use boats.

---

## Workflow

**Note: Bleeding edge tools and techniques are used and encouraged and they are a feature not a bug. Our approach is to be always on the bleeding edge with versions and tools/languages alike. The reason is that in the AI landscape software dev is moving fast and we need to be ahead of the curve even if this means we will be the first to come across new issues and challenges. To that end never downgrade versions of languages, tools or libraries. Evaluate alternative tools, packages and libraries that might be more modern and cutting edge.**

### Before Writing Code
- Read existing code and documentation—understand context first
- Search the codebase for similar functionality before creating new
- Understand how domains interconnect and where this work fits
- Verify assumptions by checking, not guessing

### When Implementing
- Refactor in place—no "enhanced", "improved", "new", "v2" file variants
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

---

## Anti-Patterns

### Error Handling
- Silent failures—operations that fail without surfacing errors
- Error swallowing—catch blocks that log-and-continue
- Missing error context—re-throws without wrapping
- Ignored errors—unchecked return values, unhandled rejections

### Type Safety
- `any` in TypeScript—use `unknown` with narrowing, unions, or generics
- `type: ignore` in Python—requires justification comment
- Implicit `any`—untyped function parameters and returns
- Non-exhaustive switches—all variants handled or explicitly unreachable
- Unsafe casts—assertions that bypass compiler checks
- Nullable access without guards

### Implementation Integrity
- Stubs/mocks outside tests—no placeholder logic in production
- Dead code—unreachable branches, unused functions, commented blocks
- Partial implementations—happy path only, missing error paths
- Orphaned code—no call sites, no integration
- Broken invariants—state that violates contracts

### Language-Specific

**TypeScript:** No `unknown` casts without narrowing; exhaustive switches required

**Rust:** No `.unwrap()`/`.expect()` outside tests—use `?`; `unsafe` requires justification

**Python:** No bare `except:`; no broad `except Exception` without re-raise

**Go:** No `_ = err`—handle or propagate

### Framework (Next.js/React)
- Server/client boundary leaks
- Misplaced `"use client"` directives
- Hydration mismatches

### Database
- Missing FK indexes
- Constraints enforced in app logic instead of schema
- Schema drift—type changes without migrations


### Tooling

## General
- Use mise for package and library management
- Use homebrew when appropriate for system-level dependencies


## Node.js/TypeScript Projects
- Use oxlint, oxfmt and oxlint-tsgo 
- Use tsgo instead of tsc for faster incremental builds and better error reporting
- Use viteplus ecosystem where appropriate and its satelite tools for linting, building, formatting, bundling and testing
- Use Knip for dependency analysis and dead code detection
- Use Syncpack for consistent dependency versions across packages
- Use tsdown or more modern and robust bundles where appropriate
- Use vite for non Next.js projects for fast development and optimized production builds
- Use Next.js for React projects with server-side rendering needs, but avoid it for non
- Use pnpm for package and script management
- Use turborepo for monorepo management and task orchestration

## Go Projects
- Use golangci-lint for comprehensive linting
- Use goimports for formatting and organizing imports
- Use go mod for dependency management
- Use go test with coverage for testing

## Tauri Projects
- Use vite for frontend development and bundling
- Use Rust's cargo for backend development and dependency management
- Use tauri's built-in tooling for building and packaging

## Python Projects
- Use ruff for linting and formatting
- Don't use legacy overlapping tools like black, isort, flake8, mypy—ruff can handle all of these
- Use pytest for testing
- Use uv for dependency management and task running
- Use python 3.13.11 or later for best performance and features
- Use python 3.13 cpu optimizations for production deployments
- Always use the highest version of packages that are compatible with your codebase to benefit from latest features and security patches (even prerelease versions )

## Docker and Docker Compose
- Use latest versions of base os and application images for security and performance
- Use multi-stage builds to optimize image size
- Use .dockerignore to exclude unnecessary files from build context
- Use environment variables for configuration and secrets management
- Use latest versions of actions and tools in CI/CD pipelines for building and deploying Docker images


---

## Documentation

- README with setup instructions
- Document complex algorithms and business logic
- Keep docs adjacent to code they describe
- Update docs when code changes

**JS/TS:** JSDoc | **Python:** Google/NumPy docstrings | **Rust:** `///` with examples | **Go:** Godoc for exports

---

## Communication Style

- Direct, factual—no marketing tone or consultant-speak
- No timelines, roadmaps, or projected outcomes
- No HR allocation or ROI discussion
- Realistic assessments over aspirational statements
- Concrete and actionable, not speculative