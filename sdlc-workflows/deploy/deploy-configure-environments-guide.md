# Deploy: Configure Environments with Amp

Use this prompt‑first workflow to define environment invariants, parameterize configs, and validate safe, auditable changes.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Repeatable environments reduce drift, outages, and onboarding time.
- Clear invariants protect data, costs, and compliance posture.
- Dev/staging/prod parity enables safe validation before customer impact.

## Pre‑flight checklist
- Access: permissions for env management, secrets, deploys, and observability.
- Secrets policy: ownership, rotation cadence, storage location, handling rules.
- Naming & scope: agreed env names, isolation boundaries, data residency.
- Data handling: policy for prod data in lower envs (masking/synthetic datasets).
- Change control: approvers, change windows, rollback authority.

---

## 1) Find the landmarks (env files, manifests, secrets)

Prompt (single message):
```text
Inventory environment definitions, runtime configs, parameter sets, secret references and owners,
databases/caches/queues/external vendors and their env equivalents, ingress/egress, DNS/TLS, and
sources of truth. Highlight shadow copies to eliminate.
```

What you’ll get:
- Environment manifest and dependency maps
- Secrets ownership/rotation notes
- Network contracts and sources of truth

---

## 2) Plan the change (env matrix and invariants)

Prompt (single message):
```text
Define an environment matrix (region, scale, data class, flags, dependencies, quotas). Specify
invariants (must never vary) and deliberate differences. Propose migration order (infra→network→data→app)
with backout plan and canary scope.
```

What you’ll get:
- Env matrix with invariants and intentional differences
- Migration order and rollback plan
- Blast‑radius controls (canary, ramp)

---

## 3) Implement (templates and policy)

Prompt (single message):
```text
Create a parameterized environment template with validation rules and deny‑list policies. Externalize
parameters (endpoints, credentials, sizes, flags, CIDRs). Bind least‑privilege secret scopes and document
rotation. Propose small, reviewable increments.
```

What you’ll get:
- Parameterized templates and policies
- Least‑privilege secret scopes and rotation guidance
- Incremental change plan with owners

---

## 4) Validate (health, smoke, connectivity)

Prompt (single message):
```text
Run pre‑deploy checks (schema/policy validation, config diffs, dependency availability). Verify data
safety (masking, backups/restore points). Run health/smoke (liveness/readiness, critical flows, auth),
connectivity (DNS/TLS/reachability/egress), and observability (alerts green). Drill rollback.
```

What you’ll get:
- Validation outcomes and remediation items
- Health/connectivity/observability evidence
- Rollback rehearsal results

---

## 5) Risk & compliance (least privilege, auditability)

Prompt (single message):
```text
Apply least‑privilege, rotations, change records (approvers/diffs/timestamps/rationale), PII boundaries,
backups/retention, tested restores, and DR assumptions per environment. Propose controls to close any gaps.
```

What you’ll get:
- Compliance checklist with evidence points
- Gaps and controls to implement
- Clear ownership for ongoing operations

---

## Exit criteria and handoffs
- Dev/staging/prod templates applied with env‑specific parameters and secrets bound
- Health checks/smoke pass; metrics/alerts green
- Env matrix, invariants, runbook (deploy/rollback), and ownership map updated
- Approvals from environment owner, security, data

---

## Quick reference

Prompt templates
```text
Landmarks: env manifests/configs/secrets/dependencies/network; sources of truth; shadow copies.
Matrix: invariants and deliberate differences; migration order; rollback/canary plan.
Implement: parameterized templates, validation rules, deny‑lists, least‑privilege scopes.
Validate: schema/policy checks; health/smoke; connectivity; observability; rollback drill.
Compliance: least‑privilege, rotations, audit trail, PII, backups/DR.
```

Developer‑run verification (optional)
```bash
http GET https://<env>.<domain>/healthz || true
```

---

## Closing note
Use prompts to keep changes explainable and auditable. Amp chooses tools automatically and returns synthesized results—not raw logs.
