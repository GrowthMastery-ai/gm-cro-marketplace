# Handoff + strategy memo

Two things happen once the completeness contract's hard-required set is filled: you drive
the authored-first build handoff, then you hand the founder a plain-English strategy memo
plus the review/approve path.

---

## Part A — The `create_funnel` handoff (authored-first)

You call the `create_funnel` tool (title **"Build my funnel"**). It is authored-first: **you
write the content**, the tool validates and builds deterministically. No platform-key LLM
generation runs on this path (Joe #9).

**Preconditions (all must hold before you call it):**

- The deep-capture intake is persisted to `business_profiles` (Step 5 of the skill).
- **Brand voice is on record** (`hasBrandVoiceOnRecord` passes) — the voice card is saved.
- You have a **recommendation summary** (≥20 chars) — your one-paragraph read of the
  archetype + why it fits this founder.
- The **five scalars** are ready: `offer_name`, `audience`, `price`, `transformation`,
  `brand_voice`.

**What you pass:**

- `archetype`: `"webinar"` or `"application"` (webinar is the default launch archetype).
- `recommendation_summary`: your plain-English rationale.
- `offer_name`, `audience`, `price`, `transformation`, `brand_voice`: the five scalars.
- `training_mode`: `"evergreen"` or `"live"` as the founder chose.
- `authored_config.pages`: one authored page per page in the archetype's sequence
  (registration, watch, enrollment for a webinar). **You author each page's copy** from the
  intake, in the founder's captured voice, honoring the offer/proof/objection strategy and
  the dark-pattern guardrails (no fake scarcity, price shown, no manipulative defaults).

**What comes back:** a **complete funnel as a DRAFT**, campaigns and automation **OFF**,
standing by for approval. Nothing is live; no email will send until the founder approves.

**The approve-flip is not yours.** Shape this handoff to feed the platform's build-parity /
approve path; do not flip draft→live from the interview. Point the founder to the review
surface (below) and let them approve there.

---

## Part B — The 7-part strategy memo

After the draft exists, hand the founder a plain-English memo that reads like a strategist
explaining *why this funnel will convert* — not a build receipt, not a field dump. Seven
parts, each two to four sentences, in their language:

1. **The offer read.** What you're selling, to whom, at what price — and why that shape
   fits. ("A $399 founding-cohort entry into your $2,999 program, so cold traffic can say
   yes without a leap.")
2. **The avatar read.** The one person this whole funnel speaks to, in their lived terms —
   proof you understood them, not a demographic.
3. **The one belief the webinar must shift.** The single core belief change everything
   hinges on ("that they're 'not a designer' — the webinar proves the process does the
   seeing").
4. **The pricing logic.** Why the price/structure is what it is, tied to traffic
   temperature and the value anchor — especially if you ran the price-vs-traffic challenge.
5. **The traffic plan.** Where the first registrations come from and how the message meets
   that temperature (cold vs warm).
6. **The proof you're leading with.** The concrete transformation(s) anchoring the page —
   or, if none yet, the honest plan to lead with story + method + guarantee and add proof
   first post-launch.
7. **The one risk you'd watch.** The single thing most likely to underperform and what
   you'd test first (LIFT/PIE framing) — honest, not a victory lap.

**Tone:** direct, warm, specific, evidence-led — the CRO voice from
`CLAUDE.md`. Lead with the recommendation, then the reasoning. Use the
founder's own numbers.

---

## Part C — Review / approve

Point the founder to the visual review surface and let them approve there:

> "Your funnel's built and standing by as a draft — nothing's live, and no emails send
> until you say go. Here's the plan and why it'll convert: [memo]. You can see the whole
> thing at **`/builder/context`** and approve it there when it feels right. Want to walk any
> part of it together first — the offer, the pricing, or the opening?"

If the founder wants changes, make them (respecting the non-destructive, per-field-approval
write rules) and re-present. The approve action itself lives on the web review surface /
the platform build-parity path — you shaped the handoff to feed it.
