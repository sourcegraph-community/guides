# Discover: Explore Codebase and History with Amp

Use this prompt-first workflow to map your repository, locate the important landmarks, read recent history, and perform focused code reads—fast. It’s built for enterprise monorepos and multi-service setups where context density is high.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include the repository path in prompts.

## Why this phase matters
- Accelerates onboarding and de-risks early decisions with a shared mental model.
- Surfaces “center of gravity” codepaths (auth, routing, data) and implicit contracts.
- Highlights high‑churn, high‑risk areas from real history, not guesswork.
- Maps build/test commands and environments so changes land safely.
- Produces artifacts you can hand off to reviewers and adjacent teams.

## Pre‑flight checklist
- Access: Repo is cloned/readable; required registries, env vars, and allowlists are set.
- Context: `AGENTS.md` captures team conventions (commands, structure, naming). If missing or stale, ask Amp to propose a draft.
- Safe branch: `git switch -c explore/<date>-<initials>`
- Optional baseline: Ask Amp to snapshot a baseline repo map before large refactors.

---

## 1) Map the repo

Prompt (single message):
```text
Explore the current workspace and produce a high-level map for a monorepo:
- Top-level workspaces (apps/*, services/*, packages/*, tools/*), primary languages, frameworks
- Build/test/lint commands from manifests
- Entrypoints (CLI, servers, web), routing conventions, and config sources
- Data layer: ORMs, migrations, schema files, and seed locations
- CI basics and release/versioning signals
Assume common patterns like src/**/*.ts and server/index.*. Return a concise overview I can share.
```

What you’ll get:
- Inventory of workspaces and boundaries with key paths
- Language/framework breakdown and how builds/tests run
- Entrypoints, routing conventions, and configuration sources
- Data layer summary (schemas, migrations, seeds)
- CI/release notes and immediate risks or anomalies

---

## 2) Find the landmarks

Prompts (use individually or as a short sequence):

Auth boundary
```text
Identify the auth boundary:
- Where sessions/tokens are created, verified, and refreshed
- Middlewares/interceptors/guards and their order
- Key files and responsibilities with brief one-liners
Include paths under services/auth/** and apps/* that enforce auth at the edge.
```

Routing and endpoints
```text
Outline HTTP and RPC entrypoints:
- How routes are declared (files, decorators, routers) and matched
- The main server(s) and glue code
- Example paths with handlers and notable middleware
Focus on patterns like src/**/*.ts and server/**/*.*
```

Data schemas and migrations
```text
Locate data schemas and migrations:
- ORM(s) used and model locations
- Migration directories and the migration run command(s)
- Generated types and where they’re consumed
```

What you’ll get:
- A curated landmarks list: auth, routing, configs, schemas, migrations, feature flags
- Why each landmark matters, plus the minimal set of files to read first
- Pointers to cross‑cutting concerns (logging, metrics, error handling)

---

## 3) Read the history

Prompt (single message):
```text
Analyze recent history for stability and risk:
- Time window: last 90 days
- Focus paths: services/auth/**, apps/web/**, packages/shared/**, migrations/**
- Summarize change themes, hotspots, and high-churn files
- Flag notable incidents (outage, rollback, perf, security) and related PRs/issues if referenced
- Call out contributors who can review risky areas
Return a short narrative plus a table of hotspots with rationale.
```

What you’ll get:
- Narrative timeline of themes, spikes, and risky areas
- Hotspot table with paths, churn/rationale, and suggested next steps
- Pointers to commits/PRs/issues where relevant

Optional verification with Git (run from repo root):
```bash
# Limit to a path set and time window
git log --since="90 days ago" -- services/auth apps/web packages/shared migrations

# Top contributors for those paths
git shortlog -sn --since="90 days ago" -- services/auth apps/web packages/shared migrations

# Quick churn view
git diff --stat HEAD~200..HEAD -- services/auth apps/web packages/shared migrations | tail -n 20

# Recent tags/releases
git tag --sort=-creatordate | head -n 10
```

---

## 4) Read with intention

Prompt (single message):
```text
Perform an intentional read of the auth request lifecycle:
- Trace a request from ingress to handler to response
- Show where auth is enforced, errors are handled, and metrics are emitted
- Include file:line pointers for each hop and a brief sequence diagram
- Call out surprising dependencies or hidden coupling
Paths of interest: services/auth/**, packages/shared/http/**, apps/web/src/routes/**.
```

Focused reading outcomes:
- File-by-file walkthrough of the critical path with line anchors
- A simple sequence diagram that clarifies flow
- Specific follow-ups: tests to add, invariants to assert, docs to update

---

## 5) Optional deep dive (architectural assessment)

Prompt:
```text
Assess architecture fitness across boundaries:
- Identify coupling across apps/*, services/*, and packages/*
- Note layering violations and runtime-only vs build-time contracts
- Suggest 3–5 low-risk refactors and the first pragmatic steps
- Include quick wins for build/test/runtime performance
Return a crisp assessment (one page) with a prioritized plan.
```

---

## Exit criteria and handoffs
- Repo map captured and shareable (one page, links to key paths)
- Landmarks list (auth, routing, configs, schemas, migrations, flags) with why‑it‑matters
- History summary with hotspots and owners for review
- Intentional read artifacts (flow notes, file:line pointers, sequence sketch)
- Open questions and risks logged; next steps clarified (tests, docs, refactors)
- Optional: Update `AGENTS.md` with common commands, structure notes, and reading order

---

## Quick reference

Prompt templates
```text
Map: Explore the current workspace; produce a high-level map (workspaces, build/test, entrypoints, routing, config, data, CI).

Landmarks: List and explain auth, routing, config, schemas, migrations, and flags with key file paths.

History: Last 90 days on services/auth/** apps/web/** packages/shared/** migrations/**; themes, hotspots, incidents, reviewers.

Intentional read: Trace <critical-flow> end-to-end with file:line pointers and a simple sequence diagram.

Architecture: Boundary fitness, coupling, layering; 3–5 low-risk refactors with first steps.
```

Git (optional verification)
```bash
git log --since="30 days ago" -- src/**/*.ts
git shortlog -sn --since="30 days ago" -- src
git blame -C -M path/to/file.ts
git diff --stat HEAD~100..HEAD -- src
git tag --sort=-creatordate | head -n 10
```

---

## Closing note

Amp chooses tools automatically from your prompts and surfaces only synthesized results—not raw invocations or logs. Use the prompts above to drive end‑to‑end discovery, validate selectively with Git, and capture outcomes in `AGENTS.md` so the next engineer ramps even faster.
