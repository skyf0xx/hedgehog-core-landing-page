---
name: hedgehog-landing-loop
description: Use for every unit of work on the landing-page core, from planning intake through the final build phase — the Chain Method's brief → feeling → tokens/element → sequence → artifact pipeline, gated by `hedgehog verify` and committed one phase at a time. Triggers on "next step", "next phase", "what's next", or the start of any work session on a bootstrapped landing-page project. Also covers this core's own planning intake and Correction Protocol.
---

# Hedgehog Landing Loop

The operating loop for a bootstrapped `landing-page` project. The
claim, dispatch, verify cycle, the Friction log, the Correction Protocol,
its Post-build entry, and the Stop Condition are owned by
`hedgehog-orchestrating` (its `## The cycle`, `## Friction log

`hedgehog-orchestrating`'s `## Friction log` applies. On this core, the
friction worth logging includes a stage's instructions unclear and the
traceability self-check redlining the same underlying gap twice.

## Correction Protocol

`hedgehog-orchestrating`'s `## Correction Protocol` applies, triggered
most often by Stage 6's traceability self-check surfacing something that
doesn't trace back to the subject statement or matches a known
AI-default cluster. Core-specific additions:

- **Chain files are patched in place.** `.hedgehog/chain/*.md` hold each
  stage's reasoning; the protocol's patch step edits the upstream
  stage's file, and the commit messages explain the change.
- **Fast-forwarding ripples further.** A token system change (Stage 2)
  ripples through the signature element (same stage), the sequence
  (Stage 3), the headline (Stage 4, if the voice spec shifted, re-run by
  `landing-copywriter`) and the locked section copy (Stage 5, re-drafted
  by `landing-copywriter` for whichever sections the patch actually
  touches, still passing through the AI-tell self-check before it counts
  as locked again), and the build (Stage 7) — each its own small commit,
  in order.
- **Re-run Stage 6's traceability self-check against the patched chain
  before resuming**, since traceability is what the whole chain rests on.
- `landing-builder` re-runs the affected stage when the patch is to a
  stage it owns directly (1, 2, 3, 6, 7); `landing-copywriter` re-runs
  Stage 4 or re-drafts the affected Stage 5 sections.

### Post-build entry

`hedgehog-orchestrating`'s `### Post-build entry` applies; the return
target is `tweaker`. This core routes here for two reasons: something
structural is wrong rather than small (the voice spec itself rather than
one line of copy), or new scope is genuinely additive but has nowhere
else to go — a new section under a brief that still holds, since this
core has no module axis for `planner`'s Re-entry pass to add an intent
to. In the additive case the protocol's "patch" step reads as "add".
Stage 6's traceability self-check re-runs against the patched chain
before handing back.

## Phase Transition Checks

Before `landing-builder`'s Stage 2 starts, confirm Stage 1's subject/
audience/job statement has been shown to and confirmed by the user — not
just drafted. This is the cheapest point in the whole chain to correct
the core framing (nothing downstream exists yet); every stage after it
inherits that framing silently, and by the time copy is reviewed at
Stages 4–5, a wrong framing means unwinding several committed stages via
the Correction Protocol instead of one free revision here. If Stage 1
was run by a delegated `landing-builder` subagent instance, the
confirmation reaches it as a relay from the orchestrating session — see
The Loop above for the provenance statement that relay must carry.

Before Stage 5 starts, confirm Stage 4's headline has been presented to
and locked by the user, not just drafted — the page's section copy is
written against whichever headline is locked at Stage 4, so an unlocked
headline means the copy written against it is provisional too. Both
checkpoints run inside `landing-copywriter`'s own session, since it owns
both stages.

Before Stage 6 starts, confirm Stage 5's full section copy has been
presented to, locked by the user, and passed its AI-tell self-check —
Stage 6's traceability check reads confirmed, self-checked copy, not a
draft still awaiting review or still carrying an open finding.

Before Stage 7 starts, confirm:

- Stage 6 resolved clean, not with an open finding — a chain that hasn't
  cleared Stage 6 never reaches Stage 7; an open finding routes back to
  the stage it names.
- `hedgehog status` shows the `sequence` task `complete` (Stages 1–5's
  commits have landed).

Before `landing-builder`'s Stage 1 starts, confirm planning intake's
Confirm & Lock has held and its commit has landed. If not, stop and ask.

Before the Polish Loop starts, confirm `hedgehog status` shows the
`artifact` task `complete` — `landing-builder`'s initial build has
landed. The Polish Loop never opens against an unbuilt or partially
built page.

## Polish Loop

Once the `artifact` task's `hedgehog verify` commits `feat(landing):
build`, the compiled graph is done, but the orchestrating session runs one more uncompiled
pass before offering the Stop Condition's handoff: a bounded loop
(`landing-executor` plus `landing-visual-reviewer` and
`landing-ux-reviewer`, up to 10 iterations) that polishes the rendered
page for visual and interaction quality independent of the chain's own
traceability concerns. This is not a compiled layer — no `hedgehog
claim` packet, no `hedgehog verify` gate. See
[the Polish Loop](references/polish-loop.md) for the full step sequence,
the decision rule for exiting or iterating, and why it's separate from
Stage 6. The iteration number is the count of `feat(landing): polish
iteration <n>` commits (`git log --grep "polish iteration"`) made since
the loop was last opened.

At the 10-iteration cap with redlines still open, record each open
redline with `hedgehog debt add LANDING-ARTIFACT "<redline>"`, then
commit the records (`chore: build graph records`) so they survive
`/clear`.

## Rules

- **No stage introduces a choice that doesn't originate in an earlier
  stage's output.** This is the chain's core discipline — enforced by
  Stage 6's traceability self-check, not by tooling, so treat a Stage 6
  finding with the same weight a failed typecheck gets elsewhere in
  Hedgehog.
- **Ingredients move in agreement.** Color, type, space, motion, copy
  rhythm, and pacing are reconciled into one system at Stage 2 — a
  mismatch (warm color, cold type) is a defect fixed there, not in a
  later polish pass.
- **Sequential except Stage 2's two parallel inputs.** The dial table
  and the voice spec, inside Stage 2, read the same sorted-adjectives
  input and can be produced together; every other stage waits on the one
  before it. This is design, not a gap to close: the chain is a linear
  sequence, so there is no scheduler fan-out to reason about here.
- **A wrong stage gets fixed at its source** — the Correction Protocol,
  not a downstream workaround (e.g. don't patch Stage 7's output to fix
  a token that's wrong at Stage 2).
- **The traceability self-check is real, and it blocks the build.**
  Stage 6 can send the chain back to any earlier stage, naming which
  check failed, before Stage 7 starts — a finding there stops the build
  the same way a failed gate stops a commit elsewhere in Hedgehog. It's
  `landing-builder` checking its own work at the same self-graded trust
  level every self-test in this discipline carries, not a second agent's
  veto — there is no separate agent positioned to check this chain from
  outside it, and this core doesn't claim otherwise.

## Stop Condition

`hedgehog-orchestrating`'s `## Stop Condition` applies, with one
difference: offer the fresh-context handoff once the Polish Loop above
has exited (clean or capped), not at the `artifact` task's completion
directly. The `artifact` task being
`complete` opens the Polish Loop; the Polish Loop exiting is what actually
ends the build session. The subject statement or an adjective being
genuinely ambiguous mid-chain is the other, earlier trigger, same as
before. Nothing gets deleted either way — the permanent record is the
committed intent (`.hedgehog/intents/landing.json`), `.hedgehog/chain/`,
the friction log, and the git commit history itself, including every
`feat(landing): polish iteration <n>` commit the loop made.
`.hedgehog/hedgehog.db` is gitignored: a derived index, rebuildable at
any time via `hedgehog db rebuild`.

Confirm it with `hedgehog boundary` before offering the handoff: it exits
0 only when nothing is in flight, the working tree is clean, and the last
closed task completed its intent, and names which of the three failed
otherwise. `hedgehog quiesce` answers only the in-flight third — the
right check while waiting out a correction, not the one for clearing
context. The same command is what decides any mid-chain `/clear` too, and
`hedgehog boundary --handoff` prints the block the next session opens
with: where the build is, what's next and why, and what's blocked.

Tell the user plainly that the build (including the polish pass) is
complete, and that clearing context now costs nothing — the chain
artifacts, the build graph, and the commit log hold everything a fresh
session needs. Name **both** ways forward:

- **Adjustments to what's built** — a `tweaker` session, in a *new* chat
  window, not a subagent call inside this one. Tell the user plainly:
  close this chat window and open a new one, then paste this to start
  it:

  > The build is complete — `landing-builder` and `landing-copywriter`
  > built the page and its copy, and the Polish Loop (`landing-executor`
  > plus `landing-visual-reviewer` and `landing-ux-reviewer`) has
  > finished polishing it. Use the tweaker agent: first review the
  > friction log and ask me for feedback on the build, then take my
  > tweak requests one at a time.

  If the Polish Loop exited at its 10-iteration cap with redlines still
  open, say so in this handoff and name the debt records
  (`hedgehog debt list LANDING-ARTIFACT`), so the fresh `tweaker`
  session treats those as its first tweak requests rather than assuming
  the page is fully clean.

**New scope** — anything beyond adjusting what exists — and on this
core the deciding question is whether `.hedgehog/chain/00-brief.md`
still holds:

- **It holds** (a new section on a page whose subject, audience, and
  job are unchanged): this core has no module axis to add an intent
  to — the `landing` intent already compiles into the fixed five-phase
  chain, and a section is new content inside phases already `complete`,
  not a new graph row. Route it to the Correction Protocol's post-build
  entry instead of `planner`: run `landing-builder` again to place the
  new section in the beat structure (Stage 3), hand off to
  `landing-copywriter` to draft its copy (Stage 5, locked only once its
  AI-tell self-check passes), re-run the traceability self-check
  (Stage 6) against the full patched chain, then rebuild (Stage 7) —
  each its own small commit, same as any other correction.
- **It doesn't hold** (a different subject, audience, or job): that's a
  different page, and belongs in its own landing-page project via
  `planner`'s first run there, not an edit to this one's locked brief.
  Never rewrite `00-brief.md` to accommodate new scope — it's the root
  every stage's traceability audit walks back to.

Don't start making tweaks or planning new scope in the current,
already-large context; that's what the fresh session is for.
