# Chapter 21 — Subagents and Agent Teams

![Several organized desks connected by thin lines, suggesting coordinated agent work.](assets/images/part-07-context-assembler.png)

So far in this book we have treated the AI as a single thing. One model. One context window. One conversation at a time.

This is true for most daily work and will remain so. But it is no longer the whole picture. A growing share of serious AI work — particularly at the edge of what the field is currently capable of — involves multiple agents working together, coordinating through messages, task lists, or shared memory. The pattern goes by a few names, and the distinctions matter.

## The distinction that matters

There are, in practice, two recognizable patterns for multi-agent work.

A **subagent** is a short-lived agent spawned by a main agent to do a specific task, and which then returns its result. The main agent hands off a contained piece of work — *go figure out what's in this directory*, *summarize these fifty files*, *read the PR and report findings* — and waits for the subagent to come back. The main agent's context stays clean; the subagent's context is its own, bounded problem; the result flows back as a single return value. Everything the user sees is mediated by the main agent.

An **agent team**, by contrast, is a collection of agents with their own persistent identities, a shared task list, and the ability to message each other directly. No single agent is the sole conduit to the user. The agents negotiate, challenge each other's work, hand tasks back and forth, and arrive at a result through something closer to a collaboration than a delegation.

These are different tools for different problems. The common confusion is to treat them as the same thing at different scales. They are not.

Subagents are what you want when **only the result matters** — when the work needs doing, you do not need to watch the process, and consolidating all the reasoning in the main agent would blow its context budget. Summarizing a large codebase. Extracting facts from many documents. Running a batch of similar tasks. Having one agent read the research archive while another keeps drafting the brief. The subagent handles one piece, reports back, and disappears.

Agent teams are what you want when **the agents need to challenge each other's work** — when the quality of the output genuinely benefits from two or more perspectives, when one agent's draft needs to be reviewed by another, when a task has multiple components that can be worked in parallel and then integrated. More expensive, more complex, but capable of outcomes a single agent would struggle to reach alone.

Take an editorial review of a long manuscript, which is a pleasingly low-stakes example because the worst likely outcome is a paragraph with too much enthusiasm for semicolons. A main agent can read the outline and own the final memo. It can send one subagent to inspect the opening chapters for pacing, another to check the source claims, and a third to read only the exercises at the end of each chapter. Each comes back with a narrow report. The main agent integrates them and keeps the author's actual taste in view.

That is subagent work. Nobody needs the pacing reader and the citation checker to have a meeting.

An agent team would make sense only if the manuscript needed genuine argument between roles: an editor pushing for clarity, a technical reviewer defending precision, a market reader asking whether a beginner would care, and a lead deciding what survives. That can be useful. It can also become, with alarming speed, a small committee. And as anyone who has watched a small committee edit a sentence knows, more minds are not automatically more mercy.

Both patterns exist across every major tool. The implementations differ; the categories are the same.

## How it looks in each tool

**Claude Code.** Subagents are invoked via the `Agent` tool. The main agent dispatches a task with a prompt and an optional subagent type — `Explore` for read-only investigation, `Plan` for design work, `general-purpose` for everything else. The subagent runs with its own context and tools, and returns a single result. Agent teams, introduced in version 2.1.32, let one session act as team lead, spawning teammates via a shared task list with file-locking and direct messaging. The sweet spot is 3–5 teammates, 5–6 tasks apiece. ([agent teams docs](https://code.claude.com/docs/en/agent-teams))

**OpenAI Swarm.** A lightweight set of conventions rather than a framework: agents are defined with a name, an instruction, and a set of tools or hand-offs. Clean for simple flows; no shared state. For anything elaborate, most teams graduate to LangGraph.

**LangGraph.** The most mature of the frameworks, and the most flexible. Agents are nodes in a graph; edges describe control flow; state is explicit and checkpointable. Rewards understanding; punishes careless use. For production agents at scale, it is the de facto standard.

**CrewAI.** Opinionated and role-based — agents have roles (Researcher, Writer, Critic), goals, and backstories. Easier to pick up than LangGraph and quick to produce reasonable multi-agent behavior. Less flexible if your topology doesn't fit the role model.

**AutoGen.** The academic elder of the family, from Microsoft Research. Conversation-centric, strong research lineage, fiddly for production. Best for exploratory work.

**Google ADK.** Native framework for agents on Vertex AI. Multi-agent support is first-class; integration with Memory Bank and the rest of Google Cloud is seamless. The trade is ecosystem lock-in.

## What the research is starting to show

Multi-agent work, as a research direction, is still young. Early evidence suggests a few patterns worth naming.

**Specialization helps, up to a point.** Teams with distinct roles — reviewer, synthesizer, critic — outperform teams of generic agents. The same principle, as it happens, as specialization in human teams.

**Coordination cost is real.** Most empirical studies in 2025 put the sweet spot at 3–5 agents; past that, quality flattens or degrades. This matches the Claude Code recommendation cited above.

**Shared state beats message-passing alone.** Teams that coordinate through a shared task list or shared memory outperform teams passing messages alone, because messages can be missed, paraphrased, or lost in the middle (lost-in-the-middle, again).

**Critics help.** A team that includes a dedicated "critic" — an agent whose job is to push back — produces higher-quality output than a team of equal peers, by a margin large enough to notice even in small teams.

These findings are tentative and will evolve. They are also, I think, consistent with what anyone who has managed human teams would already suspect. The technology is new; the organizational patterns are ancient.

## When to use multi-agent at all

A heuristic, to close.

Use a **single agent** when the task is one thing, even if it is a complicated thing. A single well-directed Claude or GPT-5 session can handle most real work — including the vast majority of what this book is about.

Use **subagents** when the task involves a contained sub-problem you'd rather not consume main-agent context on. Reading many files to find one thing. Summarizing before a decision point. Any *go do this specific thing and come back* pattern.

Use **agent teams** when the task genuinely has multiple perspectives — reviewer and author, planner and executor, critic and proposer — and when the coordination cost is worth the quality gain. For most teams, this is a rare case. For complex research, elaborate refactors, or adversarial evaluation, it is worth the setup.

Do not use multi-agent for the reason most people first try it, which is to feel like you are doing advanced AI. The feeling is not a reason. The task is. If a single agent can do the work, a single agent is a better answer.

## For Monday

Two small experiments.

First, for a research-flavored task — reading a set of documents and summarizing them — try delegating to a subagent. Notice what it is like to hand off a sub-problem cleanly and get a clean return.

Second, resist the temptation to reach for agent teams unless you have a problem that genuinely benefits. The category exists; it is useful for a narrow set of work; for the other 95% of what you are doing, a single well-shaped agent remains the best answer.
