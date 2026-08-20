## This project's core: landing-page

The Chain Method: brief → feeling → tokens/element → sequence →
artifact, where every visual choice traces back to a sentence that
caused it. No domain data, no backend — a single (or few-page) marketing
site, built once through a fixed pipeline rather than iterated on
freely. See `.hedgehog/BMAD/` for the vendored BMAD-METHOD shelf's raw
output and `.hedgehog/chain/` for this core's own archival planning
intake output — the subject statement, the adjective/note tables, and
the token system, written once by `planner` and `landing-builder`,
never edited after a phase closes.

The Chain Method decides *what* the signature element is and *why* it's
there — sourced from the subject statement, audited for traceability.
`landing-shapes` decides *how* to build it and every other section
shape, divider, or icon — the concrete CSS/canvas techniques and the
pinned icon source. Neither restates the other's decision.

### The skills — invoke these, don't improvise

- **`hedgehog-landing-loop`** — every unit of work once bootstrapped:
  `hedgehog next` emits the packet for one ready compiled layer, run the
  fine-grained Chain Method phases it bundles through their owning
  agents, gate the layer via `hedgehog verify`, which commits it on a
  pass. Also holds the Correction Protocol for fixing a wrong upstream
  phase (e.g. a signature element that doesn't trace back to the subject
  statement). Invoke it at the start of any build session and for
  "what's next".
- **`hedgehog-bootstrap-landing-page-core`** — run **once**, at project
  start, to land the pre-verified Astro + Tailwind workspace. Skip if
  `astro.config.mjs` already exists.
- **`landing-shapes`** — the shape/divider/icon construction library:
  geometry personality, curve and angular CSS/canvas techniques, and
  Lucide as the pinned icon source. `landing-builder` points into it
  when naming the signature element's family at its systems stage, and
  invokes it for the concrete recipe at its sequencing and build stages.
- **`landing-copy`** — the copywriting pipeline: a fact ledger pulled from
  source material, a role-by-role drafting pass (problem, mechanism,
  proof, objection, CTA), the Writing standard, and an AI-tell
  self-check. `landing-copywriter` invokes it once for the headline (its
  Stage 4) and once for the full page's section copy (Stage 5), mapped
  onto the section list and archetype roles `landing-builder` assigned at
  its sequencing stage.
- **`conventional-commits`** — when a change spans several phases in one
  working-tree pass and needs splitting back into per-phase commits
  (mainly Correction Protocol cleanups).

### The agents — delegate the judgment calls

- **`planner`** — planning intake (which core applies, then this core's
  own brief intake: the vendored BMAD-METHOD shelf, run in full and
  mined into subject, audience, single page job) at project start. Writes
  the `landing` intent (`hedgehog intent add`, one call — this core has
  no module axis), `.hedgehog/BMAD/`, and `.hedgehog/chain/00-brief.md`.
  On first run, hands off to the `bootstrap` agent once Confirm & Lock
  holds. This core has no module axis for a later `planner` run to add an
  intent to, so new scope after the build is complete doesn't return to
  `planner` at all: a new section on a page whose subject, audience, and
  job are unchanged (`.hedgehog/chain/00-brief.md` still holds) is
  additive work inside the existing chain, routed to
  `hedgehog-landing-loop`'s Correction Protocol post-build entry instead.
  A different subject, audience, or job is a different page and belongs
  in its own landing-page project; `00-brief.md` is never rewritten to
  fit new scope, since it's the root every phase's traceability audit
  walks back to.
- **`bootstrap`** — runs `hedgehog-bootstrap-landing-page-core`'s steps.
  Triggered automatically by `planner` after its first run; skip if
  `astro.config.mjs` already exists.
- **`landing-builder`** — runs the Chain Method's structural spine as
  one continuous session, in five stages, delegating the other two to
  `landing-copywriter`: the subject/audience/job statement → adjective
  pairs → visceral/behavioral/reflective sort → top/heart/base note
  timing and the page's single peak moment (Stage 1, the emotional
  target spec, confirmed by the user); the ingredient dial table, the
  copy voice spec, the token system that reconciles them, and the
  signature element (Stage 2, everything that becomes a Tailwind token
  or a copy rule); per-section transition type, weight, spacing, beat
  structure, and copy archetype role — Hero/Problem/Mechanism/Proof/
  Objection/CTA — the Motion/Lenis pacing spec (Stage 3); a
  traceability, default-cluster, swap test, BMAD-fidelity, Chanel cut,
  Fitts's Law, affordance, and gutter self-check against the whole
  chain before building (Stage 6); and the Astro/Tailwind/Motion
  implementation itself, placing the locked headline and every
  section's copy verbatim and mapping each section's markdown structure
  to the matching markup (Stage 7). Anything that can't be built as
  specified, or a stage's output that seems wrong once a later stage
  depends on it, is flagged and resolved at its source stage, never
  silently improvised around downstream.
- **`landing-copywriter`** — runs the Chain Method's two copy stages,
  handed off from `landing-builder` after Stage 3 locks and handed back
  once the headline and section copy are locked: the headline plus
  backups from distinct rhetorical patterns via the `landing-copy`
  skill, locked by the user before section copy is drafted (Stage 4);
  and the full page's section body and CTA text, drafted in one pass via
  `landing-copy` against the voice spec and Stage 3's section list, beat
  structure, and archetype roles, with an AI-tell self-check run against
  the full draft before it's presented for lock (Stage 5).
