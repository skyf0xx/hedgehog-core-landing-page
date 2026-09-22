# The Chain Method stages

`hedgehog-landing-loop` is the operating loop for a bootstrapped
`landing-page` project — the Chain Method: a pipeline where every visual
choice traces back to a reason. No stage may introduce a choice that
doesn't originate in an earlier stage's output.

`landing-builder` runs Stages 1–3 and 6–7, and delegates Stages 4–5 to
`landing-copywriter` — every stage below runs in this exact order, in
one continuous session across the two agents, from the confirmed
subject statement through the built page. Every stage's input is the
prior stage's output; no stage works from anything but what was actually
produced before it. Two sub-steps inside Stage 2 (the dial table and the
voice spec) are the only parallel-input point in the chain, both reading
the same upstream artifact; everything else is strictly sequential.

This table maps `landing-builder`'s stages against the compiled build
graph's 5 layers (this core's `workspace/core.yaml`) — the coarser,
one-task-per-commit view. The two views are intentionally not the same
granularity: don't "fix" either one to match the other's — see
`hedgehog-landing-loop/SKILL.md`'s "The Loop" for how the stages inside
one compiled layer relate to that layer's single commit.

| Stage | Runs | Produces | Compiled layer | Commit |
|---|---|---|---|---|
| 1 | Subject/audience/job statement, adjective pairs, emotional sort, note timing | The emotional target spec, confirmed by the user | `feeling` | `feat(landing): strategy` |
| 2 | Dial table + voice spec, token system, signature element | The token system (`src/styles/global.css`) and signature element (`src/shapes/`) | `tokens` | `feat(landing): systems` |
| 3 | Per-section transition, weight, spacing, beat structure, archetype role | The pacing spec | `sequence` | `feat(landing): sequence` |
| 4 | Headline generation (via the `landing-copy` skill), run by `landing-copywriter` | The locked headline plus backups (`.hedgehog/chain/04-headline.md`) | `sequence` | bundled into `feat(landing): sequence` |
| 5 | Section copy, drafted in one pass by `landing-copywriter` via `landing-copy`, mapped onto Stage 3's section list, then an AI-tell self-check | Every section's locked body and CTA copy (`.hedgehog/chain/05-copy.md`) | `sequence` | bundled into `feat(landing): sequence` |
| 6 | Traceability, default-cluster, swap test, BMAD-fidelity, Chanel cut, Fitts's Law, affordance, gutter checks | Findings resolved against the chain, before building | `artifact` | bundled into `feat(landing): build` |
| 7 | The Astro/Tailwind/Motion implementation | The built page | `artifact` | `feat(landing): build` |

This strict, no-branching sequence is what `workspace/core.yaml` declares
as `pattern: layered` — no module axis, one dependent per layer, each
stage building only on what actually came before it.

`hedgehog-authored-loop`'s "Test depth follows verify radius" rule reads
cadence off `verify_radius`/`exclusive: true` — this core's chain
declares neither (`workspace/core.yaml`): every stage above already runs
its own self-test as a matter of course, and there is no module axis, so
nothing ever builds concurrently for the radius/exclusivity distinction
to protect against. The nearest thing this chain has to that rule's
integration point is `artifact` — the widest scope (`src/**`) and the
only layer whose verify (`pnpm build`) proves the whole page compiles,
not just one stage's own output.

Stages 1 and 2 are each one continuous judgment call — subject into
feeling into timing (Stage 1), then dial table into voice spec into
token system into signature element (Stage 2) — not separable steps
with different tool footprints, which is why each is one stage rather
than several. `landing-builder` runs both directly. The headline is its
own stage (4), one artifact, one review checkpoint, because it's the
single highest-leverage line on the page — every section beneath it
either delivers on its promise or doesn't, so it locks before any
section copy is drafted. Copy (Stage 5) is drafted for the whole page in
one pass, mapped onto Stage 3's locked section list, beats, and
archetype roles, then read once against the AI-tell self-check before
the user reviews and locks it — see `landing-copywriter`'s own file for
the writing standard and self-test; both Stages 4 and 5 run inside
`landing-copywriter`, not `landing-builder`, since they share a tool
footprint (pure prose, no code) distinct from the rest of the chain.

## Core Reference Points

The chain's judgment calls, across every stage, are grounded in these —
not restated per-stage since they're shared foundation, not one stage's
procedure:

- Donald Norman, *Emotional Design* — visceral / behavioral / reflective
  (Stage 1's emotional sort)
- Scott McCloud, *Understanding Comics* — panel transition taxonomy,
  closure (Stage 3's sequencing)
- Will Eisner, *Comics and Sequential Art* — page as one composition
  before it's a sequence (Stage 3's sequencing)
- Rudolf Arnheim, *Art and Visual Perception* — visual weight, tension,
  balance (Stage 2's dial reconciliation)
- Josef Albers, *Interaction of Color* — color as relational, not
  absolute (Stage 2's color dial)
- Dieter Rams / Massimo Vignelli — restraint as an emotional register
  (Stage 6's Chanel cut)
