# Preface — How to Read This Book

This book exists because, sometime in early 2026, I found myself giving the same sixty-minute talk to the same sort of audience — engineers, designers, product managers — over and over again, and noticing each time that sixty minutes was nowhere near enough.

The talk, called *Context Fundamentals*, was about why AI sessions drift and what to do about it. The short answer it offered is the thesis of this book, which is printed in Chapter 1 and which I won't spoil here. The problem with the short answer is that it is short. It fits in a sentence. The *practice* that follows from it — the ways of writing, organizing, and thinking that turn the sentence into working habits — does not fit in a sentence, or an hour, or even a long afternoon.

What you are holding is, in effect, the long version of the talk. It is a companion, not a transcript. If you attended the live session, you will recognize the four-part structure (why sessions drift, rules, commands, knowledge) and several of the running metaphors. The book goes deeper on each. It also adds three Parts the talk didn't have time for: how to carry context across tools, a practitioner's tour of the major AI tools of 2026, and a set of reflections on where the field is heading.

## Who it's for

You, probably. The book is written for anyone who uses AI tools for work — designers, engineers, product managers, writers, researchers, analysts, anyone else who finds themselves in conversation with a language model for some meaningful fraction of their working week. It assumes no particular technical background beyond a general familiarity with *what an AI chatbot is*. It does not require you to be building AI products yourself, though the principles apply if you are.

It is not a technical manual. It will not teach you to fine-tune a model, write a RAG pipeline from scratch, or build a multi-agent orchestration framework. Those are all interesting things. They are other books.

## How it's organized

Seven Parts: twenty-four short chapters, plus a coda.

**Part I** establishes the mechanics of what an AI actually sees when you work with it. The context window, its size, its limits, how it compresses over time. Read this Part in order; the rest of the book refers back to it constantly.

**Parts II through IV** cover what the talk calls the *three layers* of a good AI session: the rules that persist across every conversation, the commands you write for specific tasks, and the knowledge the agent assembles along the way. These are the heart of the practice.

**Part V** pulls back slightly, to consider context that travels *with* you — across tools, across sessions, across jobs. Markdown's quiet victory, the personal-knowledge-management movement's accidental alignment with AI, the memory-service industry, and the principle of curation over comprehensiveness.

**Part VI** is a single reference chapter — a compact tour of the major AI tools of 2026. If you are trying to get oriented in a specific tool, skim the relevant section there. The tool-specific details will age fastest; the patterns from Parts I–V are what carry.

**Part VII** looks forward: agents and teams, the harness discipline that is emerging around production AI systems, the practice of spec-driven development, and the role of the context assembler — the person on a team whose job is to own this work.

The **back matter** collects sources, by chapter, and a condensed keyboard reference for the major AI-developer tools.

## How to read it

Three paths, depending on what you want.

**Straight through.** The book is designed to be read cover to cover, in roughly one to two hours. The chapters are deliberately short — most are around a thousand to fifteen hundred words — and each is self-contained enough that you can put the book down at the end of any one without losing the thread. Picking back up is easy.

**By Part.** Each Part stands on its own, reasonably well. If your immediate interest is rules files, read Part II. If you want to understand the tool you use, skip to Part VI. Once you've finished the Part you came for, the rest remains useful whenever you want it.

**By chapter.** The chapters are also independently useful. Each opens with a hook, states its idea plainly, walks through the evidence, and closes with a small habit for Monday morning. If you prefer to graze, the chapter-level structure supports grazing.

Wherever you read from: if a chapter refers back to an earlier one by number, the reference is usually load-bearing. You can skip it, but the earlier chapter will explain something that the later one is counting on.

## A note on the voice

The book is written in what might charitably be called a discursive style. There are asides. There are occasional jokes. There are sentences that go on for longer than is strictly necessary because the cadence felt right. I make no apology for this; technical books about emerging technologies have a short half-life, and a voice that treats the reader like an intelligent adult having a conversation ages better, I think, than one that treats them like a user reading a manual.

If the tone reminds you of Bill Bryson writing about something other than AI, that is deliberate. The subject is technical; the reader is a person; the balance between the two is the thing this book tries, imperfectly, to hold.

## A note on accuracy

Everything quantitative in this book that appears in bold — percentages, token counts, publication dates, feature specifications — is cited to a primary source, usually a vendor's documentation or a peer-reviewed paper. Where a claim circulated in industry coverage couldn't be traced to a primary source, I have either softened the claim or flagged it explicitly. The field moves quickly; some of the specific numbers will be out of date before this book reaches you, and I have tried to avoid leaning on any claim whose truth would embarrass me two years hence.

If you find an error, I would genuinely like to know.

## A last thing, before we start

The final chapter of the book, which you will reach in an hour or so, closes with the sentence *Go well.* I mean it there. I mean it here too.

These tools are new. The practices around them are newer still. The work we do with AI in 2026 is, in a real sense, being invented by the people doing it, in rooms and at desks all over the world, mostly without fanfare. You are one of those people. The fact that you are reading this book suggests you are trying to do the work well, which is — always and in every era — the first and most important thing.

I hope the pages that follow are useful. I hope they are, occasionally, enjoyable. And I hope, at the end, that you will do the work a little better than you did before, which is the only real ambition I have for any book of this kind.

On, then, to Chapter 1.
