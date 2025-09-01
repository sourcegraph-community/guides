# Build: Implement Code with Amp

Use this prompt‑first workflow to implement changes in small, reversible slices with strong validation and clear handoffs.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Translates specs into reliable, maintainable code with tests.
- Catches defects early via fast, incremental loops.
- Preserves consistency by following style and contracts.
- Reduces risk with feature flags and least‑privilege design.

## Pre‑flight checklist
- Scope and acceptance criteria are explicit; non‑goals clear.
- Interfaces/contracts to touch are listed; flag strategy defined.
- Local environment runs; build/test commands known; secrets managed.
- Style/naming/commit conventions confirmed.
- Safe branch: `git switch -c feat/<slug>`

---

## 1) Plan the change (scope, contracts)

Prompt (single message):
```text
Outline the minimal stepwise plan for <change>. Define user impact, inputs/outputs, invariants,
updated contracts, flag strategy, and migration path. Return 3–6 small, reversible slices with
acceptance criteria and risks.
```

What you’ll get:
- Sequenced plan with scoped diffs and tests per slice
- Contracts and invariants to preserve
- Risks and rollback notes

---

## 2) Read with intention (targeted paths)

Prompt (single message):
```text
Given these targets <paths/types/functions>, summarize responsibilities, key call sites, side effects,
and invariants to preserve. Return only what’s essential for safe edits.
```

What you’ll get:
- Focused reading outcomes for just‑enough context
- Call‑site and side‑effect awareness
- Hidden coupling and edge cases to watch

---

## 3) Implement (incremental diffs)

Prompt (single message):
```text
Implement slice N: <small change>. Adhere to style/naming rules. Produce a focused diff and updated
tests/docstrings. Call out any necessary knock‑on changes and why.
```

What you’ll get:
- Minimal diff with updated tests
- Rationale for any adjacent edits
- Clear next step for the next slice

---

## 4) Validate (build, diagnostics, tests)

Prompt (single message):
```text
Run typecheck/lint/tests for touched areas. Report failures with smallest repro and propose fixes.
If behind flag <name>, verify both on/off behavior. Summarize pass/fail and next actions.
```

What you’ll get:
- Targeted validation results and fixes
- Confidence behind feature flags
- Evidence for reviewer handoff

---

## 5) Risk & compliance (least privilege, data types)

Prompt (single message):
```text
Review changes for least‑privilege access, sensitive data handling, input validation, and error
messaging. Propose stricter types or guards where appropriate and note any logging redactions.
```

What you’ll get:
- Security/privacy checklist applied to the diff
- Tighter types/guards and safer error handling
- Logging guidance without secrets

---

## Exit criteria and handoffs
- Acceptance criteria pass locally; typecheck/lint/build/tests green
- Tests added/updated for new behavior; brittle cases avoided
- Feature guarded, off by default unless release‑ready; rollback documented
- Review package prepared: summary, scope, risks, test evidence, rollout/rollback

---

## Quick reference

Prompt templates
```text
Plan: propose small, reversible slices with tests and risks.
Read: summarize responsibilities, call sites, side effects, invariants.
Implement: focused diff with updated tests and rationale.
Validate: typecheck/lint/tests; flag on/off; pass/fail and fixes.
Risk: least‑privilege, sensitive data, validation, error messaging; stricter types.
```

Developer‑run verification (optional)
```bash
# Build, typecheck, lint (adapt to your repo)
npm run build || pnpm build || yarn build
npm run typecheck || pnpm exec tsc -b || yarn tsc -b
npm run lint || pnpm lint || yarn lint

# Tests (focused first, then broader)
npm test -- --run --no-color || pnpm test -- --run --no-color || yarn test
```

---

## Closing note
Keep changes small, typed, and reversible. Amp chooses tools automatically and returns synthesized results—not raw logs—so you can stay focused on outcomes.
