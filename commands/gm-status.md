---
description:
  "Check your CRO status — whether it's switched on for your workspace and what's
  flowing — plus one clear next step if anything looks off."
version: 1.0.0
---

# /gm-status — Your CRO status

<objective>
Show the user where they stand: whether their always-on CRO is switched on, what data is
flowing, and — if anything looks off — the one clear next step. Delegates to the
connector's get_go_live_status tool. This command is always safe to run — it never gates
anything.
</objective>

<user-provides>
Nothing.
</user-provides>

<steps>
1. Call the connector's `get_go_live_status` tool.
1a. Also resolve **"Read your Growth Tracker"** (`get_my_growth_tracker`, or the legacy
   name `get_my_canopy` — same tool) — by `gm-cro` alias if present, else by title — and
   read the current tiles so your status answer quotes the EXACT numbers on the user's
   `/cro/dashboard`. Never contradict the Growth Tracker; a tile with no data yet speaks
   its anticipation state, never a fabricated number.
2. Report plainly, per the returned state:
   - **On and flowing:** the CRO is switched on for this workspace and learning from
     every session; note if the Weekly Business Automation Masterclass add-on is active.
   - **Being set up:** the CRO isn't fully switched on for this workspace yet — a quick
     fix on our side. Point to `/gm-concierge`; their partner sorts it, same day.
   - **Something looks off (our side):** full access continues and nothing is lost;
     their GrowthMastery partner is already on it. Point to `/gm-concierge`.
   In every case: history is always preserved, and any hiccup is ours to fix — never
   something the user did.
3. Never present this as a wall — it's a status read plus the next step.
</steps>

<guardrails>
- This command never blocks or degrades anything; it only reports.
- If a scored tool comes back as being-set-up, the tool itself returns the warm handoff
  path — this command just explains the state.
</guardrails>
