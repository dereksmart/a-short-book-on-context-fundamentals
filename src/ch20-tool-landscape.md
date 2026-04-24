# Chapter 20 — The Tool Landscape

![A restrained transit-map-style desk diagram with unnamed tool paths converging on one shared context window.](assets/images/part-06-tool-landscape.png)

There is a small ritual I suspect many readers will recognize. You open your laptop in the morning, and across the top of your browser sit anywhere from four to eight tabs from AI tools you were using the day before. ChatGPT for the email. Claude for the spec. Cursor for the refactor. A Gemini tab you opened to check one thing and then didn't close. NotebookLM with a paper in it. A Copilot chat you meant to get back to.

At some point, standing in the kitchen waiting for the coffee to brew, it occurs to you — not for the first time — that you used to have *a* computer, and that you now have something closer to a small committee of specialized ones, each with its own handwriting and its own moods.

This chapter is a compact tour of that committee as it stood in April 2026: what each of the major tools is distinctively good at, what its quirks are, and how to pick one when you are making a first-time choice. It is also the chapter that will age fastest. The principles of Parts I through V will not. If you are reading this some distance from its publication, treat the tool-specific details as snapshots and the patterns as load-bearing.

## ChatGPT / OpenAI

ChatGPT is, for most of the world, what they mean when they say *the AI*. When someone who doesn't work in tech mentions using AI for something — to draft an email, plan a trip, make sense of a contract — they are almost certainly talking about ChatGPT.

The surface features worth knowing. **Custom Instructions** are two free-text fields at the account level that apply to every chat — the user-scope rules file from Chapter 9. **Projects** bundle chats with a shared system prompt, uploaded files, and isolated memory; the right container for any piece of work that spans more than a few conversations. **Custom GPTs** are ChatGPT's version of reusable commands from Chapter 12. **Memory**, since April 2025, has two layers: explicit saved memories and a quieter *chat history reference* that implicitly pattern-matches across your past chats. ([announcement](https://openai.com/index/memory-and-new-controls-for-chatgpt/))

