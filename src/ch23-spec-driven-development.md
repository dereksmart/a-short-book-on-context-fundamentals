# Chapter 23 — Spec-Driven Development

One of the more interesting shifts in how engineers work with AI, during 2025 and 2026, has had nothing to do with any particular new model or tool. It has to do with a change in the order of operations.

The old order, which still dominates casual use of AI coding tools, is: *prompt → code*. You describe what you want. The AI writes the code. You review, correct, iterate.

The new order, which an increasing share of serious engineering teams have adopted, is: *spec → code → verification*. You first write (or co-write) a specification of what the work should do. The AI writes the code from the spec. The specification becomes, at the end, the criteria against which the work is checked.

The inversion is modest in description and significant in practice. The genre goes by the name **spec-driven development**, and it is — for teams shipping AI-written code at scale — one of the more consequential habit shifts of the decade so far.

## The pitch

When you prompt an AI directly, you are describing what you want in the same moment you are asking for the output. The description is usually incomplete — you leave things out, implied by context or assumed to be obvious. The AI, filling in the gaps, makes plausible guesses. Sometimes the guesses match what you wanted. Often they do not. The result is a cycle of correction: output, correct, output, correct. It converges, more or less, but it is not efficient, and the final product is rarely what a better-specified initial ask would have produced.

When you write a spec first, several things change.

**The spec is a thinking tool.** Writing it forces you to make the implicit explicit. You discover, in the act of describing, that you hadn't decided what should happen at the edges, how the API should handle the error case, or what the performance target is. These discoveries happen *before* the model has produced anything, which is the cheapest place for them to happen.

**The spec is delegatable.** Once written, the spec is a document another person — or another agent — can execute against. You can hand it to a teammate. You can hand it to an agent. You can hand it to several agents in parallel. The work is not trapped in your head.

**The spec is verifiable.** A well-written spec includes acceptance criteria. When the work comes back, you do not squint at it and guess whether it is correct. You have a list, explicit and agreed, of what *correct* means. You run it against the list.

**The spec is durable.** A prompt vanishes after use. A spec lives in source control and becomes the canonical description of what was built. Future changes are proposed against it. The history of the work is legible.

## What the industry is reporting

Published coverage of spec-driven development, through 2025 and 2026, has been consistent in direction if not in specific numbers. Teams using written specs before agent runs report notably lower rollback rates than teams prompting without them. A growing majority of engineering teams now use at least one autonomous coding agent as part of their workflow.

I am being deliberately loose with the numbers. Specific percentages have circulated widely in secondary coverage — *a 67% reduction in rollbacks*, *72% of engineering teams*, and so on — but during the fact-check underlying this book we were unable to trace those figures to a primary study. Treat the direction as clear and the exact magnitudes as uncertain.

What is clearer, if you talk to people doing the work, is the shape of the improvement. The wins are not small. They are also not, primarily, about code quality in the narrow sense. They are about *predictability* — the work shipping in the form and at the time it was expected to, with fewer surprises and fewer late rounds of correction.

## What a spec looks like

A spec, in the spec-driven sense, is not a formal document in the IEEE-1234 tradition. It is a markdown document, usually a few hundred to a few thousand words, that answers roughly four questions. In software, the spec describes code. In product, it might describe a launch decision. In design, it might describe a handoff package. In editorial work, it might describe a revision brief. The shape is the same.

**What is being built?** The thing, in plain terms. What it does. What problem it solves. The scope, defined more by what is *not* included than by what is.

**How will it work?** The approach, at a level of detail sufficient to distinguish this solution from others. Not implementation detail — the approach. The data model, the key interfaces, the interaction pattern, the algorithmic choice, whatever the *how* is for this thing.

**What are the acceptance criteria?** The specific, checkable things that must be true for the work to be considered complete. Ideally written as tests, or as statements that could be turned into tests. *The endpoint returns 200 for valid input and 400 for invalid. The migration completes in under thirty seconds for databases up to 10M rows. The UI matches the Figma frame at 1x, 2x, and 3x densities.*

**What is out of scope?** The things someone might reasonably expect to be part of this work and which are deliberately deferred, declined, or excluded. This is the section that prevents the most arguments later.

That's it. Four sections. The document might be half a page or five depending on the work; it might have supporting diagrams or links. The shape is the same.

A spec written this way is legible to humans, legible to AI, testable, and durable. It is also, notably, much cheaper to write than most people expect. The first time, it will feel like a heavy tax on what you thought was a simple task. The second time, less so. By the tenth, you won't want to work without one.

## Executable specs

A related development, which some teams in 2026 have begun to lean into, is the **executable spec**: a spec structured so an agent can directly execute against it — parsing acceptance criteria into tests, scope definitions into file lists, the approach section into a sequence of operations. The tooling is nascent; the patterns vary. The direction is clear: specs are evolving from *documents humans read before doing the work* to *artifacts agents can partially automate*. A well-written spec in 2028 will be more programmatic still.

## Where this leaves the rest of the book

Spec-driven development is, in one sense, a particular instance of the principles we have been covering.

A spec is a **rules file for a specific piece of work**: short, dense, high-signal, human-produced, reviewable. It is therefore a very effective piece of context for an AI asked to do that work.

A spec is a **shaped command made durable**: job, anchors, return, written down once so it can be executed against many times.

A spec enables **directed reconnaissance**: by bounding what is in scope and what is out, it tells the agent where to look and where not to.

A spec supports **harness engineering**: the acceptance criteria become the eval suite; the scope definition becomes the block list.

Spec-driven development is, in effect, what happens when the habits of this book are applied with discipline to the practice of shipping software. You get a working artifact — the spec — that compresses many of the individual habits into a single place.

## For Monday

One thing to try.

For your next non-trivial coding task — or any task with enough moving parts to go wrong quietly — write a short spec first. Four sections, a page or so. Walk through what's being built, how, what counts as done, and what's out of scope. Then prompt the AI with *build to this spec, and when you think you're done, walk through the acceptance criteria and tell me how each one is satisfied.*

You will find — and this is one of those predictions I make with unusual confidence — that the result is better than what you would have gotten from a prompt alone, and that you had to write less than you expected to get there.
