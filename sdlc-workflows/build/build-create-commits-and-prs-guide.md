# Build: Create Commits and PRs with Amp

Use this prompt‑first workflow to plan atomic commits, prepare a clear PR narrative, and keep changes safe and reviewable.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Improves traceability with clear intent and scope per commit.
- Speeds reviews and reduces defects with focused diffs.
- Enforces git hygiene and avoids leaking secrets or generated files.
- Aligns with branch protections and CI requirements.

## Pre‑flight checklist
- Branching: `feature|fix|chore/<scope>-<short-desc>` from correct base.
- Sync: local up to date with remote; no unresolved merges.
- Permissions: can push and open PRs; required checks and approvals known.
- Context: linked issue/ticket; CODEOWNERS/merge strategy understood; PR template ready.
- Local health: lint/typecheck/tests pass; no generated/large binaries staged.

---

## 1) Read the history (reviewers, hotspots)

Prompt (single message):
```text
Summarize recent changes to <paths>, note hotspots and common failure modes, and suggest likely reviewers
by contributions and ownership. Keep it short and actionable.
```

What you’ll get:
- Context for touched areas and risky patterns
- Suggested reviewers and owners
- Notes on reverts/flaky tests to watch

---

## 2) Plan the change (commit granularity, messages)

Prompt (single message):
```text
Propose 3–5 atomic commits for <change>. Use Conventional Commits in titles and write concise bodies.
Draft the PR narrative: problem, approach, alternatives, impact, rollout, validation. Include test notes.
```

What you’ll get:
- Commit plan with titles/bodies
- PR storyline ready to paste
- Validation notes to include

---

## 3) Implement (stage diffs, summarize changes)

Prompt (single message):
```text
Stage only relevant hunks for commit 1 (<scope>). Summarize the diff and generate a commit message
with scope, rationale, and bullets. Repeat per commit. Keep unrelated edits out.
```

What you’ll get:
- Readable diff summaries for each commit
- Commit messages aligned to scope and rationale
- Clean staging without noise

---

## 4) Validate (local checks)

Prompt (single message):
```text
Run local checks (format/lint/typecheck/tests) and summarize failures with minimal repros. Recommend minimal
additional tests for new behavior if any.
```

What you’ll get:
- Local pass/fail evidence and fixes
- Targeted test additions if needed
- Confidence before pushing

---

## 5) Risk & compliance (git hygiene, no secrets)

Prompt (single message):
```text
Scan staged changes for secrets and generated files. Flag policy risks and propose mitigations.
Confirm branch protections are satisfied.
```

What you’ll get:
- Secret/generated file scan results
- Policy risk summary and mitigations
- Confidence gates before PR

---

## Exit criteria and handoffs
- Small, self‑contained commits with conventional titles and clear bodies
- PR has accurate title/summary (problem, approach, validation, risks); evidence attached
- Reviewers/labels/milestone set; links to issue/ticket; rollout/backout noted
- Local checks green; CI green or clear plan to fix

---

## Quick reference

Prompt templates
```text
History: review recent changes to <paths>, hotspots, failure modes, reviewers.
Commit plan: 3–5 atomic commits with titles/bodies; PR narrative.
Stage + summarize: commit by commit diff summary and message.
Validate: run checks; summarize failures; minimal repros; test additions.
Risk: scan for secrets/generated files; branch protections status and risks.
```

Developer‑run verification (optional)
```bash
# Branch and sync
git branch --show-current && git fetch origin && git rebase origin/main

# Stage, verify, commit
git add -p && git diff --staged && git commit -m "feat(<scope>): short summary"

# Push and open PR
git push -u origin HEAD
```

---

## Closing note
Favor small, intentional commits and PRs with crisp narratives. Amp chooses tools automatically and returns synthesized results—not raw logs.
