# Support & Scale: Debug Errors with Amp

Use this prompt‑first workflow to triage incidents quickly, trace failures precisely, implement minimal‑risk fixes, and validate outcomes.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Restores stability and meets SLAs/SLOs faster.
- Prevents repeat failures with targeted tests and observability.
- Turns firefighting into a repeatable practice.
- Captures knowledge for future responders.

## Pre‑flight checklist
- Repro: failing input, expected vs actual behavior, impact scope.
- Context: version/commit, environment, feature flags, recent changes, owners.
- Access: code, logs, traces, dashboards, error pages.
- Safety: separate branch and rollback/flag plan.

---

## 1) Map the repo (error surfaces)

Prompt (single message):
```text
Inventory logging, metrics, tracing, and error boundaries for the suspected path. Note entry points,
cross‑service calls, and highest‑risk choke points with blast radius.
```

What you’ll get:
- Error surface map for the failing area
- Cross‑service and choke‑point awareness
- Immediate high‑signal probes to add

---

## 2) Read the history (incidents, regressions)

Prompt (single message):
```text
Summarize related incidents, recent regressions, risky diffs, and flaky tests. Cluster similar stack traces
and suggest likely defect classes.
```

What you’ll get:
- Incident and regression context
- Risky pattern inventory with hypotheses
- Reviewer/owner suggestions

---

## 3) Read with intention (trace the failing flow)

Prompt (single message):
```text
Trace the failing flow end‑to‑end and include file:line pointers for each hop. Highlight guardrails,
invariants, and missing checks. Propose high‑signal log/tracing additions.
```

What you’ll get:
- File:line trace of the failure path
- Guardrails and missing checks identified
- Observability improvements to land

---

## 4) Implement (minimal‑risk fix)

Prompt (single message):
```text
Propose the smallest safe change to prevent this failure. Include toggles/flags, blast radius,
side effects, and a rollback plan. Provide a focused diff with rationale.
```

What you’ll get:
- Minimal fix diff and rationale
- Flag/rollback guidance and risk notes
- Side‑effect review

---

## 5) Validate (repro → tests → checks)

Prompt (single message):
```text
Reproduce the failure and confirm it disappears. Add/update unit/integration tests for the defect shape.
Run targeted deployment checks (logs quieting, error rates normalizing, user path restored).
```

What you’ll get:
- Repro evidence pre/post fix
- Tests guarding against recurrence
- Deployment health confirmation

---

## Exit criteria and handoffs
- Root cause documented with precise trigger and scope
- Minimal fix merged with tests and observability added
- Error/latency rates normal; no new warnings in adjacent areas
- Postmortem/runbook updated; follow‑ups created and owned

---

## Quick reference

Prompt templates
```text
Map error surfaces for <path>; list choke points and probes.
Cluster incidents/regressions and propose likely defect classes.
Trace failure with file:line pointers and missing checks.
Minimal fix with flags/rollback and focused diff.
Verify: repro disappears, tests added, deployment checks green.
```

Developer‑run verification (optional)
```bash
git switch -c fix/debug-errors && git status
npm test -- --run --no-color || pnpm test -- --run --no-color
```

---

## Closing note
Use Amp as your debugging copilot: ask for maps, traces with file:line pointers, small fixes, and crisp validation. Amp returns synthesized results—not raw logs.
