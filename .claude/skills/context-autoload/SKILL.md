---
name: context-autoload
description:
  Use on the CRO's FIRST run for a user to make it "already know their business" without
  asking them to type anything. Read-only sweeps whichever of the user's OWN connected
  sources are present in this session (Google Drive brand docs, Gmail sent-mail voice,
  Calendar, GoHighLevel/CRM, Stripe revenue, Fathom call recordings), fills the repo
  knowledge files itself, seeds the decision log, ingests a de-identified business
  snapshot to the growth graph, then presents the "here's your business as I understand
  it — correct me" moment. Invoke from /gm-diagnose or /gm-connect first-run, or when
  the knowledge files are still unfilled placeholders.
---

# Context Autoload — know the business before the user types a word

## Why this exists

A Claude Code session **cannot** read the user's claude.ai chats, Projects, or memory —
there is no API and no bridge (hard wall). So the "already knows my whole business"
magic can't come from claude.ai. It comes from what the session **can** read: the user's
own connected sources. This skill delivers the same feeling by sweeping those sources
read-only, filling the repo knowledge files itself, and showing the user a business
snapshot to confirm — instead of handing them a blank cursor and asking them to brief
you.

## When to use

- The CRO's **first run** for a user (invoked by `/gm-connect` or `/gm-diagnose`).
- The knowledge files at `project/knowledge/` still hold
  `{{PLACEHOLDER}}` values — i.e. no one has filled the business context yet.
- The user says something like "you don't know my business yet" or "set yourself up."

Skip (or run silently and briefly) if the knowledge files are already filled with real
values — don't re-sweep a business you already know; just confirm and move on.

## The Method

### Step 1 — Detect which sources actually exist (never assume)

The set of connected sources varies per user. **Discover, don't presume.** Use
`ToolSearch` to see which of the user's own MCP tools are present in THIS session, then
map them to the context they can yield:

| Source (detect via ToolSearch keywords) | What it grounds                                  |
| --------------------------------------- | ------------------------------------------------ |
| `google drive` / `gdrive` / `docs`      | Brand docs, proposals, offer decks → brand/offer |
| `gmail` / `mail` (sent mail)            | The founder's real voice & tone → brand.voice    |
| `calendar` / `gcal`                     | Cadence, launch dates, call volume → funnel-math |
| `gohighlevel` / `ghl` / `crm`           | Funnel/stage counts, pipeline → funnel-math/icp  |
| `stripe`                                | Revenue truth, price points, MRR → offer/funnel  |
| `fathom` / `call recording` / `meeting` | Objections, ICP language, sales motion → icp     |

Run one `ToolSearch` per plausible source (e.g.
`ToolSearch "google drive brand documents"`, `ToolSearch "stripe revenue payments"`,
`ToolSearch "gohighlevel funnel contacts"`,
`ToolSearch "fathom call recording transcript"`). Only the sources that return real
tools exist. **Be graceful when few connectors exist** — even one source (say, only
Stripe) is enough to fill a meaningful snapshot; zero sources means you fall back to
asking the user two or three plain-English questions instead. Never claim to have read a
source that isn't connected.

### Step 2 — Read-only sweep, counts/amounts/summaries only (guardrails first)

For each source that exists, pull the **minimum** needed to fill the knowledge files —
and nothing more:

- **Read-only.** Never write, move money, send, or post through any source. If a tool
  looks like it mutates, don't call it.
- **Counts, amounts, and short summaries only.** Revenue totals, price points, stage
  counts, the number of calls last month, a one-line read of the offer. **Never** copy
  raw content, names, emails, clinical/financial specifics, or full transcripts into the
  knowledge files or the connector. (Same PHI/PII zone as the rest of the plugin — see
  the plugin CLAUDE.md guardrails.)
- **Distill in your own environment.** From a Drive proposal, extract "offer = 12-week
  1:1 coaching, $4k" — not the document. From Gmail sent-mail, infer voice ("warm,
  direct, no hype") — not the emails. From Fathom, extract the top 3 recurring
  objections as short phrases — never the transcript.

