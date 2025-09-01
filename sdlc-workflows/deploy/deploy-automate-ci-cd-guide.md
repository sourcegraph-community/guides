# Deploy: Automate CI/CD with Amp

Use this prompt‑first workflow to map your pipeline landscape, add quality gates and artifacts, and validate promotion flows.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Ships faster with consistent, repeatable builds and zero‑touch deploys.
- Enforces quality gates (tests, coverage, security) before release.
- Produces traceable artifacts with provenance and retention.
- Reduces risk with validated promotion and rollback paths.

## Pre‑flight checklist
- Access: CI provider/project permissions; envs exist and are named.
- Secrets: centralized management; short‑lived tokens; no long‑lived keys.
- Build/test: install/build/test commands; coverage target.
- Artifacts: registries/stores, SBOM/signing strategy, retention policy.
- Branching: default branch, protections, release/tag strategy, versioning scheme.

---

## 1) Map the repo (CI configs, commands)

Prompt (single message):
```text
Map CI for this workspace. Identify build/test/lint commands, existing pipeline configs,
workflow per app/service/package, artifacts and destinations, integration/E2E deps, and owners.
Return a pipeline inventory and risks (flaky tests, long builds, secrets usage).
```

What you’ll get:
- Pipeline inventory and gaps
- Artifact catalog and destinations
- Risk summary and owners

---

## 2) Plan the change (stages, triggers, gates)

Prompt (single message):
```text
Propose stages for PR/main/tag: prepare → build → test → scan → package → integ/E2E → publish → deploy.
Define triggers, concurrency/cancellation, quality gates (status checks, coverage, lint/static, security),
and cache strategy (keys/restore policy). List artifacts to produce/sign/store.
```

What you’ll get:
- Stage/trigger/gate plan with cache keys
- Artifact and signing/SBOM strategy
- Estimated durations and bottlenecks

---

## 3) Implement (pipelines, caching, artifacts)

Prompt (single message):
```text
Generate pipeline configs for PR, main, and tag releases with dependency and build caching.
Produce artifacts (binaries/images/packages), generate SBOMs, sign and upload. Parameterize per‑env
deploy jobs (staging first), promotion on approval, canary if needed, and concurrency groups.
```

What you’ll get:
- CI config updates with caches and artifacts
- Parameterized deploy jobs and promotion flows
- Protections (required checks, approvals, drift detection)

---

## 4) Validate (dry runs, branch rules)

Prompt (single message):
```text
Lint CI configs, run dry runs if supported, and open a test PR to exercise PR pipelines.
Confirm gates: failing tests block merges; coverage enforced; scans fail jobs on issues.
Verify artifacts (download, checksum/signature) and test release path with a pre‑release tag.
```

What you’ll get:
- Validation results and fixes
- Artifact verification evidence
- Baselines: duration, cache hit rate, flake rate

---

## 5) Risk & compliance (secrets, approvals)

Prompt (single message):
```text
Harden secrets (short‑lived/OIDC), enable secret/dependency/container scanning, generate SBOM and
provenance, sign artifacts, and wire approvals/policy rules for protected branches/environments.
Document rollback procedures and verify in staging.
```

What you’ll get:
- Hardened pipeline with security checks
- Policy gates and audit log coverage
- Tested rollback path and runbook notes

---

## Exit criteria and handoffs
- Pipelines green (PR/main/tag) with alerts; quality gates enforced
- Reproducible, signed artifacts with SBOM and retention
- Staging auto‑deploy; production gated with rollback verified
- CI/CD docs and runbooks updated; owners assigned

---

## Quick reference

Prompt templates
```text
Map: build/test commands, pipelines, artifacts, environments, and risks.
Plan: stages, triggers, caches, and quality gates with artifacts and estimates.
Implement: configs for PR/main/tag, caching, artifacts, signing, parameterized deploys.
Validate: dry runs, test PR, artifact verification, pre‑release tag.
Harden: secrets, scans, SBOM/provenance, approvals, rollback.
```

Developer‑run verification (optional)
```bash
# Tag a pre‑release to test release workflows
git tag -a v0.0.0-rc.1 -m "pre-release test" && git push origin v0.0.0-rc.1
```

---

## Closing note
Automate for consistency, gate for quality, and instrument for insight. Amp chooses tools and returns synthesized results—not raw logs.
