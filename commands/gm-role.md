---
description:
  "Pick or switch which role-tailored face of your one shared growth brain shows up this
  session — CRO (chief), Operations Partner, or Front-Office Partner. Same repo, same
  connector, same growth graph; the right lens for whoever's at the keyboard."
version: 1.0.0
---

# /gm-role — the right face for whoever's here

<objective>
Detect (or switch) which teammate is driving this session and adopt the role-tailored
persona that fits their job, without splitting the shared brain. One tenant, one
connector, one growth graph — each teammate meets the face tuned to their work, and every
captured turn is stamped with that role so the shared memory knows who did what. Delegates
to the `role-picker` skill.
</objective>

<user-provides>
Optionally who they are or what they're here for ("I'm Dana, I run operations", "switch to
front-office", "I handle bookings"). If they say nothing, the skill detects from the
opening ask or the cross-session digest, and asks at most one short question only if
genuinely unsure.
</user-provides>

<steps>
1. Invoke the `role-picker` skill. It reads the signal already in the session
   (self-identification, the opening ask, or a prior role for this person from
   `get_cross_session_digest`), and adopts the matching role — **cro** (the chief and the
   default), **operations-partner**, or **front-office** — without making the user pick
   from a menu when the job is already clear.
2. Load the chosen persona (`.claude/agents/<role>.md`) and operate as that face for the
   rest of the session: its lens and framing, the same shared knowledge files, connector
   tools, and guardrails.
3. Stamp the role: call the capture tool once with a role-marker turn carrying
   `session_role` so the shared graph attributes this session to the right teammate, and
   keep passing `session_role` on every later `ingest_turn`.
4. On a later switch (`/gm-role` again, or "actually, let's look at operations"), re-detect
   and stamp a fresh role-marker turn with the new role.
</steps>
