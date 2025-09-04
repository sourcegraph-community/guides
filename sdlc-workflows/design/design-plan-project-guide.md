# Design: Plan Project with Amp

Use this prompt-first workflow to turn intent into a concrete, actionable plan. You’ll align scope, map dependencies, define a realistic schedule, and produce handoff-ready artifacts for engineering, security, and stakeholders.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Establishes scope, objectives, deliverables, and timelines grounded in current code and constraints.
- Breaks the effort into clear work packages with owners, estimates, and checkpoints.
- Surfaces dependencies, risks, and compliance needs early to de‑risk execution.
- Produces shareable artifacts (charter, dependency map, WBS, milestones, risk register) for cross‑team alignment.

From the SDLC workflow inventory: Plan project = “Defining project scope, objectives, deliverables, and timelines; breaking down into smaller tasks and assigning responsibilities.”

## Pre‑flight checklist
- Access and permissions: You can read required repos/services and organizational policy docs.
- Context: `AGENTS.md` captures conventions (commands, structure, naming). If missing/stale, ask Amp to propose updates.
- Safe branch: `git switch -c design-plan/<date>-<initials>`
- Optional baseline: Ask Amp to snapshot current repo map and release signals as a planning baseline.

---

## 1) Align scope and outcomes (project charter)

Prompt (single message):
```text
Draft a one-page project charter from the current workspace context:
- Problem statement, goals, non-goals, measurable success criteria (leading/lagging)
- Scope boundaries across apps/*, services/*, packages/*; key stakeholders and decision owners
- Constraints and assumptions (security, data, compliance, infra, SLAs)
- Initial risks and dependencies; open questions and how to resolve them
Return a concise charter I can share in kickoff.
```

What you’ll get:
- Charter with goals/non-goals, scope boundaries, stakeholders, and metrics
- Constraints/assumptions synthesized from the codebase and policy cues
- Early risk/dependency list with next-step clarifications

---

## 2) Map dependencies and critical path

Prompt (single message):
```text
Map technical and organizational dependencies for this initiative:
- Internal: shared libraries, services, data stores, feature flags, migrations
- External: 3rd-party APIs, identity, billing, analytics, infra constraints
- For each dependency: owner/team, readiness, lead time, and blocking risks
- Propose a critical path and earliest feasible milestone sequence
Include a simple dependency diagram and a prioritized blocker list.
```

What you’ll get:
- Dependency inventory with owners, readiness, and lead times
- A clear critical path with gating decisions and fallback options
- A simple architecture/dependency sketch to align stakeholders

---

## 3) Work Breakdown Structure (WBS) and milestones

Prompt (single message):
```text
Propose a WBS and milestone plan:
- Group into epics → stories/tasks with clear acceptance criteria
- For each task: objective, key files/paths, interfaces, test/validation hints
- Estimates (T-shirt or ranges), sequencing, and parallelizable work
- Milestones with entry/exit criteria, demo points, and rollback considerations
Add a provisional RACI across key roles.
```

What you’ll get:
- Epics/stories/tasks with acceptance criteria and key paths to touch
- Estimates and sequencing with what can run in parallel
- Milestone schedule with entry/exit criteria and demo checkpoints
- Lightweight RACI matrix for ownership clarity

---

## 4) Plan the change across the repo

Prompt (single message):
```text
Outline the concrete change plan:
- Code changes by domain (APIs, UI, services, data); interface contracts and invariants
- Data model/migration impacts and safety plan (backfills, toggles, dual-writes if needed)
- Testing strategy (unit, integration, E2E) and non-functional checks (perf, security)
- Documentation updates (README, ADRs), and acceptance validations before merge
- Clear "definition of done" for each milestone
Return a sequenced plan tied to key files and verification steps.
```

What you’ll get:
- Sequenced change plan with key files, contracts, and migration notes
- Test and validation strategy mapped to artifacts and checkpoints
- Documentation updates list (ADRs/notes) with owners and timing

---

## 5) Risk and compliance lens

Prompt (single message):
```text
Assess risks and compliance requirements:
- Security/privacy risks (authN/Z, data classification, PII, secrets, logging)
- Regulatory/enterprise controls (approvals, reviews, change windows, audits)
- Operational risks (blast radius, rollback, incident playbooks)
- Compliance matrix: control → how we satisfy → when/where it’s evidenced
Provide a prioritized risk register with mitigations and owners.
```

What you’ll get:
- Prioritized risk register with mitigations, owners, and due-by milestones
- Compliance checklist mapped to concrete actions and evidence
- Rollback/contingency notes aligned to milestones

---

## 6) Optional deep dive: Architecture sketch

Prompt (single message):
```text
Produce a high-level architecture sketch for the planned system changes:
- Components, boundaries, and key flows (ingress → processing → persistence → egress)
- Sequence for the critical user/system journey we’ll impact
- Hotspots to watch (coupling, latency-sensitive paths, data contracts)
- Tradeoffs considered and open questions to track
Return a concise diagram and a page of notes for review.
```

What you’ll get:
- Simple diagram of components/boundaries and a key sequence
- Hotspots and tradeoffs with targeted follow-ups
- Open questions list with decision/owner suggestions

---

## Exit criteria and handoffs
- Approved charter (goals/non-goals, scope boundaries, metrics)
- Dependency map and critical path with owners and lead times
- WBS and milestone plan with entry/exit criteria and demo points
- Change plan with key files, contracts, migration approach, and tests
- Risk register and compliance checklist with mitigations and evidence owners
- Handoffs: planning bundle shared with delivery teams; ADRs drafted; next steps scheduled

---

## Quick reference

Prompt templates
```text
Charter: Draft a one-page charter with goals, non-goals, scope, stakeholders, constraints, risks; include measurable success criteria and open questions.

Dependencies: Map internal/external dependencies with owners, readiness, lead time; propose a critical path and blockers.

WBS/Milestones: Break into epics → stories/tasks with acceptance criteria, estimates, sequencing; define milestone entry/exit criteria and RACI.

Change plan: Outline code changes, interfaces, migrations, tests, docs; define definition-of-done and verification steps.

Risk/Compliance: Produce a prioritized risk register and compliance matrix with mitigations and evidence.

Architecture (optional): Provide a simple diagram and sequence for the critical flow, with hotspots and tradeoffs.
```

Developer-run verification (optional)
```bash
# Capture a planning baseline
git rev-parse HEAD

# Ensure workspace health before scheduling
pnpm check && pnpm build

# Tag approved plan (lightweight)
git tag -a plan/<name>-v1 -m "Approved plan"
```

---

## Closing note

Amp coordinates specialized sub-agents, performs targeted research, and generates diagrams and plans automatically from your prompts. It chooses the right tools under the hood and surfaces synthesized results only—not raw invocations or logs.
