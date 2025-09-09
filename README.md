# Amp SDLC Workflow Guides

[![Built with Amp](https://img.shields.io/badge/Built%20with-Amp-F34E3F?logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjQwMCIgdmlld0JveD0iMCAwIDE5IDE5IiBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjxwYXRoIGQ9Ik0zLjQxNTA4IDE3LjI5ODNMNy44ODQ4NCAxMi43NjUzTDkuNTExNDYgMTguOTQxMkwxMS44NzQ1IDE4LjI5NDlMOS41MjAxOCA5LjMyNzU4TDAuNjk1MjcgNi45Mzc0N0wwLjA2Njg2NCA5LjM1MTk5TDYuMTM5MjYgMTEuMDAxNUwxLjY4ODA2IDE1LjUyNzlMMy40MTUwOCAxNy4yOTgzWiIgZmlsbD0id2hpdGUiLz48cGF0aCBkPSJNMTYuMzA0NCAxMi4wNDM2TDE4LjY2NzUgMTEuMzk3M0wxNi4zMTMyIDIuNDMwMDNMNy40ODgyNCAwLjAzOTkyNDZMNi44NTk4NCAyLjQ1NDQ0TDE0LjMxMiA0LjQ3ODgxTDE2LjMwNDQgMTIuMDQzNloiIGZpbGw9IndoaXRlIi8+PHBhdGggZD0iTTEyLjkxMjYgMTUuNDkwMkwxNS4yNzU2IDE0Ljg0MzlMMTIuOTIxMyA1Ljg3NjU5TDQuMDk2MzkgMy40ODY0OEwzLjQ2Nzk5IDUuOTAxTDEwLjkyMDEgNy45MjUzN0wxMi45MTI2IDE1LjQ5MDJaIiBmaWxsPSJ3aGl0ZSIvPjwvc3ZnPgo=)](https://ampcode.com/)

A curated, prompt‑first set of developer‑facing guides for running enterprise SDLC tasks with Amp. These guides provide generalized templates that should be adapted to your specific repository and project context. They are repository‑agnostic, assume your repo contains an AGENTS.md with team conventions, and Amp selects tools automatically and returns synthesized results only.

## About these guides
- Consistent structure: Why this phase matters, Pre‑flight checklist, numbered sections with "Prompt (single message)" + "What you’ll get", Exit criteria, Quick reference, Closing note.
- Prompt‑first: natural‑language prompts; no repository paths (Amp infers the current workspace).
- Enterprise‑ready: oriented for monorepos, multiple services, manifests, CI/CD, and compliance.

## Start here
- Orchestrate end‑to‑end: [orchestrate-chain-end-to-end-workflows-guide.md](./sdlc-workflows/orchestrate-chain-end-to-end-workflows-guide.md)

## Directory structure

- discover/
  - [discover-explore-codebase-and-history.md](./sdlc-workflows/discover/discover-explore-codebase-and-history.md)
  - [discover-search-documentation-guide.md](./sdlc-workflows/discover/discover-search-documentation-guide.md)
  - [discover-onboard-and-learn-guide.md](./sdlc-workflows/discover/discover-onboard-and-learn-guide.md)
- design/
  - [design-plan-project-guide.md](./sdlc-workflows/design/design-plan-project-guide.md)
  - [design-develop-tech-specs-guide.md](./sdlc-workflows/design/design-develop-tech-specs-guide.md)
  - [design-define-architecture-guide.md](./sdlc-workflows/design/design-define-architecture-guide.md)
- build/
  - [build-implement-code-guide.md](./sdlc-workflows/build/build-implement-code-guide.md)
  - [build-write-and-execute-tests-guide.md](./sdlc-workflows/build/build-write-and-execute-tests-guide.md)
  - [build-create-commits-and-prs-guide.md](./sdlc-workflows/build/build-create-commits-and-prs-guide.md)
- deploy/
  - [deploy-automate-ci-cd-guide.md](./sdlc-workflows/deploy/deploy-automate-ci-cd-guide.md)
  - [deploy-configure-environments-guide.md](./sdlc-workflows/deploy/deploy-configure-environments-guide.md)
  - [deploy-manage-deployments-guide.md](./sdlc-workflows/deploy/deploy-manage-deployments-guide.md)
- support-and-scale/
  - [support-and-scale-debug-errors-guide.md](./sdlc-workflows/support-and-scale/support-and-scale-debug-errors-guide.md)
  - [support-and-scale-large-scale-refactor-guide.md](./sdlc-workflows/support-and-scale/support-and-scale-large-scale-refactor-guide.md)
  - [support-and-scale-monitor-usage-and-performance-guide.md](./sdlc-workflows/support-and-scale/support-and-scale-monitor-usage-and-performance-guide.md)

## How to use
1. Open the orchestrator guide and frame your mission with goals, scope, and success metrics.
2. Follow the phase guide(s) relevant to your task; adapt prompts to your repository context and paste as "single messages" and iterate.
3. Keep artifacts (maps, specs, tests, plans) in‑repo; link them in your PRs/issues.
4. Share your Amp thread with reviewers when useful; avoid pasting raw logs.

## Authoring standards (for contributors)
- Follow the shared format (Why, Pre‑flight, numbered sections with Prompt/What you’ll get, Exit criteria, Quick reference, Closing note).
- Use kebab‑case filenames; place guides in the appropriate phase subfolder.
- Keep links relative; update the orchestrator guide when adding/removing guides.
- Prompts must be repository‑agnostic; no explicit tool names, APIs, or tool‑call JSON.
- Optional Git/CLI commands are only for developer‑run verification, not Amp output.

## Notes
- Amp infers repository context from your IDE/CLI; prompts never include repo paths.
- Amp chooses tools automatically and surfaces synthesized results only.
