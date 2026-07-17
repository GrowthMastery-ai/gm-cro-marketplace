---
description:
  "The single highest-leverage next move for your business right now — sequenced and
  grounded in your own numbers."
version: 1.0.0
---

# /gm-next-move — Your one next move

<objective>
Name the single highest-leverage next move for the user's business right now, with the
rationale and what it's worth. Delegates to the `growth-scorecard` skill's prioritization
read, which asks the `gm-cro` connector to `prioritize_next_move` across the assembled
funnel, channel, and growth context.
</objective>

<user-provides>
Nothing required. Optionally a constraint ("no new spend", "this week only").
</user-provides>

<steps>
1. Invoke the `growth-scorecard` skill for the prioritized next move (or chain from a
   recent `/gm-diagnose` / `/gm-channels` read if one exists in the conversation).
1a. Cross-check against the Growth Tracker: resolve **"Read your Growth Tracker"**
   (`get_my_growth_tracker`, or the legacy name `get_my_canopy` — same tool; by `gm-cro`
   alias if present else by title) and read the `next_move` and `funnel_health` tiles so
   the move you name matches the founder's `/cro/dashboard` exactly. Never contradict the
   Growth Tracker; an anticipation tile means no play surfaced yet.
2. Return the `priority: 1` move, its rationale, and the revenue it's expected to move —
   grounded in the returned evidence.
3. Offer to set it up as a tracked decision in the Growth Project.
</steps>

<guardrails>
- The connector prioritizes; you present. No rubric lives in this plugin.
- If the move touches spend, pricing, or a commitment, surface it for approval — never
  enact it.
</guardrails>
