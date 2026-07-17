---
name: conversational-routines
description:
  Use whenever the user expresses recurring intent — "every morning", "each week", "keep
  an eye on", "check this daily", "watch overnight", "remind me", "run this on a
  schedule". Set the recurring work up conversationally as a DURABLE account-level
  Routine that persists across sessions and runs as a fresh cloud session — NEVER a
  session-only task that dies when the chat closes. Also invoked by /gm-autopilot for
  the standard suite.
---

# Conversational Routines

## Overview

The Always-On CRO's autonomy is set up **by talking to the CRO** — the user does the
wiring by asking, not by hunting through a dashboard. When the user wants something to
happen on a schedule, you translate that intent into a concrete recurring routine and
create it, right here in the conversation, as a **durable, account-level Routine** (a
claude.ai/code Routine): one that **persists across sessions** and **runs as a fresh
cloud session** on its own cadence, even after this chat is closed and the user is away.
Durable scheduled runs execute against this tenant repo, so they inherit the plugin, the
capture hooks, and CLAUDE.md automatically — the scheduled CRO is as informed as the
live one.

**Never create a session-only task.** A one-shot / session-scoped scheduled task fires
**only while this exact session is alive and idle** and dies when the session ends — it
inherits nothing once the chat is gone and silently breaks the whole promise of an
Always-On CRO. Durability across sessions is the requirement; conversational setup is
just how you reach it. If the only scheduler you can reach in context is session-scoped,
**say so plainly and guide the user to the one-tap durable alternative** rather than
quietly wiring a task that dies with the session.

There is **no rubric in this skill** — scheduling is orchestration only; all scoring
stays server-side in the CRO Engine.

## When to use

Trigger on any recurring-intent phrasing, e.g.:

- "Every morning give me the brief" → a daily morning Routine.
- "Watch my funnels overnight" → a nightly monitor Routine.
- "Send me a weekly scorecard" → a weekly Routine.
- "Keep an eye on my ad spend and tell me if it spikes" → a recurring monitor Routine.
- "Remind me to review the offer each Friday" → a weekly Routine.

Each of these is a **durable account-level Routine**, never a session-only task. If the
user asks for the whole standard set at once, hand off to `/gm-autopilot`.

## How you operate (on rails)

1. **Read the intent** — what should run, and how often (cadence + time + time zone).
   Ask one short clarifying question only if cadence or time is genuinely ambiguous.
2. **Propose it in plain English** — "I'll run your morning brief every day at 7am
   Eastern. Good?" — and get a quick confirmation.
3. **Create it as a durable account-level Routine** — conversationally, bound to this
   repo, saved so it persists across sessions and runs as a fresh cloud session. Do the
   wiring for the user; never make them open or configure anything themselves — and
   never stand up a session-only task that dies when this chat closes. If the only
   scheduler you can reach in context is session-scoped, say so plainly and guide the
   user to the one-tap durable alternative instead.
4. **Confirm back** — restate what will run, when, in which time zone, and that it's a
   durable Routine that keeps running while they're away, so the user knows their CRO is
   on it.
5. **Offer control conversationally** — they can change, pause, or remove any Routine
   just by asking here.

## Guardrails (non-negotiable)

- **Durable account-level Routine, never a session-only task.** What you create must
  persist across sessions and run as a fresh cloud session — a task that fires only
  while this chat stays open breaks the core promise of the Always-On CRO. Set it up
  conversationally; if the only scheduler in context is session-scoped, say so and guide
  the one-tap durable alternative rather than silently creating a task that dies with
  the session.
- **Human on top.** Scheduled runs brief and recommend; they never enact anything
  touching spend, pricing, or a commitment. Surface those flagged for approval.
- **Requires a paid Claude seat + a live GrowthMastery CRO.** If the connector ever looks
  switched off, point to `/gm-concierge` warmly before scheduling — their GrowthMastery
  partner sorts it, history is always retained and it switches back on; never a dead end.
- **No rubric here.** Scheduling only; the Engine scores server-side.
