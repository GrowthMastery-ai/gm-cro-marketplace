# gm-cro-agent — GrowthMastery CRO Agent

**Your own CRO, inside Claude.** Connect your accounts read-only and your Claude becomes
a growth operator that already knows your business — it diagnoses your funnel, coaches
your sales calls, scores your channels, and names the single highest-leverage next move.
Fully on from your first session — every capability live, set up with you by your
GrowthMastery partner.

> **The moat, and why this is safe:** every skill, command, and agent here **calls** the
> GrowthMastery Intelligence Engine (the `gm-cro` connector) and contains **no rubric**.
> The thresholds, weights, benchmarks, and scoring formulas execute server-side and
> never land on your machine. When GrowthMastery improves the methodology, your next
> call is better automatically — zero re-install. It also means the product is cleanly
> self-contained: if the intelligent scoring is ever being set up or re-enabled on our
> side, the plugin still installs and the commands still type, and it warmly hands you
> to your GrowthMastery partner while your history stays retained.

## Use it in Claude Cowork — zero setup

Your CRO's intelligence already works in Cowork: the `gm-cro` connector is authorized on
your Claude **account**, so on web, desktop, or mobile you can open Cowork and just say
hello — it knows your business with nothing to install.

Want it fully moved in (personas, `/gm-*` commands, scheduled morning briefs that run
with your laptop closed)? **This repository is also your personal plugin marketplace.**
Three taps, once:

1. In Claude, open **Settings → Plugins** → add marketplace
2. Paste **this repository's GitHub URL** (the page you're reading)
3. Install **gm-cro-agent** — then say "put yourself on autopilot"

## What's in the plugin

```
gm-cro-agent/
  .claude-plugin/plugin.json     plugin name + version + marketplace metadata
  .mcp.json                      binds ONE hosted connector: gm-cro (HTTP MCP + OAuth)
  .claude/settings.json          every-turn capture hooks (mcp_tool → gm-cro › ingest_turn / get_cross_session_digest)
  commands/
    gm-connect.md                first-run setup — connect accounts read-only + first diagnosis
    gm-import-claude.md          import your claude.ai export → distilled business context
    gm-diagnose.md               biggest funnel leak + the one fix     → analyze_funnel
    gm-coach-call.md             coach a sales call (de-identified)     → grade_call
    gm-channels.md               score channel ROI                     → score_channel_roi
    gm-scorecard.md              the weekly growth read                → score_growth (+)
    gm-next-move.md              the single highest-leverage next move  → prioritize_next_move
    gm-status.md                 is your CRO on + what's flowing        → get_go_live_status
    gm-concierge.md              reach your GrowthMastery partner (account/access, same-day human)
  skills/
    context-autoload/            first-run: sweep the user's own sources → fill knowledge files + ingest_turn snapshot
    import-claude-export/        parse a claude.ai export → distilled durable business context
    diagnose-funnel-leak/        → gm-cro › analyze_funnel  (first run autoloads context first)
    coach-sales-call/            → gm-cro › grade_call  (references/: de-identify + reading-the-grade)
    growth-scorecard/            → gm-cro › score_growth + score_channel_roi + prioritize_next_move
  agents/
    cro-operator.md              the AI CRO subagent (briefs + recommends; human decides)
  project/
    PROJECT-INSTRUCTIONS.md      copy-paste seeded Growth Project ("CRO for [Brand]")
    knowledge/                   brand · icp · offer · funnel-math · decisions-log stubs
```

Every skill is **human-on-top, progressive-disclosure, rubric-free**. The agent briefs
and recommends; the human always decides anything touching spend, pricing, or a
commitment.

## Always-on capture (how the moat actually fires)

`.claude/settings.json` declares four **`mcp_tool` hooks** — the deterministic,
every-turn capture layer. They call the already-connected `gm-cro` connector directly
(no LLM in the capture path, so they fire even on tool-less turns):

- `UserPromptSubmit` + `Stop` → `gm-cro › ingest_turn` (the write half of the growth
  graph)
- `PostToolUse` → `gm-cro › ingest_turn` (action capture, passing the tool that ran)
- `SessionStart` → `gm-cro › get_cross_session_digest` (the "informed by all"
  cross-session read)

**Runtime path (where these load):** GrowthMastery provisions each seat a private
**tenant repo** pre-committed with this plugin's contents at the repo root, so
`.claude/settings.json` is loaded as **project settings** for every session and Routine
run against that repo — which is exactly where Claude Code honors a project's `hooks`
block. Distillation, thresholds, and ranking all execute **server-side** in the
connector; nothing rubric-bearing lives in these hooks (they carry only the event name
and the session id). Capture is fail-open and idempotent: if the connector is
unavailable or the account has lapsed, the turn completes normally and nothing is
surfaced to the user.

**Two binding paths — capture is alias-robust across both.** The connector can reach a
session either as the plugin's **repo binding** (server alias `gm-cro`, from this
plugin's `.mcp.json`) **or** as an **account-level custom connector you added yourself
under any name** (e.g. "GrowthMastery.ai"). The four `mcp_tool` hooks target the
`gm-cro` alias and fire deterministically **when that alias is present** — the preferred
path. But an account-level connector exposes the same tools under a **different** alias
(e.g. `mcp__GrowthMastery_ai__ingest_turn`), which the `server: "gm-cro"` hooks cannot
see. So `CLAUDE.md` instructs the agent to resolve the two capture tools by their
**unique, alias-independent titles** — **"Capture a CRO turn (always-on)"**
(`ingest_turn`) and **"Cross-session CRO briefing"** (`get_cross_session_digest`) —
regardless of the `mcp__<alias>__` prefix, preferring the `gm-cro` binding when present.
A **SessionStart self-check** calls ingest once to confirm capture is live and **warns
in-context** (never silently) if it is not — so an account-level-connector session can
never again leave `tier2_turn_events` empty without the user being told.

