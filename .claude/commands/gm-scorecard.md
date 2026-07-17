---
description:
  "Your branded weekly growth scorecard — overall growth score, channel ROI, and the
  prioritized next move, in one read."
version: 1.0.0
---

# /gm-scorecard — Your weekly growth read

<objective>
Produce the branded weekly scorecard: overall growth score, channel ROI, and the
prioritized next move — the ritual read a CRO would bring you each week. Delegates to the
`growth-scorecard` skill, which assembles the snapshot from the user's own tools and asks
the `gm-cro` connector to score growth, score channels, and prioritize the next move.
</objective>

<user-provides>
Optionally the window ("last 7 days" default).
</user-provides>

<steps>
1. Invoke the `growth-scorecard` skill.
2. Render the branded scorecard: growth score + band, top channel movement, and the
   `priority: 1` next move — using the templates in the skill.
3. Close with the single most important thing to do this week.
</steps>

<guardrails>
- The connector scores; you assemble and present. No rubric lives in this plugin.
- Flag anything touching spend, pricing, or a commitment for the human to decide.
</guardrails>
