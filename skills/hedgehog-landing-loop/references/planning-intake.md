# Planning intake (Phase 0, before any build phase)

Run once, before `bootstrap` scaffolds the workspace, on the
`landing-page` core (the Chain Method: brief → feeling → tokens/element
→ sequence → artifact). `planner` owns this section; see that agent for
when it runs.

Opens with `hedgehog-planning-intake`'s Phase 0 — the same vendored
BMAD-METHOD shelf `full-stack-app` runs, in the same full sequence,
archived to the same `.hedgehog/BMAD/` layout. After that Phase 0
completes, this section does its own mining — a one-paragraph subject
statement, the landing-page counterpart to `hedgehog-planning-intake`'s
own Phase 1 (domain modules and an Add-ons decision on full-stack-app).
That mined draft becomes the first draft of `.hedgehog/chain/00-brief.md`,
shown back at Confirm & Lock for the user to accept or correct.

1. **Run `hedgehog-planning-intake`'s Phase 0 in full**: state the BMAD
   attribution it states, then run `bmad-forge-idea`, `bmad-brainstorming`,
   `bmad-product-brief`, `bmad-prfaq`, `bmad-prd`, `bmad-ux`,
   `bmad-deep-recon`, archived to `.hedgehog/BMAD/` with the fixed layout
   and `00-manifest.md` attribution header that skill's Phase 0 defines.
   `.hedgehog/BMAD/` is archival and immutable once written, same as
   `full-stack-app` — nothing in this core's day-to-day loop reads it
   live after this step mines it once. **Before `bmad-ux` runs**, write
   this core's `bmad-ux.toml` (see `references/bmad-ux-customize.toml` in
   this package) to `{project-root}/_bmad/custom/bmad-ux.toml`, unless a
   project-specific override already exists there — this is a
   `bmad-ux`-native override file (`customize.toml`'s own documented
   mechanism, not an edit to the vendored skill), and it points `bmad-ux`'s
   Design handoff working mode at Google Stitch with a landing-page-shaped
   directive. `bmad-ux` itself decides whether Discovery runs fast-path,
   coaching-path, or Design handoff — offered, not forced — so this step
   only makes the option well-formed when the user picks it, never removes
   the other two paths.
2. **Mine a draft subject statement** from `.hedgehog/BMAD/`: the
   concrete subject (what is this actually selling/announcing/showing),
   the audience, and the page's single job, sourced from the brief and
   PR-FAQ (a landing page's brief and PR-FAQ are the closest BMAD
   artifacts to a subject statement — the PRD's Glossary and deep-recon
   output are read for supporting color, not required to resolve a
   one-page subject/audience/job). `00-brief.md` itself stays this thin
   by design — it's the root traceability walks back to, not a copy of
   BMAD's full archive. The PRD's Features/FRs and the UX spec
   (`05-ux-spec/DESIGN.md`/`EXPERIENCE.md`), where BMAD produced them, are
   read directly by `landing-builder`, at the corresponding stage of its
   run (see that agent's own file for which stage reads which file),
   rather than mined into the brief here — a locked color, typeface,
   mascot requirement, or section list is BMAD's own committed material,
   not something this mining step compresses into one paragraph and the
   rest of the chain then works without. Where BMAD's material leaves any
   of the subject/audience/job three genuinely unresolved, ask directly —
   don't proceed on vagueness, and don't invent an audience or job that
   wasn't stated, mined, or confirmed.
3. **Write `.hedgehog/chain/00-brief.md`** — the mined subject statement,
   one paragraph, plus the audience and single job named explicitly.
   This is the root every downstream phase's traceability audit walks
   back to; it draws from BMAD's archive but is its own file, in this
   core's own `.hedgehog/chain/` layout, not a pointer into
   `.hedgehog/BMAD/`.
4. **Confirm & Lock** — show the mined subject statement, audience, and
   job back in plain terms, alongside which BMAD skills ran and where
   their output lives (`.hedgehog/BMAD/`), before writing anything to the
   build graph. State plainly what happens on confirmation: *"This locks
   in the brief, adds the `landing` intent to the build graph
   (`hedgehog intent add`), compiles it into the five-phase chain
   (`hedgehog plan`), commits (`chore(planning): intake`), and hands off
   to `bootstrap` to scaffold the Astro workspace. `landing-builder`'s
   Stage 1 starts once that closes. Anything wrong or missing — say so
   now."* Wait for explicit go-ahead — a revision here is just another
   mining pass against the same BMAD archive, not a Correction Protocol
   entry, since nothing downstream exists yet.
5. **Add the intent and compile the graph**: `hedgehog intent add --id
   landing --goal "<subject statement>" --outcome "<audience + single
   job>"` — one call, no `--rule`/`--depends-on` needed; landing-page has
   no module axis, so this single intent is what `hedgehog plan` compiles
   against this core's `workspace/core.yaml` into the five phase
   tasks. Run `hedgehog plan` next, then `hedgehog status` to show the
   compiled chain.
6. **Commit planning intake's output as one commit**,
   `chore(planning): intake` — the committed intent
   (`.hedgehog/intents/landing.json`), `.hedgehog/BMAD/`,
   `.hedgehog/chain/00-brief.md`, and root `CLAUDE.md`'s filled
   placeholders. `.hedgehog/hedgehog.db` is gitignored and derived —
   `hedgehog plan` compiles it from the committed intent, and `hedgehog db
   rebuild` re-derives it from that same intent plus git history.
7. **Hand off to `bootstrap`** once the commit lands.