> **Why `mcp_tool` hooks (not `prompt`, and never raw HTTP):** per the Claude Code
> [hooks reference](https://code.claude.com/docs/en/hooks), `mcp_tool` is a first-class
> hook type that calls a tool on an already-connected MCP server, and its `input` object
> supports `${…}` substitution from the hook's JSON payload (e.g. `${session_id}`,
> `${tool_name}`) — which is what lets each capture record the real session id
> deterministically, with no LLM in the loop. A `prompt` hook runs an isolated,
> tool-less evaluation and cannot call the connector, and `SessionStart` does not accept
> `prompt` hooks at all — so `mcp_tool` is the only type that makes the every-turn
> capture actually fire.
>
> **Verified in the cloud sandbox:** these hooks MUST be `mcp_tool` — never a
> `command`/shell hook that shells out to `curl` or otherwise makes a raw HTTP request.
> **Raw outbound HTTP egress is blocked in the Claude Code cloud sandbox** (verified),
> so a shell hook that tried to `POST` to the connector directly would be silently
> dropped — capture would fail in exactly the autonomous/scheduled cloud runs where it
> matters most. `mcp_tool` reaches the `gm-cro` connector through Claude's own
> already-authorized MCP transport, which is permitted in the sandbox. That is why
> **every hook in `.claude/settings.json` is `"type": "mcp_tool"`** and no capture path
> ever depends on raw HTTP.

## Install

1. **Add the GrowthMastery marketplace** in Claude Code:
   `/plugin marketplace add GrowthMastery-ai/growth-mastery` (the marketplace manifest
   lives at `plugins/.claude-plugin/marketplace.json`).
2. **Install the plugin:** `/plugin install gm-cro-agent@growthmastery`.
3. **Approve the connector OAuth** — on first use, Claude runs the one consent screen
   for the `gm-cro` GrowthMastery CRO Engine. No token to paste; the grant is stored by
   Claude.
4. **Run `/gm-connect`** — connect one of your own accounts read-only and get your first
   real diagnosis on real data (the Day-1 "wow" — your actual funnel leak, named).

After install: `/gm-diagnose`, `/gm-coach-call`, `/gm-channels`, `/gm-scorecard`,
`/gm-next-move`, `/gm-status`, `/gm-concierge` — or just talk to the `cro-operator` in
plain English ("where am I losing the most money?", "coach my last call").

## "Already knows your business" — the first-run experience

The CRO doesn't hand you a blank cursor and ask you to brief it. On first contact it
**offers to learn your business for you**, two ways:

- **Autoload from your connected sources (default).** `context-autoload` detects which
  of your OWN sources are connected in the session — Google Drive brand docs/proposals,
  Gmail sent-mail voice, Calendar, GoHighLevel/CRM, Stripe revenue, Fathom call
  recordings (**detected, never assumed**) — sweeps them **read-only** (counts, amounts,
  and short summaries only — no raw content, no PHI/PII), fills the knowledge files
  itself, seeds the decision log, ingests a de-identified snapshot to your growth graph,
  and shows you _"here's your business as I understand it — correct me."_ It's graceful
  when few sources are connected: one is enough to start.
- **Import your claude.ai context.** A Claude Code session **can't** read your claude.ai
  chats, Projects, or memory (no API — hard wall). `/gm-import-claude` closes that gap:
  you export your own claude.ai data (**Settings → Privacy → Export data**), drop
  `conversations.json` into the session, and the CRO distills your durable business
  context (offer, ICP, pricing, decisions, voice) into the knowledge files + your growth
  graph — chunked, size-tolerant, distilled summaries only, never verbatim transcripts.

Either way, you **confirm and correct** — you never type your whole business out.

## The seeded Growth Project (your agent's memory)

The full "named agent that knows you" experience comes from a private Claude Project.
See `project/PROJECT-INSTRUCTIONS.md` for the copy-paste instructions block and
knowledge-file stubs. `/gm-connect` walks you through setting it up.

## Your engagement (what happens, plainly)

- **Fully on from day one.** Every capability is live from your first session — nothing
  is held back, nothing is gated. Your GrowthMastery partner sets it up with you.
- **A real person, not a portal.** Anything about your account, access, or how your CRO
  is configured goes to your GrowthMastery partner — reachable anytime via
  `/gm-concierge`, with a same-day human answer. No forms, no self-serve billing to
  wrangle.
- **Your history is always yours.** Everything the CRO learns compounds and stays saved.
  If anything ever looks switched off, that's a quick fix on our side — your access and
  full history are preserved the entire time. Never a dead end.
- **Optional Masterclass.** The Weekly Business Automation Masterclass can be part of
  your engagement — just ask your partner.

## Updating

| What changed              | How it propagates                                      | Your action                                                              |
| ------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------ |
| A skill / command / agent | Bump `plugin.json` semver → publish to the marketplace | One `/plugin update`                                                     |
| **The CRO Engine rubric** | GrowthMastery deploys the connector                    | **None** — instant for everyone, your next call uses the new methodology |

## PHI / PII

The `gm-cro` connector is a **PHI/PII-free zone**. Skills de-identify in your own
environment **before** any connector call; the server-side detector is only a backstop.
Send counts, spend, revenue, and de-identified call _features_ — never names, contact
details, or clinical/financial specifics.
