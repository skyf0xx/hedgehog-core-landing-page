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

- **`hedgehog-landing-loop`** — the operating loop for this core, start
  to finish: planning intake, the Chain Method's stage-by-stage build
  through `landing-builder` and `landing-copywriter`, the Correction
  Protocol, and the Polish Loop. Invoke it at the start of any build
  session and for "what's next"; it owns which agent runs which stage
  and in what order.
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

`planner` runs planning intake and hands off to `bootstrap`, which lands
the workspace. `landing-builder` and `landing-copywriter` then run the
Chain Method's seven stages between them, and the Polish Loop
(`landing-executor`, `landing-visual-reviewer`, `landing-ux-reviewer`)
runs after the build lands. See `hedgehog-landing-loop` for exactly
which agent owns which stage, the stage-to-compiled-layer mapping, and
the Polish Loop's own sequencing — that skill is the source, not
restated here.

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
```

### Core rule

**One page, one job.** The subject statement names it; every downstream
choice traces back to that sentence or gets cut — the discipline
`hedgehog-landing-loop`'s Rules section enforces stage by stage.
