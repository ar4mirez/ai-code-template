# CLAUDE.md

AI-assisted development instructions. Opinionated guardrails for writing quality software.

---

## Quick Reference

**Task Classification:**
- **ATOMIC** (<5 files, clear scope) → Implement directly | Lines 67-74
- **FEATURE** (5-10 files) → Break into subtasks | Lines 76-82
- **COMPLEX** (>10 files, new subsystem) → Use PRD workflow | Lines 84-108

**Common Guardrails** (validate first):
✓ Function ≤50 lines | ✓ File ≤300 lines | ✓ Input validation | ✓ Parameterized queries
✓ Tests >80% (critical) | ✓ Conventional commits | ✓ No secrets in code

**Emergency Quick Links:**
- Security issue? → Lines 28-36
- Tests failing? → @.agent/workflows/troubleshooting.md
- Stuck >30 min? → @.agent/workflows/troubleshooting.md
- Complex feature? → @.agent/workflows/create-prd.md
- Language-specific? → @.agent/language-guides/

**Load Language Guide** (automatic based on file extensions):
- TypeScript/JavaScript → @.agent/language-guides/typescript.md
- Python → @.agent/language-guides/python.md
- Go → @.agent/language-guides/go.md
- Rust → @.agent/language-guides/rust.md

---

## Core Guardrails (ALWAYS ENFORCE)

### Code Quality
- ✓ No function exceeds 50 lines (split with helper functions)
- ✓ No file exceeds 300 lines (components: 200, tests: 300, utils: 150)
- ✓ Cyclomatic complexity ≤ 10 per function
- ✓ All exported functions have type signatures and documentation
- ✓ No magic numbers (use named constants)
- ✓ No commented-out code in commits (use git history)
- ✓ No `TODO` without issue/ticket reference
- ✓ No dead code (unused imports, variables, functions)

### Security (CRITICAL)
- ✓ All user inputs validated before processing
- ✓ All API boundaries have input validation (prefer schema validators: Zod, Pydantic, etc.)
- ✓ All database queries use parameterized statements (no string concatenation)
- ✓ All environment variables have secure defaults (never hardcode secrets)
- ✓ All file operations validate paths (prevent directory traversal)
- ✓ All async operations have timeout/cancellation mechanisms
- ✓ Dependencies checked for known vulnerabilities before adding
- ✓ Dependencies checked for license compatibility before adding
- ✓ All database migrations include rollback (down) function

### Testing (CRITICAL)
- ✓ Coverage targets: >80% for business logic, >60% overall
- ✓ All public APIs have unit tests
- ✓ All bug fixes include regression tests
- ✓ All edge cases explicitly tested (null, empty, boundary values)
- ✓ Test names describe behavior: `test_user_login_fails_with_invalid_password`
- ✓ No test interdependencies (tests run in any order)
- ✓ Integration tests for external service interactions
- ✓ All deployments include smoke test validation

### Git & Commits
- ✓ Commit messages: `type(scope): description` (conventional commits)
- ✓ Types: feat, fix, docs, refactor, test, chore, perf, ci
- ✓ One logical change per commit (atomic commits)
- ✓ All commits must pass tests before pushing
- ✓ Branch naming: `type/short-description` (e.g., `feat/user-auth`)
- ✓ No commits directly to main/master (use PRs)
- ✓ Breaking API changes require major version bump (Semantic Versioning)

### Performance
- ✓ No N+1 queries (batch database operations)
- ✓ Large datasets use pagination/streaming (not full loads)
- ✓ Expensive computations memoized/cached when appropriate
- ✓ Frontend bundles < 200KB initial load (code-split when needed)
- ✓ API responses < 200ms for simple queries, < 1s for complex

---

## 4D Methodology (Enhanced)

Apply appropriate mode based on task complexity:

### ATOMIC Mode (Default)
For single-file changes, bug fixes, small features:

1. **Deconstruct**: What's the minimal change needed?
2. **Diagnose**: Will this break anything? Check dependencies.
3. **Develop**: Make the change with tests.
4. **Deliver**: Validate (run tests, check guardrails) → Commit.

### FEATURE Mode
For multi-file features, new components, API endpoints:

1. **Deconstruct**: Break into 3-5 subtasks (each atomic).
2. **Diagnose**: Identify integration points and dependencies.
3. **Develop**: Implement subtasks sequentially with tests.
4. **Deliver**: Integration test → Documentation → Review → Commit.

### COMPLEX Mode
For architecture changes, major refactors, new systems:

1. **Deconstruct**: Full decomposition into phases/milestones.
2. **Diagnose**: Analyze risks, dependencies, migration paths.
3. **Develop**: Create `.agent/project.md` with plan → Implement incrementally.
4. **Deliver**: Staged rollout → Documentation → Retrospective.