### Step 3 — Fill the knowledge files yourself

Write real values over the `{{PLACEHOLDERS}}` in
`project/knowledge/`:

- `brand.md` — what they sell (one line), vertical, voice/tone (from sent-mail), primary
  goal, any must-never-say.
- `offer.md` — offer name, price, guarantee, bonuses, payment options (from Stripe +
  Drive).
- `icp.md` — who it's for, core pain, prior attempts, desired outcome, top objections
  (from Fathom calls + CRM).
- `funnel-math.md` — the stage table with counts, spend, revenue in cents (from GHL/CRM
  and Stripe), for the last 30 days.
- Leave a field as its placeholder ONLY if no connected source could ground it — and
  note which fields you inferred vs. which need the user's confirmation.

### Step 4 — Seed the decision log

Append one opening entry to `project/knowledge/decisions-log.md`
recording that the CRO autoloaded context on this date, which sources it swept, and the
headline it read (e.g. "Autoloaded from Stripe + GHL + 1 Drive proposal; primary goal =
fill the Sept cohort"). This is the first link in the compounding memory chain.

### Step 5 — Ingest the business snapshot to the growth graph

Persist a **structured, de-identified** snapshot to the tenant growth graph via the
existing capture path — call **`mcp__gm-cro__ingest_turn`** once with:

```jsonc
{
  "session_id": "<this session id>",
  "event": "Stop",
  "session_role": "cro",
  "intent": "first-run business context autoload",
  "action_summary": "Autoloaded business context from the user's own connected sources; filled brand/offer/icp/funnel-math knowledge files.",
  "entity_refs": {
    "journey_signal": "autoload", // exact marker — roots the journey step
    "sources_swept": ["stripe", "gohighlevel", "google_drive"],
    "brand_vertical": "<vertical, e.g. health-coaching>",
    "offer_shape": "<e.g. 1:1_12wk>",
  },
  "metric_refs": {
    "price_cents": 400000,
    "revenue_30d_cents": 7000000,
    "spend_30d_cents": 1200000,
    "lp_view": 10000,
    "optin": 1800,
    "booking": 220,
    "show": 150,
    "sale": 28,
  },
}
```

Only counts, amounts, and opaque keys go into the bags — **never** names, emails, or raw
content. This is the same fail-open capture the every-turn hooks use; if it errors, keep
going (the knowledge files are the source of truth regardless).

### Step 6 — The "here's your business as I understand it — correct me" moment

Present a short, plain-English snapshot back to the user and invite correction. Founder
tone, no tables in chat:

> Here's your business as I understand it from your own accounts — tell me what's off: •
> You sell **<offer>** at **<price>** to **<ICP one-liner>**. • Last 30 days:
> **<revenue>** on **<spend>**, roughly **<lp→sale>** of visitors buying. • Your voice
> reads **<voice>**; your #1 goal right now looks like **<goal>**. • Biggest thing
> stalling the sale: **<top objection>**.
>
> Did I get that right? Correct anything and I'll update — then I'll show you where
> you're losing the most money.

Fold any correction straight into the knowledge files (and append a decision-log line),
then hand off to `diagnose-funnel-leak` for the first real leak read.

## Guardrails

- **Read-only, always.** Never write/move/send/post through any connected source.
- **Counts, amounts, summaries only** into the knowledge files and the connector — no
  raw content, no PHI/PII, no transcripts.
- **Detect, never assume.** Only claim a source you verified exists via ToolSearch.
- **Graceful with few connectors.** One source is enough to start; zero → ask two or
  three plain questions instead of pretending.
- **The knowledge files are the source of truth** — the connector snapshot is a
  compounding echo, not the record. If the ingest fails, keep helping.
- **No rubric, no benchmark** lives here — leak ranking still comes from the Engine.
