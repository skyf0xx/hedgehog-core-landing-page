---
name: landing-copy
description: Writes landing page copy (headline, subhead, sections, CTAs) from source material — a confirmed brief, a README, repo, docs, or product description. Use for the Chain Method's headline and per-section copy stages, or any time landing page copy, hero sections, headlines, or CTAs are needed for a project. Do NOT summarize or lightly reformat the source doc — this skill enforces a decontamination step so the output is original persuasive copy, not source-with-headers.
---

# Landing Copy

Turns source material (a confirmed brief, README, repo docs, product notes, or past chat context) into landing page copy that reads like copy, not documentation. The core risk this skill guards against: defaulting to the source's own structure, section order, and phrasing because it's the path of least resistance. Every step below exists to break that reflex.

Before starting, confirm the source: what to read (a brief, repo URL, README path, or pasted text), the target audience, and, where the calling context has one, the voice register to write in.

## Step 1 — Extract, don't absorb

Pull raw facts from the source material into a flat **fact ledger**. Format matters here — use terse noun-phrase bullets, never full sentences lifted from source:

- Mechanism facts (what it actually does, technically)
- Problem it solves (what breaks/is painful without it)
- Differentiators vs. alternatives or the status quo
- Audience signals (who'd search for this, what they already know)
- Proof points (real numbers, stars, downloads, named users — concrete only, never invent any)
- Named features/commands worth surfacing

Do not carry over the source's headers, section order, examples, or sentence-level phrasing past this point. If you catch yourself about to write a sentence that's a close paraphrase of a source line, stop and rewrite from the fact ledger instead.

## Step 2 — Run the copywriting pipeline

Work through these roles in order. Each is a distinct pass, not a single blended draft — think of them as different people handing off a document.

1. **Diagnostician** — From the fact ledger, name the specific pain the audience feels today without this product. Write it as a felt problem, not a feature gap.
2. **Closer** — State the single core promise in one sentence. Not a feature list — the outcome. What does the visitor believe/get after using this that they didn't before.
3. **Engineer** — Build the page skeleton: hero (headline + subhead), problem section, mechanism section, differentiation section, proof section, CTA. Assign 1-2 fact-ledger items to each section — don't let sections balloon into feature dumps.
4. **Header Writer** — Write each section's visible header from the fact-ledger items assigned to it in the previous step, not from the body copy (headers are drafted before body prose exists) and never from the role label itself. Rules:
   - **State a claim, not a category.** "The Problem" → "Your agent forgot what it already built." The header does persuasive work, it doesn't organize content.
   - **Pull it from that section's own facts.** The sharpest single line the assigned fact-ledger items support, specific enough that it couldn't apply to any other product in the category.
   - **Vary construction across the page.** Don't let every header share one grammatical shape (all questions, all imperatives, all fragments). Five identical-pattern headers reads templated even with different words.
   - **Never let the scaffolding role leak through.** Role labels (problem/mechanism/differentiation/proof/CTA) are internal only, for mapping fact-ledger items to sections — they must not survive into the visible header verbatim or as a light rewording.
   - **Short beats clever.** 4-8 words, concrete and specific, over a pun or an abstraction.
   - **CTA headers name the action or the payoff**, never "Get Started."
6. **Verifier** — Check every claim in the draft, including section headers, against the fact ledger. Cut or flag anything not traceable to a fact. No invented metrics, no vague superlatives ("revolutionary," "seamless") unsupported by a concrete mechanism.
7. **Cross-Examiner** — Read as a skeptical member of the target audience would. Where would they say "sure, but"? Preempt the strongest objection directly in copy rather than ignoring it.
8. **CTA Writer** — Write 2-3 CTA variants tied to actual next steps (install, sign up, view repo/docs) — specific verbs, no generic "Get Started Now."
9. **Voice Editor** — Final pass for voice: conversational, direct, story/plain-talk register (Frank Kern-style — write like explaining it to a smart friend, not a press release) unless the calling context specifies a different register. Apply the paragraph shape and Writing standard below. Read the whole thing aloud in your head — if it sounds like it could've been copy-pasted from a docs site, rewrite the offending line. Re-check every header against the Header Writer rules once more here — voice edits to body copy sometimes leave a header's register mismatched.

### Paragraph shape

2–3 sentences per paragraph, shaped short → long → short by default. A third sentence earns its place only when the point needs a turn the first two can't carry. Two sentences each trying to do two jobs (joined by commas or "and") is the same overlength paragraph with fewer line breaks — split it instead of compressing it.

**Word-count cap, checked on every paragraph before finalizing.** A paragraph should never run past roughly 30 words. If a draft paragraph exceeds that, split it into two paragraphs at the natural break in the idea — don't compress it by cutting words, and don't let a long paragraph stand because the sentence count still looks right.

Reach for a bulleted list, numbered list, or a short bolded callout line only when the content is genuinely that shape (parallel items, a real sequence, one freestanding checkable stat) — never to pad a thin section or avoid writing the paragraph it needs.

**Comma-run check, mandatory before finalizing any paragraph.** Any single sentence that strings together 3+ comma-separated items — a sequence of steps, a set of parallel examples, a list of named things — is a list wearing prose. Pull it into a numbered list (if order matters) or a bulleted list (if it doesn't), never leave it flattened into one sentence. This applies even when the items are short and the sentence still reads grammatically; grammatical is not the bar, structural clarity is. Re-scan every paragraph against this specifically after drafting, since it's easy to write past in the moment.

### Writing standard

Every line ships or it doesn't — no draft tier.

- **Cut inflated words.** No "delve," "landscape," "robust," "comprehensive," "leverage," "seamless," "cutting-edge," "elevate," "unlock," "empower," "streamline," "game-changer," "harness," "revolutionize," "utilize," "foster," "facilitate," "pivotal," "nuanced," "multifaceted," "crucial," "garner," "vibrant," "tapestry," "testament," "interplay," "intricate," "showcase" (verb), "underscore," "navigate" (abstract), "myriad," "synergy," "paradigm shift." State the plain verb or noun.
- **No negation formulas.** Never "It's not X — it's Y." State the positive claim directly.
- **No hedge stacks.** Never pair "could potentially," "may eventually," "might ultimately" — pick one claim and state it.
- **No unnamed authority.** Never "studies show" or "experts agree" without naming the source. No source, no claim in that form.
- **No manufactured drama.** No "here's the interesting part," "the catch?", rhetorical-question openers. State the thing.
- **No stock closers.** No "the future looks bright," "only time will tell," modal-stacked predictions. End on the specific claim.
- **Vary sentence length on purpose.** Mix short (3–8 words) and long (20+) — uniform length reads as machine output.
- **No em dashes.** Reads as an AI tic. Use a comma, period, or parentheses, and rewrite the clause if the dash was load-bearing.
- **No comma/colon-chained clause stacking.** If a sentence needs more than one comma to connect independent ideas, it's two sentences wearing one.
- **No rule-of-three by default.** A three-part cascade ("time, money, trust") is a rhythm tool used sparingly, not a default shape. 2+ triplets on one page reads as a tic.
- **No adverb-as-hedge.** "Genuinely," "actually," "real" used to manufacture weight is a hedge stack in one word. If cutting the adverb leaves the sentence equally true, cut it.
- **No inline-header bullet dumps for persuasive copy.** 5+ bare noun phrases reads as generated. Where prose is called for, write prose.
- **No synonym cycling.** Name the subject the same way throughout — don't rotate "the app / the platform / the tool" to avoid repetition. Repetition of the clearest word is correct.
- **Concrete over abstract.** "Significant improvement" ships only with the number, name, or comparison that makes it checkable.
- **Every sentence earns its place.** Name each sentence's job (create tension, orient, explain, prove, illustrate, transition, resolve, prompt action). No clear job, cut it.
- **End paragraphs on movement, not restatement.** Close on an implication, reframe, transition, invitation, or the action itself — never by repeating the opening claim.

### AI-tell self-check (run once on the full draft before output)

Re-read cold, not trusting the draft because you just wrote it. Frequency, not presence, is the test — one hedge or one long sentence is normal prose, not a tell. Count instances before flagging; a clean draft passes without revision most of the time.

- **Banned vocabulary** — re-audit the Writing standard's list against the actual text.
- **Punctuation fingerprint** — em dashes that shipped anyway, semicolons outside a genuine list-with-internal-commas, curly quotes where straight ones are the project's convention.
- **Hedge and filler** — "it is important to note," "in many cases," "generally speaking," vague attribution without a named source, sycophantic openers, templated closers ("i hope this helps").
- **Connective tissue** — "moreover," "furthermore," "in conclusion" standing in for a direct logical connection or a plain paragraph break.
- **Rhetorical scaffolding** — mini-aphorism closers, thesis-first openers, parallel-subject mirrors ("What starts as X becomes Y" against "What begins as A turns into B"), anaphora, either/or binaries, tricolon beyond one-per-page, "turns out" reveal pivots.
- **Burstiness** — sentence-length variance. Flag a paragraph where every sentence clusters in the same 10–20 word band with no short (under 8) or long (20+) line breaking it.
- **Structural flattening** — re-run the comma-run check from the Paragraph shape section against every sentence in the final draft, not just while drafting: any sentence still stringing together 3+ comma-separated items is a list that should have become one.

## Step 3 — Decontamination check (before output)

Before presenting the draft, scan it against the original source one more time:

- Does any headline or subhead reuse a source heading almost verbatim? Rewrite it.
- Does the section order mirror the source's table of contents? If so, deliberately reorder around the Engineer's skeleton (problem → mechanism → proof → CTA), not the source's structure.
- Any sentence that's a light rewording of a source sentence rather than a fresh formulation? Rewrite from the fact ledger, not the sentence.

## Output format

Markdown, ready to drop into the landing page draft. Every section header below is a Header Writer output (a claim, per the rules in Step 2.4) standing in for the generic role name — never ship "The Problem," "How It Works," or "Proof" verbatim, those are the roles being illustrated here, not the headers to write:

```
# [Headline]
### [Subheadline]

## [Problem-role header: a claim naming the felt pain]
[...]

## [Mechanism-role header: a claim naming how it works]
[...]

## [Differentiation-role header: a claim naming why this over the alternative]
[...]

## [Proof-role header: a claim naming the concrete evidence]
[...]

## [CTA-role header: names the action or payoff, never "Get Started"]
[2-3 CTA variants]
```

If the calling context has a specific landing page stack/section structure (e.g. the Chain Method's Stage 3 section list and beat structure), map the copy onto it section-by-section rather than emitting the generic template above — copy content and section structure are separate concerns, but the final output should fit the structure it's landing in. The Header Writer's claim-style header is still required in that case: where the calling context's own format reserves a line for a visible subhead (e.g. a `###` line inside a section block), put the claim there rather than leaving the section identified only by its internal role label.
