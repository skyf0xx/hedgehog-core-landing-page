# @skyf0xx/hedgehog-core-landing-page

Hedgehog's landing-page core: a pre-built, pre-verified Astro +
Tailwind v4 workspace plus the Chain Method's agent pipeline — brief,
feeling, tokens, sequence, artifact — and the skills that drive a
Hedgehog project built on it.

## Contents

- `workspace/` — the workspace a Hedgehog install copies to a
  project's repo root: Astro config, the Tailwind v4 CSS-first token
  layer, the animation/icon library set (Motion, Lenis, SplitType, ogl,
  Lucide), and every enforcement file.
- `agents/` — the Chain Method's chain agents (`landing-strategist`,
  `landing-systems`, `landing-sequencer`, `landing-headline-writer`,
  `landing-copywriter`, `landing-critic`, `landing-builder`) and its
  Polish Loop agents (`landing-executor`, `landing-visual-reviewer`,
  `landing-ux-reviewer`).
- `skills/` — `hedgehog-landing-loop`,
  `hedgehog-bootstrap-landing-page-core`, `landing-shapes`, and the
  per-section copy archetype skills (`landing-copy-hero`,
  `landing-copy-problem`, `landing-copy-mechanism`, `landing-copy-proof`,
  `landing-copy-objection`, `landing-copy-headline`, `landing-copy-cta`).
- `CLAUDE.core.md` — fills a Hedgehog project's root `CLAUDE.md`
  `{{CORE_SECTION}}` placeholder for this core.
- `hedgehog-core.yaml` — this package's manifest: name, flag, the
  selection prose the Hedgehog planner matches a project description
  against, and which agents/skills it carries.
- `scripts/regenerate-landing-page-core.sh` — the deterministic
  generator that regenerates `workspace/` from scratch. Run by hand
  when a workspace dependency needs bumping; not part of any install
  path.

## Using this package

A Hedgehog installation depends on this package for the `landing-page`
core rather than carrying its content directly. See the Hedgehog engine
(`@skyf0xx/hedgehog`) for the installer and build-graph tooling that
consumes it.

## Working on this core

This is a versioned npm package that the Hedgehog engine's `init` fetches
by name, carrying `landing-page`'s own agents, skills, a pre-built
workspace, and the `hedgehog-core.yaml` manifest that names all three to
the engine. See the engine repo
([`skyf0xx/hedgehog`](https://github.com/skyf0xx/hedgehog)) and its
[`ARCHITECTURE.md`](https://github.com/skyf0xx/hedgehog/blob/master/ARCHITECTURE.md)
for how `init` resolves and fetches a core package — that mechanism lives
there, not here.

No root `CLAUDE.md` lives in this repo. `CLAUDE.core.md` is a payload
file: its content is installed into a *consuming project's* generated
`CLAUDE.md`, filling that project's `{{CORE_SECTION}}` placeholder. A
plain root `CLAUDE.md` here would auto-load into any coding agent working
on this package itself, bleeding project-build context into a repo where
no Hedgehog build ever runs — build guidance for a project using this
core lives in that project's own generated `CLAUDE.md`, never here.

Changing this core means editing one of: the `workspace/` template (the
scaffold a Hedgehog install copies into a project's repo root), a Chain
Method or Polish Loop agent under `agents/`, or a skill under `skills/`
(the loop, bootstrap, `landing-shapes`, or one of the per-section copy
archetype skills). `scripts/regenerate-landing-page-core.sh` is the
deterministic generator that rebuilds `workspace/` from scratch — run it
by hand after bumping a workspace dependency, then diff the result before
committing. A change here is a release of this package, not of the
engine: bump `package.json`'s version, commit, and merge to `main` — this
repo's own `publish.yml` tags and publishes from there.

This core has no generator tooling of its own — no `tools/`,
`generators/`, or equivalent directory, unlike `full-stack-app`'s Nx
generators (`workspace/tools/generators/`). When `workspace/`'s template
needs a new piece of repeatable boilerplate, prefer building or
extending a generator over hand-authoring the output once; if this core
grows one, model it against `full-stack-app`'s, the concrete working
example.
