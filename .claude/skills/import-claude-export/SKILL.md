---
name: import-claude-export
description:
  Use when the user wants their existing claude.ai context (chats, Projects, memory)
  brought into their Always-On CRO. A Claude Code session cannot read claude.ai directly
  (no API — hard wall), so this skill has the user export their claude.ai data (Settings
  → Privacy → Export data) and drop the file into the session; it then parses
  conversations.json, distills durable business context (offer, ICP, pricing, decisions,
  voice) into the repo knowledge files + a growth-graph ingest — chunked and
  size-tolerant, distilled summaries only, never verbatim transcripts. Invoke from
  /gm-import-claude or when the user says "import my Claude history / my
  ChatGPT-of-Claude context."
---

# Import claude.ai export — bring your existing context to the CRO

## Why this exists

The CRO runs in Claude Code, which **cannot** read your claude.ai chats, Projects, or
memory — there's no API and no native bridge. But claude.ai lets you **export your own
data**, and once that file is in this session the CRO **can** read it. This skill turns
that export into durable business context: it distills your months of Claude
conversations into the offer, ICP, pricing, decisions, and voice the CRO carries forward
— so the CRO "already knows" everything you've been working through with Claude, without
re-briefing.

## When to use

- The user runs `/gm-import-claude`, or says "import my Claude history / my Projects /
  my memory into the CRO."
- A user migrating from doing growth work in claude.ai chat into the Always-On CRO.

## The Method

### Step 1 — Walk the user through the export (they own the data)

Tell them plainly how to get the file (it's their data, one click):

> In claude.ai: **Settings → Privacy → Export data**. Claude emails you a link; download
> the `.zip`, unzip it, and drop **`conversations.json`** into this session (or tell me
> the path to it). That's the only file I need. It never leaves your machine except as
> the short distilled summaries you'll approve.

Wait for the file. If they paste a path, read from there; if they drop it into the chat,
read it from the attached location. Don't proceed without it.

### Step 2 — Parse conversations.json, chunked + size-tolerant

The export can be **large** (tens of MB, hundreds of conversations). Do not try to load
it whole into reasoning context.

- Read it **incrementally** — stream/iterate conversation objects; if the file is big,
  process it in chunks (e.g. by conversation, or in batches), summarizing as you go and
  discarding the raw text between batches.
- Each conversation object typically has a `name`/title and a list of messages with
  `sender` (human/assistant) and text. You care about **what the user said about their
  business**, not the assistant's replies.
- Be tolerant of schema drift and truncation — if a record is malformed, skip it and
  keep going. Never let one bad record abort the import.

### Step 3 — Distill durable business context (summaries, never transcripts)

As you pass over the conversations, extract only **durable, business-relevant** facts
and roll them into the knowledge files at `project/knowledge/`:

- **offer.md** — offer name(s), price points, guarantee, bonuses, payment terms the user
  described.
- **icp.md** — who they sell to, the core pain, prior attempts, desired outcome, and the
  objections they keep mentioning.
- **brand.md** — what they sell in one line, vertical, and their **voice/tone** (infer
  from how they write across many messages — "warm, plain, no hype").
- **funnel-math.md** — any real numbers they mentioned (traffic, opt-ins, bookings,
  close rate, revenue) — as counts/amounts only.
- **decisions-log.md** — the meaningful **decisions** they made in Claude ("switched
  from webinar to VSL in March", "dropped the $2k tier") as dated log lines, newest
  first, so the compounding memory starts already deep.

Distillation rules:

- **Distilled summaries only.** Never store a verbatim transcript, a full message, or a
  long quote in the knowledge files. A fact is "offer = $4k 12-week 1:1", not the
  paragraph they wrote it in.
- **Durable over ephemeral.** Keep the stable business truths; drop one-off debugging
  chats, drafts, and anything not about their business.
- **Counts/amounts only for numbers** — no names, emails, client identifiers, or
  clinical/financial specifics (same PHI/PII zone as the whole plugin).
- **Latest wins.** If the export shows the offer changed over time, record the current
  state in the knowledge file and log the change history in the decision log.

### Step 4 — Ingest a distilled snapshot to the growth graph

Persist the distilled business snapshot to the tenant growth graph via the existing
capture path — call **`mcp__gm-cro__ingest_turn`** once with a de-identified bag:

```jsonc
{
  "session_id": "<this session id>",
  "event": "Stop",
  "session_role": "cro",
  "intent": "claude.ai export import — distilled business context",
  "action_summary": "Imported the user's claude.ai export; distilled durable offer/ICP/pricing/decisions/voice into the knowledge files.",
  "entity_refs": {
    "source": "claude_ai_export",
    "conversations_scanned": 214,
    "brand_vertical": "<vertical>",
    "offer_shape": "<e.g. 1:1_12wk>",
  },
  "metric_refs": {
    "price_cents": 400000,
    "decisions_imported": 6,
  },
}
```

Opaque keys, counts, and amounts only — never message text. Fail-open: if the ingest
errors, the knowledge files remain the source of truth and you keep going.

### Step 5 — Confirm what you learned, then diagnose

Show the user a short, plain-English read of what you imported and invite correction
(founder tone, no tables in chat):

> I read <N> of your Claude conversations and here's the durable context I kept: •
> Offer: **<offer>** at **<price>** — guarantee **<guarantee>**. • You sell to
> **<ICP>**; the objection you keep hitting is **<objection>**. • Decisions I logged:
> **<2-3 headline decisions>**. • Your voice reads **<voice>**.
>
> Anything off or out of date? Correct it and I'll update — then I'll show you where
> you're losing the most money.

Fold corrections into the knowledge files (+ a decision-log line), then hand off to
`diagnose-funnel-leak` for the first leak read on their real data.

## Guardrails

- **The user exports their own data** — you never reach into claude.ai (impossible) and
  never ask for credentials.
- **Distilled summaries only** — no verbatim transcripts, full messages, or long quotes
  stored anywhere. Counts/amounts for numbers; no names/emails/PHI/PII.
- **Chunked + size-tolerant** — process large exports incrementally; one bad record
  never aborts the run.
- **Knowledge files are the source of truth**; the connector ingest is a compounding
  echo.
- **No rubric, no benchmark** here — leak ranking still comes from the Engine.
