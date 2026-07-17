# De-identifying a call transcript (do this first, in your own environment)

The `gm-cro` connector is a **PHI/PII-free zone**. Strip identifiers from the transcript
**before** any connector call. The connector's server-side detector is only a backstop.

## Checklist

- **Names** — replace prospect, rep, and third-party names with roles: `[REP]`,
  `[PROSPECT]`, `[SPOUSE]`, `[COMPANY]`.
- **Contact details** — remove emails, phone numbers, addresses, and account/booking
  IDs.
- **Health / financial specifics** — remove any diagnosis, medication, clinical detail,
  or specific account/card numbers. Keep only the _features_ that matter for coaching
  (objection type, pricing moment, next-step handling).
- **Free-text quotes** — keep the _shape_ of what was said ("raised a price objection at
  minute 12"), not verbatim identifying content.

## What the Engine actually needs

Coaching-relevant **call features**, not raw content: objection points, discovery depth,
framing of price/value, close attempt, and next-step clarity. Send those, not the
identifiable transcript.

If in doubt, leave it out — a slightly thinner feature set still grades; a leaked
identifier is never acceptable.
