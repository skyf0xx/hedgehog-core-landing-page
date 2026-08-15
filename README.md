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
