# Support & Scale: Large‑Scale Refactor with Amp

Use this prompt‑first workflow to restructure code safely, preserve behavior, and ship value in small, reversible slices.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Eliminates structural debt without breaking external behavior.
- Improves team throughput by reducing coupling and cognitive load.
- Unlocks performance and reliability improvements.
- De‑risks big moves with flags, shims, and phased rollout.

## Pre‑flight checklist
- Goals/non‑goals and invariants; “no behavior change” principle explicit.
- Baselines: perf, error rate, build times, test pass rates.
- Safety nets: golden tests, contract tests, snapshots, smoke suites.
- Target boundaries and layering rules; adapters/shims/dual‑writes as needed.
- Branching: trunk‑based slices with reversible steps; rollback path per slice.

---

## 1) Map the repo (boundaries, coupling)

Prompt (single message):
```text
Map modules and dependencies; highlight cycles, high fan‑in/out, and risky edges. Propose cohesive
boundaries and layering rules with fan‑in/out counts. Identify seams for safe slicing.
```

What you’ll get:
- Boundary map with coupling hotspots
- Suggested layering rules and seams
- First safe slice candidates

---

## 2) Read the history (hotspots, churn)

Prompt (single message):
```text
Analyze commit history for top churn files/change clusters. Flag modules with repeated bug‑fixes, large
diffs, or frequent reversions. Correlate to incidents and test flakiness.
```

What you’ll get:
- Churn and defect heatmap
- Risky modules and anti‑patterns
- Reviewer/owner suggestions

---

## 3) Plan the change (phasing, flags, safety nets)

Prompt (single message):
```text
Propose a 3–5 phase refactor plan. Each phase should be small, reversible, and independently valuable.
Include flags/shims/adapters, test additions (golden/contract), rollback steps, exit criteria, and risks.
```

What you’ll get:
- Phased plan with flags/shims and tests
- Explicit rollback per phase
- Exit criteria that preserve behavior

---

## 4) Implement (incremental, reversible steps)

Prompt (single message):
```text
Generate mechanical steps (rename/move/codemod) first, then parity integrations. Update call sites in
slices and provide a checklist per slice with validation gates. Keep PRs small with clear messages.
```

What you’ll get:
- Codemods/adapters and updated call sites
- Checklists and gates per slice
- Small PRs with clear intent

---

## 5) Validate (tests, perf, smoke)

Prompt (single message):
```text
Create a validation matrix: targeted tests for changed areas, contract tests for new seams, golden outputs,
and quick perf checks. Summarize any diffs and likely root causes. Propose fixes or rollbacks.
```

What you’ll get:
- Validation matrix and results
- Diff explanations with root‑cause hypotheses
- Fixes or rollback recommendations

---

## Exit criteria and handoffs
- Behavior parity proven; golden tests unchanged
- Builds green; targeted + full tests pass; no new critical alerts
- Perf baselines at or better than pre‑refactor
- Boundaries documented; layering/dependency rules enforced
- Temporary flags cataloged with removal plan and owners

---

## Quick reference

Prompt templates
```text
Boundaries: map dependencies, cycles, fan‑in/out; propose seams and layering rules.
History: identify churn and defect hotspots; correlate to incidents/tests.
Plan: 3–5 phased refactor with flags/shims, tests, rollback, exit criteria.
Implement: codemods/adapters; call‑site updates; checklists/gates; small PRs.
Validate: targeted/contract/golden/perf; summarize diffs and fixes.
```

Developer‑run verification (optional)
```bash
git switch -c refactor/<area>
```

---

## Closing note
Favor simplicity, crisp boundaries, and reversible steps. Amp chooses tools automatically and returns synthesized results—not raw logs.
