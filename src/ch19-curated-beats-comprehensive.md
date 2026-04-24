# Chapter 19 — Curated Beats Comprehensive

In April 2026, Meta's engineering team published a [blog post](https://engineering.fb.com/2026/04/06/developer-tools/how-meta-used-ai-to-map-tribal-knowledge-in-large-scale-data-pipelines/) that, if you read it carefully, overturned a quiet pile of received wisdom about how to give AI agents the context they need.

Meta had built more than fifty specialized AI agents for internal use — for data pipelines, developer tooling, and mapping what they called the "tribal knowledge" of their engineering teams. For each agent, the team wrote a context file. The files were, on average, about **a thousand tokens** — twenty-five to thirty-five lines of text — and contained four sections: **Quick Commands**, **Key Files**, **Non-Obvious Patterns**, and **See Also**.

These tiny files, the post reported, substantially outperformed the longer, encyclopedic context files the team had initially tried.

The compass, to borrow the post's own metaphor, beat the encyclopedia.

I have held on to this finding for several chapters now, because it is the concrete evidence for a principle that has been implicit throughout the book so far. Without it, "keep your rules file short" sounds like stylistic preference. With it, the principle has a shape you can work from.

## The Meta pattern

Four sections. One thousand tokens. Here is what each section does.

**Quick Commands** is a short list of the most useful commands the agent will run in typical work. Build commands. Test commands. Deploy-check commands. Whatever the agent is likely to reach for, with exact syntax. The kitchen's mise-en-place — the things already laid out because you will reach for them.

**Key Files** points at three to six files that together characterize the shape of the codebase. Not every file. The *key* ones: the entry point, the main configuration, one representative feature implementation, the critical test file. The equivalent of "if a new hire reads these four files, they'll understand the project."

**Non-Obvious Patterns** captures the handful of conventions the model would not otherwise guess. The flaky test. The custom error-handling pattern. The reason this particular module is bigger than the others. Operational invariants, in the language of Chapter 6, curated for this agent's work rather than for the whole team's daily use.

**See Also** is a short list of references: related docs, related agents, the canonical source of truth for anything not covered above. Footnotes, restrained to what would actually be followed.

Taken together, the four sections come out to roughly a thousand tokens — twenty-five to thirty-five lines, depending on density. Not a character longer than necessary.

## Why it outperforms

Every mechanism we have covered predicts this outcome.

Attention is finite (Part I). A thousand-token file lands squarely in the useful part of the window. A ten-thousand-token file scatters most of its contents into the dim middle, where the model will skim. The longer file is mostly *not being read*, even though it is technically in context.

Rules dilute as they multiply (Chapter 8). Fifty rules in a short file each get substantial attention; five hundred rules in a long file each get very little. The shorter file has more *effective* rules than the longer one, despite containing fewer raw words.

Just-in-time beats just-in-case (Chapter 14). Anything not covered in the short file can still be retrieved when needed — the See Also section points the way. The model needs the compass, not the whole map up front.

And concise files are rules files; long files are documentation (Chapter 9). These are different artifacts. Documentation is for humans reading linearly; rules are for models attending stochastically. Conflating them produces files that are bad at both.

The Meta finding is not a new principle. It is an empirical confirmation of principles we already had reasons to believe. What it provides is a specific, replicable template — the four-section shape — that takes the principles out of the abstract and into a form you can copy.

## Porting the pattern

The four-section template generalizes beyond engineering. For a product team, Quick Commands become the decision-making shortcuts (*always ask who signs off, always check the pricing page, always run the impact-rollback check*); Key Files become the PRD template, the current OKRs, the latest research; Non-Obvious Patterns become the things the team consistently gets wrong and wants caught; See Also points at the roadmap, the interview archive, the competitive analysis. For **design**, the sections might hold critique prompts, the current system library, the spacing rules specific to this product, and the full design system respectively. For **editorial**, the house style guide, three exemplar pieces, the terminology that differentiates this publication, and the canonical back issues.

The template is not a formula. It is a starting shape. Your own four sections might be named differently, and one might be absent or replaced. What matters is the *density* and the *orientation* — toward what the agent needs right now, and away from what it might someday need.

## The failure mode to watch

There is a recognizable failure mode when people try to write a thousand-token context file for the first time. They begin well — Quick Commands is tight, Key Files is concise — and then, as they work through Non-Obvious Patterns, they start adding everything. Every pattern is non-obvious, if you look at it hard enough. Every convention has some rationale. By the end of the Patterns section, the file is three thousand tokens and growing, and its discipline has collapsed into the encyclopedic form it was supposed to avoid.

The cure is to hold the token budget as a hard constraint. A thousand tokens, plus or minus a couple of hundred. Not three thousand. Not five hundred. If you need more, you do not need a longer file; you need a *different* file, for a different agent, with a different focus.

This is the discipline Meta's team, by their own account, learned the hard way. Their first attempts were long, thorough, and not especially useful. The thousand-token constraint forced them to choose. Choosing is what made the files work.

## A closing argument for Part V

Part V has been about context that travels with you: why Markdown won, how a second-brain vault intersects with AI tools, what the memory-layer landscape looks like, and — in this chapter — why curated beats comprehensive.

If there is one idea worth carrying out of Part V, it is this. The temptation, when handed a large context window or a new memory service or a vast personal vault, is always to fill it. To pour more in. To hope the AI will find what it needs by sheer volume of what you have provided.

This is almost never the path to better output. The path to better output is the discipline of *choosing*. A shorter file. A curated subset. A handful of well-placed pointers. A thousand tokens, not ten thousand. What makes an AI session good is not how much the model has access to. It is what, of what the model has access to, actually lands in the usable part of its attention.

This is the same principle that opened the book. The right fifty lines outperform five thousand lines of everything. Every Part of this book has been a different facet of the same stone.

## For Monday

One exercise.

For the AI tool or agent you use most, write a thousand-token context file. Pick your own four sections; they need not be Meta's. Aim for twenty-five to thirty-five lines. No more. If you cannot fit what you want to say into that budget, cut. If you can, save the file, use it for a week, and see what happens.

You will find, I think, that the discipline of writing it forces a kind of clarity about your own working context that you didn't know you lacked. That is often the most useful side effect of the whole exercise: not better AI, but a better grasp of your own work.
