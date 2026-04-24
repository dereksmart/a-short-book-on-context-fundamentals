# Outline: Context Fundamentals (the Book)

Companion ebook to the AI Enablement workshop talk of the same name. Covers context as a universal LLM skill — not Claude-specific. Written in the voice defined in `style-guide.md`.

Target reading time: **1–2 hours** (~15–30K words). Chapters are independently readable.

## Front matter

- Preface — why this book exists (a companion, not a transcript)
- How to read it (skim by chapter; each self-contained)

## Part I — Why sessions drift

Universal mechanisms. Cross-vendor framing throughout.

1. **The window is the world** *(drafted)* — one-buffer mental model. How ChatGPT, Claude, Gemini, Cursor all expose it differently but share the same constraint.
2. **The library in the dark** *(drafted)* — advertised vs. effective context. RULER, NoLiMa, LongBench v2, BABILong. The 4-10x gap that holds across vendors.
3. **Lost in the middle, still** *(drafted)* — Liu et al. 2023 (TACL) and the 2025 follow-ups. Why causal masking plus RoPE makes the U-curve structural, not a bug. The four habits that follow from accepting it.
4. **The screenshot of a screenshot** *(drafted)* — compaction across ChatGPT, Claude, Gemini, Cursor. Why both implicit memory extraction and explicit `/compact` degrade the same way. Why compacting at 60% beats 95%. Anchors and breadcrumbs.
5. **Where longer is cheaper** *(drafted)* — prompt caching across vendors. Google 90% automatic (2.5+), Anthropic 90% opt-in, OpenAI 50% automatic. Prefix rules, minimums, TTLs. The consequence nobody talks about: your rules file is the most cache-friendly thing you own.

## Part II — Rules (persistent instructions)

6. **Invariants, not motivation** *(drafted)* — the new-hire test. Invariants vs. motivation. Strong verbs (MUST/NEVER). Cross-role examples: engineering, product, design, editorial.
7. **The rules-file landscape** *(drafted)* — AGENTS.md as the cross-vendor standard (Linux Foundation Agentic AI Foundation). Tour of CLAUDE.md, Cursor's four-type system, Copilot path-scoped instructions, Gemini CLI three-level hierarchy, Aider's CONVENTIONS, plus the rest in brief.
8. **Size discipline** *(drafted)* — the 200-line guidance, attention math (0.5% per rule at 200 rules), two-strikes maintenance. Why stale rules are worse than no rules. Quarterly review.
9. **Three scopes** *(drafted)* — project / user / auto memory. How ChatGPT Memory, Cursor Memories, Vertex AI Memory Bank, and Claude auto memory all map to a common frame.

## Part III — Command (the job right now)

10. **Anatomy of a command** *(drafted)* — job, anchors, return. Worked example. Universal anatomy across tools.
11. **Letting the model ask** *(drafted)* — clarifying questions as a feature. When to declare vs. ask. Scope / constraint / context questions.
12. **From command to reusable unit** *(drafted)* — Claude Skills (open standard), Custom GPTs, Gemini Gems, Cursor Agent Requested rules, Copilot Spaces. The three-times rule for promotion.

## Part IV — Knowledge (what the agent learns along the way)

13. **Directed reconnaissance** *(drafted)* — aim, bound, encode. Cross-role examples.
14. **Just-in-time, not just-in-case** *(drafted)* — the payload approach vs. retrieval. Anthropic's "finite resource, diminishing returns" framing. Chunking and ordering (contextual retrieval, late chunking).
15. **MCP, the universal context protocol** *(drafted)* — timeline (Nov 2024 → Dec 2025 Linux Foundation). What MCP is. Examples. Why it's the plumbing.

## Part V — Context that travels with you

