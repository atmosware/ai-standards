# CLAUDE.md — Project Standards

> This file is read automatically by Claude Code at the start of every session.  
> It is the single source of truth for how Claude should behave in this codebase.  
> Keep it honest. Keep it short. Every line should earn its place.

---

## 1) Philosophy

1. **Write simple, unabstracted code.** Do not introduce patterns, interfaces, or boilerplate unless absolutely necessary to solve the immediate problem.
2. **Explicit over implicit.** Don't hide execution flow behind clever framework magic. Let the code read top-to-bottom like a script.
3. **No premature optimization.** Build the simplest thing that works. Don't build for "what if we need 10x scale" unless explicitly asked.
4. **Small diffs.** Change only what needs to be changed. Do not "clean up" adjacent code or switch syntax to your preference unless it's the requested feature.
5. **Readability is king.** Write code a junior engineer can read linearly and understand immediately.
6. **Focus on the data.** Understand the data structures and transformations first. The logic should naturally follow.
7. **Light dependencies.** Before adding a package, ask: "Can we write this in ~20 lines of standard library code?" If yes, write the code.

---

## 2) Project

- **Name**: {{PROJECT_NAME}}
- **Description**: {{ONE_LINE_DESCRIPTION — what the project does, for whom}}
- **Language(s)**: {{e.g., TypeScript, Python 3.12, Go 1.23, Java 21}}
- **Framework(s)**: {{e.g., Next.js 15, FastAPI, Spring Boot 3, Gin}}
- **Package manager**: {{e.g., pnpm, uv, poetry, npm, gradle}}
- **Architecture style**: {{e.g., layered, hexagonal, feature-first, clean architecture}}
- **Primary users**: {{USER_TYPES}}
- **Monorepo**: {{yes/no — if yes, list workspace roots}}

---

## 3) Non-Negotiables

If any item below is violated, the change is invalid.

1. No secrets in code, tests, logs, or docs.
2. No unvalidated external input reaches business logic.
3. No breaking API/schema changes without explicit migration notes.
4. No architectural boundary violations.
5. No TODO placeholders in shipped code.
6. No silent test skips.
7. No untyped escape hatches without a justification comment.
8. No dependency additions without rationale.

---

## 4) Commands

Claude should know how to build, test, lint, and run this project without asking.

```bash
# Install dependencies
{{INSTALL_COMMAND}}

# Run dev server
{{DEV_COMMAND}}

# Lint + format check
{{LINT_COMMAND}}

# Lint fix
{{LINT_FIX_COMMAND}}

# Type check
{{TYPECHECK_COMMAND}}

# Unit tests
{{TEST_UNIT_COMMAND}}

# Integration tests
{{TEST_INT_COMMAND}}

# Run a single test file
{{SINGLE_TEST_COMMAND}}

# Build for production
{{BUILD_COMMAND}}

# Database migrations
{{MIGRATE_COMMAND}}

# Security / dependency audit
{{SECURITY_AUDIT_COMMAND}}
```

Remove any command your project doesn't use. Add any command it does.

---

## 5) Working Agreement

### Before changing code

- Read nearby code and follow local patterns.
- Identify constraints from existing tests, types, and interfaces.
- Prefer editing existing modules over creating new ones.
- If multiple plausible implementations exist, pick the one that matches repository precedent.

### While changing code

- Keep edits minimal and localized.
- Keep public interfaces stable unless explicitly requested.
- Handle failure paths as first-class behavior.
- Add short intent comments only where logic is genuinely non-obvious. Comment the *why*, not the *what*.

### After changing code

- Run lint, typecheck, and tests.
- Fix all regressions introduced by the change.
- Verify error messages and logs are actionable.
- Ensure commit-ready state: no debug leftovers, no dead code.

---

## 6) Code Style

### Formatting

- {{e.g., Use Prettier defaults. Do not configure Prettier differently.}}
- {{e.g., 2-space indentation for TS/JS, 4-space for Python.}}
- {{e.g., Max line length: 100 characters.}}
- {{e.g., Trailing commas: always (ES5+).}}
- {{e.g., Semicolons: always / never.}}
- {{e.g., Quotes: single for JS/TS, double for Python.}}
- Match the surrounding code. Don't fight the existing style.

### Naming