**Structured Workflow (for COMPLEX tasks):**

**MANDATORY when:**
- New subsystem (authentication, payments, real-time features)
- Breaking architectural changes
- Affects >15 files
- Unclear requirements (needs scope definition)

**RECOMMENDED when:**
- Affects 10-15 files
- Multiple stakeholders
- Complex domain logic

**OPTIONAL when:**
- Affects <10 files with clear scope
- Well-defined refactoring

**Workflow:**
1. Use `@.agent/workflows/create-prd.md` to define requirements
2. Use `@.agent/workflows/generate-tasks.md` to break down implementation
3. Implement tasks step-by-step with verification checkpoints
4. See `.agent/workflows/README.md` for full documentation

**Escalation Triggers:**
- Task affects >5 files → FEATURE mode
- Task affects >10 files → COMPLEX mode (consider PRD workflow)
- Task affects >15 files OR new subsystem → COMPLEX mode (PRD workflow MANDATORY)
- Task unclear/ambiguous → Ask user for clarification first

---

## Software Development Lifecycle

### Stage 1: Planning
**Atomic**: Read existing code → Identify change location
**Feature**: Review related code → Sketch interfaces/contracts
**Complex**: Create `.agent/project.md` OR use PRD workflow

**Checkpoints:**
- [ ] Requirements clear and testable
- [ ] Scope defined (what's included, what's not)
- [ ] Dependencies identified
- [ ] Breaking changes flagged

### Stage 2: Implementation
**Always:**
- Write tests first (TDD) or alongside code
- Load language-specific guide: @.agent/language-guides/{language}.md
- Follow language/framework idioms
- Validate against guardrails continuously
- Keep changes focused (resist scope creep)

**Checkpoints:**
- [ ] Code follows all guardrails (review each ✓ above)
- [ ] Tests written and passing
- [ ] No linter errors/warnings
- [ ] Types correct (strict mode)

### Stage 3: Validation
**Automated:**
- Run full test suite
- Check coverage thresholds
- Run linter/formatter
- Verify build succeeds

**Manual:**
- [ ] Edge cases considered
- [ ] Error handling implemented
- [ ] Performance acceptable
- [ ] Security implications reviewed

### Stage 4: Documentation
**Code Level:**
- Function/class docstrings (what, why, params, returns)
- Inline comments for complex logic (why, not what)
- API documentation updated

**Project Level:**
- Update `.agent/patterns.md` if new pattern emerged
- Update `.agent/state.md` with progress
- Add `.agent/memory/YYYY-MM-DD-topic.md` for key decisions

### Stage 5: Commit
**Pre-Commit Checklist:**
- [ ] All tests pass
- [ ] Coverage thresholds met
- [ ] No linter errors
- [ ] All guardrails validated
- [ ] Commit message follows convention
- [ ] No sensitive data (secrets, credentials, PII)

**Commit:**
```bash
git add <files>
git commit -m "type(scope): description

- Detail 1
- Detail 2

Refs: #issue-number"
```

---

## Context System

### CLAUDE.md (This File)
**Loaded**: Always (every conversation)
**Purpose**: Guardrails, methodology, SDLC workflow
**Current**: 400 lines (target: <500, ideal: <300)

### .agent/ Directory
**Loaded**: On-demand, when needed
**Purpose**: Project-specific context that grows over time

**Structure:**
```
.agent/
├── README.md              # How to use .agent/
├── project.md             # Tech stack, architecture (create when tech chosen)
├── patterns.md            # Coding patterns (create when patterns emerge)
├── state.md              # Current work (create for multi-session work)
├── language-guides/      # Language-specific guardrails (pre-created)
│   ├── typescript.md
│   ├── python.md
│   ├── go.md
│   └── rust.md
├── workflows/            # Structured workflows (pre-created)
│   ├── create-prd.md
│   ├── generate-tasks.md
│   ├── initialize-project.md
│   └── troubleshooting.md
├── tasks/                # PRDs and task lists (created during COMPLEX mode)
│   ├── NNNN-prd-feature-name.md
│   └── tasks-NNNN-prd-feature-name.md
└── memory/               # Decision logs (created as needed)
    └── YYYY-MM-DD-topic.md
```

**Loading Protocol:**
- **Session Start**: AI loads CLAUDE.md → Checks for state.md → Reads if exists
- **During Work**: Load language guide based on file extensions (automatic)
- **Complex Features**: Load workflows (PRD, task generation)
- **Reference Needed**: Load patterns.md, project.md, memory/ on-demand

**Progressive Growth:**
- Day 1: Only CLAUDE.md + templates ✓
- First code: Language guide loaded automatically
- Week 1: Create `.agent/project.md` when architecture decided
- Month 1: `.agent/patterns.md` populated with conventions
- Ongoing: `.agent/memory/` captures complex decisions

