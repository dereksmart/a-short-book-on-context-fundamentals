# Chapter 18 — The Memory-Layer Landscape

There are, in 2026, quite a lot of companies whose job is to be the memory between you and a language model.

They have names like **mem0**, **Zep**, **Letta**, **Cognee**, **Supermemory**. They offer, in broad strokes, the same thing: a persistent store of facts, patterns, and user preferences that an AI application can read and write across conversations. The pitch is that dedicated memory is a first-class primitive — on par with a database or an embedding store — and deserves its own service, its own SDK, and its own pricing.

The pitch is partly true and partly marketing. This chapter is about which part is which, and — more usefully — when any of it matters for you.

A word about who this chapter is for, before we go further. If you are a person using AI for your own work, you probably do not need any of the services in this chapter. Your AI tool's built-in memory — ChatGPT's, Cursor's, Claude's — is almost certainly sufficient. The companies named below exist for a different audience: developers *building* AI-powered products at some scale, who need memory as infrastructure. If that is not you, skim this chapter or skip it. If it is, or if you are curious where the field is heading, read on.

## The problem

Say you are building a customer-support agent. A user talks to it today, says they prefer email over phone, complains about a subscription issue, and goes away reasonably satisfied. A week later, the same user returns. They expect the agent to remember, at minimum, the email preference and the subscription context. They wouldn't expect perfect recall of last week's words; they would expect *something* to have stuck.

Without a memory layer, nothing sticks. Every conversation starts from zero. The user re-explains the preference, re-describes the issue, and gradually loses patience. This is the problem. It is real. The memory-layer landscape is a catalogue of competing answers to it.

## The approaches

Three, in rough order of complexity.

The simplest is also the newest: **give the model a filing cabinet**. Anthropic's memory tool, shipped in beta in 2025, does exactly this — a `/memories` directory that the model can create, read, and update files in, and that gets re-read at the start of each conversation. When the user says something worth remembering, the model writes a short file. When a new conversation starts, the model scans the folder. No separate service. No vector store. Just a folder and a model with file-editing abilities. ([Anthropic docs](https://docs.claude.com/en/docs/agents-and-tools/tool-use/memory-tool)) Anthropic's own evaluations report a **39% improvement on agentic search tasks** and an **84% reduction in token usage on 100-turn tasks** using this pattern — their numbers, so calibrate accordingly, but the mechanism is conceptually clean and the memory is something you can open and read.

The more common approach, and the one most of the named companies have built around, is to **run a service that extracts, stores, and serves**. The service watches conversations, pulls out facts, drops them into a vector database or a knowledge graph, and serves them back when the model needs them. **mem0** is the best-known here — Y Combinator-backed, with something like fifty thousand stars on GitHub at time of writing, and a clean extract-embed-retrieve pipeline ([mem0](https://mem0.ai/)). **Zep** takes a more elaborate path, storing facts in a temporal knowledge graph that knows about time and invalidation: *the user used to live in Berlin, as of March 2024; now lives in Lisbon, as of November 2025.* Zep reports 71.2% on the LongMemEval benchmark with GPT-4o, a respectable number ([Zep](https://www.getzep.com/)). **Letta** (formerly MemGPT) takes an operating-system metaphor seriously, paging the model between a hot core, a warm recall, and a cold archive the way a CPU pages between registers, RAM, and disk ([Letta](https://www.letta.com/)). Cognee, Supermemory, OMEGA, and Mastra round out the field. A few of the newer entrants claim LongMemEval scores above 90%; I would treat those with the skepticism they deserve until independently reproduced — more on that below.

The third approach is to **let the platform handle it**. Google's Vertex AI Memory Bank, in public preview since July 2025, is the most developed example: it runs asynchronously, extracts topic-scoped facts, reconciles them over time, and integrates with the Agent Development Kit, LangGraph, and CrewAI — all on Google Cloud. ([Google blog](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview)) OpenAI has so far kept its own memory offering primarily user-facing in ChatGPT, with the Responses API covering some of the developer-facing gap.

## What actually works

The pattern, from what I have observed and what people I trust have reported, is this.

For **personal use**, built-in memory — ChatGPT's, Cursor's, Claude's — is sufficient. None are perfect; all beat rolling your own.

For **small and medium applications**, the Anthropic-style file-based memory tool is often the best starting point. Conceptually simple. Cheap to operate. Memory you can read and edit yourself, in Markdown, in a folder. When something goes wrong, you open the folder and look. Compare this to debugging a vector database, which is a different class of activity altogether.

For **applications at scale**, a dedicated memory service starts to earn its keep — thousands of users with persistent context, multi-agent coordination where different agents read each other's state, or specific requirements like temporal reasoning over changing facts (Zep's specialty).

For **enterprise deployments**, a managed service like Vertex Memory Bank offers governance, compliance, and scaling. The trade is vendor lock-in, in exchange for not operating the memory layer yourself.

Start simple. Graduate to a service only when the simpler approach is visibly failing, and only to the service whose strengths match your specific problem shape.

## The benchmark caveat

**LongMemEval**, the primary benchmark for multi-session memory, is an ICLR 2025 paper with 500 carefully-constructed questions across extraction, multi-session reasoning, temporal reasoning, knowledge updates, and abstention. ([paper](https://arxiv.org/abs/2410.10813)) It is legitimate. The numbers that vendors publish, though, are often self-reported, run on specific backbone models (one vendor might use GPT-5, another GPT-4o), on specific splits, without independent reproduction. Mem0 and Letta, notably, have not published LongMemEval scores at time of writing — which is itself a piece of information. Treat the leaderboard as a way to identify candidates worth trying, not a ranking to trust. Build a small eval for your specific use case. Run each candidate. Compare.

## For Monday

One thing to check, for each audience.

If you are an individual user: open the memory view in your primary AI tool. Delete what's stale. Ensure the saved memories reflect current you, not past you.

If you are a developer building an agent: don't reach for a memory service yet. Start with the file-based pattern — Anthropic's or something like it — and see how far it carries you. Most agents built in 2026 that advertise "memory" are using this pattern, and most produce results indistinguishable from the ones built on dedicated memory infrastructure, at a tenth of the operational complexity.

If the simple pattern starts failing, that is when to look at mem0, Zep, Letta, or whichever matches your application's shape. Evaluate carefully before committing. The field is moving quickly, and the right answer today is not necessarily the right answer six months from now.
