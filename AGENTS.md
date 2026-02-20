# Agent Instructions: Tracepipe Frontend

## Purpose

Storefront web application for Tracepipe — user accounts, payments (Stripe/Link), and API key management.

## Project Type

**Application** — Production web application meant for deployment (Next.js or Astro).

## Documentation

For platform-level documentation and cross-repository coordination, see [tracepipe](https://github.com/CRSS-AI/tracepipe) and [tracepipe-docs](https://github.com/CRSS-AI/tracepipe-docs).

## Before Writing Code

1. **Plan first** — outline approach before coding; pause if user jumps to implementation
2. **Get verification criteria** — ask "How should I verify this works?" (tests, expected UI behavior, build command)
3. **Match existing patterns** — read relevant code to understand project style

## Code Style

**Naming**: Descriptive names; avoid type-redundant suffixes

**Type annotations**: Required on all new code; use TypeScript strict mode

**Imports**: Organize imports consistently; use path aliases configured in `tsconfig.json`

**Formatting**: Trailing commas in multi-line collections; named arguments for multi-param calls

**Comments**: Only when providing non-obvious context; code should be self-explanatory, DRY, SOLID

**Terminology**: "model" over "LLM"

**Circular imports**: Avoid circular module dependencies entirely

**Exception handling**: Route and test exceptions by type, not by error message phrasing

## Quality Checks

Run before committing:

```bash
npm run lint         # ESLint/Biome
npm run type-check   # TypeScript compiler (tsc)
npm run test         # Unit/integration tests (Vitest)
npm run build        # Verify production build succeeds
```

**Pre-commit requirement**: Run type checking before committing — **type errors are unacceptable in committed code**. Fix legitimate type issues; document pre-existing ones but ensure your new code is correctly typed.

## Verification

- Verify app starts without runtime errors (`npm run dev`)
- **Run the application and test manually in browser** — not just automated tests
- Test key user flows (registration, payment, API key management)
- Verify production build succeeds (`npm run build`)
- Summarize: what changed, why, verification results
- Fix failures before claiming success

## Testing

**Test types** (all required for each feature):

- **Unit tests**: Test a single component/module in isolation
- **Integration tests**: Test a single feature end-to-end with external calls mocked (APIs, Stripe, etc.)
- **E2E tests**: Use Playwright to test critical user flows in a real browser

**Requirements**:

- **Vitest** (or Jest) with **Arrange-Act-Assert** pattern for unit/integration tests
- **Playwright** for E2E tests
- Mock external dependencies (APIs, payment providers) in unit and integration tests
- Production-quality: type-safe, documented, DRY, SOLID
- **80% coverage per feature** (not average) — all three test types should exist when adding features

## Test Maintenance

**When making breaking changes:**

- Update ALL affected tests (unit, integration, E2E) to reflect the new contract
- "Expected failures" is never acceptable — if a test fails due to your change, fix the test
- E2E test specs are code — treat them like any other test file

**Regression test failures after your changes mean:**

1. Your change broke something unintentionally → fix your code
2. Your change intentionally altered the contract → update the tests

Never report test failures as "expected" or "intentional" without also fixing them.

## Don'ts

- Hard-code values to pass tests
- Suppress errors without fixing root cause
- Modify files outside task scope
- Claim success without verification
- Skip planning for non-trivial tasks

## Git Workflow

**Branching**: `feature/{JIRA_ticket}` from default branch; commit frequently; **never push until instructed**

**Commits**: Clear messages; single logical change per commit; **NEVER commit when tests are failing** — all tests must pass before creating a commit

**Pre-commit**: Run type checking before committing — type errors are unacceptable in committed code
