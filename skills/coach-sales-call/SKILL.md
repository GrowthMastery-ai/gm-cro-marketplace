---
name: coach-sales-call
description:
  Use to coach a sales call — grade what worked, where the deal leaked, and the one
  change for the next call. De-identifies the transcript in the user's own environment
  BEFORE any connector call. Invoke for "coach my last call", "review this call", or
  /gm-coach-call.
---

# Coach the Sales Call

## Overview

You turn a call transcript into a graded coaching read — what worked, where the deal
leaked, and the single highest-leverage change for the next call. You are on rails: you
de-identify the transcript in the user's own environment, then ask the `gm-cro`
connector to grade the **de-identified call features**. The grading rubric stays
server-side. There is **no rubric in this skill**.

## When to Use

- "Coach my last call" / "review this call" / "where did I lose that deal?"
- After a sales or discovery call, or when a rep wants to prep the next one.
- When `/gm-coach-call` is run.

## The Method

### Step 1 — De-identify in the user's own environment (required)

Before anything leaves the machine, strip names, emails, phone numbers, and any PHI/PII
from the transcript. See `references/deidentify.md` for the checklist. The connector's
server-side detector is only a backstop — the de-identification happens here, first.

### Step 2 — Ask the Engine to grade

Call **`gm-cro › grade_call`** with the de-identified call features. It returns ONLY the
graded read — the score/band, the moments that moved the deal, and the coaching
recommendation with evidence — never the scoring formula.

### Step 3 — Coach

1. **The grade + band** as context.
2. **The moment that mattered** — the biggest point that moved (or lost) the deal.
3. **The one change** — the `priority: 1` recommendation for the next call, grounded in
   its evidence.

See `references/reading-the-grade.md` for how to read the returned envelope.

## Guardrails

- **Never send PHI/PII to the connector.** De-identify first; the server detector is a
  backstop only.
- The Engine grades; you coach. This is a sparring partner, not a script to read
  verbatim.
- No rubric or scoring constant lives in this skill — only the call to `gm-cro`.
