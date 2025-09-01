# Design: Develop Technical Specs with Amp

Use this prompt‑first workflow to turn goals into implementation‑ready specifications with contracts, diagrams, risks, and validation.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Aligns stakeholders and reduces rework with explicit decisions.
- Produces clear contracts (APIs, schemas) and testable criteria.
- Surfaces risks early and proposes targeted spikes.
- Creates artifacts ready for build, test, and deploy.

## Pre‑flight checklist
- Problem statement: goals, non‑goals, success metrics, guardrails.
- Context: current flows, dependencies, constraints (security, privacy, infra).
- Stakeholders: reviewers across product, engineering, QA, security/data.
- Standards: naming, API style/versioning, privacy/security requirements.
- Rollout: flags/migrations, observability hooks, compatibility needs.
- Safe branch: `git switch -c design-spec/<date>-<initials>`

---

## 1) Read with intention (existing flows)

Prompt (single message):
```text
Map current behavior for <feature-area>. Summarize flows (happy/edge/error), inputs/outputs,
side effects, components/services touched, external dependencies, implicit contracts, and
risky assumptions. Return a Current State Overview and a short sequence diagram.
```

What you’ll get:
- Current state summary with call/sequence overview
- Dependencies and assumptions/unknowns
- Keep/change/remove candidates per component

---

## 2) Plan the change (goals, constraints, risks)

Prompt (single message):
```text
Produce an actionable plan for <feature>. Include Goals/Non‑Goals, Success Metrics, Guardrails,
Acceptance Criteria (user/system), Phase Scope & Milestones, Top Risks (impact/mitigation/spikes),
and Open Questions. Keep it concise and decision‑ready.
```

What you’ll get:
- Change plan and acceptance criteria
- Risk register and spike list
- Decision log (initial) and open questions

---

## 3) Architecture sketch (components, sequences)

Prompt (single message):
```text
Propose a simple, evolvable design for <feature>. Provide a component map (boundaries,
responsibilities, ownership), sequence for the critical path, error handling (timeouts,
retries/backoff, idempotency), and 2–3 alternatives with trade‑offs/recommendation.
```

What you’ll get:
- Component/sequence diagrams (text) with responsibilities
- Error and resilience strategies
- Options matrix with trade‑offs and recommendation

---

## 4) Data shapes & contracts (schemas, migrations)

Prompt (single message):
```text
Define contracts for <feature>. Provide request/response shapes (types, constraints, examples,
validation rules), endpoints (method, path, auth, params, responses/errors), and persistence
changes (schema deltas, migrations, back/forward compatibility, backfill/rollback strategy).
```

What you’ll get:
- Contracts catalog and endpoint specs
- Schema/migration plan with compatibility
- Policies: versioning, pagination, idempotency, rate limits, error model

---

## 5) Validation plan (tests, non‑functional)

Prompt (single message):
```text
Create a validation strategy for <feature>. Include Unit/Integration/E2E matrix, fixtures/data,
non‑functional checks (performance/security/resilience) with thresholds, observability plan
(signals/dashboards/alerts), rollout validation (canary/flags/smoke), and rollback triggers.
```

What you’ll get:
- Validation plan mapped to acceptance
- Observability and rollout checks
- Clear rollback triggers and evidence

---

## Exit criteria and handoffs
- Spec complete: overview, goals/non‑goals, architecture, endpoints, data, risks, validation, rollout, decisions
- Review sign‑offs across product/engineering/QA/security/data/ops
- Implementation backlog: tasks, migrations, observability, spikes; milestones/owners
- Compatibility and rollback plans documented

---

## Quick reference

Prompt templates
```text
Read with intention: Summarize current behavior and dependencies for <feature>; add a sequence diagram.
Plan the change: Goals/Non‑Goals, metrics, acceptance, milestones, risks/spikes, open questions.
Architecture sketch: Components/boundaries, critical sequence, error model, options matrix.
Contracts: Request/response shapes, endpoints, schema/migrations, compatibility and rollback.
Validation: Test matrix, non‑functional, observability, rollout validation, rollback triggers.
```

Developer‑run verification (optional)
```bash
# Manage spec artifacts on a design branch
git switch -c design/<feature-slug>-spec
git add <spec-path> && git diff --staged && git commit -m "design: spec for <feature-slug>"
```

---

## Closing note
Amp coordinates work from prompts and returns synthesized results—not raw logs. Keep specs concise, decisions explicit, and contracts testable to enable smooth handoffs into build.