- **Polish Loop** (`landing-executor`, `landing-visual-reviewer`,
  `landing-ux-reviewer`) — runs after `landing-builder`, uncompiled (no
  graph task, no `hedgehog verify` gate). All three work on their own
  editorial judgment, not the chain's generation-time constraints —
  critiquing a finished page is a different instinct than building one
  from a brief. `landing-visual-reviewer` and `landing-ux-reviewer`
  build, screenshot, and interact with the rendered page, redlining
  AI-tell patterns, dead/uneven gaps, scan-pattern and interaction
  friction, and taste, on their own judgment rather than a fixed
  checklist — independent of `landing-builder`'s traceability/usability
  self-check, which already ran before the page existed. `landing-executor`
  has full license over the rendered page's markup, styling, and copy
  substance to fix each redline (a rewritten sentence or cut paragraph,
  not just a word swap), bounded only by the locked stack/token system
  and by never touching `.hedgehog/chain/*.md`. Loops until both reviewers return
  clean or 10 iterations pass, one commit per iteration
  (`feat(landing): polish iteration <n>`), then hands off to `tweaker`.

## The constants (do not deviate)

### Stack (locked, every project — no add-ons on this core)

**Astro** (zero-JS-by-default shell, islands only where interaction is
genuinely needed) · **Tailwind v4, CSS-first** (config as token layer
only — no component library on top) · **Motion**, scoped to
CSS/transform targets only, no plugins (primary animation engine; owns
the sequencing pacing and top/heart/base fade timing) · **Lenis**
(smooth-scroll feel, the "weight and suspension" dial) · **SplitType**
(line/word/char copy-reveal splitting) · **Signature element & shape
construction** — the `landing-shapes` skill: geometry personality, the
curve/angular CSS and Canvas 2D technique library, Lucide as the pinned
icon source · **`@fontsource-variable/*`** (self-hosted variable
typefaces, picked per brief at step 5 — never `system-ui`, never an
external font request) · **`astro:assets`** (`<Image />`/`<Picture />`
for every raster image — format conversion, `srcset`, and reserved
space; a bare `<img>` is a defect) · **`ogl`** (lightweight WebGL) or a raw shader (a
continuous background field spanning the full page height, so sections
read as windows onto one surface) · **CSS `clip-path` irregular edges +
`mix-blend-mode` overlap + negative-margin overlap** (section boundary
treatment — breaks the hard horizontal seam between sections without a
new dependency) · **CSS `mask-image` + noise pattern** (texture/grain
layer) · **React Three Fiber** (rare — only when the subject is
genuinely spatial; default is to skip it).

This core has no design-handoff tool. All visual decisions are derived
directly through `landing-builder`'s token system (its systems stage)
and the `landing-shapes` techniques — never imported from an external
design file.

Don't substitute libraries. If a package name changed upstream, verify
against current docs before running — don't swap in a different one, and
don't reach for a component library or a second icon set to fill a gap
one of the above doesn't cover; that gap is a signal to go back to the
Ingredient Vocabulary and derive the right choice, not to default to
something off-the-shelf.

The signature element and every other section shape is always
constructed from a generator, a formula, a measurement, or a sourced
Lucide icon — never hand-typed coordinates. See the `landing-shapes`
skill for the technique.

### Layout

```text
astro.config.mjs     Astro workspace root
src/
  pages/              one file per page (usually just index.astro)
  sections/           one component per page section, in sequencing order
  shapes/             the signature element + any other section shapes/dividers, built via landing-shapes
  assets/             raster images, imported as modules and rendered through astro:assets `<Image />`
  styles/             global.css — @fontsource-variable imports + Tailwind v4 CSS-first import + the `@theme` token layer (hex values, font families, `--text-*` scale, spacing unit, easing family from the systems stage)
.hedgehog/
  hedgehog.db         the build graph — the landing intent, its five compiled tasks, verifications, committed to git
  BMAD/               vendored BMAD-METHOD shelf's raw output (brief, PR-FAQ, PRD, UX spec, research) —
                       write-once, from planner
  chain/              this core's own archival planning intake output — subject statement, adjective tables,
                       token system, signature element spec, sequence spec — write-once, from planner and landing-builder
docs/
  design/              the reconciled traceability and usability self-check landing-builder builds from
```

### Core rules

- **One page, one job.** The subject statement names it; every
  downstream choice traces back to that sentence or gets cut.
- **No stage introduces a choice that doesn't originate in an earlier
  stage's output.** A signature element the systems stage didn't source
  from the subject, a color the dial table didn't derive from an
  adjective — both get flagged by the traceability self-check, not
  waved through.
- **Ingredients move in agreement.** Color, type, space, motion, copy
  rhythm, and pacing are one system reconciled at the systems stage — a
  page warm in color but cold in type is a defect, not a style choice.
- **Sequential through the pipeline.** A stage starts only once the
  stage before it is checkpointed and committed — the systems stage's
  dial table and voice spec run in parallel (same input), everything
  else is strictly sequential.
- **One phase = one commit**, in the exact Conventional Commit format
  from `hedgehog-landing-loop`.
- **Fix wrong phases at the source** via the Correction Protocol — never
  a downstream workaround (e.g. don't patch the build stage's output to
  fix a token that's wrong at the systems stage).
- **The traceability self-check is real.** A traceability or
  default-cluster failure blocks the build stage from starting, the same
  way a failing gate blocks a commit elsewhere in Hedgehog.
