# Support & Scale: Monitor Usage & Performance with Amp

Use this prompt‑first workflow to instrument key journeys, set SLIs/SLOs, trace bottlenecks, and wire actionable alerts.

Note: Run Amp from your repo root (CLI) or open the workspace in your IDE; there’s no need to include repository paths in prompts.

## Why this phase matters
- Proves critical paths meet expectations under real load.
- Turns runtime signals into actionable backlog items.
- Controls cost and data noise before they grow.
- Keeps on‑call focused on decisions, not noise.

## Pre‑flight checklist
- Journeys: top 2–3 flows named, sketched, and agreed.
- Golden signals: latency, traffic, errors, saturation defined in plain terms.
- Data hygiene: PII policy, redaction rules, retention windows.
- Change window: thresholds, alert routes, and on‑call alignment.

---

## 1) Find the landmarks (metrics, tracing, logs)

Prompt (single message):
```text
Audit observability coverage. For <service>, instrument RED (Requests/Errors/Duration) and USE
(Utilization/Saturation/Errors) where applicable. Add spans for <journey>, propagate IDs end‑to‑end,
and convert logs to structured with redaction. Return a short coverage delta report.
```

What you’ll get:
- Metrics map for endpoints/resources
- Trace design across async boundaries
- Structured logging with redaction

---

## 2) Plan the change (SLIs/SLOs, thresholds)

Prompt (single message):
```text
Propose SLIs/SLOs for <journey>. Include targets/windows, burn‑rates (fast/slow), alert thresholds,
and rationale. Set cardinality and ingestion budgets, storage retention per data class, and sampling strategy.
```

What you’ll get:
- SLIs/SLOs with error budgets
- Alert policies and routing
- Data cardinality and retention budgets

---

## 3) Read with intention (trace critical journeys)

Prompt (single message):
```text
Trace <journey> end‑to‑end and attribute time to self vs children. Flag N+1s, chatty calls, cold starts.
List top 5 bottlenecks with proposed fixes and expected impact.
```

What you’ll get:
- Journey profile and hot spans by self‑time
- Bottlenecks and proposed fixes
- Quick‑win opportunities

---

## 4) Validate (dashboards, alerts, load smoke)

Prompt (single message):
```text
Create dashboards for RED/USE and error budgets; link traces/logs by ID. Add actionable alerts with
runbook links. Test with a small load smoke; observe burn‑rate behavior and alert dedupe.
```

What you’ll get:
- Dashboards and alerting wired
- Load smoke results and tuning
- Runbook linkage for on‑call

---

## 5) Risk & compliance (retention, PII)

Prompt (single message):
```text
Review observability data for PII/tenant leakage. Add redaction rules and retention settings.
Propose least‑privilege access controls and audit for reads/exports.
```

What you’ll get:
- PII and retention posture verified
- Access controls and audit recommendations
- Multitenancy guardrails

---

## Exit criteria and handoffs
- Dashboards show stable RED/USE; traces exist for key journeys; logs correlated
- SLOs approved; alerts tested and routed with runbooks
- PII redaction verified; retention and access documented; audit trail enabled
- Bottlenecks triaged into backlog with owners/impact

---

## Quick reference

Prompt templates
```text
Landmarks: audit metrics/traces/logs; instrument RED/USE; add spans; structured logs with redaction.
SLOs: targets/windows; burn‑rates; thresholds; routing; budgets.
Trace: profile <journey>; top spans by self‑time; top 5 bottlenecks with fixes.
Validate: dashboards; alerts; runbooks; load smoke and tuning.
Compliance: PII redaction, retention, access controls, audit.
```

Developer‑run verification (optional)
```bash
# Quick sanity on a health endpoint
printf "GET /healthz\n\n" | nc <host> <port> || true
```

---

## Closing note
Treat observability as a product: instrument with intent, set budgets, validate with load, and wire alerts to decisions—not noise. Amp chooses tools automatically and returns synthesized results—not raw logs.
