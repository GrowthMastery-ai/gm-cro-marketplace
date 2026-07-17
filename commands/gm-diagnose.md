---
description:
  "Find the single biggest leak in your funnel — the one stage-to-stage drop costing the
  most revenue right now — and name the one highest-leverage fix."
version: 1.0.0
---

# /gm-diagnose — Where you're losing the most money

<objective>
Name the user's biggest funnel leak and the single fix that moves revenue most — not a
list of ten things, the ONE. Delegates to the `diagnose-funnel-leak` skill, which
assembles the funnel snapshot from the user's own tools and asks the `gm-cro` connector
to rank the leaks against vertical benchmarks (the benchmarks stay server-side).
</objective>

<user-provides>
Optionally the window ("last 30 days" default) and which funnel, if they run more than
one.
</user-provides>

<steps>
1. Invoke the `diagnose-funnel-leak` skill. On the CRO's FIRST run (knowledge files still
   `{{PLACEHOLDER}}`), it autoloads the business first via `context-autoload` — sweeping the
   user's own connected sources read-only, filling the knowledge files, and presenting
   "here's your business as I understand it — correct me" before diagnosing.
2. Return the read in plain English: the dominant stage-to-stage drop, the one fix, and
   what it's worth in revenue at risk (using the user's own numbers).
3. **Record the diagnosis in the growth graph** (fail-open — never block the user on
   this): call `mcp__gm-cro__ingest_turn` once with
   `{"session_id": "<this session id>", "event": "Stop", "session_role": "cro",
   "intent": "gm-diagnose funnel read", "action_summary": "<one de-identified line:
   which stage leaked + the named fix>", "entity_refs": {"journey_signal": "diagnose"}}`.
   The `journey_signal` marker is what roots the user's journey step — include it
   exactly. If the ingest fails, keep helping; never surface the failure.
4. Offer `/gm-next-move` to sequence the fix, or `/gm-scorecard` for the full weekly read.
</steps>

<guardrails>
- Diagnose from the user's own data; the connector ranks. Never invent a benchmark.
- Spend-affecting fixes come back flagged for approval — surface them, never enact them.
- No rubric or benchmark constant lives in this plugin.
</guardrails>
