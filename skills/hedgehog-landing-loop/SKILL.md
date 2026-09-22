---
name: hedgehog-landing-loop
description: Use for every unit of work on the landing-page core, from planning intake through the final build phase — the Chain Method's brief → feeling → tokens/element → sequence → artifact pipeline, gated by `hedgehog verify` and committed one phase at a time. Triggers on "next step", "next phase", "what's next", or the start of any work session on a bootstrapped landing-page project. Also covers this core's own planning intake and Correction Protocol.
---

# Hedgehog Landing Loop

The operating loop for a bootstrapped `landing-page` project: `hedgehog
claim --owner <owner> --count <n>` emits the packet for one ready phase
(this core's chain is linear, so `--count N` always returns 1), run it
through its owning agent, `hedgehog verify` gates and commits it. The
build graph (`.hedgehog/hedgehog.db`) is the live list — query it via
`hedgehog status`/`hedgehog ready`, never re-derive state from prose. The
five compiled phases (this core's `workspace/core.yaml`, already
the source of truth) are the degenerate one-module case of the layer
graph: one task per phase, each depending on the one before it.

This is the **Chain Method**: a pipeline where every visual choice traces
back to a reason. No stage may introduce a choice that doesn't originate
in an earlier stage's output — that discipline is what this skill
enforces mechanically, the same role Nx module boundaries play for
`full-stack-app`.

## Planning intake (Phase 0, before any build phase)

Run once, before `bootstrap` scaffolds the workspace — the vendored BMAD
shelf plus this core's own subject-statement mining into
`.hedgehog/chain/00-brief.md`, ending in Confirm & Lock. See
[planning intake](references/planning-intake.md) for the full procedure.
`planner` owns this section; see that agent for when it runs.

## The Chain Method stages

`landing-builder` runs Stages 1–3 and 6–7 directly, and delegates Stages
4–5 (headline and section copy) to `landing-copywriter` — every stage
runs in this exact order, in one continuous session across the two
agents, from the confirmed subject statement through the built page.
See [the Chain Method stages](references/chain-stages.md) for the full
stage table (what each stage runs, produces, and which compiled layer
and commit it bundles into) and the literary/design grounding each
stage's judgment calls draw on.

## The Loop (every unit of work)

1. **Run `hedgehog claim --owner <owner> --count <n>`.** `<owner>` is
   this session (a stable id — session id or equivalent). It emits the
   task packet for one ready compiled layer (STATUS/INTENT/RELEVANT
   RULES/INHERITED DEBT/WHY NOW/BLOCKED DOWNSTREAM/ALLOWED
   SCOPE/VERIFICATION) — trust it: `hedgehog claim`
   never hands out a layer whose dependency isn't `complete`, so there's
   no separate gate check to run by hand. This core's chain is linear, so
   `--count N` always returns 1 task, never more — see Rules below.
   `hedgehog ready` previews the same decision without claiming anything.
2. **Map the packet's layer to the stages it bundles**, per [the Chain
   Method stages](references/chain-stages.md) table (`feeling` = Stage 1,
   `tokens` = Stage 2, `sequence` = Stages 3–5, `artifact` = Stages 6–7),
   and **delegate to `landing-builder`,
   which runs every stage inside the claimed layer in one continuous
   session**, passing the full chain so far (every upstream artifact, not
   just the immediately prior one) — an agent that only sees its direct
   input can't verify its own traceability back to the subject statement.
   If a dispatch by name reports `landing-builder` or `landing-copywriter`
   as not found — expected right after `init`/`update` installed it this
   same session — see root CLAUDE.md's "Delegating on this host" note
   rather than treating it as fatal.
   For the `sequence` layer, `landing-builder` runs Stage 3 itself, then
   hands off to `landing-copywriter` for Stages 4–5, passing it the same
   full chain plus Stage 3's own output, and resumes only once
   `landing-copywriter` reports the headline and the full set of section
   copy locked — `landing-builder` still presents the whole layer's
   artifact and runs its own self-test against `landing-copywriter`'s
   output before the task is ready for `hedgehog verify`. Within a
   bundled layer, its stages run in order and in one continuous pass:
   Stage 4 locks the headline first, then Stage 5 drafts every section's
   copy in one pass against Stage 3's locked section list and runs the
   AI-tell self-check on the full draft before it's presented for lock,
   all still inside the one `sequence` task.

   **Relaying a live user-confirmation checkpoint to a delegated
   subagent.** Stage 1 carries a hard-stop checkpoint per Phase
   Transition Checks below, and a delegated `landing-builder` subagent
   instance has no channel for the user to address it directly. The
   orchestrating session relays the confirmation instead, and the relay
   is sufficient only if it quotes the user's actual words with its
   provenance stated plainly (*"Relaying the user's own confirmation,
   verbatim — user said: '\<exact words\>'"*) rather than asserting the
   outcome ("the user approved"). This trusts the orchestrator's honesty
   about provenance, the same trust the rest of this discipline already
   places in it for relaying artifacts and task packets.
3. `landing-builder` and `landing-copywriter` each **run their own
   self-test** at every stage they own (see each agent's own file for
   what each stage checks) before presenting its artifact — necessary,
   not sufficient. This is a sanity check the owning agent does for
   itself; neither moves the task and neither commits its own work,
   whether run directly or delegated to a subagent instance. Committing
   is always the orchestrating session's act via `hedgehog verify`,
   regardless of which agent or stage produced the artifact —
   `landing-builder` carries `Bash` for running dev/build/lint commands
   during Stage 7, and `landing-copywriter` carries it only for
   reading/opening files, neither for writing commits itself, so this
   stays consistent with every earlier stage's commit path.
4. Once every stage inside the packet's layer has been presented and
   locked by the user, **run `hedgehog verify <task-id> --owner
   <owner>`.** It checks the touched files against the packet's ALLOWED
   SCOPE, runs the layer's `VERIFICATION` command, and on a pass writes
   the commit (the exact Conventional Commit message from [the Chain
   Method stages](references/chain-stages.md) table) and unlocks the
   next layer. On a scope violation or a failing
   check, the task moves to `blocked` with a `blocked_reason` of
   `scope_violation` or `verification_failed`, and nothing downstream
   unlocks. Fix the work, then run `hedgehog retry <task-id>` to return
   the task to `planned`, claim it again by task id, and verify again —
   `hedgehog verify` only accepts a task you currently hold in
   `building`, so a blocked task has to go back through `retry` and
   `claim` first. Don't hand-commit around it.

   A `blocked` task anywhere in the graph makes `hedgehog claim --count
   <n>` refuse to hand out anything at all, with a non-zero exit naming
   the blocked task(s). Fix and `retry` it before claiming more. A
   **targeted** `hedgehog claim <task-id> --owner <owner>` is exempt —
   that's how the just-retried task gets reclaimed above. A lease the
   same `claim` call reaps for having just expired is exempt too: that
   call still claims whatever else is ready, and the reaped task lands in
   NEEDS ATTENTION for the next `claim` call to stop on.
5. **Repeat** — `hedgehog claim --owner <owner> --count <n>` again for
   the following layer.

Each `hedgehog verify` call commits exactly one compiled layer's
artifact; a wrong stage is fixed forward later via the Correction
Protocol.

## Friction log

Same mechanic as `hedgehog-loop`'s Friction log — log real friction (a
stage's instructions unclear, the traceability self-check redlining the
same underlying gap twice, a repeated user correction) via `hedgehog
friction add "<note>" [--task <task-id>]`, `tweaker` reads it at the
Stop Condition.

