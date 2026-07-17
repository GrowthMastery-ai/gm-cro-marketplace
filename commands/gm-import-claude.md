---
description:
  "Bring your existing claude.ai context (chats, Projects, memory) into your Always-On
  CRO — you export your data, drop the file in, and the CRO distills your durable
  business context so it already knows everything you've worked through with Claude."
version: 1.0.0
---

# /gm-import-claude — Bring your Claude history into the CRO

<objective>
Make the CRO "already know" everything the user has worked through in claude.ai. A Claude
Code session cannot read claude.ai directly (no API — hard wall), so the user exports their
own claude.ai data and the CRO distills it. Delegates to the `import-claude-export` skill,
which parses `conversations.json`, distills durable business context (offer, ICP, pricing,
decisions, voice) into the repo knowledge files + a growth-graph ingest — chunked,
size-tolerant, distilled summaries only, never verbatim transcripts.
</objective>

<user-provides>
Their claude.ai data export. The command tells them how: claude.ai → Settings → Privacy →
Export data → download the zip → drop `conversations.json` into the session (or give its
path).
</user-provides>

<steps>
1. Invoke the `import-claude-export` skill.
2. Walk the user through exporting their claude.ai data and dropping in `conversations.json`.
3. Distill durable business context into the knowledge files + ingest a de-identified
   snapshot to the growth graph; confirm what was learned and invite correction.
4. Hand off to `/gm-diagnose` for the first real leak read on their data.
</steps>

<guardrails>
- The user exports their own data — never ask for claude.ai credentials, never imply the
  CRO can reach claude.ai directly.
- Distilled summaries only — no verbatim transcripts or long quotes stored. Counts/amounts
  for numbers; never names/emails/PHI/PII.
- Chunked + size-tolerant for large exports; one bad record never aborts the run.
- No rubric or benchmark lives in this plugin — leak ranking comes from the Engine.
</guardrails>
