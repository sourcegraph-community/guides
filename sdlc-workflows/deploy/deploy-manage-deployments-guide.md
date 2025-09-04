# Deploy: Manage Deployments with Amp

Use this prompt‑first workflow to plan strategy, promote safely, validate health, and keep a clean audit trail with reversible paths.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Moves changes to users with minimal disruption and clear guardrails.
- Balances velocity and safety via progressive exposure and gates.
- Produces an auditable trail of intent, actions, and outcomes.
- Captures learning for faster, safer future deploys.

## Pre‑flight checklist
- Strategy: rolling, blue‑green, or canary; rationale and fallback.
- Backout: clear rollback steps, ownership, and time budget.
- Observability: health checks, error/latency/SLO dashboards, alert thresholds.
- Data safety: backward‑compatible migrations, flag‑gated behavior, recovery path.
- Change control: approvals recorded, window confirmed, comms plan ready.

---

## 1) Plan the change (strategy and gates)

Prompt (single message):
```text
Select a deployment strategy (rolling, blue‑green, canary) for <service>. Define traffic ramps,
entry/exit gates, kill‑switches, and database compatibility approach. List required dashboards and alerts.
```

What you’ll get:
- Strategy with ramps and stop conditions
- DB compatibility and flag defaults
- Observability plan for promotion

---

## 2) Implement (deploy & promote)

Prompt (single message):
```text
Prepare steps to deploy to pre‑prod, verify, then canary, ramp by cohorts/percent, and promote to full.
Keep feature flags default‑safe and configuration decoupled. Provide a step‑by‑step checklist.
```

What you’ll get:
- Promotion checklist with ramp schedule
- Flag and config guidance
- Owners per step

---

## 3) Validate (smoke & health)

Prompt (single message):
```text
Run smoke tests; verify health, error rate, latency, and saturation against baselines and SLOs.
Confirm key user journeys and downstream/backward compatibility. Capture artifacts for audit.
```

What you’ll get:
- Health and journey verification results
- SLO burn‑rate view and regression flags
- Artifacts for audit trail

---

## 4) Read the history (incidents & rollback triggers)

Prompt (single message):
```text
Review prior incidents and known risky areas for <service>. Define rollback triggers (e.g., error rate,
p95 latency, SLO burn) and decision points (stop/pause/rollback) with owners.
```

What you’ll get:
- Context from past incidents
- Concrete rollback triggers and owners
- Decision points synchronized to the ramp

---

## 5) Risk & compliance (controls)

Prompt (single message):
```text
Ensure approvals, audit notes, change ticket linkage, and freeze exceptions. Capture evidence of checks,
sign‑offs, and timing within change windows. Provide a post‑deploy summary template.
```

What you’ll get:
- Change management evidence
- Post‑deploy summary template
- Clear audit trail coverage

---

## Exit criteria and handoffs
- Metrics stable vs baseline; SLO burn within budget; no critical errors
- Smoke tests pass; critical journeys verified; flags in intended state
- Dashboards/alerts updated; runbook deltas captured
- Release notes and change ticket finalized; audit trail complete
- Ops/on‑call briefed; support informed of known issues

---

## Quick reference

Prompt templates
```text
Strategy: plan rolling/blue‑green/canary; ramps, gates, DB compatibility, required dashboards.
Promote: pre‑prod → canary → cohorts → full; step‑by‑step checklist with owners.
Validate: smoke, health, journeys, SLOs; capture artifacts for audit.
History: prior incidents and rollback triggers with owners and thresholds.
Compliance: approvals, tickets, evidence, and post‑deploy summary.
```

Developer‑run verification (optional)
```bash
# Create a release tag and branch
git tag -a vX.Y.Z -m "Release vX.Y.Z" && git push origin vX.Y.Z
```

---

## Closing note
Use Amp to plan, gate, and document every deployment. Amp chooses tools automatically and returns synthesized results—not raw logs.
