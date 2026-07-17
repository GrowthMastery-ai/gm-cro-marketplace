# Voice card — capture the founder's voice by listening

The funnel and every downstream email must sound like the founder, not like generic
marketing copy written over them. You capture that voice **by listening across the whole
interview** — never by bolting on a "describe your brand voice" question, which produces
adjectives the founder thinks they *should* say rather than how they actually talk.

## What a voice card is

Three parts, persisted to brand voice via the deep-capture write path so it passes the
`hasBrandVoiceOnRecord` gate and steers the build:

1. **Tone words (3–6).** The felt qualities of how they talk — e.g. *warm, plain-spoken,
   anti-hustle, a little wry, grounded.* Derive these from how they actually spoke, not from
   asking "what three words describe your brand."
2. **5–8 real sample phrases.** Actual sentences the founder said during the interview,
   verbatim, that capture their cadence and vocabulary. These are gold — the build uses them
   as the voice fingerprint. Pull them *as they say them*; do not polish them into
   marketing copy.
3. **An explicit ban list.** The words, moves, and tones the founder would never use — e.g.
   *no hype, no "crush it / dominate", no hard dollar figures in body copy, no ALL-CAPS
   urgency, no exclamation stacks.* Ask for this directly once you've heard their voice:
   "Anything that would make you cringe to see under your name?"

## How to capture it

- **Listen for the tells.** Their verbs ("tend", "settle", "sort out" vs "scale",
  "crush", "dominate"), their metaphors, whether they're formal or casual, whether they
  swear, whether they use lowercase or exclamation points.
- **Quote, don't paraphrase.** When a founder says something that sounds exactly like them
  ("I just want people to stop feeling guilty about their own backyard"), save it verbatim
  as a sample phrase.
- **Confirm the ban list explicitly** near the end: "Here's the voice I'm hearing — [tone
  words]. And I'm hearing you'd never do [X]. Right? Anything else that's a hard no?"
- **Reflect the card back** before persisting: "So under your name, everything reads
  [tone], sounds like [a sample phrase], and never [ban]. Good?" A founder who confirms
  their own voice trusts every page that follows.

## Depth bar (exemplar)

The concierge voice card was **anti-hustle, plain-spoken, gentle**: sample phrases in
lowercase, no hard dollar figures in body copy, gentle lowercase subject lines, and a hard
ban on urgency theater. That card became a rule set the entire funnel obeyed. Yours will be
different for a different founder — the point is that it's captured from *their* real voice,
with a real ban list, and it's specific enough to steer every line the build writes.

## Persist

Write the voice card to brand voice through the deep-capture write path (authored-first —
the words are the founder's and yours, never a platform LLM's). Once on record, the
`create_funnel` handoff sees brand voice present and every email default speaks in the
founder's voice.
