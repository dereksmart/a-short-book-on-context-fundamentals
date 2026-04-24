# Sources

Inline citations throughout the book link to primary sources. This file collects them by chapter, for readers who want the reference map in one place. Where a claim could not be traced to a primary source during fact-check, the book either softens the claim or flags it explicitly; those cases are listed below under "Claims intentionally softened."

---

## Part I — The Window

### Chapter 1 — The Window Is the World
- No specific citations; material developed from research notes and workshop script.

### Chapter 2 — The Library in the Dark
- Liu et al., *Lost in the Middle: How Language Models Use Long Contexts*, TACL 2023. [aclanthology.org/2024.tacl-1.9](https://aclanthology.org/2024.tacl-1.9/), [arxiv.org/abs/2307.03172](https://arxiv.org/abs/2307.03172)
- Hsieh et al. (NVIDIA), *RULER*, COLM 2024. [arxiv.org/abs/2404.06654](https://arxiv.org/abs/2404.06654), [github.com/NVIDIA/RULER](https://github.com/NVIDIA/RULER)
- Modarressi et al. (Adobe Research), *NoLiMa*, ICML 2025. [arxiv.org/abs/2502.05167](https://arxiv.org/abs/2502.05167), [github.com/adobe-research/NoLiMa](https://github.com/adobe-research/NoLiMa)
- Kuratov et al., *BABILong*, NeurIPS 2024. [arxiv.org/abs/2406.10149](https://arxiv.org/abs/2406.10149)
- Kamradt, *Needle in a Haystack*, 2023. [github.com/gkamradt/LLMTest_NeedleInAHaystack](https://github.com/gkamradt/LLMTest_NeedleInAHaystack)

### Chapter 3 — Lost in the Middle, Still
- Liu et al., *Lost in the Middle* (above).
- "Attention Is All You Need," Vaswani et al., 2017 (not cited inline; foundational reference).

### Chapter 4 — The Screenshot of a Screenshot
- Anthropic, *Effective Context Engineering for AI Agents*, September 2025. [anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- OpenAI, *Memory and new controls for ChatGPT*, April 2025. [openai.com/index/memory-and-new-controls-for-chatgpt](https://openai.com/index/memory-and-new-controls-for-chatgpt/)
- Google Cloud, *Vertex AI Memory Bank in public preview*, July 2025. [cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview)
- Cursor, *1.2 changelog* (Memories GA in 1.2). [cursor.com/changelog/1-2](https://cursor.com/changelog/1-2)

### Chapter 5 — Where Longer Is Cheaper
- Google, *Gemini API context caching*. [ai.google.dev/gemini-api/docs/caching](https://ai.google.dev/gemini-api/docs/caching)
- OpenAI, *API prompt caching*. [openai.com/index/api-prompt-caching](https://openai.com/index/api-prompt-caching/)
- Anthropic, *Prompt caching*. [platform.claude.com/docs/en/build-with-claude/prompt-caching](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)

---

## Part II — Rules

### Chapter 6 — Invariants, Not Motivation
- No primary citations; principles drawn from research notes and Claude Code docs.

### Chapter 7 — The Rules-File Landscape
- AGENTS.md specification. [agents.md](https://agents.md/), [agentsmd.io](https://agentsmd.io/)
- Cursor rules. [docs.cursor.com/context/rules](https://docs.cursor.com/context/rules)
- GitHub Copilot custom-instructions support. [docs.github.com/en/copilot/reference/custom-instructions-support](https://docs.github.com/en/copilot/reference/custom-instructions-support)
- Gemini CLI GEMINI.md. [geminicli.com/docs/cli/gemini-md](https://geminicli.com/docs/cli/gemini-md/)
- Aider conventions. [aider.chat/docs/usage/conventions.html](https://aider.chat/docs/usage/conventions.html)
- Zed rules. [zed.dev/docs/ai/rules](https://zed.dev/docs/ai/rules)

### Chapter 8 — Size Discipline
- Claude Code, *Memory*. [code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory) — 200-line recommendation, two-strikes rule.

### Chapter 9 — Three Scopes
- Claude Code, *Memory* (above) — for auto memory, 200-line / 25KB loading.
- OpenAI memory announcement (Ch. 4 reference).
- Cursor changelog (Ch. 4 reference).
- Vertex AI Memory Bank blog (Ch. 4 reference).

---

## Part III — Command

### Chapters 10–12
- Material developed from research notes and workshop script; no specific inline citations in Ch. 10 or Ch. 11.
- Ch. 12 references: Anthropic's Agent Skills open standard and adopters. [thenewstack.io/agent-skills-anthropics-next-bid-to-define-ai-standards](https://thenewstack.io/agent-skills-anthropics-next-bid-to-define-ai-standards/)

---

## Part IV — Knowledge

### Chapter 13 — Directed Reconnaissance
- No specific citations; principles derived from Anthropic's effective context engineering and workshop script.

### Chapter 14 — Just-in-Time, Not Just-in-Case
- Anthropic effective context engineering (Ch. 4 reference).
- Chunking evaluation: [arxiv.org/abs/2504.19754](https://arxiv.org/abs/2504.19754)
- Snowflake finance-RAG: [snowflake.com/en/engineering-blog/impact-retrieval-chunking-finance-rag](https://www.snowflake.com/en/engineering-blog/impact-retrieval-chunking-finance-rag/)

### Chapter 15 — MCP, the Universal Context Protocol
- Anthropic, *Donating the Model Context Protocol*, December 2025. [anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation)
- OpenAI, *New tools and features in the Responses API*, May 2025. [openai.com/index/new-tools-and-features-in-the-responses-api](https://openai.com/index/new-tools-and-features-in-the-responses-api/)
- Microsoft, *Build 2025: The age of AI agents and building the open agentic web*, May 2025. [news.microsoft.com/source/asia/2025/05/20/microsoft-build-2025-the-age-of-ai-agents-and-building-the-open-agentic-web-en](https://news.microsoft.com/source/asia/2025/05/20/microsoft-build-2025-the-age-of-ai-agents-and-building-the-open-agentic-web-en/)
- Google Cloud, *Announcing Model Context Protocol support for Google services*, December 2025. [cloud.google.com/blog/products/ai-machine-learning/announcing-official-mcp-support-for-google-services](https://cloud.google.com/blog/products/ai-machine-learning/announcing-official-mcp-support-for-google-services)

---

## Part V — Context That Travels

### Chapter 16 — Why Markdown Won
- Gruber, *Markdown*, 2004. [daringfireball.net/projects/markdown](https://daringfireball.net/projects/markdown/)

### Chapter 17 — Your Second Brain as LLM Context
- Smart Connections: [github.com/brianpetro/obsidian-smart-connections](https://github.com/brianpetro/obsidian-smart-connections)
- Obsidian Copilot: [github.com/logancyang/obsidian-copilot](https://github.com/logancyang/obsidian-copilot)
- Obsidian Claude Code MCP: [github.com/iansinnott/obsidian-claude-code-mcp](https://github.com/iansinnott/obsidian-claude-code-mcp)
- Obsidian MCP via Local REST API: [github.com/MarkusPfundstein/mcp-obsidian](https://github.com/MarkusPfundstein/mcp-obsidian)
- Reor: [github.com/reorproject/reor](https://github.com/reorproject/reor)

### Chapter 18 — The Memory-Layer Landscape
- Anthropic memory tool: [docs.claude.com/en/docs/agents-and-tools/tool-use/memory-tool](https://docs.claude.com/en/docs/agents-and-tools/tool-use/memory-tool)
- mem0: [mem0.ai](https://mem0.ai/)
- Zep: [getzep.com](https://www.getzep.com/)
- Letta: [letta.com](https://www.letta.com/)
- LongMemEval: Wu et al., ICLR 2025, [arxiv.org/abs/2410.10813](https://arxiv.org/abs/2410.10813)

### Chapter 19 — Curated Beats Comprehensive
- Meta engineering blog, *How Meta used AI to map tribal knowledge in large-scale data pipelines*, April 6, 2026. [engineering.fb.com/2026/04/06/developer-tools/how-meta-used-ai-to-map-tribal-knowledge-in-large-scale-data-pipelines](https://engineering.fb.com/2026/04/06/developer-tools/how-meta-used-ai-to-map-tribal-knowledge-in-large-scale-data-pipelines/) — re-verified April 24, 2026: post loads with substantive content confirming 50+ specialized agents, ~1,000-token files (25–35 lines), and the four sections *Quick Commands / Key Files / Non-Obvious patterns / See Also*.

---

## Part VI — The Tool Landscape

### Chapter 20 — The Tool Landscape
- OpenAI Memory announcement (Ch. 4 reference).
- OpenAI API deprecations: [developers.openai.com/api/docs/deprecations](https://developers.openai.com/api/docs/deprecations)
- GPT-5.4 model specs: [developers.openai.com/api/docs/models/gpt-5.4](https://developers.openai.com/api/docs/models/gpt-5.4)
- NotebookLM FAQ: [support.google.com/notebooklm/answer/16269187](https://support.google.com/notebooklm/answer/16269187)
- Gemini context caching (Ch. 5 reference).
- Cursor rules (Ch. 7 reference).
- Cursor 1.2 changelog (Memories GA).
- Copilot custom-instructions support (Ch. 7 reference).
- Agent Skills coverage: [thenewstack.io/agent-skills-anthropics-next-bid-to-define-ai-standards](https://thenewstack.io/agent-skills-anthropics-next-bid-to-define-ai-standards/)
- Anthropic prompt caching (Ch. 5 reference).
- Claude Code keybindings: [code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings)

---

## Part VII — Where This Is Heading

### Chapter 21 — Subagents and Agent Teams
- Claude Code agent teams: [code.claude.com/docs/en/agent-teams](https://code.claude.com/docs/en/agent-teams)
- Multi-agent research findings are paraphrased from industry literature; individual studies not cited inline.

### Chapter 22 — Harness Engineering
- "Harness engineering" evolution: [epsilla.com/blogs/harness-engineering-evolution-prompt-context-autonomous-agents](https://www.epsilla.com/blogs/harness-engineering-evolution-prompt-context-autonomous-agents)

### Chapter 23 — Spec-Driven Development
- Industry coverage of spec-driven development. Specific percentages (e.g., "67% lower rollback rate") circulated in secondary coverage but were not traceable to a primary study during fact-check; the book softens these claims to "notably lower rollback rates" and "a growing majority."

### Chapter 24 — The Context Assembler
- No primary citations; reflections on emerging roles.

---

## Claims intentionally softened

During the fact-check pass conducted for this book (April 2026), the following claims were softened or qualified because they circulated in secondary coverage but could not be traced to a primary source:

- **"67% lower rollback rate"** for spec-driven development teams — softened to *notably lower rollback rates* (Ch. 23).
- **"72% of engineering teams now use at least one autonomous coding agent, up from 31% in 2025"** — softened to *a growing majority* (Ch. 23).
- **"~30% less attention to the middle"** figure attributed to Liu et al. — the paper does not quantify this precisely; book uses *measurable performance drops* and *U-curve* language instead (Ch. 3).

## URLs flagged for re-verification before print

- **Meta engineering blog post on AI agents and tribal knowledge** — re-verified April 24, 2026. Post loads, content substantive; the four sections and ~1,000-token figure match what Ch. 19 describes. Citation is safe to keep.
- **Tool-specific features in rapid flux** — Windsurf ownership, Cursor version features, context-window offerings across vendors. These age fast; confirm current state before print. The Cursor Memories-GA citation was corrected from `/changelog/1-0` to `/changelog/1-2` during the April 24, 2026 re-verification pass.
