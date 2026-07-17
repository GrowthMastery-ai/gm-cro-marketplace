---
name: diagnose-funnel-leak
description:
  Use to find the single biggest leak in the user's funnel — the one stage-to-stage drop
  costing the most revenue right now. Pulls funnel counts + spend + revenue from the
  user's own tools and asks the GrowthMastery CRO Engine to rank the leaks. Invoke for
  "where am I losing people", "diagnose my funnel", or /gm-diagnose.
---

# Diagnose the Funnel Leak

## Overview

You find the user's **biggest** funnel leak and name the single highest-leverage fix —
not a list of ten things, the ONE that moves revenue most. You are on rails: you
assemble the funnel snapshot from the user's own data and ask the `gm-cro` connector to
rank the leaks against vertical benchmarks. The benchmarks and the leak-ranking logic
stay server-side. There is **no rubric in this skill**.

## When to Use

- "Where am I losing the most people / money?"
- Weekly funnel review, or when conversion feels off.
- When `/gm-diagnose` is run, or the seeded Growth Project needs a leak read.

## The Method

### Step 0 — First run: autoload the business before you diagnose

**Before you assemble any snapshot, check whether you already know this business.** Read
the knowledge files at `project/knowledge/` (`brand.md`,
`offer.md`, `icp.md`, `funnel-math.md`). If they still hold `{{PLACEHOLDER}}` values —
i.e. this is the CRO's first run for this user — **invoke the `context-autoload` skill
first**. It sweeps whichever of the user's OWN connected sources exist (detected via
ToolSearch — Google Drive, Gmail, Calendar, GoHighLevel/CRM, Stripe, Fathom; never
assumed), fills the knowledge files itself, seeds the decision log, ingests a
de-identified business snapshot to the growth graph, and presents the "here's your
business as I understand it — correct me" moment. That is what makes the CRO feel like
it already knows the user, instead of a blank cursor.

If the user would rather bring their existing claude.ai context, offer
`/gm-import-claude` (the `import-claude-export` skill) as the alternative first-run path
— they export their claude.ai data and the CRO distills their durable context from it.

If the knowledge files are already filled with real values, skip the autoload — you
already know the business — and go straight to Step 1.

### Step 1 — Assemble the funnel snapshot (the user's own numbers)

From the user's own connectors, build an ordered stage list for the window the user
asked about (default last 30 days). **Prefer the official free platform MCP for every
source** — funnel/stage counts from the official **GoHighLevel MCP**, revenue from the
official **Stripe MCP**, ad spend + results from the official **Meta Ads MCP**
(`mcp.facebook.com/ads` — free, no app review), and traffic from the **YouTube/GA MCP**
where available. A paid aggregator (Supermetrics, Funnel.io, etc.) is only an optional
fallback the user may already own — never required; if its trial or auth has lapsed,
recommend the free official platform MCP for that source instead of renewing it:

```jsonc
{
  "stages": [
    { "name": "lp_view", "count": 10000 },
    { "name": "optin", "count": 1800 },
    { "name": "booking", "count": 220 },
    { "name": "show", "count": 150 },
    { "name": "sale", "count": 28 },
  ],
  "spend_cents": 1200000,
  "revenue_cents": 7000000,
}
```

Use the stage names the user actually runs. No identifiers are needed — these are
counts, spend, and revenue only (no PHI/PII).

### Step 2 — Ask the Engine to rank the leaks

Call **`gm-cro › analyze_funnel`** with the snapshot plus the user's vertical/currency
context (pull the vertical from the seeded Growth Project if set). It returns ONLY the
graded read — the ranked leak, the fix, and the evidence — never the benchmark table or
the ranking formula.

### Step 3 — Name the leak and the one fix

1. **The read** — which stage-to-stage drop is the dominant leak.
2. **The one fix** — the `priority: 1` recommendation, grounded in its evidence (the
   user sees "4% vs 12% benchmark", not a threshold).
3. **What it's worth** — translate the leak into revenue at risk, using their own
   spend/revenue numbers, if it helps them decide.
4. Score + band, last, as context.

## Guardrails

- You diagnose from the user's own data; the Engine ranks. You never invent a benchmark.
- Spend-affecting recommendations come back flagged `requiresApproval: true` — surface
  them for the human to decide; never enact a budget change yourself.
- No rubric, no benchmark constants live in this skill — only the call to `gm-cro`.
- Never send PHI/PII to the connector.
