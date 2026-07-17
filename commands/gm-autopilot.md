---
description:
  "Turn your CRO fully autonomous: stand up the standard routine suite — morning brief,
  overnight monitor, and weekly scorecard — in one confirmation, all as durable
  account-level Routines that persist across sessions (never session-only tasks)."
version: 1.3.0
---

# /gm-autopilot — Put your CRO on autopilot

<objective>
Stand up the standard Always-On CRO routine suite in a single "yes." Each routine is
created conversationally as a **durable, account-level Routine** — in Claude Cowork use
**`/schedule`** (scheduled tasks run in the cloud with no device online); in claude.ai/
code use a Routine — bound to this tenant repo, one that **persists across sessions**
and **runs as a fresh cloud session** on its own cadence, even after this chat is
closed. Every
scheduled run inherits the plugin, the capture hooks, and this CLAUDE.md automatically —
the autonomous CRO is as informed as the live one. The user does the wiring by talking to
the CRO; their only job is a one-tap confirmation.

**Never stand up a session-only task.** A one-shot / session-scoped scheduled task fires
only while this exact chat stays alive and idle and dies when the session ends — that
silently breaks the whole promise of an Always-On CRO. Durability across sessions is the
non-negotiable requirement of this command. </objective>

<user-provides>
Nothing required. Optionally: preferred morning-brief time and time zone, and which day
the weekly scorecard should land. Sensible defaults are used if they don't say.
</user-provides>

<the-standard-suite>
Propose these three routines (adjust wording to the user's business), then create them on
one confirmation:

1. **Morning brief** — daily, ~7:00am in the user's time zone (pick a minute other
   than :00 — e.g. 7:07 or 7:23 — so the fleet doesn't stampede on the hour). Reads
   the overnight cross-session digest, asks the connector for the day's ranked work
   queue when available, names the single highest-leverage move, presents any
   overnight-staged drafts for one-tap approval, and flags anything that needs the
   human (spend/pricing/commitment decisions).
2. **Overnight monitor** — nightly, ~1:00am (again, an off-hour minute). Watches the
   connected funnels/channels for meaningful movement (new leaks, spend spikes,
   conversion drops), and in Cowork may PREPARE work — draft follow-ups, refresh
   internal sheets, stage a brief — strictly under the cowork-operator overnight
   rule: **create-only, nothing external ever sent from an overnight run**;
   everything outbound queues for the morning approval.
3. **Weekly scorecard** — weekly, e.g. Monday ~8:00am. Runs the growth scorecard
   (`/gm-scorecard`), summarizes channel ROI and the week's decisions, and sets the
   week's focus. </the-standard-suite>

<accountability-texts-optional>
If the user wants their daily accountability nudge as a **text message** AND their own
GoHighLevel MCP connector is connected in this workspace, the routine may send the
day's nudge as an SMS **to the USER'S OWN phone, through THEIR GHL connector** — their
registered number, their deliverability, their bill; zero GrowthMastery infrastructure.
Non-negotiable rules:

- **Explicit opt-in first.** Send nothing until the user clearly confirms in
  conversation that they want texts. Record the consent (and its date) in the decision
  log at `project/knowledge/decisions-log.md` before the first send.
- **Max one nudge per day.** Respect quiet hours: send only between **8am and 8pm in
  the user's time zone**.
- **Stop instantly on request.** "Stop the texts" ends it that turn — no confirmation
  loop; note the stop in the decision log too.
- **No GHL connector, no promise.** If their own GHL connector isn't present in this
  workspace, the nudge lives in the morning brief — never promise a text you cannot
  send.
</accountability-texts-optional>

<steps>
1. **Speak the plan first.** Show the three routines with their proposed times in plain
   English and ask for one confirmation (or a quick tweak to times/timezone/day).
2. **Create each one as a durable account-level Routine** — conversationally, in this
   chat. Translate each item above into a concrete Routine (what runs + cadence + time
   zone) bound to this repo, saved at the account level so it persists across sessions and
   runs as a fresh cloud session. Do NOT stand up a session-only task for any of them. If
   the only scheduler you can reach in context is session-scoped, **say so plainly and
   guide the user to the one-tap durable alternative** rather than silently wiring a task
   that dies when this chat closes.
3. **Confirm the schedule back** in plain English: what will run, when, in which time
   zone, and that each is a durable Routine that keeps running while they're away — so the
   user knows their CRO is now on autopilot.
4. **Name the guardrail:** every routine briefs and recommends; nothing that touches
   spend, pricing, or a commitment is ever enacted without the human. Spend-affecting
   items come back flagged for approval.
5. **Offer control:** tell the user they can add, change, or pause any routine anytime
   just by asking here — always conversationally, and always as durable Routines.
6. **Record autopilot-on in the growth graph** (fail-open — never block the user on
   this): once the Routines are confirmed, call `mcp__gm-cro__ingest_turn` once with
   `{"session_id": "<this session id>", "event": "Stop", "session_role": "cro",
   "intent": "gm-autopilot routines armed", "action_summary": "<one line: which
   routines were created and their cadence>",
   "entity_refs": {"journey_signal": "autopilot"}}`.
   The `journey_signal` marker is what roots the user's journey step — include it
   exactly. If the ingest fails, keep helping; never surface the failure.
</steps>

<guardrails>
- **Durable Routines only, never a session-only task.** Set them up conversationally; each
  must persist across sessions and run as a fresh cloud session. If the only scheduler in
  context is session-scoped, say so and guide the one-tap durable alternative — never
  silently create a task that dies with this chat.
- **Human on top.** Autonomous runs surface decisions for approval; they never move money,
  change pricing, or make commitments.
- **One confirmation.** Don't nickel-and-dime the user with a prompt per routine — propose
  the suite, get one "yes," create all three.
- **Requires a paid Claude seat + a live GrowthMastery CRO.** If the connector ever looks
  switched off, point to `/gm-concierge` warmly before scheduling — their GrowthMastery
  partner sorts it and history is always retained; never a dead end.
</guardrails>
