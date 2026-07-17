# Completeness contract — the interview is done only when…

Modeled on the discipline of `lib/funnels/completeness-contract.ts`: a set of fields, each
with a severity, that you track a live fill map against. The interview does not hand off to
the build until the **hard-required** set is filled to quality (or an explicit honest flag
stands in for it). **Enrich-and-circle-back** fields deepen the funnel but do not block the
build — you note them and offer to strengthen them after the founder sees the draft.

You are *not* running a checklist in front of the founder. You hold this map in your head,
keep quiet score as the conversation flows, and circle back conversationally on what's thin.
Persist the fill state to `business_profiles.completion_status` so the interview can resume
if the founder stops.

---

## Hard-required (the build MUST NOT proceed without these)

If any of these is missing or thin, circle back before handing off. These are the fields
without which the headless build cannot produce a funnel worth approving:

| Field | Filled to quality means… |
|---|---|
| `offer_name` + `pricing` | A named offer with a real price (and, if you ran the price-vs-traffic challenge, the chosen pricing structure + its logic). |
| `transformation` | The concrete before→after in the customer's terms — not "live better." |
| `ideal_customer` | A lived, specific person (the "Tuesday", not the demographic). |
| `primary_channel` + existing audience | How the first registrations will actually arrive, and whether traffic is warm or cold. |
| Brand voice on record | `hasBrandVoiceOnRecord` passes — the voice card is captured (see `voice-card.md`). |
| ≥1 proof point **OR** honest "no proof yet" flag | One concrete transformation captured, **or** an explicit, honest no-proof flag that reshapes the strategy. Never a fabricated stand-in. |
| `signature_method` | A named method/process (even one you helped the founder name from their real steps). |
| `top_objections` (≥1) | At least the single biggest real reason people don't buy, with its honest answer. |

**The honest-flag rule:** a hard-required field can be satisfied by an explicit honest flag
where a real value doesn't exist yet (most commonly proof). The flag is captured truthfully
and the strategy adapts around it (see strategist playbook). A flag is *not* permission to
skip the conversation — you still ask; you just record the true answer.

---

## Enrich-and-circle-back (deepen the funnel; do not block the build)

Capture these where the conversation offers them; circle back to strengthen after the draft:

- `secret_desires`, `empowering_truths`, `limiting_beliefs` (deeper avatar interior)
- `root_cause`, `common_mistakes`, `daily_pain_points` (fuller problem texture)
- 2nd and 3rd `top_objections` with answers
- `guarantee`, `bonuses`, `deliverables` detail, `differentiation`, mechanism explanation
- `struggle_story`, `breakthrough_moment`, `credibility_experience` (fuller founder story)
- The three belief shifts (`external`/`internal`/`vehicle`) beyond the one core shift
- `impact_metrics`, structured testimonials, `credentials` (proof depth beyond the first)
- `sender_name` / `sender_email` if not yet confirmed

---

## How to track and circle back

1. **Keep a live tally.** After each exchange, note silently which hard-required fields are
   now filled to quality and which are still thin.
2. **Circle back conversationally, never as an error.** "Before I build this, I still want
   the one thing that moves a premium webinar most — a real client result. Got one?" Not:
   "ERROR: proof_points is empty."
3. **Surface progress to keep momentum.** "We've got your person, your offer, and your
   story — I need your top objection and one proof point and then I can build."
4. **Persist the fill map** via the deep-capture write path to `completion_status`, so a
   resumed session picks up exactly where this one stopped.
5. **Gate the handoff.** Do not call `create_funnel` until every hard-required row is
   filled to quality or carries an honest flag. Enrich gaps ride along and get strengthened
   after the founder sees the draft.
