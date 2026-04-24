# Chapter 15 — MCP, the Universal Context Protocol

The field of AI tools, until late 2024, had a quiet problem that nobody especially wanted to talk about.

Every tool had its own way of connecting to external services. ChatGPT had Plugins. Claude had an extension system. Cursor had something else again. If you wanted to build an integration — say, a tool that let an AI read your company's Linear tickets — you had to write it separately for every tool you wanted it to run in. And when the next tool came along, you wrote it again.

The result was a land of walled gardens. Every tool had its own small ecosystem of integrations, most of which didn't exist in any other tool. A user who switched from ChatGPT to Claude lost their plugins. A developer who built a clever integration for one reached, at most, the users of that one. The field had, in miniature, the same kind of splintering that had afflicted every previous era of software before standards arrived to unify it.

In November 2024, Anthropic released a specification called the **Model Context Protocol** — MCP, in the inevitable acronym — which described, in modest and fairly readable terms, how a server could expose tools and resources to a language model, and how a client (any tool with a model in it) could discover and use them. It was not, on its face, a revolutionary document. What happened next, however, was remarkable.

## The adoption

Within twelve months, MCP had been adopted by almost every major AI vendor.

**March 2025:** OpenAI adopted MCP across the Agents SDK, the Responses API, and the ChatGPT desktop client.

**April 2025:** Google DeepMind announced adoption.

**May 2025 (Build):** Microsoft rolled it out across Windows 11, Semantic Kernel, and Azure OpenAI.

**December 2025:** Anthropic formally donated MCP to the Linux Foundation, establishing the Agentic AI Foundation as its long-term steward. ([announcement](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation))

The list of tools that speak MCP at time of writing is, frankly, most of them. Claude Desktop, Claude Code, ChatGPT (desktop and API), Cursor, GitHub Copilot (via agent mode), Gemini CLI, Windsurf, Zed, Aider, and a lengthening tail of smaller tools. What you write once, as an MCP server, you can plug into any of them.

This is, I would submit, one of the least-noticed and most consequential developments of 2025. A year earlier, "write it for each tool" was simply how things were. A year later, it wasn't. That is, more or less, how standards become plumbing.

## What MCP actually is

Underneath the fanfare, MCP is a modest protocol. Its central idea is to separate the concerns of *the tool that is running the model* (the **client**) from *the service that provides context or capabilities* (the **server**).

The server advertises two kinds of things. **Tools** are functions the model can call — *read a file from this filesystem, query this database, post to this Slack channel.* **Resources** are documents or data the model can read — *this file, this record, this conversation.* The server describes each with a name, a short description, and a schema for its inputs or format.

The client — the AI tool you happen to be using — connects to any MCP servers you've configured. At startup, or on demand, it discovers what tools and resources each server exposes. When you ask the model a question, the client makes that catalog available. If the model decides it needs to call a tool or read a resource, it does so through the server, via the client.

The crucial consequence: if you run a company, you can write *one* MCP server that exposes your tickets, your dashboards, your internal docs, your Slack archive, or whatever. Every employee using any MCP-capable AI tool gets access to that context, in their tool of choice. You do not have to write a Claude plugin, a ChatGPT GPT, a Gemini extension, and a Cursor integration separately. You write once. Everyone benefits.

The same is true for individuals. If you install an MCP server for Obsidian, your entire vault becomes readable by your AI, whichever AI you happen to be using that day. The bindings between *what you know* and *what your AI can read* become, for the first time, portable.

## Examples

To give a sense of the range: **filesystem** MCP servers expose directories on your machine, for almost any working session involving your own work. **Git and GitHub** servers expose repository history, pull requests, and issues. **Linear, Jira, Asana, and Notion** servers expose your team's tickets and documents. **Slack and Discord** servers expose message histories, scoped to channels you authorize. **Obsidian** servers expose your vault. **Web and search** servers give the model controlled access to the open internet, without each tool needing to build its own browser integration.

The full directory at time of writing runs into the low thousands, with more appearing weekly. We are still in the early years of what will end up being a substantial ecosystem.

## What this means for context

Zoom out for a moment.

Part II of this book was about rules — what the model should know about your world. Part III was about commands — what you are asking right now. Part IV, which we are closing out here, has been about knowledge: what the model learns while working.

MCP sits at the seam between all three. It lets your rules file reference an MCP server as a source of truth. It lets your commands invoke tools that live outside the AI's immediate environment. It lets the model's in-session reconnaissance pull in material from your actual working world — your repo, your tickets, your notes — rather than from a frozen snapshot you attached.

In effect, MCP is the plumbing that makes *directed reconnaissance* (Chapter 13) and *just-in-time retrieval* (Chapter 14) practical at scale. Without it, every tool had its own idiosyncratic way of accessing external material. With it, you describe the integration once, and the patterns apply uniformly.

## What changed, and what did not

MCP did not make models smarter. It did not expand context windows or fix middle-drift. What it did was *standardize* the way capabilities get added to existing tools — a much more boring and much more important thing.

Standards, once established, tend to disappear from conversation precisely because they become the substrate. Nobody talks about HTTP anymore, or DNS, or the character encoding used for your email. These are the frozen layers underneath, the ones you only notice when they break. MCP is in the process of becoming the same kind of frozen layer for AI: a protocol nobody discusses because nobody needs to. When an AI tool you've never heard of ships with MCP support, which increasingly they do, the onboarding is: *add the server config, you're done.*

This is a mild definition of progress. It is also a real one.

## For Monday

Two small explorations.

First, spend ten minutes looking at what MCP servers exist for tools you already use. GitHub. Linear. Slack. Obsidian, if you keep notes there. Your file system. Most of them have off-the-shelf MCP servers you can install in a few minutes, and which will, once running, make your AI dramatically more useful in ways you hadn't anticipated.

Second, when you next find yourself copy-pasting information from an external tool into a prompt — pricing from a spreadsheet, tickets from a tracker, messages from a channel — pause. Ask if an MCP server exists for that source. If so, install it. The copy-paste step, once eliminated, does not come back.

This closes Part IV. We have now covered all four of the questions this book set out to answer: why sessions drift, what to tell the model for every session, what to tell it for the current task, and how to shape what it learns along the way.

The remaining Parts pull back. We will look at how to carry context across tools, survey the specific tools you are most likely to use, and consider where the field is heading.

The diagnosis and the prescription are complete. What follows is the map.
