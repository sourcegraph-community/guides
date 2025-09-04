# Discover: Onboard & Learn with Amp

Use this prompt‑first workflow to ramp quickly, build a mental model, and establish a safe, fast local loop.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Shortens time to first meaningful contribution.
- Avoids surprises by revealing hotspots, conventions, and guardrails.
- Establishes a reliable local build/test loop.
- Documents flows and open questions for the team.

## Pre‑flight checklist
- Access: SSO/2FA, required repos, non‑prod secrets, package registries.
- Conventions: `AGENTS.md` with commands, structure, naming, review policy.
- Runtime: toolchains, container runtime, linters/formatters, commit signing.
- Comms: join team channels; review standups, on‑call, triage/incident flows.
- Safe branch: `git switch -c onboard/<date>-<initials>`

---

## 1) Map the repo

Prompt (single message):
```text
Provide a high‑level map: primary apps/services, core modules, build/test commands,
entry points, and configuration sources. Include where to run locally and how to observe.
Return a concise overview I can share.
```

What you’ll get:
- Architecture sketch and directory landmarks
- Build/test commands and where to run
- Config sources and how they compose
- Immediate risks or anomalies to note

---

## 2) Find the landmarks (auth, routing, configs, environments)

Prompt (single message):
```text
Identify authentication, routing, configuration loading, environment switching, feature flags,
and secret handling. Explain patterns, where they’re wired, and trade‑offs.
```

What you’ll get:
- Auth/routing/config/flags locations and how they connect
- Environment parity (local/staging/prod) and safety rails
- Minimal files to read first with why‑it‑matters

---

## 3) Read the history (themes, hotspots)

Prompt (single message):
```text
Summarize notable changes in the last 60–90 days: top churn paths, refactors, recurring bugs,
deprecations, and likely reviewers. Return hotspots and themes with rationale.
```

What you’ll get:
- Hotspot list with churn/rationale
- Themes (refactors, deprecations, known issues)
- Suggested reviewers for risky areas

---

## 4) Read with intention (first critical flows)

Prompt (single message):
```text
Trace <critical flow> end‑to‑end: inputs → validation → business logic → I/O.
List key files, data shapes, and error handling. Include a simple sequence diagram
and immediate test gaps.
```

What you’ll get:
- File‑by‑file walkthrough with line anchors
- Sequence diagram clarifying flow
- Specific follow‑ups: tests, invariants, docs

---

## 5) Validate (local build/test sanity)

Prompt (single message):
```text
Outline the minimal local checks for sanity: format/lint, typecheck, nearest unit tests,
a focused integration check, and the simplest smoke run. Keep it under 5 minutes.
```

What you’ll get:
- A fast, reliable local loop
- What’s required vs nice‑to‑have before PR
- Any setup gaps to close

---

## Exit criteria and handoffs
- Project runs locally; minimal tests pass; release cadence understood
- 1–2 critical flows documented with edge cases
- A small, low‑risk PR is ready (docs or trivial fix)
- Open questions, risks, and next steps are captured and owned

---

## Quick reference

Prompt templates
```text
Map the repo: summarize apps, modules, entry points, configs, and how they connect.
Find landmarks: auth, routing, config loading, env switching, flags, secrets.
History: last 90 days; hotspots, refactors, recurring bugs, deprecations; reviewers.
Trace a flow: inputs/validation/logic/I-O; sequence diagram; test gaps.
Sanity checks: minimal format/lint/typecheck/unit/integration/smoke under 5 minutes.
```

Developer‑run verification (optional)
```bash
# Identity and remote
git config --get user.name && git config --get user.email
git remote -v

# Safe branch
git switch -c yourname/onboard-discover

# Recent activity and hotspots
git log --oneline -30
git log --name-only --since="90 days ago" | sort | uniq -c | sort -nr | head -20
```

---

## Closing note
Amp chooses tools automatically and returns synthesized results only—not raw logs. Keep prompts outcome‑focused; Amp infers the workspace from your CLI/IDE context.
