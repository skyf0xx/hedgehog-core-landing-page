---
name: landing-copy-hero
description: Use whenever `landing-builder` drafts the section directly beneath the locked headline — the subhead/lede that makes the headline's claim credible. Trigger when the section's role is "hero support" in the sequencing stage's list, distinct from the headline itself (`landing-copy-headline`) or the problem/agitation section (`landing-copy-problem`).
---

# Landing Copy: Hero (subhead/lede)

The hero section's job is narrow: make the headline's claim credible in
one breath, before the reader has committed to reading further. It is not
the place to make the full case — that's every section after it. A hero
section that tries to argue, prove, or handle objections has taken on a
different section's job.

This skill covers the section immediately beneath the locked headline
only. The headline itself is drafted using the
`landing-copy-headline` skill, at an earlier stage of `landing-builder`'s
run.

## What this section answers

One question, in this order:

1. **What is the mechanism, named plainly?** The headline led with the
   outcome and deliberately withheld the mechanism (per
   `landing-copy-headline`'s outcome-subject test) — this section is
   where that mechanism gets named, in plain language, for the first
   time.
2. **Why should the reader believe the headline's claim is achievable,
   not aspirational?** One line of credibility, not a proof point (proof
   points belong to `landing-copy-proof`) — a plain statement of how the
   mechanism gets the reader from their current state to the headline's
   promise.

## The algorithm

Per this core's fixed paragraph algorithm (`landing-builder`'s own
file): this section's paragraph count is set by however many beats the
sequencing stage assigned it, almost always 1 (a hero is rarely a
multi-beat section). Within that single paragraph:

1. **Sentence 1 — name the mechanism.** Plain verb, plain noun. No
   abstraction standing in for the thing itself (the same plain-verb
   discipline applied at the subject-statement stage).
2. **Sentence 2 (only if the beat has room) — the credibility bridge.**
   One sentence connecting the mechanism to the headline's promise: how
   doing this thing gets the reader that outcome. Not evidence, not a
   number — that's `landing-copy-proof`'s job — just the logical link
   made explicit.

Two sentences is the ceiling for a single-beat hero. If it's taking a
third sentence to make the mechanism credible, the mechanism itself is
underspecified — flag it back rather than padding the section to compensate.

**Write the mechanism sentence at the voice spec's actual register, not
a neutral default.** The hero sits directly under the headline with the
least room of any section to build up voice — that makes it the section
most likely to default to flat, procedural phrasing (a hedged, passive
restatement of the mechanism) even when the voice spec calls for
something blunter. Naming the mechanism plainly (per Sentence 1 above)
and naming it at the target register are two different checks — a plain
sentence can still be flat if it's hedged, passive, or abstract where
the register calls for short and direct. Neither is a Writing standard
violation to route around; both are the same instruction applied more
literally.

## Writing standard (this section's delta from `landing-builder`'s full standard)

- **No proof, no numbers, no named evidence here.** A stat or case study
  in the hero section is `landing-copy-proof`'s content pulled forward —
  redirect it downstream, keep this section to the plain claim.
- **No objection-handling here.** "But you might be wondering..." belongs
  to `landing-copy-objection`, not this section.
- Match the token system's CTA styling intent only if this section
  carries a CTA (rare — most builds put the CTA in `landing-copy-cta`'s
  section instead).

## Self-test

- The mechanism is named in plain language, not gestured at.
- The sentence is written at the voice spec's named register, not a
  neutral procedural default — read it cold: does it sound like the
  target register, or like a specification restated in prose? The
  latter fails even if the mechanism is technically named plainly.
- Paragraph count matches the beat count the sequencing stage assigned —
  1 paragraph for a single beat, not padded to 2 for weight.
- Read against the locked headline: does this section make the headline
  more believable, or does it just restate the headline in different
  words? Restating fails this test.

## Constraints

- Never draft the headline itself — that's `landing-copy-headline`,
  already locked before this section starts.
- Never pull proof points, stats, or objection-handling into this
  section to make it feel more substantial — a thin hero section is
  correct; padding it borrows from a downstream section's job.