## Correction Protocol

Same core mechanic as `hedgehog-loop`'s Correction Protocol (stop, patch
the upstream step in place — for Stage 7's generated code, checking the
LSP tool's findReferences/incomingCalls against a symbol before patching
it — fast-forward every dependent step as its own commit, commit
messages as the explanation, resume the loop), triggered most often by
Stage 6's traceability self-check surfacing something that doesn't trace
back to the subject statement or matches a known AI-default cluster. Two
differences for this core:

- **Fast-forwarding ripples further.** A token system change (Stage 2)
  ripples through the signature element (same stage), the sequence
  (Stage 3), the headline (Stage 4, if the voice spec shifted, re-run by
  `landing-copywriter`) and the locked section copy (Stage 5, re-drafted
  by `landing-copywriter` for whichever sections the patch actually
  touches, still passing through the AI-tell self-check before it counts
  as locked again), and the build (Stage 7) — each its own small commit,
  in order.
- **Re-run Stage 6's traceability self-check against the patched chain
  before resuming** — an extra step this core adds, since traceability
  is what the whole chain rests on.

The orchestrating session runs this protocol and owns every commit in
it. `landing-builder` re-runs the affected stage when the patch is to a
stage it owns directly (1, 2, 3, 6, 7); `landing-copywriter` re-runs
Stage 4 or re-drafts the affected Stage 5 sections when the patch
touches those. Commits are always the session's act via `hedgehog
verify` — the same way they are for every other pass through The Loop.

Use `conventional-commits` when a correction touches several stages in
one working-tree pass and needs splitting back into per-stage commits.

### Post-build entry

Same shape as `hedgehog-loop`'s Post-build entry — no task to stop, no
loop to resume (return to `tweaker` instead), every touched task stays
`complete` and is fixed forward in new commits. This core routes here for
two distinct reasons: something structural is wrong rather than small
(the voice spec itself rather than one line of copy), or new scope is
genuinely additive but has nowhere else to go — a new section under a
brief that still holds, since this core has no module axis for
`planner`'s Re-entry pass to add an intent to. Either way, the protocol's
"patch" step reads as "add" in the additive case, and re-running Stage
6's traceability self-check against the patched chain still holds before
handing back, since traceability is what the whole core rests on.

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

Once `landing-builder` commits `feat(landing): build`, the compiled
graph is done, but the orchestrating session runs one more uncompiled
pass before offering the Stop Condition's handoff: a bounded loop
(`landing-executor` plus `landing-visual-reviewer` and
`landing-ux-reviewer`, up to 10 iterations) that polishes the rendered
page for visual and interaction quality independent of the chain's own
traceability concerns. This is not a compiled layer — no `hedgehog
claim` packet, no `hedgehog verify` gate. See
[the Polish Loop](references/polish-loop.md) for the full step sequence,
the decision rule for exiting or iterating, and why it's separate from
Stage 6. The loop's iteration count resets on every fresh invocation.

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
  sequence (this core's `workspace/core.yaml`), so `hedgehog claim
  --count N` always returns one task — there is no scheduler fan-out to
  reason about here, and this core's docs stay free of the
  conflict-predicate machinery that `full-stack-app` needs.
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

Offer the fresh-context handoff once the Polish Loop above has exited
(clean or capped) — not at the `artifact` task's completion directly, the
way `hedgehog-loop`'s Stop Condition works. The `artifact` task being
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
  open, say so explicitly in this handoff too, so the fresh `tweaker`
  session knows to treat those as its first tweak requests rather than
  assuming the page is fully clean.

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
