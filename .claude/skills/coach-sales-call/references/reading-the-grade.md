# Reading the grade envelope

`gm-cro › grade_call` returns a wire-safe envelope — the graded read only, never the
scoring formula. Read it in this order:

```jsonc
{
  "score": 0, // 0-100, context — mention it last
  "band": "strong|watch|weak",
  "headline": "One-line read on how the call went.",
  "findings": [
    {
      "code": "...",
      "severity": "high|med|low",
      "evidence": "what in the call drove this",
    },
  ],
  "recommendations": [
    { "action": "...", "rationale": "...", "requiresApproval": false, "priority": 1 },
  ],
  "degraded": false,
}
```

## How to coach from it

1. **Lead with the moment** — the highest-severity `finding` and its `evidence`. That's
   the point that moved (or lost) the deal.
2. **Give the one change** — the `priority: 1` recommendation and its `rationale`.
3. **Band + score last**, as context — not the headline of your coaching.

## The `degraded` flag

If `degraded: true`, full grading is being set up on our side and the read is the
diagnose-only version (no full grade). Do not treat it as a failure — surface the warm
handoff the envelope carries (`/gm-concierge`) and keep coaching from whatever read is present.
**Never** a crash or a 401 — the tool always returns a usable body.

## The evidence rule

Always attribute a finding to its `evidence` (what happened on the call), never to a
threshold or a number the user can't see. The rubric stays server-side; you speak in
terms of what the call actually did.
