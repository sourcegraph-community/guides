# Orchestrate: Chain End‑to‑End Workflows with Amp

Use this prompt‑first workflow to run your SDLC as a single thread: set goals, map phases, parallelize safely, drive daily execution, enforce gates, and hand off cleanly.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Reduces context switching by chaining phase guides into one plan.
- Aligns owners on artifacts, gates, and decision timelines.
- Produces a predictable cadence with traceable evidence.
- Scales across teams and repos with consistent prompts.

## Pre‑flight checklist
- Conventions: `AGENTS.md` reflects naming, branches, CI gates, and review policy.
- Access: repo, logs/artifacts, non‑prod secrets, and approved deploy targets.
- Thread sharing: share the orchestration thread with stakeholders; set visibility.
- Safe branch: work on a non‑default branch; define PR policy and merge gates.
- Quality gates: definitions‑of‑done per phase (tests, coverage, security, compliance, approvals).

---

## 1) Frame the mission (goals, scope, success metrics)

Prompt (single message):
```text
Frame the mission for <project> end-to-end across the SDLC.
Include goals, in-scope/out-of-scope, stakeholders, success metrics (leading/lagging),
key risks, assumptions to validate, and a 2-sprint milestone sketch.
Reflect our conventions in AGENT(S).md. Ask 3 clarifying questions if anything’s fuzzy.
```

What you’ll get:
- Mission brief with scope and success metrics
- Assumptions, risks, and open questions to resolve
- Near‑term milestones aligned to conventions

---

## 2) Compose the chain (phases → artifacts, dependencies, owners)

Prompt (single message):
```text
Create a phase→artifact map for discover, design, build, test, deploy, and support.
For each artifact: owner, inputs/outputs, dependency gates, acceptance criteria, and verification.
Include handoffs between phases and links to relevant workflow guides by filename.
Propose a 10–15 step execution plan.
```

What you’ll get:
- Chain map of phases, artifacts, dependencies, and owners
- Acceptance and verification per artifact
- Execution plan with explicit handoffs

---

## 3) Parallelize safely (what runs concurrently; gates)

Prompt (single message):
```text
Identify tasks that can run in parallel without violating dependencies.
Define serialization points (gates), interim reviews, and rollback checkpoints.
Tag each stream with risk level and evidence required to pass the next gate.
Propose a daily sync posture to keep streams aligned.
```

What you’ll get:
- Concurrency map with clear gates and checkpoints
- Risk‑labeled streams and rollback points
- Sync pattern to keep streams coordinated

---

## 4) Drive execution (daily loop, status, blockers, next steps)

Prompt (single message):
```text
Daily loop: summarize status since last check-in, blockers, decisions needed,
next 24h steps, changes to plan, and owner-specific nudges.
If risks change, update the chain map and propose mitigations.
Keep it actionable and under 10 bullets.
```

What you’ll get:
- Concise, actionable daily status
- Prioritized next steps and owner prompts
- Continuously updated plan with risk deltas

---

## 5) Quality gates & compliance (across phases)

Prompt (single message):
```text
Run cross-phase quality gates aligned to AGENT(S).md: code quality, tests/coverage,
security/dependency rules, change control, and audit trail.
Report pass/fail with evidence, list exceptions, and propose fixes with effort estimates.
Flag anything that needs formal approval before advancing.
```

What you’ll get:
- Gate results with evidence and exception list
- Remediation plan with estimated effort
- Clear approvals required to proceed

---

## 6) Close & handoff (bundle artifacts)

Prompt (single message):
```text
Bundle the closeout: mission brief, designs/specs, PR list, test evidence, release notes,
known issues, rollback/runbook, and acceptance sign-offs.
Create a lightweight handoff summary for downstream ops/support and link all artifacts.
```

What you’ll get:
- Tidy release/handoff bundle with links
- Acceptance sign‑offs and support‑ready runbook
- Traceable record of decisions and evidence

---

## Exit criteria and handoffs
- Chain map complete; phases have owners, artifacts, and gates
- Daily loop stabilized; high‑risk uncertainties resolved or time‑boxed
- All gates passed with evidence; exceptions addressed or accepted
- Handoff bundle published with links and clear next‑team ownership
- Retro items captured for next iteration

---

## Quick reference

Prompt templates
```text
Mission: goals, scope, success metrics, assumptions/risks, 2-sprint milestones; align to AGENT(S).md.
Chain: discover→design→build→test→deploy→support; owners, artifacts, dependencies, acceptance, handoffs.
Parallelize: safe concurrency; gates, interim reviews, rollbacks, sync cadence.
Execute (daily): status, blockers, decisions, next 24h, plan deltas, owner nudges.
Quality: gates (quality, tests, security, change control). Evidence, exceptions, remediations, approvals.
Close: bundle mission, specs, PRs, tests, notes, issues, rollback/runbook, sign-offs; publish links.
```

Developer‑run verification (optional)
```bash
git branch --show-current
git status -s
pnpm check && pnpm build
pnpm -C core test --run --no-color
```

### SDLC workflow guides (relative links)
- [discover-explore-codebase-and-history.md](./discover/discover-explore-codebase-and-history.md)
- [discover-search-documentation-guide.md](./discover/discover-search-documentation-guide.md)
- [discover-onboard-and-learn-guide.md](./discover/discover-onboard-and-learn-guide.md)
- [design-plan-project-guide.md](./design/design-plan-project-guide.md)
- [design-develop-tech-specs-guide.md](./design/design-develop-tech-specs-guide.md)
- [design-define-architecture-guide.md](./design/design-define-architecture-guide.md)
- [build-implement-code-guide.md](./build/build-implement-code-guide.md)
- [build-write-and-execute-tests-guide.md](./build/build-write-and-execute-tests-guide.md)
- [build-create-commits-and-prs-guide.md](./build/build-create-commits-and-prs-guide.md)
- [deploy-automate-ci-cd-guide.md](./deploy/deploy-automate-ci-cd-guide.md)
- [deploy-configure-environments-guide.md](./deploy/deploy-configure-environments-guide.md)
- [deploy-manage-deployments-guide.md](./deploy/deploy-manage-deployments-guide.md)
- [support-and-scale-debug-errors-guide.md](./support-and-scale/support-and-scale-debug-errors-guide.md)
- [support-and-scale-large-scale-refactor-guide.md](./support-and-scale/support-and-scale-large-scale-refactor-guide.md)
- [support-and-scale-monitor-usage-and-performance-guide.md](./support-and-scale/support-and-scale-monitor-usage-and-performance-guide.md)

---

## Closing note
Amp chooses the right tools automatically and infers your workspace context. Keep prompts natural and outcome‑focused—the orchestration follows.
