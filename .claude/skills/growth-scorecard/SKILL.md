---
name: growth-scorecard
description:
  Use to produce the weekly growth read — overall growth score, channel ROI, and the
  single prioritized next move. Assembles the snapshot from the user's own tools and
  asks the GrowthMastery CRO Engine to score it. Invoke for "weekly scorecard", "how's
  growth", "score my channels", "what's my next move", or /gm-scorecard, /gm-channels,
  /gm-next-move.
---

# The Growth Scorecard

## Overview

You assemble the user's weekly growth read: overall growth score, channel ROI, and the
one prioritized next move — the ritual a CRO would bring each week. You are on rails:
you build the snapshot from the user's own data and ask the `gm-cro` connector to score
it. The scoring, benchmarks, and prioritization logic stay server-side. There is **no
rubric in this skill**.

## When to Use

- The weekly ritual read, or `/gm-scorecard`.
- Just the channel-ROI read (`/gm-channels`) or just the next move (`/gm-next-move`).
- When the seeded Growth Project or the revenue-manager agent needs the current read.

## The Method

### Step 1 — Assemble the snapshot (the user's own numbers)

From the user's own connectors, build the window's snapshot (default last 7 days):
growth metrics (leads, sales, revenue, trend), spend + revenue **by channel**, and the
funnel context from a recent `diagnose-funnel-leak` read if one exists. Counts, spend,
and revenue only — no PHI/PII.

**Prefer the official free platform MCP for every source.** Ad spend + results should
come from the official **Meta Ads MCP** (`mcp.facebook.com/ads` — free, no app review),
funnel/stage numbers from the official **GoHighLevel MCP**, revenue from the official
**Stripe MCP**, and traffic from the **YouTube/GA MCP** where available. A paid
third-party aggregator (Supermetrics, Funnel.io, etc.) is only an optional fallback the
user may already own — never required. If a source is behind an aggregator whose trial
or auth has lapsed (e.g. an expired Supermetrics trial), recommend adding the free
official platform MCP for that source rather than renewing the aggregator.

### Step 2 — Ask the Engine to score

Call the connector tools for the read the user asked for:

- **`gm-cro › score_growth`** — overall growth score + band.
- **`gm-cro › score_channel_roi`** — ranked channel ROI (read-only).
- **`gm-cro › prioritize_next_move`** — the single `priority: 1` next move across the
  assembled context.

Each returns ONLY the graded envelope — score/band/findings/recommendations — never the
formula or benchmark table.

### Step 3 — Render the scorecard

Use `templates/scorecard.md` as the layout:

1. **Growth score + band** — the headline read.
2. **Channels** — the ranked ROI and the one reallocation that matters.
3. **Your one next move** — the `priority: 1` recommendation, its rationale, and what
   it's worth, grounded in the returned evidence.

Close with the single most important thing to do this week.

## Guardrails

- The Engine scores; you assemble and present. No rubric or benchmark lives in this
  skill.
- Spend-affecting moves come back flagged `requiresApproval: true` — surface them for
  the human to decide; never enact a spend change.
- If a tool returns `degraded: true`, full scoring is being set up on our side: present
  the retained-history reassurance + the warm handoff (`/gm-concierge`), never a crash.
- Never send PHI/PII to the connector.
