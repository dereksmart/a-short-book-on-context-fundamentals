# CLAUDE.md — Context Fundamentals (the Book)

Companion ebook to the AI Enablement workshop talk of the same name. Markdown source, destined for epub via bookbind.

## Objectives

1. A read-for-pleasure companion to the talk — deeper than slides allow, accessible to any role (designer, PM, engineer, writer, ops).
2. **Model-agnostic throughout.** Every major LLM tool gets fair treatment; no single vendor is the frame.
3. A reference people return to — each chapter self-contained, cited where it matters.

Target reading time: **1–2 hours** (~15–30K words), currently leaning toward the 2-hour end. 25 chapters (24 content + coda) across 7 Parts plus preface and back matter.

## Canonical docs

- **[outline.md](outline.md)** — chapter-by-chapter plan, status, guiding principles. Update when chapters ship or the plan changes.
- **[style-guide.md](style-guide.md)** — voice (Bill Bryson), sentence craft, per-chapter structure. Read before drafting.
- **[references/context-fundamentals-research.md](references/context-fundamentals-research.md)** — source of truth for claims and citations. Fact-checked Apr 23, 2026; Part 6 is the cross-LLM landscape. Write chapters *from here*. If a claim isn't supported there, add it with citation or don't include it.
- **[references/speaking-script.md](references/speaking-script.md)** — the talk itself. Useful for voice callbacks and the back-matter script.

## The throughline

Four threads run through every chapter:

1. **Thesis** — *Drift is a context problem, not a model problem.* Stated in Ch. 1, returned to at major pivots, restated at the close.
2. **Two sibling metaphors** — the **brilliant new hire** (carries rules/command/knowledge) and the **window-as-room, eventually as library** (carries the mechanics).
3. **Recurring characters** — researchers as people. Liu et al., Hsieh's NVIDIA RULER team, the Adobe NoLiMa crew, Anthropic/Google/OpenAI engineers. A small cast, named with affiliations.
4. **The reader's desk** — most chapters end with something small they could change Monday morning. Habits accumulate into a practice.

## Rules for drafting

- **Voice**: Bryson of *A Short History of Nearly Everything*. Curious, warm, dry, understated. See style-guide.md.
- **Rotate tools.** If the central example in one chapter is Claude, the next should reach for ChatGPT, Gemini, Cursor, or Copilot. No Claude-as-default.
- **Cite bold claims inline** as markdown links. If the number is specific, the URL is mandatory. If a claim can't be traced to a primary source: soften or remove.
- **One thesis per chapter.** Two ideas means two chapters.
- **No marketing voice.** No *game-changing, unlock, revolutionary, supercharge, next-generation.*
- **Name researchers.** "A team at NVIDIA led by Cheng-Ping Hsieh" > "(Hsieh et al., 2024)."
- **End chapters with an invitation, not a recap.**
- **Target ~1,000–1,500 words per chapter typical; up to ~2,000 for heavier chapters.** Tightening discipline: a clear 1,200-word chapter beats a wandering 2,500-word one.
- **Never quote a context-window number without its benchmark-effective number** when one exists (see research Part 6).

## What not to do

- Don't default to Claude examples.
- Don't pad word counts to hit a target. A tight 1,400-word chapter beats a flabby 2,800-word one.
- Don't add features, sections, or framings beyond what the outline calls for. If the outline needs to change, update it first.
- Don't create planning or scratch docs in this directory. Drafts live in chapter files; decisions live in outline and style-guide.

## File layout

```
book/
├── README.md          (build command and repo layout)
├── CLAUDE.md          (imports AGENTS.md)
├── AGENTS.md          (this file — orientation)
├── outline.md         (the plan + chapter status)
├── style-guide.md     (voice)
├── asset-notes.md     (image inventory and usage notes)
├── references/        (research and source workshop script)
├── src/               (publication inputs only)
│   ├── ch00-*.md      (preface)
│   ├── ch00a-part-*.md, ch05a-part-*.md, ... (Part openers)
│   ├── ch01-*.md      (chapters, numbered + slugged)
│   ├── ...
│   ├── keyboard-reference.md
│   ├── sources.md
│   └── assets/
└── dist/              (generated output; ignored)
```

Chapter filenames live under `src/`: `ch<NN>-<slug>.md`, where `NN` is the final number from outline.md.

## Chapter status

Keep current. When a chapter ships, update this and outline.md's status section together.

**Tightening pass complete.** Final book: **25 chapters + preface + back matter**, ~30K words, ~2 hour read. Ch. 25 is a short dedicated coda.

- Part I (Ch. 1–5) — 9,950 → 6,365 words (~25 min)
- Part II (Ch. 6–9) — 6,038 → 4,914 words (~20 min)
- Part III (Ch. 10–12) — 4,373 → 3,286 words (~13 min)
- Part IV (Ch. 13–15) — 4,476 → 3,899 words (~16 min)
- Part V (Ch. 16–19) — 6,470 → 5,027 words (~20 min)
- Part VI (Ch. 20) — 9,015 → 1,203 words (~5 min) *(consolidated from six per-tool chapters)*
- Part VII (Ch. 21–24) — 6,318 → 5,237 words (~21 min)
- Back matter: `src/sources.md`, `src/keyboard-reference.md`

Note: Part VII was renumbered from Ch. 26–29 to Ch. 21–24 after Part VI consolidation. Sources.md and any cross-references that mention Ch. 26+ may need updating before publication.

## Fact-check discipline

The research doc was fact-checked once (Apr 23, 2026). Before final publication, re-verify:

- Any URL dated 2026 (some may have been speculative at research time — flag especially the Meta engineering.fb.com post).
- Tool-specific claims (these age fast — Windsurf ownership, Cursor version features, context-window numbers).
- Any remaining bold numeric claims in Parts II-VII as they get drafted.

Every chapter draft should leave the research doc at least as clean as it found it. If a chapter surfaces a new claim not in research, add it there first (with citation), then cite in the chapter.
