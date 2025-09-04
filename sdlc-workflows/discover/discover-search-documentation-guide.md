# Discover: Search Documentation with Amp

Use this prompt‑first workflow to inventory, evaluate, and align documentation across your workspace, then plan targeted improvements.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Establishes a single source of truth before changes begin.
- Surfaces stale or duplicative docs and missing coverage.
- Connects documentation to real business flows and code ownership.
- Produces a prioritized plan to fix gaps quickly.

## Pre‑flight checklist
- Access: You can read docs, specs, ADRs, runbooks, onboarding, and release notes.
- Context: `AGENTS.md` reflects naming, ownership, and documentation conventions.
- Safe branch: `git switch -c discover-docs/<date>-<initials>`
- Optional baseline: Ask Amp to snapshot a current documentation map.

---

## 1) Map the repo (doc surface inventory)

Prompt (single message):
```text
Map documentation across this workspace: READMEs, design docs, ADRs, API specs, runbooks,
onboarding, manuals, and release notes. Group by purpose, owner, last update, freshness risk,
and related code areas. Return a concise overview and prioritized review targets.
```

What you’ll get:
- Inventory of doc surfaces with purpose, owner, and freshness signals
- Doc density heatmap and suspected staleness by area
- Missing categories (e.g., runbooks for critical services)
- Quick‑win candidates for immediate cleanup

---

## 2) Find the landmarks (manuals, API specs, runbooks, onboarding)

Prompt (single message):
```text
From the inventory, list authoritative landmarks: manuals, API references, ADRs, incident/runbooks,
onboarding guides, style/conventions, and release notes. Rank by authority and freshness.
Explain how they interlink and where duplicates/conflicts exist.
```

What you’ll get:
- Curated “Landmarks” set with authority and freshness scores
- Relationship map among manuals, specs, ADRs, and runbooks
- Conflicts and duplications called out with suggested resolution
- Coverage gaps for onboarding and operations

---

## 3) Read the history (doc churn, gaps, skew)

Prompt (single message):
```text
Analyze documentation history for the last 6–12 months. Identify churn hotspots, long‑stale or
orphaned docs, and places where code changed but docs did not. Summarize by subsystem with risk
scores and examples.
```

What you’ll get:
- Churn hotspots by area with trendlines and examples
- Stale docs and “code‑docs skew” candidates
- Releases/PRs that implied updates but lack doc changes
- A prioritized review list for high‑risk topics

---

## 4) Read with intention (trace a business flow)

Prompt (single message):
```text
Trace the “<business flow>” across current documentation. Extract steps, inputs/outputs, key
APIs/schemas, queues/topics, SLAs, and handoffs. Call out contradictions, missing steps, or
ambiguous terms. Provide a concise narrative with cited sources.
```

What you’ll get:
- End‑to‑end flow summary with handoffs and SLAs
- API/schema list tied to the flow with current vs implied behavior
- Contradictions and ambiguities highlighted with sources
- Open questions and owners to resolve them

---

## 5) Plan the change (doc gaps, owners, next steps)

Prompt (single message):
```text
Create a documentation improvement plan. For each gap, propose the smallest effective fix, the
owner (per our team conventions), acceptance criteria, and review workflow. Organize into quick
wins (<1h), near‑term (1–2 days), and follow‑ups. Include follow‑up prompts for execution.
```

What you’ll get:
- Prioritized backlog with owners and acceptance criteria
- Draft outlines for new or updated docs
- Review checklist and suggested approval path
- Risks, dependencies, and a 2‑week schedule

---

## Exit criteria and handoffs
- Landmarks list agreed, with owners and freshness status
- Flow narrative with contradictions/open questions documented
- Improvement backlog prioritized with quick wins scheduled
- Risk summary tying code churn to doc quality
- Handoff to the relevant phase (Explore/Design) with next‑step prompts

---

## Quick reference

Prompt templates
```text
Inventory docs with freshness and ownership; produce prioritized review targets.

Identify authoritative manuals, API references, ADRs, runbooks, onboarding; rank by authority and freshness.

Show doc churn vs code changes over 6–12 months; flag skew and stale docs with examples.

Trace “<business flow>” end‑to‑end across docs; list steps, APIs, SLAs, contradictions, and missing pieces.

Propose a doc improvement plan with owners, acceptance criteria, and a 2‑week schedule.
```

Developer‑run verification (optional)
```bash
# Count documentation files
git ls-files '*.{md,mdx,adoc,rst,svx,txt}' | wc -l

# Doc churn and staleness signals
git log --since=180.days --name-only --pretty=tformat: \
| grep -E '\\.(md|mdx|adoc|rst|svx|txt)$' | sort | uniq -c | sort -nr | head -20

git grep -niE 'deprecated|outdated|stale|todo|tbd|draft|wip|not maintained' -- '*.md*' '*.adoc' '*.rst' '*.svx' '*.txt'
```

---

## Closing note
Amp chooses tools automatically from your prompts and surfaces synthesized results—not raw invocations or logs. Keep prompts outcome‑focused; Amp infers the current workspace from your CLI/IDE context.
