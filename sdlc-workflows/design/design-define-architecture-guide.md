# Design: Define Architecture with Amp

Use this prompt‑first workflow to map current systems, propose a target architecture, set NFR budgets, and de‑risk with focused spikes.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Aligns system boundaries with business domains and change cadence.
- Surfaces constraints early to avoid expensive rework.
- Establishes NFR budgets that guide implementation and operations.
- Documents decisions (ADRs) and risk mitigations.

## Pre‑flight checklist
- Inputs: goals, constraints (data residency/PII, compliance, cost, skills), workload model.
- Current‑state: services inventory, data stores, entry points, interfaces.
- NFR targets: latency/throughput, availability/SLOs, RTO/RPO, cost.
- Decision flow: stakeholders, approval criteria, ADR template/location.
- Safe branch: `git switch -c design-arch/<date>-<initials>`

---

## 1) Map the repo (current architecture signals)

Prompt (single message):
```text
Map the current architecture. Produce a component inventory, dependency graph, and C4 Context/Container
sketch (text). List interfaces and data stores. Call out smells (cycles, mixed concerns, shared state)
and hotspots (change/churn). Keep it concise and actionable.
```

What you’ll get:
- Component inventory and dependency overview
- C4‑style context/container sketches (text)
- Architecture smells and risk notes

---

## 2) Optional deep dive (boundary fitness)

Prompt (single message):
```text
Assess boundaries for cohesion/coupling, change frequency, ownership, runtime calls, and data authority.
Propose realignments (bounded contexts), event flows, and interfaces; note migration implications.
```

What you’ll get:
- Domain map and fitness scores
- Recommended boundary changes and event flows
- Migration outline with risks

---

## 3) Architecture proposal (components, boundaries, interfaces)

Prompt (single message):
```text
Propose a target architecture for <goal> under <constraints>. Define components/responsibilities, interfaces
(REST/gRPC/events) with versioning, communication patterns (sync/async, retries/backoff, timeouts,
circuit breakers, sagas), and infra choices (runtime/orchestration/persistence/messaging/caching/observability).
Include sequence diagrams (text) for critical flows and an options matrix with trade‑offs.
```

What you’ll get:
- Target architecture with components and contracts
- Critical path sequences and error handling strategies
- Options/trade‑offs with a recommendation

---

## 4) Non‑functional requirements (budgets and policies)

Prompt (single message):
```text
Convert NFRs into budgets: latency p95/p99, throughput (rps), availability, cost envelopes, RTO/RPO.
Propose capacity plan, backpressure/retry/circuit‑breaker policies, and observability requirements
(metrics/traces/logs, dashboards, alerts). Include security/privacy and compliance controls.
```

What you’ll get:
- NFR budgets with capacity plan
- Resilience policies and observability requirements
- Security/privacy/compliance controls at architecture level

---

## 5) Validation (spikes, risk matrix)

Prompt (single message):
```text
Define 2–4 spikes to test hardest assumptions (e.g., throughput, cross‑region latency, ordering).
Create a risk matrix (likelihood/impact/detectability) with mitigations, fallbacks, kill switches,
and rollout plans. Propose accept/reject criteria to gate implementation.
```

What you’ll get:
- Spike plan and success criteria
- Risk register with mitigations and rollout plans
- Gate criteria for implementation readiness

---

## Exit criteria and handoffs
- Architecture v1 approved with diagrams, interfaces, and decisions recorded
- NFR matrix with budgets and acceptance thresholds; SLOs and alerts defined
- Risk register and spike results documented; critical risks mitigated or time‑boxed
- Implementation backlog created (interfaces, migrations, infra, observability), with owners/milestones

---

## Quick reference

Prompt templates
```text
Map architecture: component inventory, dependency graph, C4 sketches, smells/hotspots.
Boundary fitness: cohesion/coupling, ownership, runtime calls, data authority; propose realignments.
Architecture proposal: components, interfaces, comms patterns, infra; sequences and options matrix.
NFR budgets: latency/throughput/availability/cost; capacity/resilience/observability.
Validation: spikes, risk matrix, mitigations, rollout, gate criteria.
```

Developer‑run verification (optional)
```bash
git switch -c design/architecture-v1
mkdir -p docs/adr diagrams && $EDITOR docs/adr/0001-architecture.md
git add docs diagrams && git commit -m "Architecture v1: proposal, NFRs, risks" && git push -u origin HEAD
```

---

## Closing note
Iterate quickly: map → propose → budget → validate → decide. Amp chooses tools automatically and returns synthesized results—no raw tool logs.