16. **Why markdown won** *(drafted)* — Gruber 2004, five properties, Markdown as the LLM-context lingua franca.
17. **Your second brain as LLM context** *(drafted)* — Obsidian + Smart Connections/Copilot/MCP, Reor, Heptabase, Tana; honest notes on Logseq slowdown and mem.ai. When vaults help and when they don't.
18. **The memory-layer landscape** *(drafted)* — who this is for (mostly builders, not end users). Anthropic memory tool, mem0, Zep/Graphiti, Letta, Vertex AI Memory Bank. Benchmark caveats.
19. **Curated beats comprehensive** *(drafted)* — Meta's 1K-token four-section pattern (Quick Commands, Key Files, Non-Obvious Patterns, See Also). The empirical close to Part V.

## Part VI — The tool landscape

A single consolidated reference chapter. (Originally drafted as six per-tool chapters; consolidated during the tightening pass to keep the book's focus on the universal principles of Parts I–V.)

20. **The tool landscape** *(drafted)* — compact tour of ChatGPT, Gemini, Cursor, GitHub Copilot, Claude Code, plus a one-paragraph run-through of Aider, Windsurf, Zed, Warp, Cline, Continue, and the agent-orchestration frameworks (LangGraph, CrewAI, AutoGen, Swarm, ADK). Closes with a "picking one" guide by audience.

## Part VII — Where this is heading

21. **Subagents and agent teams** *(drafted)* — the key distinction (result-only vs. negotiating agents); tool-by-tool implementations (Claude Code, Swarm, LangGraph, CrewAI, AutoGen, ADK); 3–5 teammate sweet spot.
22. **Harness engineering** *(drafted)* — blocks, measurements, repairs; evaluation and monitoring layers; connection to rest of book.
23. **Spec-driven development** *(drafted)* — spec → code → verification; four-section spec template; executable specs (with softened numbers per fact-check).
24. **The context assembler** *(drafted)* — the emerging role; four threads (authorship, curation, integration, diagnosis); role at different team scales.

## Coda

25. **Coda** *(drafted)* — a short closer. Restates the thesis, reflects on craft as slow-accumulating habit, closes with *Go well.*

## Back matter

- Full speaker script + slide deck (the workshop itself, preserved)
- Keyboard shortcut reference (Claude Code, Cursor, VS Code, Gemini CLI)
- Sources, by chapter
- About the authors / about the cohort

## Guiding principles

- **Mechanisms are universal, tools are examples.** Every Claude-specific example gets a sibling from another tool.
- **Bold claims cite.** Fact-check pass complete; write from clean ground.
- **Effective > advertised.** Never quote a context-window number without the benchmark-effective number beside it, when available.
- **Rotate examples.** Don't let one tool dominate any single Part.
- **End each chapter with something the reader carries.** A question, a habit, a way of looking.

## Status

- Research document: fact-checked Apr 23, 2026, Part 6 (cross-LLM) added.
- Style guide: drafted.
- CLAUDE.md: drafted.
- First draft: complete.
- **Tightening pass: complete.** All seven Parts tightened; Part VI consolidated from six per-tool chapters into one; Part VII renumbered from Ch. 26–29 to Ch. 21–24; dedicated closer added as Ch. 25 (Coda). Final book is **25 chapters + preface + back matter**.
  - Part I (Ch. 1–5) — 9,950 → 6,365 words (~25 min)
  - Part II (Ch. 6–9) — 6,038 → 4,914 words (~20 min)
  - Part III (Ch. 10–12) — 4,373 → 3,286 words (~13 min)
  - Part IV (Ch. 13–15) — 4,476 → 3,899 words (~16 min)
  - Part V (Ch. 16–19) — 6,470 → 5,027 words (~20 min)
  - Part VI (Ch. 20) — 9,015 → 1,203 words (~5 min) *(consolidated)*
  - Part VII (Ch. 21–24) — 6,318 → 5,237 words (~21 min)
- **Total chapter prose: ~30K words, ~2 hour read.**
- Remaining work: re-verify any URL-dated-2026 claims before publication; decisions on cover, front matter design, and epub styling. Optional second pass for voice consistency and cross-reference verification after full read-through.
