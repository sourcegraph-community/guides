# Build: Write and Execute Tests with Amp

Use this prompt‑first workflow to derive a test strategy from requirements, implement unit/integration/E2E tests, and validate results efficiently.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Converts requirements into verifiable behavior and prevents regressions.
- Improves refactor confidence with meaningful coverage.
- Enforces quality, security, and PII protections.
- Produces artifacts CI can gate on consistently.

## Pre‑flight checklist
- Scope: critical flows, acceptance criteria, risk areas, non‑functional needs.
- Environments: ephemeral deps, seeded test data, secrets policy (no prod data).
- Quality bars: coverage target, flake tolerance, performance budgets.
- Traceability: tests linked to stories/risks; prioritize high‑impact paths first.
- Safe branch: `git switch -c test/<area>-<date>`

---

## 1) Map the repo (test stack, conventions)

Prompt (single message):
```text
Summarize testing frameworks/runners, directory and naming conventions, tagging, fixtures/mocks,
data seeding, E2E setup, relevant environment variables, CI triggers, and coverage reporting.
Return a 1‑page "test map" with do/don't guidance.
```

What you’ll get:
- Test stack inventory and conventions
- Data/fixture strategy and E2E harness
- Coverage thresholds and CI triggers

---

## 2) Read with intention (critical flows → test cases)

Prompt (single message):
```text
For <flow>, derive a test matrix (happy, boundary, error, security). Include preconditions/data,
expected side effects, and observability hooks. Output Given‑When‑Then scenarios with priorities.
```

What you’ll get:
- Prioritized test matrix and scenarios
- Inputs/outputs and side‑effects noted
- Observability hooks to assert

---

## 3) Implement tests (unit, integration, E2E)

Prompt (single message):
```text
Generate tests for <module/service/feature> following the matrix. Use builders over fragile fixtures,
control time, isolate dependencies, and capture artifacts (logs/screenshots/traces) where useful.
Flag any long‑running or flaky candidates.
```

What you’ll get:
- Unit tests for logic and invariants
- Integration tests for boundaries and contracts
- E2E scenarios with stable selectors and artifacts

---

## 4) Validate (selective then broad)

Prompt (single message):
```text
Run tests impacted by recent changes; report failures with root‑cause hypotheses and suggest minimal
fixes. Then outline a plan to validate the entire suite efficiently (order, caching, shards).
```

What you’ll get:
- Focused failure analysis and fixes
- Plan to scale up to full‑suite validation
- Coverage deltas and quality signals

---

## 5) Risk & compliance (security/PII paths)

Prompt (single message):
```text
Assess security and PII coverage. Propose tests for authn/z, sensitive logging/redaction, key rotation
behavior, audit trails, rate‑limiting, and data retention. Tie each test to flows and severity.
```

What you’ll get:
- Security/PII test additions mapped to risks
- Clear redaction and retention expectations
- Auditability checkpoints for CI

---

## Exit criteria and handoffs
- Critical flows covered across unit/integration/E2E; acceptance criteria reflected
- Suite green; flake rate within policy; meaningful assertions, not just percent
- Compliance upheld (no secrets in data/logs; PII redaction verified)
- CI surfaces reports; docs updated for test map and run instructions

---

## Quick reference

Prompt templates
```text
Test map: frameworks, conventions, fixtures/mocks, E2E harness, coverage, CI triggers.
Matrix: derive Given‑When‑Then scenarios with priorities and observability hooks.
Implement: unit/integration/E2E; builders; time control; artifacts; flag flaky candidates.
Validate: impacted tests first; failure analysis; plan for full suite; coverage deltas.
Compliance: authn/z, redaction, key rotation, audit trails, rate limiting, retention.
```

Developer‑run verification (optional)
```bash
# Run tests (adapt to your runner)
<runner> test <path-or-pattern>
<runner> test --coverage
<runner> test <file> -t "<case name>"
```

---

## Closing note
Build on earlier stages: discover and design guide what to test. Amp chooses tools automatically and returns synthesized results—not raw logs—so you can focus on behavior and signal.
