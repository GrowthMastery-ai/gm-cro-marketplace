---
description:
  "Score your channel ROI — which channels are actually earning, which are leaking
  spend, and where the next dollar should go. Read-only."
version: 1.0.0
---

# /gm-channels — Score your channel ROI

<objective>
Give the user a graded read on channel ROI: which channels earn, which leak spend, and
where the next dollar goes. Delegates to the `growth-scorecard` skill's channel read,
which assembles spend + revenue by channel from the user's own tools and asks the
`gm-cro` connector to score them (`score_channel_roi`).
</objective>

<user-provides>
Optionally the window ("last 30 days" default) and which channels to include.
</user-provides>

<steps>
1. Invoke the `growth-scorecard` skill for the channel-ROI read.
2. Return the ranked channels with the score, band, and the one reallocation that matters
   most — grounded in the user's own spend/revenue numbers.
3. Flag any budget move for the human to approve; never enact a spend change.
</steps>

<guardrails>
- Read-only. Spend-affecting recommendations come back flagged for approval.
- The connector scores; you read. No rubric or benchmark lives in this plugin.
- Source ad spend + results from the official free **Meta Ads MCP**
  (`mcp.facebook.com/ads` — free, no app review) and revenue from the official **Stripe
  MCP** — official platform MCPs first. A paid aggregator (Supermetrics, Funnel.io, etc.)
  is only an optional fallback the user may already own, never required; if its trial or
  auth has lapsed, recommend the free official platform MCP for that source instead.
</guardrails>