On the API side: the **Assistants API** was deprecated August 26, 2025, with final shutdown August 26, 2026; the **Responses API** is its successor, with cleaner state and MCP support ([deprecations](https://developers.openai.com/api/docs/deprecations)). Context windows run 128K (GPT-5.1 Chat), 400K (5.1 Codex, 5.2), and 1.05M on opt-in GPT-5.4 ([model docs](https://developers.openai.com/api/docs/models/gpt-5.4)). Prompt caching is automatic at a 50% discount — half of what Google and Anthropic offer.

## Gemini / Google

Google invented the transformer and then, for organizational reasons that will keep business-school case writers busy for years, watched other companies ship products with it first. Gemini's pitch in 2026 is quieter: reach, integration, long-context throughput.

What stands out. Gemini reads from your Gmail, Drive, Calendar, and Docs when you grant permission — meaningful if you live in the Google ecosystem, irrelevant if you don't. **NotebookLM** is the easiest way for non-technical users to put curated context in front of an AI: upload up to 50 sources (300 on Plus, 600 on Ultra), ask questions grounded only in those sources, get citations back ([FAQ](https://support.google.com/notebooklm/answer/16269187)). **Gemini CLI** reads `GEMINI.md` in the three-level hierarchy described in Chapter 7, and the `/memory show` command prints the fully-assembled context — a debugging affordance the other tools could stand to copy.

Context windows advertise 1M (Gemini 2.5 Pro), with an often-promised 2M still unshipped at time of writing. Google's recall claims on those windows are vendor-reported; NoLiMa tells a different story (Chapter 2). **Implicit caching is default-on for Gemini 2.5+** at a ~90% discount — the most generous automatic deal in the industry ([caching docs](https://ai.google.dev/gemini-api/docs/caching)).

## Cursor

If ChatGPT is the AI non-technical people use, Cursor is the one engineers picked up first and never quite put down. A VS Code fork with AI baked in, designed by and for people who spend their days in code.

The distinguishing feature is the rules system: `.cursor/rules/*.mdc` files with four types — **Always**, **Auto Attached** (glob-matching), **Agent Requested** (description-driven), and **Manual** (invoked with `@`) — covered in Chapter 7. The `@`-mention picker is the primary aiming device: files, folders, docs, git refs, web pages, rules. **Memories** went GA in Cursor 1.2, per-project and per-user, with approval required for anything background-generated ([changelog](https://cursor.com/changelog/1-2)). **Background Agents** handle longer-horizon async tasks.

Cursor doesn't have its own model. You point it at Claude, GPT, or Gemini; window size and caching follow the backing model. For everyday coding in 2026, Claude Sonnet is the most common choice.

## GitHub Copilot

The oldest of the mainstream AI coding tools, arriving in 2021, and still the quiet default for teams already in GitHub's workflow. Less exciting to write about than Cursor or Claude Code; more integrated.

Copilot reads `.github/copilot-instructions.md` at the repo root and `.github/instructions/*.instructions.md` for path-scoped rules (same shape as Cursor's Auto Attached). Since August 2025, it also reads `AGENTS.md` ([docs](https://docs.github.com/en/copilot/reference/custom-instructions-support)). **Spaces** bundle curated files and docs into a named context set — closer to ChatGPT's Projects than to reusable commands. **Agent mode** is the multi-step execution mode with MCP support. **Copilot Coding Agent**, GA since September 2025, is the async issue-to-PR execution path — the same category as Cursor's Background Agents.

For most Copilot users, inline completions remain the daily driver. Everything else is gravy.

## Claude / Claude Code

The tool whose design choices this book has most often echoed — partly because the workshop this book grew from used Claude Code, partly because Anthropic's engineering team has been unusually candid about how their tools work.

Three surfaces. **claude.ai** for conversation and long-form reasoning, with its own Projects and memory. **Claude Code** for terminal-first agentic work. **The API** for developers, with prompt caching, tool use, extended thinking, context editing, and the memory tool.

Claude Code is where the design is most visible. Rules live in `CLAUDE.md` (typically one line: `@AGENTS.md`) with hierarchical loading. Auto memory lives at `~/.claude/projects/<project>/memory/`. **Skills** — the Agent Skills open standard released December 2025 ([coverage](https://thenewstack.io/agent-skills-anthropics-next-bid-to-define-ai-standards/)) — are Anthropic's version of reusable commands, adopted by Atlassian, Canva, Cloudflare, Figma, Notion, Ramp, and Sentry. **Agent teams** (v2.1.32+) support 3–5 teammates with a shared task list. Caching is opt-in at a 90% discount ([caching docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)).

The one keybinding worth knowing if you live in Claude Code: **Shift+Tab**, which cycles permission modes (Normal → Auto-Accept → Plan) and replaces ever typing `/plan` again ([keybindings](https://code.claude.com/docs/en/keybindings)).

## The rest, briefly

**Aider** (open source, terminal) has `CONVENTIONS.md` via `/read` and the cleanest editable-vs-reference distinction in any tool. **Windsurf** (now Cognition-owned after the mid-2025 three-way acquisition saga) has Cascade, Memories, and `.windsurfrules`. **Zed** (fast Rust-based editor) reads `.rules`, `CLAUDE.md`, and `AGENTS.md` as equals. **Warp** (terminal emulator with AI built in) reads `AGENTS.md` and translates natural language to shell commands. **Cline** (VS Code extension, model-agnostic) reads `.clinerules` and `AGENTS.md`. **Continue.dev** (open source, bring-your-own-model) has pluggable context providers.

On the agent-orchestration side: **LangGraph** for production multi-agent workflows; **CrewAI** for role-based shapes; **AutoGen** for research and exploration; **OpenAI Swarm** for simple multi-agent flows; **Google ADK** for agents on Vertex AI.

## Picking one

A rough guide, if you are deciding today.

**Daily coder in an IDE:** Cursor or GitHub Copilot. Cursor for the rules system and `@`-mention ergonomics; Copilot for the GitHub integration and inline completions.

**Terminal-first:** Claude Code (richest skills ecosystem), Aider (model-agnostic, `/read`/`/add` discipline), or Codex CLI (if you're already on OpenAI billing).

**In Google Workspace:** Gemini for chat, Gemini CLI for the terminal, NotebookLM for research.

**Writing, thinking, non-coding work:** ChatGPT with Projects, Claude in claude.ai for longer-form reasoning, Gemini via NotebookLM for grounded research.

**Building agents at scale:** LangGraph as default; CrewAI for clearly role-based shapes; Vertex AI Memory Bank if you need production memory on Google Cloud.

None of these are forever choices. The tools you use in 2027 will be different from the ones you use today, and that is fine. The habits you carry — short rules files, shaped commands, curated context, directed reconnaissance — will port cleanly. The tool is the instrument. The instrument is easier to swap than the practice.
