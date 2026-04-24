# Style Guide: Context Fundamentals (the Book)

Target voice: **Bill Bryson writing about LLMs.** Specifically, the Bryson of *A Short History of Nearly Everything* and *Notes from a Small Island* — curious, warm, lightly self-deprecating, allergic to jargon, quietly funny, respectful of the reader's intelligence.

This is a book for anyone who works with AI — designers, PMs, engineers, writers, operators — not a technical manual. If someone's aunt picks it up, she should find the first page pleasant. She should not, however, feel talked down to.

## Voice

- **Friendly, not chummy.** You are the well-read friend at the pub, not the viral tweeter. No "hey friends." No "let's dive in."
- **Astonish gently.** Numbers land when anchored to something ordinary. "A million tokens is about seven hundred and fifty thousand words — *War and Peace*, twice, with room left for a receipt." The facts do the work; the writer steps aside.
- **Understatement over emphasis.** "Well. Not quite." is louder than "Actually, it's WRONG."
- **Light humor, never sarcasm.** Warmth toward the subject, including its absurdities. The people who build this stuff are characters, not punchlines.
- **Respect the reader.** Don't dumb down. Bridge jargon on first use, then trust.
- **First person sparingly.** "I" is fine when it earns the moment. Never "we" as an editorial crutch. Never hector ("you must").

## Sentence craft

- Vary length. Short sentences punch. Long ones wander, and they can be wonderful when they're earning the walk.
- Parentheticals are welcome (the Bryson aside is basically a personality trait).
- Em dashes — used sparingly — for asides that want to stand out.
- Concrete over abstract. Not *large-scale retrieval inefficiencies* but *asking the librarian to read every book in the north wing before you'll tell her what you want*.
- A good rhythm: set up, set up, surprise. The third beat is where the small reveal lands.

## Structure per chapter

1. **Hook.** A small scene, odd image, or surprising claim. Never "In this chapter we will..."
2. **The one idea.** State it early, plainly, before the evidence arrives.
3. **A guided walk through the evidence.** Introduce researchers and benchmarks as characters — with names, affiliations, and the occasional charming biographical note.
4. **A reveal.** The counterintuitive turn that pays off the hook.
5. **A quiet landing.** What this changes for the reader. No hype finish.

Target length: ~1,000–1,500 words per chapter typical; up to ~2,000 for heavier chapters. Tightening discipline: a clear 1,200-word chapter beats a wandering 2,500-word one. The book as a whole aims for a 1–2 hour read (~15–30K words total).

## What to avoid

- Marketing voice: *game-changing, revolutionary, unlock, supercharge, next-generation.*
- Bullet-point fatigue. Use bullets when the content is a list. Use prose when it's a thought.
- Acronym stews. Spell things out on first use; abbreviate afterwards.
- Padded throat-clearing: *It's important to note that..., In today's fast-moving world..., It should come as no surprise...*
- Claude-as-default. Treat all frontier tools as siblings. Rotate examples across Claude, ChatGPT, Gemini, Cursor, Copilot.
- Bold claims without citations. If the number is specific, the inline link is mandatory.

## What to do

- **Name researchers.** "A team at NVIDIA led by Cheng-Ping Hsieh" is warmer than "RULER (Hsieh et al., 2024)."
- **Use the historical aside.** Context windows have a short but recognizable history. Draw on it.
- **Let metaphors run.** The library, the brilliant new hire, the screenshot of a screenshot, the small reading lamp in the middle of a Victorian library. If a metaphor is working, return to it.
- **Cite inline** as markdown links, not footnotes. The ebook is a read-through, not a textbook.
- **Close chapters with something the reader carries.** A question, a habit, a way of looking. Not a recap.

## On citations

When a specific number appears in bold prose — "a 90% discount on cached reads," "only half the tested models maintain satisfactory performance at 32K" — the inline URL goes with it on the same sentence or paragraph. If the number can't be traced to a primary source, either remove it, soften it ("industry coverage suggests..."), or flag uncertainty in-line.

The fact-check pass on the research document (Apr 23, 2026) is the canonical source for which claims are verified. When in doubt, check there first; correct the research doc before writing; write from clean ground.

## On pacing the book

- **Open big, narrow fast.** The first chapter earns the reader's attention for the rest.
- **One thesis per chapter.** If a chapter has two ideas, it is two chapters.
- **Rotate tools.** If Chapter 5 uses Cursor for its central example, Chapter 6 should reach for Gemini, ChatGPT, or Copilot.
- **Don't forget the reader's desk.** End most chapters with something small the reader could change Monday morning.

## Sample opening, for calibration

> There is a small ceremony that plays out every few months now in Silicon Valley, in which a company unveils a new large language model and announces, with the solemn confidence of a physicist reporting a new particle, that it can hold a million tokens in memory.

That sentence is the target register. One idea, stated with dry warmth, that sets up the whole chapter. Not breathless, not dry. Curious.