**For details on any .agent/ file, see:** `.agent/README.md`

---

## Protected Boundaries

### DO NOT Modify Without Explicit Permission
- `package-lock.json`, `yarn.lock`, `Gemfile.lock` (dependency locks)
- `.env`, `.env.local` (environment configs)
- Database migration files (once applied)
- `tsconfig.json`, build configs (without testing)
- Git hooks, CI/CD configs

### DO NOT Commit
- Secrets, API keys, credentials (use environment variables)
- `.env` files (commit `.env.example` instead)
- `node_modules`, `venv`, build artifacts (use `.gitignore`)
- Personal IDE configs (`.vscode/`, `.idea/` unless team-shared)
- Large binaries, datasets (use Git LFS or external storage)
- Debug logs, `console.log` statements in production code

### ALWAYS Ask Before
- Changing authentication/authorization logic
- Modifying database schemas (after production deployment)
- Updating major dependencies (breaking changes possible)
- Refactoring public APIs (breaks consumers)
- Changing build/deploy processes

---

## Anti-Patterns (Avoid These)

### Code
- ❌ Premature optimization (measure first, optimize after)
- ❌ Over-engineering (YAGNI: You Aren't Gonna Need It)
- ❌ Copy-paste code (extract to shared function/component)
- ❌ Ignoring errors (every error needs handling)
- ❌ Mutable globals (use dependency injection, immutable state)

### Testing
- ❌ Testing implementation details (test behavior, not internals)
- ❌ Flaky tests (non-deterministic results indicate bad design)
- ❌ Test interdependencies (each test should be isolated)
- ❌ No assertions (tests must verify something)

### Process
- ❌ Committing directly to main (use feature branches + PRs)
- ❌ Batch commits (commit after each logical change)
- ❌ Skipping tests because "it's a small change" (small bugs exist too)
- ❌ Not reading error messages fully (they often tell you the fix)

### Documentation
- ❌ Outdated docs (worse than no docs)
- ❌ Obvious comments (`i++; // increment i`)
- ❌ No comments on complex logic (future you needs context)
- ❌ Docs separate from code (keep close: docstrings, inline, README)

---

## Initialization

**For new projects:** Use `@.agent/workflows/initialize-project.md`

**For existing projects:** Use `@.agent/workflows/initialize-project.md`

AI will ask questions, analyze codebase, and create `.agent/project.md` with findings.

---

## When Stuck

**See:** `@.agent/workflows/troubleshooting.md`

**Quick recovery:**
1. STOP trying random solutions (>30 min = stuck)
2. Document what you've tried
3. Simplify & isolate (minimal reproduction)
4. Check fundamentals (dependencies, config, versions)
5. Ask user with clear problem statement
6. Record solution in `.agent/memory/`

---

## Success Criteria

### Per Task
- [ ] All guardrails validated
- [ ] Tests pass with coverage thresholds
- [ ] No security vulnerabilities introduced
- [ ] Documentation updated
- [ ] Commit follows conventions

### Per Session
- [ ] State documented in `.agent/state.md` (if multi-session)
- [ ] New patterns added to `.agent/patterns.md` (if emerged)
- [ ] Key decisions in `.agent/memory/` (if significant)
- [ ] No broken tests left behind
- [ ] Progress measurable

---

## Version & Changelog

**Current Version**: 1.1.0
**Last Updated**: 2025-01-15

### Changelog

**v1.1.0 (2025-01-15) - Phase 1 Optimization**
- ✅ Reduced from 490 → 400 lines (18% reduction)
- ✅ Added Quick Reference section (lines 7-21)
- ✅ Added critical missing guardrails:
  - Dependency license checking
  - Database migration rollbacks
  - Semantic versioning for breaking changes
  - Smoke test validation
- ✅ Clarified workflow requirements (MANDATORY vs RECOMMENDED)
- ✅ Extracted language-specific guides to .agent/language-guides/
- ✅ Extracted initialization to .agent/workflows/initialize-project.md
- ✅ Extracted troubleshooting to .agent/workflows/troubleshooting.md
- ✅ Created comprehensive language guides (TypeScript, Python, Go, Rust)

**v1.0.0 (2025-01-14) - Initial Release**
- Initial CLAUDE.md system with 30+ guardrails
- 4D methodology (ATOMIC/FEATURE/COMPLEX)
- Integrated ai-dev-tasks workflows
- Progressive .agent/ directory structure

### Update This File When
- Adding/removing guardrails
- Changing methodology
- Project-wide quality standards shift
- New language guides added

---

**Remember**: This file is your guardrails. The `.agent/` directory is your memory. Small atomic changes. Validate continuously. Document progressively.
