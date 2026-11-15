---
name: hedgehog-bootstrap-landing-page-core
description: Use once, at the start of a new Hedgehog project on the landing-page core, to land the pre-verified Astro + Tailwind v4 workspace and verify it's green. Runs as the only move of the `bootstrap` agent on this core — there are no add-on steps, unlike full-stack-app. Invoked automatically by `planner` after Confirm & Lock.
---

# Hedgehog Bootstrap — landing-page Core

Lands the whole of a `landing-page` project's workspace — there's no
add-on layer to run after it, unlike `full-stack-app`'s
`hedgehog-bootstrap` — by copying a pre-built, pre-verified workspace
(this package's `workspace/`) rather than generating it live: Astro
workspace, Tailwind v4 CSS-first token-layer
config, the library set this core is built on (Motion, Lenis, SplitType,
ogl, Lucide).
This piece is deterministic — the same commands produce the same output
on every project — so the output is committed once, upstream, and copied
here instead of re-derived by an agent on every run.

This skill has no per-project decisions to make: no add-ons, no
dependency beyond confirming its own commit hasn't already landed,
nothing to ask. Landing-page's core is identical on every project
running it.

## What lands

Everything under this package's `workspace/`, copied to the repo root:

- Root: `astro.config.mjs`, `package.json` (with the `dev` script —
  `astro dev` — and every library in the stack pinned), `tsconfig.json`,
  `eslint.config.mjs`, `.prettierrc.js`, `.gitignore`, `pnpm-lock.yaml`.
- `src/pages/index.astro` — a minimal placeholder page (proves the build
  pipeline works end to end), replaced by `landing-builder`'s own output
  at the build phase.
- `src/styles/global.css` — the Tailwind v4 CSS-first import and the
  `@theme` token block: no component classes, no plugin beyond the base.
  Ships with placeholder tokens (a neutral starting palette, a system
  type stack, a 1.25-ratio `--text-*` scale, a 4px spacing unit) that
  `landing-builder` overwrites entirely at its systems stage — including
  swapping the system type stack for real `@fontsource-variable` faces.
  This block existing and being wired into the build is what core
  guarantees, not any specific token values.
- `src/sections/`, `src/shapes/`, `src/assets/` — empty, with a
  `.gitkeep`; real content starts at the systems and build phases.

`node_modules` is not part of the copy — `pnpm install` regenerates it
from the committed `pnpm-lock.yaml`.

## Steps

### 1. Confirm this hasn't already run

Check for a prior `feat(landing): workspace` commit
(`git log --grep="^feat(landing): workspace"`). It means core already
landed — stop, don't re-copy. `astro.config.mjs` at the repo root without
that commit means the files are on disk but not yet installed, verified,
and committed: continue at step 3. If something about the landed core seems
wrong, that's a Correction Protocol case (`hedgehog-landing-loop`), not a
re-copy: patch the specific file at its source.

### 2. Land this package's `workspace/`

`hedgehog init --landing-page` and `hedgehog core install landing-page`
both land this package's `workspace/` at the repo root (including
`core.yaml`) and fill this core's section into root `CLAUDE.md`. `planner`
runs `hedgehog core install landing-page` before planning intake, so by
this step the files are normally on disk: check for `astro.config.mjs`. If
it is missing, run `hedgehog core install landing-page` now. By the end of
this step every file listed in "What lands" above is on disk.

### 3. Install

```bash
pnpm install
```

Resolves against the committed `pnpm-lock.yaml` — this should be fast
and produce no lockfile changes. A lockfile diff here means the shipped
`pnpm-lock.yaml` doesn't match `package.json` — that's a packaging bug in
this package's `workspace/`, not something to patch locally (see **If
verification fails**, below).

### 4. Verify

```bash
pnpm astro check
pnpm build
```

Both must be clean: no type errors from the first command, a successful
build with no warnings from the second. This is the live check that
proves core isn't correct by trusting the copy, but by actually running
the same gate every phase in this core's loop runs.

### 5. Commit

```
feat(landing): workspace
```

One commit for all of core, landed as a verified copy. That commit
existing is the record that core landed — `bootstrap` checks for it via
the commit log, not a checklist line.

## If verification fails

A clean copy of `workspace/` that fails `astro check`
or `pnpm build`, or needs a lockfile change, means the shipped template
itself is broken — not a per-project problem to hand-patch around. Stop
and report exactly what failed. The fix is a new package version of this
core's `workspace/`; never patch a consuming project's copy to route
around a broken template and call core done.

## Constraints

- Run once per project, as the `bootstrap` agent's only move on this
  core — never invoked on its own by a user.
- No add-on awareness, because this core has no add-ons. If a future
  landing-page variation genuinely needs one (a CMS integration, a form
  backend), that's a new core decision for `planner`'s Phase 0, not an
  add-on bolted onto this one.
- Don't hand-edit any file this step lands to work around a verification
  failure; see **If verification fails**.
- Don't write any Chain Method phase content (adjectives, tokens,
  signature element, sequence, or the built page) — that's
  `landing-builder`'s work, after this Bootstrap box is checked.
