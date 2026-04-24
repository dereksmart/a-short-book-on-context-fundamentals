# Chapter 17 — Your Second Brain as LLM Context

There is a movement, now several years old, that has introduced a great many people to the idea of keeping all their notes in one place. It goes by various names — *second brain*, *personal knowledge management*, *the vault* — and in its most enthusiastic form involves spending somewhat more time organizing notes than actually working with them.

This book is not going to tell you whether to join the movement. What it is going to tell you is that, once AI arrived in earnest, the second-brain vaults turned out to be in exactly the right place for a technology nobody had yet built.

## The accidental alignment

The typical second-brain setup looks like this. You have a directory — a *vault*, in Obsidian's vocabulary — full of plain-text Markdown files. Each file is a note: a meeting summary, a reading reflection, a half-formed idea, a recipe. Notes link to other notes. Some are tagged. Most have a title and a short body. There are, over the years, hundreds of them. Sometimes thousands.

Three things are true of a vault of this shape, all at once. It is in Markdown, which — as the previous chapter established — is the format LLMs read most fluently. It is on your filesystem, meaning any AI tool that can read files can read it. And the organization is human-curated: you chose what to write down and how to link it, so the signal-to-noise ratio is very much higher than an automatic capture of everything you've ever typed.

This was not a trio anyone deliberately designed. The second-brain movement predates the rise of usable AI tooling by several years. It just so happened that the practice of keeping hand-curated Markdown notes on your filesystem turned out to be almost exactly the shape that an AI hoping to have access to your working context would want. The vault is, in effect, a purpose-built context library that was built before the purpose existed.

## What plugs into what

A small ecosystem has grown up to connect AI to your notes. A quick tour.

**Smart Connections** is an Obsidian plugin that runs embedding generation locally — on your own machine — and maintains a semantic index of your vault, surfacing related notes as you write. It can also chat with the vault via roughly a hundred providers, from Claude and Gemini to local models through Ollama. ([GitHub](https://github.com/brianpetro/obsidian-smart-connections)) **Copilot for Obsidian** takes the cloud-first, chat-oriented path instead, with vault-wide retrieval and agentic note-editing. ([GitHub](https://github.com/logancyang/obsidian-copilot)) The two are complementary in practice.

**MCP servers for Obsidian** are the newer and, I would argue, most interesting development. Rather than embedding an AI inside Obsidian, they expose the vault *to* external AI tools. Point an MCP server at your vault, connect it to Claude Desktop, ChatGPT, Cursor, or any MCP-capable tool, and your notes become a queryable resource across all of them. ([iansinnott/obsidian-claude-code-mcp](https://github.com/iansinnott/obsidian-claude-code-mcp), [MarkusPfundstein/mcp-obsidian](https://github.com/MarkusPfundstein/mcp-obsidian)) This is the Chapter 15 pattern applied to personal notes: portable context, no per-tool rewrites.

Beyond Obsidian, a small field of alternatives: **Reor** (local Markdown files with an embedded vector store and local-first RAG chat), **Heptabase** (card- and canvas-level summarization, multi-provider), and **Tana** (AI tightly integrated with its schema-aware supertag system). In the contested middle sit **mem.ai**, relaunched as Mem 2.0 in 2025 amid divided opinions, and **Logseq**, whose development pace has visibly slowed. A reader picking a tool in 2026 should know where the tectonic plates are moving.

## The critical question

None of this is quite the point I want to make, though. The plugins are interesting; the underlying question is more interesting still:

*Does feeding your vault to an AI actually help?*

The honest answer is: it depends, in ways that track exactly with the principles of the preceding chapters.

**If you dump your whole vault into the context window, it usually doesn't help.** The vault is large; the window's useful middle is thin; the model skims most of your notes and latches onto whatever sits near the edges. A vault of a thousand notes poured into a million-token window is a vault the model has mostly not read.

**If you curate a small set of vault notes for a specific task, it can help quite a lot.** Three or four notes, each a few hundred tokens, pulled into context with the task — this is just-in-time retrieval from Chapter 14, applied to your personal notes rather than your team's code. The model reads them carefully and uses them well.

**If you let an embeddings plugin do the selection, the results are tool-dependent but often good.** Smart Connections, Copilot, Reor, the MCP servers — all do some version of this. Quality depends on the embeddings, the query, and the vault's size. Expect tuning. Expect surprises in both directions.

**If the vault is poorly maintained, the AI inherits the mess.** A vault full of half-written notes, inconsistent terminology, stale opinions, and contradictions will feed the model noise. The signal quality of your notes becomes the signal quality of your AI-assisted work. Garbage in, garbage referenced-authoritatively-by-your-AI-in-front-of-your-colleagues.

A vault is a context source. Context sources need maintenance. This is one more reason to review your notes occasionally, which the second-brain evangelists were going to suggest anyway.

## The empirical gap

There is, it should be said, a gap in the public research. I have not been able to find a clean independent benchmark comparing *dumping a vault into context* against *retrieving from a vault* against *using curated task-specific Markdown files* against *no vault at all*. The second-brain marketing tells you the vault helps. The engineering intuition, from everything in the preceding chapters, suggests a vault used well helps and a vault used poorly hurts. The honest state of the evidence is that we have intuition and anecdote, not a rigorous cross-tool benchmark. If you are an academic reading this: there is a paper here.

## When the vault helps most

From what I have seen, the vaults that demonstrably improve AI-assisted work tend to share a few properties. They are **narrow in scope** — about one kind of work, not all of life — because narrow vaults have more consistent vocabulary and retrieval works better. Their notes are **atomic and titled**: one idea, one file, clear heading. (The old second-brain discipline around atomic notes turns out to have been unintentionally good training for the AI era.) They are **recent**, or at least pruned — a note from five years ago, when you thought differently about the subject, can mislead the model into echoing views you no longer hold. And they have **clear structure**, via wikilinks, supertags, or plain directory organization, so the AI has something to follow.

## For Monday

One experiment, one skeptical note.

The experiment: if you have a vault, spend a week using an embeddings-based plugin — Smart Connections or Copilot, whichever appeals — and see whether the AI's output improves when it has access to your notes. Pick real tasks, not toy ones. Notice whether retrieval is surfacing the right notes and whether the AI is using them well.

The skeptical note: if you don't have a vault, this is not a required step. A well-maintained `AGENTS.md` and a few carefully chosen reference files often do more for your AI than a vast unsorted vault would. The second brain is one context source among several. It is not the ticket to AI-assisted greatness. It is a tool, with the usual properties: useful when well-made, neutral when neglected, occasionally counterproductive when it replaces the smaller, sharper piece of writing you could have done instead.