- **Files**: {{e.g., kebab-case for all files. No PascalCase filenames except React components.}}
- **Variables/functions**: {{e.g., camelCase in TS/JS, snake_case in Python.}}
- **Classes/types**: {{e.g., PascalCase everywhere.}}
- **Constants**: {{e.g., UPPER_SNAKE_CASE for true constants, camelCase for derived values.}}
- **Database**: {{e.g., snake_case for tables and columns. Plural table names.}}
- **Booleans**: {{e.g., Prefix with is/has/should/can — never bare adjectives.}}
- **Private**: {{e.g., Prefix with underscore in Python. Use # in TS/JS.}}
- Use clear, descriptive, plain-English names. `calculateTotalUserScore` is better than `processData`.

### Imports

- Order: stdlib → external → internal → relative. Blank line between groups.
- No default exports. Use named exports everywhere.
- Use path aliases (`@/...`) for imports crossing more than two directory levels.
- Never use wildcard imports (`import *`).

### Logging

- Structured logs only.
- Include correlation/request IDs where available.
- Never log credentials, tokens, or sensitive payloads.

---

## 7) Architecture

### Directory Structure

```
{{PROJECT_ROOT}}/
├── src/
│   ├── {{LAYER_1}}/       # {{Purpose — e.g., domain models, business logic}}
│   ├── {{LAYER_2}}/       # {{Purpose — e.g., use cases, application services}}
│   ├── {{LAYER_3}}/       # {{Purpose — e.g., API routes, controllers}}
│   ├── {{LAYER_4}}/       # {{Purpose — e.g., database repos, external adapters}}
│   └── {{LAYER_5}}/       # {{Purpose — e.g., shared utilities, helpers}}
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── config/
└── scripts/
```

### Dependency Direction

```
{{LAYER_A}} → {{LAYER_B}} → {{LAYER_C}}
```

Forbidden reverse links: {{EXAMPLES}}

### Boundary Rules

- Domain logic cannot import framework code.
- Transport layer cannot contain business decisions.
- Persistence layer cannot leak storage-specific models into domain.
- Shared utils cannot become a dumping ground for feature logic.
- Features communicate via typed interfaces/events, not deep imports.

### Patterns to Follow

- {{e.g., Repository pattern for all data access. No raw SQL in services.}}
- {{e.g., DTOs at the boundary — never pass domain objects to/from API layer.}}
- {{e.g., Result types for error handling (no throwing for expected failures).}}
- {{e.g., Factory functions over constructors when object creation has logic.}}
- {{e.g., Prefer composition over inheritance. No class hierarchies deeper than 2 levels.}}

### Patterns to Avoid

- {{e.g., No God objects. If a class has more than 5 dependencies, split it.}}
- {{e.g., No barrel files (index.ts re-exports). Import from the source directly.}}
- {{e.g., No circular dependencies. The build will fail if one is introduced.}}
- {{e.g., No string-typing. Use enums or literal union types for fixed sets of values.}}
- {{e.g., No `any` type in TypeScript. Use `unknown` and narrow.}}

### Environment & Config

- All configuration comes from environment variables. Keep `.env.example` current.
- Never commit `.env` files.
- {{e.g., Config loaded once at startup via src/config.ts. Do not read process.env elsewhere.}}
- Fail fast on missing required config — crash at startup, not at first request.

---

## 8) Error Handling

- Use typed/custom errors for domain failures. Don't throw generic `Error`.
- Log errors at the boundary (route handler, queue consumer). Don't log and rethrow.
- Never swallow errors silently. Catch specific exceptions, print detailed actionable logs, and crash if you can't recover safely.
- Return structured error responses from APIs:

```json
{
  "error": "human-readable message",
  "code": "MACHINE_CODE",
  "details": {}
}
```

- {{e.g., Global error handler in src/middleware/error-handler.ts catches unhandled exceptions.}}

---

## 9) Testing

### Standards

- New logic requires tests. No exceptions.
- Bug fix requires a regression test.
- Edge cases for null/empty/timeout/retry paths are covered where relevant.
- Test file naming: `{{NAMING_CONVENTION — e.g., foo.test.ts, test_foo.py}}`.
- Use `describe`/`it` blocks (or equivalent). Test names read as sentences.

### What to Test by Layer

| Layer | What to test | What to mock |
|---|---|---|
| Domain / Models | Validation, state transitions, computed properties | Nothing — pure logic |
| Services | Business rules, edge cases, error paths | Repositories, external clients |
| Routes / Handlers | Status codes, response shapes, auth guards | Services |
| Repositories | Query correctness, constraint handling | Use test DB or Testcontainers |

### Test Pyramid

- **Unit**: fast, deterministic, isolated.
- **Integration**: real wiring for boundaries.
- **E2E**: only critical user journeys.

### Anti-Patterns

- No snapshot-only confidence for complex behavior.
- No mocking what you do not own unless required.
- No assertions tied to implementation details when behavior-level assertions suffice.
- Avoid heavy, labyrinthine mocking setups. If something is hard to mock, the code is probably too coupled.
- Don't chase 100% coverage via boilerplate tests that assert nothing meaningful.

### What Not to Test

- Framework boilerplate (config files, module declarations).
- Simple getters/setters with no logic.
- Third-party library internals.

### Test Utilities

- {{e.g., Use `src/test/factories.ts` for test data builders. Do not hand-construct objects in tests.}}
- {{e.g., Database tests use Testcontainers — no shared test database.}}

---

## 10) Security

These rules are mandatory. Violations are bugs.

- **No secrets in code.** Use environment variables.
- Validate all inputs using schema validation at boundaries.
- Authorize every protected operation.
- Parameterize all database queries — no string concatenation.
- Apply output encoding where rendering user content.
- Enforce explicit CORS policy in non-dev environments.
- Rotate keys/tokens per platform policy.
- Never log credentials, tokens, or PII.
- Keep dependency vulnerabilities below threshold: {{POLICY — e.g., no open High/Critical CVEs}}.

---

## 11) Dependencies

Before adding a package:

1. Confirm no standard-library or existing dependency solution exists.
2. Check maintenance activity and license compatibility.
3. Evaluate bundle/runtime impact.
4. Record one-line rationale in PR description.

Pin exact versions (no `^` or `~`) — OR — use lockfile and allow ranges (pick one, be consistent).

Approved defaults:

- HTTP client: {{APPROVED_HTTP}}
- Validation: {{APPROVED_VALIDATION}}
- ORM: {{APPROVED_ORM}}
- Test framework: {{APPROVED_TEST_FRAMEWORK}}

---

## 12) AI Interaction Rules

- **Stop and think.** Before making changes, identify exactly how data flows and what the actual problem is.
- **Do not invent features.** Only implement what was asked for.
- **Verify.** Run the appropriate local tests or CLI commands before handing the task back. Treat every edit as a real PR.
- **Be brief.** Use short sentences. Cut the fluff. "Done, tests pass" is better than "I have successfully implemented your request and verified it with the testing suite."
