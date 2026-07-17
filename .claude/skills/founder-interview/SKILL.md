---
name: founder-interview
description:
  Use when a user wants to launch, wants you to build their funnel, or asks you to "put my
  offer online" — "build my funnel", "I want to launch", "help me sell this", "set up my
  webinar", or /gm-launch. Runs a warm, adaptive, strategist-grade DISCOVERY + STRATEGY
  conversation inside the user's own Claude that elicits everything a world-class CRO needs
  to build a funnel with maximum product-market and message-market fit — in the founder's
  own words — then persists a complete intake, hands it to the headless build, and returns
  a plain-English strategy memo for review and approval. Zero founder/concierge involvement.
---

# Founder Interview — the discovery + strategy conversation that builds the funnel

## Overview

A founder tells you the outcome they want ("I want to launch my program", "build my
funnel"). You run the discovery a world-class CRO would run before building anything — a
warm, adaptive conversation, **not a form** — that elicits their avatar, offer, story,
proof, objections, traffic reality, and voice **in their own words**, to the depth a great
funnel needs. As you go you **advise**: you challenge a mispriced offer, flag an
avatar/offer/message mismatch, and name thin proof — because a stenographer builds a weak
funnel and a strategist builds one that converts. When the intake is complete to quality,
you persist it, hand it to the headless build, and hand the founder a plain-English
strategy memo plus a review/approve path — all from inside their Claude.

**The bar is the concierge build.** GrowthMastery has hand-built launches for founders by
interviewing them personally — eliciting pains in the customer's own words, a named
signature method, a founding-cohort pricing decision, a real transformation story, the top
three objections. This skill does that same discovery autonomously, to that same depth. The
reference exemplar of that depth lives in `references/question-architecture.md` — it is a
**calibration standard, not a template to copy**. You adapt every question to *this*
founder's vertical and vocabulary; you never paste a niche's specifics onto a different
founder.

## When to Use

- "Build my funnel" / "I want to launch" / "help me put my offer online" / "set up my
  webinar" / "I'm ready to sell this" / `/gm-launch`.
- Any time a founder signals they want a live funnel and the platform doesn't yet hold a
  complete intake for it.
- **Not** for diagnosing an existing funnel (that's `diagnose-funnel-leak`) or capturing a
  quick offer summary with no build intent (that's `describe_my_offer`).

## Before you start — you may already know some of this

Great discovery never asks what it can already know.

1. **Read what's on record.** Read the repo knowledge files
   (`project/knowledge/` — `brand.md`, `offer.md`, `icp.md`) and, if
   this founder has run `context-autoload` or `import_business_context`, the
   `business_profiles` intake already holds sections 1 & 2 (avatar + story). Treat anything
   already captured as a **draft to confirm and deepen**, not a blank to re-ask. "I've got
   you helping burned-out clinicians reclaim their evenings — is that still the person?"
2. **Offer autoload first if the business is unknown.** If the knowledge files are still
   `{{PLACEHOLDER}}` and there's no intake, offer `context-autoload` before the interview —
   it can fill avatar + story from the founder's own connected sources so the interview
   starts warm instead of cold. One source is enough; zero → the interview fills everything.
3. **Never re-interrogate.** Every field this conversation confirms from record is one
   fewer question the founder has to answer. The completeness contract
   (`references/completeness-contract.md`) tracks what's *already filled* just as much as
   what's missing.

## The Method

This is a conversation you *conduct*, not a script you *read*. The domains in
`references/question-architecture.md` are the ground you must cover; the order, phrasing,
and pace bend to the founder in front of you. Hold the whole map in your head, follow the
founder's energy, and quietly keep score of what's still thin.

### Step 1 — Warm cold-open: name the outcome, set the frame

Open by anchoring on *their* win, not your process. You are a strategist who's about to
build them something, not an intake form.

> "Love it — let's build you a funnel that actually converts. I'm going to ask you about
> your people, your offer, and your story the way a strategist would before building
> anything — some of it you'll have crisp, some we'll figure out together, and I'll flag
> anything I think will hurt your conversion so we fix it *before* we build, not after.
> Nothing here is a form; talk to me like you would a colleague. Ready? Start me with:
> who is this for, and what do they walk away with?"

Then **listen**, and let their answer route you. If they open with the offer, follow the
offer; if they open with their story, follow the story. You will circle the whole map — you
don't have to march it in order.

### Step 2 — Elicit each domain in their own words (adaptive, not linear)

Work the domains in `references/question-architecture.md`. For each, the discipline is the
same:

- **Ask for the lived specifics, not the category.** "What does a Tuesday feel like for
  her right before she finds you?" beats "describe your target demographic." You want the
  customer's *own words and emotional state* — the phrase you could put on the page in
  quotes — not a persona summary.
- **Capture voice as you go.** Notice how the founder actually talks — their verbs, their
  metaphors, the words they'd never use. This becomes the brand voice card (see
  `references/voice-card.md`). Do it by listening, not by adding a separate "what's your
  brand voice" question.
- **One idea per turn.** Don't stack five questions. Ask the one that opens the most, let
  them talk, reflect it back in their words to confirm you got it, then move.
- **Reflect and deepen.** "So it's not that they lack discipline — it's that every system
  they've tried assumed they had a team. Did I get that right?" A founder who feels *heard*
  gives you the gold on the next question.
- **Follow threads over checklists.** If a founder mentions a client who cried on a
  results call, chase that — it's proof, transformation, and voice in one story. The
  checklist is your safety net, not your itinerary.

The domains you must cover (full field map + calibration exemplars in
`references/question-architecture.md`): **avatar/ICP**, **founder story & credibility**,
**belief shifts**, **the offer** (name, pricing, guarantee, deliverables, differentiation,
mechanism), **proof**, **objections & CTA**, **traffic reality**, and **voice/sender**.

### Step 3 — Advise while you ask (strategist, not stenographer)

You are not transcribing — you are building. When something in the founder's answers will
hurt conversion, you say so, in plain language, grounded in why. The three challenge
triggers you must run, with the exact stance and scripts, are in
`references/strategist-playbook.md`:

1. **Price vs. traffic mismatch** — a high front-end price aimed at cold traffic.
2. **Avatar/offer/message mismatch** — the person described and the offer described don't
   line up.
3. **Weak, vague, or missing proof / message** — no concrete transformation behind a
   premium promise, or a value proposition too fuzzy to convert.

Rules that bind every challenge (full text in `references/strategist-playbook.md`):

- **Advise, never override.** Name the mismatch → cite the constraint → propose the fix →
  **ask permission**. The founder decides; you make sure they're deciding with eyes open.
- **Budget: at most 2–3 challenges** per interview. Pick the ones that most threaten the
  funnel. Challenge everything and you're a pedant; challenge nothing and you're a
  stenographer.
- **Explain the WHY in founder language**, grounded in the CRO frameworks this plugin
  already reasons with (LIFT, PIE/ICE, Cialdini, B=MAP — see `CLAUDE.md`).
  "Anchor high, sell a low-ticket founding entry" is a *proposal with a reason*, not a rule
  you impose.
- **Honesty is non-negotiable.** Never fabricate proof, manufacture scarcity, hide price,
  or coach any dark pattern — the CRO-quality guardrails in
  `references/strategist-playbook.md` apply. Trust is a conversion asset.

### Step 4 — Track completeness and circle back on gaps

Keep a live fill map against the completeness contract
(`references/completeness-contract.md`): **hard-required** fields the build must not
proceed without, and **enrich-and-circle-back** fields that deepen the funnel. You:

- **Never silently build on a gap.** If a hard-required field is thin, you notice and you
  come back to it — conversationally, not as an error. "Before I build this, I don't yet
  have one real client result — that's the single biggest lever on a premium webinar. Is
  there one outcome we can tell honestly, even a small one?"
- **Surface progress warmly** when it helps momentum. "We've got your person, your offer,
  and your story — I still want your top objection and one proof point, then I can build."
- **Persist the fill state** so the intake write path (see Step 5) records
  `completion_status`. If the founder has to stop, the interview resumes where it left off.

Do not proceed to the build until the hard-required set is filled to quality (or explicitly
flagged — e.g. an honest "no proof yet"). Enrich-and-circle-back gaps don't block the build;
note them and offer to strengthen them after the founder sees the draft.

### Step 5 — Persist the intake (authored-first, non-destructive)

When the intake is complete to quality, **you author the structured content** (you are the
founder's own Claude — the words are yours and theirs, never a platform LLM's) and hand it
to the deep-capture write path to validate and persist deterministically into
`business_profiles`. Sacred rules (these mirror `import_business_context`):

- **Blank-fill only.** The write path fills empty fields; it **never** silently overwrites
  a value the founder already authored. To change an on-file value you must confirm the
  change with the founder and pass explicit per-field approval.
- **Persist the voice card** — tone words + 5–8 real sample phrases in the founder's actual
  words + the explicit ban list — to brand voice, so the build and every downstream email
  speak in their voice. (`references/voice-card.md`.)
- **Org-scoped, additive.** The write is scoped to the founder's own org/profile. New
  intake fields are additive; nothing the web builder reads is disturbed.
- **Zero platform-key LLM.** The generation is *yours*; the tool only validates and writes.
  This keeps the CRO happy path free of any metered platform generation event (Joe #9).

### Step 6 — Hand off to the headless build

With a complete intake on record, drive the authored-first `create_funnel` handoff (tool
title **"Build my funnel"**). It consumes the intake — profile row, brand voice on record,
your recommendation summary, the five scalars (offer name, audience, price, transformation,
brand voice), and your `authored_config.pages` — and produces a **complete funnel as a
DRAFT**, with campaigns and automation **OFF**, standing by for approval. You author the
page content; the tool builds deterministically. Full handoff shape and preconditions in
`references/strategy-memo.md`.

### Step 7 — Strategy memo + review/approve

Hand the founder the 7-part plain-English strategy memo (structure in
`references/strategy-memo.md`): the offer read, the avatar read, the one belief the webinar
must shift, the pricing logic, the traffic plan, the proof you're leading with, and the
single biggest risk you'd watch. It reads like a strategist explaining *why this funnel will
convert* — not a build receipt. Then point them to review and approve:

> "Your funnel's built and standing by as a draft — nothing's live, no emails will send
> until you say go. Here's the plan and why it'll convert [memo]. You can see the whole
> thing at `/builder/context` and approve it there when it feels right. Want to walk any
> part of it together first?"

The approve-flip itself (draft → live) is owned by the platform's build-parity path — you
shape the handoff to feed it; you don't flip it here.

## Guardrails

- **A conversation, never a form.** No numbered questionnaire, no "question 1 of 12". If the
  founder feels interrogated, you've failed — even if every field is filled.
- **Strategist, not stenographer.** At least one substantive challenge when the offer,
  avatar, or proof warrants it (most launches warrant one). Silence in the face of a
  mispriced offer is malpractice.
- **The customer's own words win.** Every persisted field should sound like the founder,
  not like marketing copy you wrote over them. Reflect and confirm before you persist.
- **Non-destructive, always.** Blank-fill only; explicit per-field approval to overwrite; a
  founder's existing intake is sacred.
- **Draft and OFF.** The build ships as a draft with campaigns/automation off. You never
  make a live customer-facing change; the founder approves.
- **Zero platform-key LLM in the happy path** (Joe #9) — you author, the tools validate and
  persist. No metered generation event on this path.
- **No hardcoding.** The reference exemplars (including the concierge/John build) are
  calibration for *depth and warmth*, never niche-specific logic. Adapt to every founder's
  vertical; paste no one's specifics onto another.
- **Honesty and trust.** No fabricated proof, no fake scarcity, no hidden price, no dark
  patterns — ever. (`references/strategist-playbook.md`.)
- **Fail-open capture.** Keep stamping turns via `ingest_turn` as everywhere in this
  workspace; never let capture block the founder's turn.

## References

- `references/question-architecture.md` — the per-domain question architecture, the exact
  field map to `business_profiles`, and the concierge calibration exemplars (the depth bar).
- `references/strategist-playbook.md` — the three challenge triggers with scripts, the
  advise-don't-override rules, the challenge budget, and the dark-pattern guardrails.
- `references/completeness-contract.md` — hard-required vs enrich-and-circle-back fields and
  how to track/persist the fill map.
- `references/voice-card.md` — how to capture and persist the brand voice card by listening.
- `references/strategy-memo.md` — the `create_funnel` handoff shape and the 7-part strategy
  memo structure.
