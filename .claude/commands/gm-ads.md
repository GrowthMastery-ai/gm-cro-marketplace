---
description:
  "Run your Meta ads review — performance trend, anomalies, and opportunity score
  through Meta's official Ads MCP, graded against your real funnel numbers. Any
  change lands as a paused draft; nothing activates without your explicit OK."
version: 1.0.0
---

# /gm-ads — Your Meta ads, orchestrated safely

<objective>
Run the user's Meta ads as one calm system: Meta's official Ads MCP (their own
`ads_*` tools, connected directly in their Claude) does the ad-account reading and
drafting; the `gm-cro` connector holds the funnel truth and the judgment. If the Ads
MCP isn't connected yet, walk the one-time connect instead — warmly, two minutes.
</objective>

<user-provides>
Optionally the window ("last 7 days" default), specific campaigns, or a change they
already have in mind ("more budget on the webinar campaign").
</user-provides>

<steps>
1. Read the doctrine first: pull the `gm://playbook/ads-orchestration` resource from
   the `gm-cro` connector — it carries the division of labor, the safety rails, and
   the connect steps. Follow it exactly.
2. Detect: are `ads_*` tools present in this conversation?
   - **Not connected** → walk the connect: Claude Settings → Connectors → Add custom
     connector → name it "Meta Ads" → paste `https://mcp.facebook.com/ads` → sign in
     with their Meta Business account → choose the ad account. Recommend starting
     read-only, or read+write with an account-level budget cap; the financial tier
     only when they're comfortable. Then stop — the review runs next session.
   - **Connected** → run the review ritual below.
3. Read (pin the date range AND the campaign/ad-set IDs on every call):
   `ads_insights_performance_trend` for the trajectory,
   `ads_insights_anomaly_signal` for what changed,
   `ads_get_opportunity_score` for Meta's own read.
4. Ground in funnel truth: pull the same window from the `gm-cro` connector
   (registrations, offer reached, enrollments, revenue) and reconcile — where did
   paid traffic actually convert? Ask the connector to score it
   (`score_channel_roi` / `prioritize_next_move`) rather than judging locally.
5. Recommend the one highest-leverage move, evidence on the table, in plain English.
6. Draft, don't act: build any agreed change through `ads_*` as a PAUSED draft
   (created entities land paused by design). Creatives route through GrowthMastery —
   Meta's MCP has no creative access.
7. Approve, then activate: name the specific entity and its daily budget and get the
   user's explicit yes in this conversation BEFORE `ads_activate_entity`. Log the
   decision to the Growth Project's decision log.
</steps>

<guardrails>
- NEVER call `ads_activate_entity` without the user's explicit approval of the
  specific entity + daily budget, in this conversation. A nod at the plan is not a
  yes to a spend number.
- Respect the learning phase: at most ~one budget/audience edit per campaign per
  day. Batch recommendations; say why you're waiting if the user is eager.
- Always pin date ranges and entity IDs when reading insights — never "whatever
  comes back".
- Creatives are generated/uploaded via GrowthMastery; Meta's MCP cannot touch them.
- The connector scores; you read. No rubric or benchmark lives in this plugin.
- Prefer the smallest reversible step: pause before delete, one campaign before
  five, a budget nudge before a rebuild.
</guardrails>
