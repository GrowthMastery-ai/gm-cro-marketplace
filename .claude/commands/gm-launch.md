---
description:
  "Build your funnel from a warm, strategist-grade discovery conversation — the CRO
  interviews you, advises you, builds a complete draft, and hands you the plan to approve.
  Zero forms, zero concierge."
version: 1.0.0
---

# /gm-launch — Build my funnel from a discovery conversation

<objective>
Turn "I want to launch" into a complete funnel standing by for approval — by running the
discovery a world-class CRO would run first. Delegates to the `founder-interview` skill,
which elicits the founder's avatar, offer, story, proof, objections, traffic, and voice in
their own words, advises where the offer or message will hurt conversion, persists a
complete intake, hands it to the authored-first headless build (`create_funnel`), and
returns a plain-English strategy memo plus a review/approve path. A conversation, never a
form.
</objective>

<user-provides>
The outcome they want in plain words ("build my funnel for my coaching program", "I want to
launch my course"). Everything else the interview elicits conversationally.
</user-provides>

<steps>
1. Invoke the `founder-interview` skill. If the business is still unknown (knowledge files
   are `{{PLACEHOLDER}}` and there's no intake), it offers `context-autoload` first so the
   interview starts warm; otherwise it confirms and deepens what's already on record.
2. It runs the adaptive discovery — covering every domain, advising on price/traffic,
   avatar/offer/message fit, and proof as it goes — and tracks the completeness contract,
   circling back on gaps rather than building on them.
3. On completeness, it persists the deep-capture intake (authored-first, non-destructive),
   drives the `create_funnel` handoff to a complete DRAFT (campaigns/automation OFF), and
   returns the 7-part strategy memo + the `/builder/context` review/approve path.
</steps>

<guardrails>
- A conversation, never a form; the founder's own words win; strategist, not stenographer.
- Non-destructive persistence: blank-fill only, explicit per-field approval to overwrite.
- Ships as a DRAFT with campaigns/automation OFF — the founder approves; nothing goes live
  from here.
- Authored-first: no platform-key LLM generation in the happy path (Joe #9).
- No fabricated proof, no fake scarcity, no hidden price — CRO-quality guardrails apply.
</guardrails>
