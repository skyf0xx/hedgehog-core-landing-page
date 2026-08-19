---
name: landing-copy-headline
description: Use whenever `landing-builder` drafts the page headline (Chain Method Stage 4). Gives the 8 named rhetorical mechanisms, the outcome-subject test, the first-time-reader (curse-of-knowledge) test, and the selection procedure for generating 3 distinct-mechanism candidates and presenting them for the user's lock. Trigger on "write the headline", "headline candidates", or the start of `landing-builder`'s headline stage.
---

# Landing Copy: Headline

The headline is the single highest-leverage line on the page — every
section beneath it either delivers on its promise or doesn't. This skill
is the algorithm `landing-builder` runs to generate it: don't
draft headline wording by feel, run the mechanism generation and the
outcome-subject test below every time.

This skill covers the headline only. The subhead or lede immediately
beneath it, if the page has one, is drafted at a later stage using
`landing-copy-hero` skill — a different section, a different algorithm.

## Step 1: Pull the raw material, don't invent it

Read, don't re-derive:

- The subject/audience/job statement — the concrete claim available to
  make
- The adjective pairs and their named opposites — what the headline is
  allowed to promise emotionally
- The voice spec — sentence rhythm, verb mode, user-side
  naming

Every candidate below is generated from this material. A headline that
doesn't trace to a specific adjective or the subject statement fails
the traceability self-check later — catch that here, not there.

## Step 2: Generate one candidate per mechanism

Generate against at least 3 of these 8, chosen as whichever the subject
statement actually supports — not the same 3 by default on every build:

- **Outcome** — state the desired outcome directly ("Build software
  that holds together.")
- **Transformation** — current state → desired state ("Turn ideas into
  products people use.")
- **Tension** — expectation → contradiction ("Your product is ready.
  Your story isn't.")
- **Reframe** — common frame → stronger frame ("Your website isn't a
  brochure. It's a decision engine.")
- **Provocation** — command → uncomfortable truth ("Stop building
  features nobody asked for.")
- **Identity** — audience → belief or standard ("For teams that refuse
  to ship generic software.")
- **Mechanism** — how it works → implied benefit ("A disciplined path
  from schema to screen.") — use only when the mechanism itself is the
  distinctive, ownable claim; it still has to pass Step 3.
- **Curiosity** — open question → implied possibility ("What happens
  when your tools finally work together?")

Generate from **distinct mechanisms**, not three phrasings of one idea —
the point is testing which mechanism the subject statement actually
supports, not polishing a single guess.

## Step 3: The outcome-subject test (run on every candidate)

**The reader wants an outcome, not the mechanism that produces it** — the
headline's grammatical subject must be what the reader gets (what
changes for them, what they now have or no longer have to worry about),
not the product, feature, or mechanism that delivers it.

Run this test by reading only the headline, with no subhead for context:
does it state what the reader gets, or does it name the thing that gets
it to them?

- "One signature. Three uses." **fails** — the signature is the subject.
- "Your agent's work outlives the session that made it." **passes.**

A headline built from the subject statement's own phrasing ("ZenBin is
one cryptographic trust primitive...") tends to smuggle the mechanism
into the subject position by default — naming it is not the same as
leading with it. Demote the mechanism one level: it belongs in the
subhead or the sentence right after, earning its specificity once the
outcome has already landed. If a candidate only works because the reader
already knows what the mechanism is for, it's failing this test, not
passing it narrowly.

**This test overrides mechanism choice.** An Outcome- or
Transformation-mechanism candidate that fails it still fails, and a
Mechanism-mechanism candidate that passes it is still eligible. Rewrite
or cut any candidate that fails before Step 4.

## Step 3.5: The first-time-reader test (run on every candidate)

The outcome-subject test checks *what the sentence is grammatically
about*; this test checks a different failure mode — whether parsing that
subject at all requires context the reader doesn't have yet. A headline
can pass Step 3 cleanly and still fail here: naming the reader's outcome
in subject position doesn't help if the outcome itself is only legible
to someone who already knows the frame, the tension, or the stance being
assumed.

This risk concentrates in four of the eight mechanisms by construction —
**Tension**, **Reframe**, **Provocation**, and **Identity** each work by
setting up a frame, contradiction, or stance the reader is assumed to
already hold or recognize, and **Curiosity** withholds the payoff
entirely, by design. Candidates from these mechanisms need this test run
deliberately, not as a formality; **Outcome** and **Transformation** are
lower-risk by construction but not exempt.

Run it by reading only the headline, cold, as a first-time visitor with
zero context would: **does the line require the reader to have already
inferred a frame, a tension, or a stance that hasn't been stated yet?**

- "Your website isn't a brochure. It's a decision engine." **fails** —
  the reader has to already accept "brochure" as the wrong frame before
  the reframe lands; nothing in the line itself establishes that.
- "For teams that refuse to ship generic software." **fails** — assumes
  the reader already self-identifies with the stance being named.
- "Your agent's work outlives the session that made it." **passes** —
  every term is legible cold; no prior frame is assumed.

A candidate that fails this test is not automatically cut — some subject
statements genuinely support an indirect mechanism better than a direct
one — but it needs either a rewrite that establishes the missing frame
within the line itself, or an explicit flag to the user at Step 5
("this candidate assumes prior context; pick it knowingly, not by
default"). Never present a candidate that fails this test as
indistinguishable in risk from one that passes it.

## Step 4: Apply the writing standard

Scoped to a single line — the same bar `landing-builder` holds section
copy to:

- **Cut inflated words.** No "delve," "landscape," "robust,"
  "comprehensive," "leverage," "seamless," "cutting-edge," "elevate,"
  "unlock," "empower," "streamline," "game-changer," "harness,"
  "revolutionize," or any word from that register.
- **No negation formulas.** Never write "It's not X — it's Y."
- **No em dashes.** Use a comma, period, or restructure the sentence.
- **Concrete over abstract.** A claim like "significant improvement"
  ships only with the number, name, or comparison that makes it
  checkable. If the brief doesn't supply one, the claim doesn't ship in
  that form.

## Step 5: Select and present

Select the 3 strongest, distinct candidates that survived Steps 3, 3.5,
and 4. Label each with its mechanism name and present all 3 to the
user — this is a hard stop; wait for an explicit pick (the other 2 stand
as backups) or a redirect. Where a presented candidate failed Step 3.5
and was kept anyway (rewrite wasn't viable, or the indirect mechanism
genuinely fit the subject statement best), flag that plainly alongside
it, not silently. Every section written afterward is
checked against whichever headline locks here, so an unconfirmed pick
compounds the same way an unconfirmed subject statement does at strategy
step 1.

## Self-test

- All 3 presented candidates came from 3 distinct mechanisms, not 3
  phrasings of the same one.
- Every candidate traces to a named adjective or the subject statement —
  a line that could run on a competitor's page unchanged (the swap test)
  was rewritten before presenting, not left for the traceability
  self-check to catch.
- Every candidate was run through the first-time-reader test
  individually (Step 3.5), not waved through because the outcome-subject
  test already passed — the two check different failure modes. Any
  candidate presented despite failing it carries an explicit flag to the
  user, not a silent pass.
- Every candidate passed the outcome-subject test individually — not
  waved through because the set as a whole "feels balanced."

## Constraints

- Never present fewer than 3 distinct-mechanism candidates.
- Never lock a headline without the user's explicit confirmation — the
  user must be shown all 3, labeled by mechanism, and explicitly pick or
  redirect, not be assumed to have chosen.
- Never draft the subhead, section body, or CTA copy here — that's
  the `landing-copy-hero` and other section skills, run only after this
  one locks.
