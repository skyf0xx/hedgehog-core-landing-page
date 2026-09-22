# Polish Loop

Once `landing-builder` commits `feat(landing): build`, the compiled
graph is done — `hedgehog status` shows every task `complete` — but the
orchestrating session runs one more uncompiled pass before offering the
Stop Condition's handoff (`hedgehog-landing-loop/SKILL.md`): a bounded
loop that polishes the rendered page for visual and interaction quality
independent of the chain's own traceability concerns. This is not a
compiled layer (no `hedgehog claim` packet, no `hedgehog verify` gate) —
it runs the same way the Correction Protocol's post-build entry does,
driven directly by the orchestrating session, because it operates on the
built page after the graph's own Stop Condition has already been
reached.

Before the Polish Loop starts, confirm `hedgehog status` shows the
`artifact` task `complete` — `landing-builder`'s initial build has
landed. The Polish Loop never opens against an unbuilt or partially
built page.

**Why this is separate from `landing-builder`'s Stage 6.** Stage 6 gates
whether the page traces back to the subject statement and clears the
usability formulas, before a single line of Astro exists. The Polish
Loop runs after the page is actually rendered and interactive, catching
what only shows up once it's real: AI-tell visual patterns, dead or
uneven gaps, scan-pattern and interaction friction, and a general taste
pass — none of which Stage 6 checks and none of which require re-opening
the chain's own artifacts.

All three Polish Loop agents work on their own editorial judgment, not a
fixed checklist derived from the chain's generation-time rules — a
finished page invites critique-and-improve the way a human editor or
designer gives it, which is a different, often sharper instinct than the
constrained judgment calls Stages 1–6 make while generating the first
draft from nothing. `landing-executor` in particular has full license
over the rendered page's markup, styling, and copy substance — it can
rewrite a sentence, cut a paragraph, or restructure a section, not just
swap a word — bounded only by the locked stack/token system and by never
touching `.hedgehog/chain/*.md` itself (see that agent's own file for
why: those are the historical record of the first draft's reasoning, not
something a later pass edits to match a rewrite).

1. **`landing-executor`** applies the current iteration's redlines (none,
   on the first pass — the first pass reviews `landing-builder`'s output
   as-is) directly to the built page.
2. **Build and screenshot** — `landing-visual-reviewer` and
   `landing-ux-reviewer` each build and serve the page fresh; don't
   review against a stale render.
3. **Both reviewers run in parallel**, independent of each other:
   `landing-visual-reviewer` for AI-tell patterns, gap/rhythm, and visual
   taste; `landing-ux-reviewer` for scan-pattern, flow/friction, and
   interaction taste. Each returns redlines or clean.
4. **Decide:**
   - Both clean → exit the loop, proceed to the Stop Condition.
   - Either has redlines, and the iteration count is below 10 → commit
     nothing yet, return to step 1 with the combined redlines for
     `landing-executor` to apply as the next iteration.
   - Either has redlines, and 10 iterations have already run → exit the
     loop anyway (the cap is a backstop against unproductive churn, not
     a quality gate) and note in the handoff to `tweaker` that the loop
     hit its cap with redlines still open.
5. **Commit each iteration separately** as `feat(landing): polish
   iteration <n>` (`landing-executor`'s own act — it carries `Bash`
   unlike most agents in this loop) — one commit per pass through steps
   1–3, not one squashed commit at the end.

The loop's iteration count resets per Polish Loop run — a later
`tweaker` session or Correction Protocol post-build entry that touches
the built page again starts a fresh count if it re-invokes this loop,
rather than inheriting a prior run's count.
