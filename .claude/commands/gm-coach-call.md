---
description:
  "Coach your last sales call — a graded read on what worked, what leaked, and the one
  thing to change on the next call. De-identified before it leaves your machine."
version: 1.0.0
---

# /gm-coach-call — Coach a sales call

<objective>
Turn a call transcript into a graded coaching read: what worked, where the deal leaked,
and the single highest-leverage change for the next call. Delegates to the
`coach-sales-call` skill, which de-identifies the transcript in the user's own
environment and asks the `gm-cro` connector to grade the de-identified call features.
</objective>

<user-provides>
A call transcript or recording notes (the skill de-identifies before any connector call).
</user-provides>

<steps>
1. Invoke the `coach-sales-call` skill.
2. Return the read: the grade and band, the biggest moment that moved (or lost) the deal,
   and the one change to make next time — grounded in the returned evidence.
3. Keep the rep on top: this is a sparring partner, not a script to read verbatim.
</steps>

<guardrails>
- **Never send PHI/PII to the connector.** De-identify in the user's own environment first;
  the server-side detector is only a backstop.
- The connector grades; you coach. No rubric lives in this plugin.
</guardrails>
