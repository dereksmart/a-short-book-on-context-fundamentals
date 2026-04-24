# Context Fundamentals: Research Notes

Deep research for AI Enablement 2026 talk and companion ebook. Compiled April 17, 2026; expanded with cross-vendor material and fact-checked April 23, 2026.

---

## Part 1: Things Most People Don't Know

### Keyboard Shortcuts That Change Everything

These are all verified against the official Claude Code keybindings docs.

- **Ctrl+G** (or Ctrl+X Ctrl+E) opens your system text editor for writing long prompts. Way better than typing multi-paragraph instructions in the terminal. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `chat:externalEditor`)

- **Shift+Tab** cycles through permission modes: Normal > Auto-Accept > Plan Mode and back. This is invisible but game-changing -- you never have to type `/plan` again. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `chat:cycleMode`)

- **Cmd+T / Meta+T** toggles extended thinking mid-session without a command. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `chat:thinkingToggle`)

- **Ctrl+B** backgrounds a running bash command so you can keep working while it runs. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `task:background`)

- **Ctrl+S** stashes your current prompt temporarily. Useful when you're mid-thought and need to check something. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `chat:stash`)

- **Ctrl+O** toggles verbose transcript view -- shows tool calls, file reads, everything Claude is doing under the hood. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `app:toggleTranscript`)

- **Ctrl+T** toggles the task list visibility. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `app:toggleTodos`)

- **Meta+O** toggles fast mode. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `chat:fastMode`)

- **Ctrl+J** inserts a newline without sending the message. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings), action: `chat:newline`)

- All keybindings are fully customizable via `~/.claude/keybindings.json` (run `/keybindings` to create/open the file). Changes are auto-detected without restarting. ([source: code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings))


### Hidden/Underused Commands

- **`/btw`** -- (community guidance, not in official Anthropic docs at time of writing) ask a side question without touching conversation history or polluting context. Reuses prompt cache so minimal cost. Good for "quick, what's the syntax for X?" while Claude is mid-task. ([source: community docs, supalaunch.com/blog/claude-code-commands-you-didnt-know-about](https://supalaunch.com/blog/claude-code-commands-you-didnt-know-about-hidden-features-shortcuts-guide))

- **`/loop`** -- schedule recurring prompts in the background. E.g., poll deploy status every 5 minutes. ([source: code.claude.com/docs/en/commands](https://code.claude.com/docs/en/commands), bundled skill)

- **Dynamic context injection in skills** -- the `` !`command` `` syntax in SKILL.md executes a shell command and substitutes the output into the prompt at runtime. E.g., `` !`gh pr diff` `` gets replaced with actual PR diff before Claude sees the prompt. ([source: code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills), "Inject dynamic context" section)

- **`$ARGUMENTS[N]`** -- skills support positional argument access. `/migrate-component SearchBar React Vue` makes `$0` = SearchBar, `$1` = React, `$2` = Vue. ([source: code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills), "Available string substitutions")

- **`/init` with `CLAUDE_CODE_NEW_INIT=1`** -- enables an interactive multi-phase flow that asks which artifacts to set up (CLAUDE.md, skills, hooks), explores with a subagent, asks follow-up questions, then presents a reviewable proposal before writing anything. ([source: code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory), "Set up a project CLAUDE.md" tip)

- **Skill lifecycle after compaction** -- when context compacts, Claude Code re-attaches the most recent invocation of each skill (first 5,000 tokens each), with a combined budget of 25,000 tokens across all skills. Most recently invoked skills get priority. ([source: code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills), "Skill content lifecycle")


### The "Lost in the Middle" Problem

Models attend more to the **beginning and end** of context, with measurable performance drops when key information sits in the middle. This is a U-shaped performance pattern rooted in causal masking and positional-encoding geometry.

- **The research**: Liu et al., "Lost in the Middle: How Language Models Use Long Contexts," Stanford + UC Berkeley + Samaya AI + Meta/FAIR, *Transactions of the ACL*, 2023. Performance is highest when relevant information is at the beginning or end of the input, and degrades when key info is buried in the middle -- even for "long-context" models. The paper does not quantify an exact "X% attention drop" figure; use directionally. ([source: aclanthology.org/2024.tacl-1.9](https://aclanthology.org/2024.tacl-1.9/), [arxiv.org/abs/2307.03172](https://arxiv.org/abs/2307.03172))

- **Practical implication**: The *position* of your rules in CLAUDE.md matters. Critical rules first, important corrections last, routine stuff in the middle.

- **Surprising benchmark finding**: Recursive 512-token chunking actually beat semantic chunking in RAG benchmarks (69% vs 54% accuracy), flipping conventional wisdom that "smarter chunking = better results." ([source: firecrawl.dev/blog/best-chunking-strategies-rag](https://www.firecrawl.dev/blog/best-chunking-strategies-rag))


### Agent Teams (Experimental, v2.1.32+)

Multiple Claude Code instances working together with shared task coordination. Verified against official docs:

- One session acts as "team lead," spawns teammates, coordinates work via shared task list
- Each teammate has its own context window -- they don't share conversation history
- Teammates can message each other directly (not just report back to lead)
- **In-process mode**: Shift+Down cycles between teammates. **Split-pane mode**: requires tmux or iTerm2
- Task list uses file locking to prevent race conditions when multiple teammates claim the same task
- Can require plan approval before teammates make changes
- Teammates inherit the lead's permission settings at spawn
- Sweet spot: 3-5 teammates, 5-6 tasks per teammate

**vs. Subagents**: Subagents report results back to the main agent only. Agent teams have inter-agent communication and a shared task list with self-coordination. Use subagents when only the result matters; use teams when agents need to discuss and challenge each other.

([source: code.claude.com/docs/en/agent-teams](https://code.claude.com/docs/en/agent-teams))


### Prompt Caching Math

Sometimes making your prompt *longer* reduces total cost.

- Cached input tokens are **10x cheaper** than regular input tokens for Anthropic reads (0.1x base price); other vendors differ (see Part 6 table)
- Cache minimum is model-dependent: 1,024 tokens on older Sonnets; 2,048 on Sonnet 4.6 and Haiku 3.5; 4,096 on Opus 4.5/4.6/4.7 and Haiku 4.5
- CLAUDE.md at project root is a perfect cache candidate: stable, read every turn
- Arrange prompts with stable content first, volatile content last, to maximize cache prefix length

([source: platform.claude.com/docs/en/build-with-claude/prompt-caching](https://platform.claude.com/docs/en/build-with-claude/prompt-caching))


### MCP Tool Loading is Deferred by Default

MCP tool names are listed at startup so Claude knows what's available, but **full schemas stay deferred** -- Claude loads specific ones on-demand via tool search when a task needs them. You can control this:
- `ENABLE_TOOL_SEARCH=auto` loads schemas upfront when they fit within 10% of the context window
- `ENABLE_TOOL_SEARCH=false` loads everything upfront

([source: code.claude.com/docs/en/context-window](https://code.claude.com/docs/en/context-window), startup event descriptions)


---

## Part 2: Things Everyone Should Know (But Many Don't Practice)

### The 200-Line Rule

Keep CLAUDE.md under ~200 lines. This is verified in the official docs:

> "Size: target under 200 lines per CLAUDE.md file. Longer files consume more context and reduce adherence. If your instructions are growing large, split them using imports or `.claude/rules/` files."

([source: code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory), "Write effective instructions")

**The attention math**: With 200 rules, each gets ~0.5% of the model's attention. With 5 rules, each gets ~20%. Community reports consistently say Claude starts treating entries as suggestions past 200 lines.


### The "Two Strikes" Maintenance Rule

Only add a correction to CLAUDE.md the second time Claude makes the same mistake. First-time issues are usually one-offs. From the docs:

> "Add to it when: Claude makes the same mistake a second time."

([source: code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory), "When to add to CLAUDE.md")


### What Survives Compaction (and What Doesn't)

This is critical and widely misunderstood:

- **Survives**: Project-root CLAUDE.md is re-read from disk and re-injected after `/compact`. Auto memory (MEMORY.md) is also re-loaded.
- **Does NOT survive automatically**: Nested CLAUDE.md files in subdirectories -- they reload only when Claude reads a file in that subdirectory again.
- **Skills after compaction**: Most recent invocation of each skill is re-attached (first 5,000 tokens), with a combined budget of 25,000 tokens. Older skills can be dropped entirely.
- **Conversation-only instructions disappear**: If you only said it in chat and never put it in CLAUDE.md, it's gone after compaction.

([source: code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory), "Instructions seem lost after /compact")
([source: code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills), "Skill content lifecycle")


### Compact at 60%, Not 95%

Most people wait until auto-compaction fires at ~95%. By then, "lost in the middle" is already corrupting responses. Compacting at 60% gives Claude a clean slate while memory is still fresh. Use `/compact focus on <what matters>` to guide what gets preserved.

([source: anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), compaction recommendations)
([source: mindstudio.ai/blog/claude-code-compact-command-context-management](https://www.mindstudio.ai/blog/claude-code-compact-command-context-management))


### Anthropic's Core Context Engineering Principles

From their September 2025 blog post by Prithvi Rajasekaran, Ethan Dixon, Carly Ryan, and Jeremy Hadfield:

> "Context, therefore, must be treated as a finite resource with diminishing marginal returns."

Key recommendations:
1. Find "the smallest possible set of high-signal tokens that maximize the likelihood of some desired outcome"
2. System prompts need balance between overly-specific brittle logic and vague ineffective guidance
3. Minimize tool overlap in functionality; return information efficiently
4. Use "just-in-time" retrieval: lightweight identifiers that let agents dynamically load data at runtime
5. For long-horizon tasks: implement compaction, use structured note-taking, deploy sub-agent architectures

([source: anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), published September 29, 2025)


### Memory System: Three Scopes

Verified from official docs:

| Scope | Who writes | What it contains | How it's shared |
|-------|-----------|-----------------|-----------------|
| **Project memory** (CLAUDE.md) | You | Instructions and rules | Team via source control |
| **User memory** (~/.claude/CLAUDE.md) | You | Personal preferences for all projects | Just you, all projects |
| **Auto memory** (~/.claude/projects/\<project\>/memory/) | Claude | Learnings and patterns | Machine-local, per git repo |

Auto memory loads the first 200 lines or 25KB of MEMORY.md at session start. Topic files (debugging.md, patterns.md, etc.) load on demand.

([source: code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory))


### Context Window: What Actually Gets Loaded at Startup

From the interactive context window visualization in the docs, here's the startup sequence:

1. System prompt (~4,200 tokens) -- always loaded, never visible
2. Auto memory / MEMORY.md (~680 tokens)
3. Environment info (~280 tokens) -- working directory, OS, git status
4. MCP tools (deferred by default, ~120 tokens for names only)
5. CLAUDE.md files (project + user + managed policy)
6. `.claude/rules/` files (unconditional ones)
7. Skill descriptions (names always included; descriptions shortened if many skills)
8. Your first prompt

([source: code.claude.com/docs/en/context-window](https://code.claude.com/docs/en/context-window))


---

## Part 3: Concepts Worth Adding to the Talk

### The Evolution Framework

The field is evolving in recognizable phases:
- **Prompt Engineering** (2022-2024): Focus on the single user instruction
- **Context Engineering** (2025): Architect the entire information environment
- **Harness Engineering** (2026): Build systems of control around agents -- what do you *block*, what do you *measure*, what do you *repair*?

([source: epsilla.com/blogs/harness-engineering-evolution-prompt-context-autonomous-agents](https://www.epsilla.com/blogs/harness-engineering-evolution-prompt-context-autonomous-agents))


### Spec-Driven Development

Industry coverage reports that teams using written specs before agent runs see notably lower rollback rates than teams prompting without them, and a growing majority of engineering teams now use at least one autonomous coding agent. (Specific percentages circulating in secondary coverage — e.g., "67% lower rollback" — were not traceable to a primary study at the time of our fact-check; treat directionally.)

A spec inverts the workflow from "prompt > code" to "spec > code > verification." Specs are parseable (agent can check completion), measurable (explicit acceptance criteria), and delegatable.

([source: venturebeat.com/orchestration/agentic-coding-at-enterprise-scale-demands-spec-driven-development](https://venturebeat.com/orchestration/agentic-coding-at-enterprise-scale-demands-spec-driven-development/))
([source: medium.com/@visrow/spec-driven-development-is-eating-software-engineering](https://medium.com/@visrow/spec-driven-development-is-eating-software-engineering-a-map-of-30-agentic-coding-frameworks-6ac0b5e2b484))


### Design Systems as Agent Context

Figma's MCP server scans codebases and outputs structured rules files with token definitions, component structure, and naming conventions. The W3C Design Tokens specification reached stable version (2025.10), establishing a production-ready, vendor-neutral format.

Design systems are becoming active carriers of craft: encoding a team's taste and judgment so AI can apply them at scale.

([source: figma.com/blog/design-systems-ai-mcp](https://www.figma.com/blog/design-systems-ai-mcp/))
([source: figma.com/blog/5-shifts-redefining-design-systems-in-the-ai-era](https://www.figma.com/blog/5-shifts-redefining-design-systems-in-the-ai-era/))


### Meta's "Compass Not Encyclopedia" Finding

Meta built 50+ specialized AI agents with pre-computed context files of ~1,000 tokens each (25-35 lines). Four sections per file: Quick Commands, Key Files, Non-Obvious Patterns, and See Also. These dense files outperformed longer encyclopedic ones. (Re-verify blog post availability before citing in print — URL carries a 2026 date that may be speculative.)

([source: engineering.fb.com/2026/04/06/developer-tools/how-meta-used-ai-to-map-tribal-knowledge-in-large-scale-data-pipelines](https://engineering.fb.com/2026/04/06/developer-tools/how-meta-used-ai-to-map-tribal-knowledge-in-large-scale-data-pipelines/))


### "Context Assembler" as an Emerging Role

As teams scale with AI agents, someone needs to own context file architecture, monitor drift, and resolve cross-discipline conflicts in the context budget.

- Small teams (10-20 devs): one developer wears the context hat part-time
- Medium teams (50+ devs): dedicated context engineer or architect
- Large orgs: center of excellence with federated context owners per team

([source: sdggroup.com/en-ae/insights/blog/agentic-ai-2026-from-assistants-to-high-productivity-digital-peers](https://www.sdggroup.com/en-ae/insights/blog/agentic-ai-2026-from-assistants-to-high-productivity-digital-peers))


### Token Budget Allocation Framework

Advanced teams dynamically allocate based on task needs:

| Component | Budget % | Rationale |
|-----------|----------|-----------|
| System instructions | 10-15% | Highest leverage tokens |
| Core rules (CLAUDE.md) | 5-10% | Project/team conventions |
| Conversation history | 20-30% | Maintain coherence across steps |
| Retrieved context (files, RAG) | 30-50% | Task-specific knowledge |
| Tools/API context | 5-15% | Available actions and integrations |

([source: getmaxim.ai/articles/context-window-management-strategies-for-long-context-ai-agents-and-chatbots](https://www.getmaxim.ai/articles/context-window-management-strategies-for-long-context-ai-agents-and-chatbots/))


### Production Reality Check

LangChain's State of Agent Engineering report (2025) puts agent adoption at **57.3% of organizations in production**, with **about one-third** citing quality as the top barrier. Many of those quality failures, per the report's analysis, trace to context management rather than to raw model capability.

([source: langchain.com/state-of-agent-engineering](https://www.langchain.com/state-of-agent-engineering))


### Agent Skills as an Open Standard

Anthropic's Agent Skills spec was released as an open standard in December 2025. Early adopters include Atlassian, Canva, Cloudflare, Figma, Notion, Ramp, and Sentry. (OpenAI and Microsoft operate parallel systems — GPT Store and Copilot declarative agents — rather than adopting the Skills spec itself.) Skills use progressive disclosure:

1. **Discovery** (startup): Agent loads only name + description -- minimal context cost
2. **Activation** (when matched): Agent reads full SKILL.md -- detailed instructions
3. **Execution** (when applied): Agent loads scripts, references, external data

([source: code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills))
([source: thenewstack.io/agent-skills-anthropics-next-bid-to-define-ai-standards](https://thenewstack.io/agent-skills-anthropics-next-bid-to-define-ai-standards/))


---

## Part 4: Skills/Commands Quick Reference

### Built-in Commands (Fixed Logic)
`/help` `/clear` `/compact` `/context` `/memory` `/model` `/plan` `/cost` `/config` `/init` `/keybindings` `/statusline` `/permissions` `/doctor` `/resume`

### Bundled Skills (Prompt-Based)
`/simplify` `/batch` `/debug` `/loop` `/claude-api` `/init` `/review` `/security-review`

### Skill Control Frontmatter

| Field | What it does |
|-------|-------------|
| `disable-model-invocation: true` | Only user can invoke (e.g., `/deploy`) |
| `user-invocable: false` | Only Claude can invoke (background knowledge) |
| `context: fork` | Runs in isolated subagent context |
| `agent: Explore` | Which subagent type to use with `context: fork` |
| `allowed-tools` | Pre-approve specific tools without per-use prompts |
| `paths` | Only activate when working with matching files |
| `model` | Override model for this skill |
| `effort` | Override effort level for this skill |

([source: code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills), "Frontmatter reference")


---

## Part 5: Key Source Links

### Official Anthropic/Claude
- [Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) -- Anthropic blog, Sep 2025
- [Claude Code: Memory](https://code.claude.com/docs/en/memory) -- CLAUDE.md, auto memory, rules
- [Claude Code: Context Window](https://code.claude.com/docs/en/context-window) -- interactive visualization
- [Claude Code: Keybindings](https://code.claude.com/docs/en/keybindings) -- full shortcut reference
- [Claude Code: Skills](https://code.claude.com/docs/en/skills) -- custom commands, SKILL.md
- [Claude Code: Agent Teams](https://code.claude.com/docs/en/agent-teams) -- multi-agent coordination
- [Claude Code: Best Practices](https://code.claude.com/docs/en/best-practices) -- official guidance
- [Prompt Caching](https://platform.claude.com/docs/en/build-with-claude/prompt-caching) -- API docs

### Research
- [Lost in the Middle (Liu et al.)](https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00638/119630/) -- TACL 2024, attention patterns
- [Agent READMEs: Empirical Study](https://arxiv.org/html/2511.12884v1) -- context file quality research
- [Budget-Aware Tool-Use](https://arxiv.org/html/2511.17006v1) -- token budget management

### Industry
- [Figma: Design Systems and AI / MCP](https://www.figma.com/blog/design-systems-ai-mcp/) -- design context
- [Meta: Mapping Tribal Knowledge](https://engineering.fb.com/2026/04/06/developer-tools/how-meta-used-ai-to-map-tribal-knowledge-in-large-scale-data-pipelines/) -- 50+ agent case study
- [LangChain: State of Agent Engineering](https://www.langchain.com/state-of-agent-engineering) -- production survey
- [VentureBeat: Spec-Driven Development](https://venturebeat.com/orchestration/agentic-coding-at-enterprise-scale-demands-spec-driven-development/) -- 67% lower rollback rate
- [How to Build AGENTS.md (2026)](https://www.augmentcode.com/guides/how-to-build-agents-md) -- practical guide

### Cross-Platform
- [AGENTS.md Specification](https://agents.md/) -- open standard
- [Agent Skills Specification](https://agentskills.io/) -- Anthropic open standard
- [Cursor Rules Docs](https://docs.cursor.com/en/context/rules) -- .cursorrules
- [GitHub Copilot Context Management](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/context-management)


---

## Part 6: Cross-LLM Context Landscape

The workshop runs on Claude Code, but the mechanisms and failure modes in Parts 1-2 are universal. This section grounds the companion ebook in what every other major tool is doing.

### Advertised vs. Effective Context (Model-Agnostic)

The single most important honest number in the field: **effective context is 4-10x smaller than advertised**, across vendors, on hard benchmarks.

- **RULER** (Hsieh et al., NVIDIA, COLM 2024): generalizes needle-in-a-haystack to 13 tasks across retrieval, multi-hop tracing, aggregation, and QA. Headline: "only half of the 17 tested models maintain satisfactory performance at 32K tokens." GPT-4-1106 and Llama-3.1-70B (both advertised 128K) showed effective context of 64K; Command-R+ and Qwen2-72B collapsed to 32K despite 128K claims; only Gemini-1.5-Pro and Jamba-1.5-Large crossed 128K. ([arxiv.org/abs/2404.06654](https://arxiv.org/abs/2404.06654), [github.com/NVIDIA/RULER](https://github.com/NVIDIA/RULER))

- **NoLiMa** (Modarressi et al., Adobe Research, ICML 2025): strips lexical overlap between question and needle so models can't shortcut via keyword matching. Across 13 models claiming ≥128K support, 11 dropped below 50% of short-context baseline by 32K. Per-model effective lengths (point where model holds ≥85% of baseline): GPT-4o ~8K, GPT-4.1 ~16K, Claude 3.5 Sonnet ~4K, Gemini 1.5 Pro ~2K. ([arxiv.org/abs/2502.05167](https://arxiv.org/abs/2502.05167), [github.com/adobe-research/NoLiMa](https://github.com/adobe-research/NoLiMa))

- **LongBench v2** (THU, 2024): 503 multiple-choice questions across 8K-2M words; six task families. Human baseline 53.7% under a 15-min time limit; top model at release (o1-preview) hit 57.7%. Reasoning-heavy models dominate. ([longbench2.github.io](https://longbench2.github.io/))

- **BABILong** (Kuratov et al., NeurIPS 2024): extends bAbI reasoning tasks into haystack form, scaling to 10M tokens. "Popular LLMs effectively utilize only 10-20% of the context and performance declines sharply with reasoning complexity." ([arxiv.org/abs/2406.10149](https://arxiv.org/abs/2406.10149))

Needle-in-a-Haystack (Kamradt, 2023) is now saturated — frontier models ace it while failing RULER variants at the same length. Successors: **OpenAI-MRCR** (multi-round coreference, [huggingface.co/datasets/openai/mrcr](https://huggingface.co/datasets/openai/mrcr)) and **Michelangelo** ([arxiv.org/abs/2409.12640](https://arxiv.org/abs/2409.12640)) require distinguishing multiple near-identical needles — defeating simple retrieval heuristics.

**Multi-session memory**: **LongMemEval** (Wu et al., ICLR 2025) is the primary benchmark. 500 questions across extraction, multi-session reasoning, temporal reasoning, knowledge updates, abstention. When required to reason across full ~115K-token history *without* retrieval, accuracy drops 30-60% vs. oracle retrieval. GPT-4o scores ~92% with oracle sessions, ~58% in interactive setting. ([arxiv.org/abs/2410.10813](https://arxiv.org/abs/2410.10813))

### Rules Files Across Tools

The cross-vendor standard is **AGENTS.md**, stewarded since late 2025 by the Agentic AI Foundation under the Linux Foundation. Verified adopters: OpenAI Codex, Cursor, GitHub Copilot (Aug 2025), Google Jules, Gemini CLI, Aider, Zed, Warp, Windsurf, RooCode, Cline, Continue.dev, Amp, Factory, goose, opencode, Kilo Code, Junie. Claimed 60K+ repos use one. ([agents.md](https://agents.md/), [agentsmd.io](https://agentsmd.io/))

| Tool | Rules format | Notes |
|------|-------------|-------|
| Claude Code | `CLAUDE.md` (+ `@AGENTS.md` import) | Hierarchical; project/user/enterprise scopes |
| Cursor | `.cursor/rules/*.mdc` | Four types: Always, Auto Attached, Agent Requested, Manual ([docs](https://docs.cursor.com/context/rules)) |
| GitHub Copilot | `.github/copilot-instructions.md` + `.github/instructions/*.instructions.md` | Path-scoped via glob frontmatter; also reads AGENTS.md ([docs](https://docs.github.com/en/copilot/reference/custom-instructions-support)) |
| Gemini CLI | `GEMINI.md` | Three-level hierarchy: global, project-upward, component-downward ([docs](https://geminicli.com/docs/cli/gemini-md/)) |
| Windsurf | `.windsurfrules` | Cascade-aware |
| Aider | `CONVENTIONS.md` (via `/read`) | Read-only + cache-eligible |
| Cline | `.clinerules` | Also reads AGENTS.md |
| Zed | `.rules` | Also reads CLAUDE.md and AGENTS.md ([docs](https://zed.dev/docs/ai/rules)) |

### Memory Systems Across Tools

| Tool | Memory mechanism | Notable |
|------|-----------------|---------|
| ChatGPT | Saved memories + chat-history reference | Expanded Apr 10, 2025 to reference all prior conversations implicitly. Deleting a chat doesn't delete derived memories. ([announcement](https://openai.com/index/memory-and-new-controls-for-chatgpt/)) |
| Claude | Project/user CLAUDE.md + auto memory + memory tool (beta) | Memory tool reports **39% lift on agentic search, 84% token reduction on 100-turn tasks** (Anthropic internal evals) ([docs](https://docs.claude.com/en/docs/agents-and-tools/tool-use/memory-tool)) |
| Gemini | Vertex AI Memory Bank | Public preview Jul 8, 2025; async extraction, topic-scoped, contradiction reconciliation ([blog](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview)) |
| Cursor | Memories (per-project, per-user) | GA in Cursor 1.2 ([changelog](https://cursor.com/changelog/1-2)) |
| Windsurf | Memories | Persist across Cascade sessions |
| Third-party | mem0, Zep/Graphiti, Letta, Cognee, Supermemory | Cross-vendor memory layers accessed via SDK/MCP. Treat leaderboard numbers as directional; benchmarks vary by backbone model. |

### Prompt Caching Across Vendors

| Vendor | Trigger | Cached-input discount | Notes |
|--------|---------|----------------------|-------|
| Google (Gemini 2.5+) | **Automatic, on by default** | **~90%** | Explicit caching available for TTL control. Gemini 2.0: 75%. ([docs](https://ai.google.dev/gemini-api/docs/caching)) |
| Anthropic | Opt-in via `cache_control` | **90%** on read | 25% write premium (5-min TTL) or 100% (1-hour TTL); min 1,024-4,096 tokens by model ([docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)) |
| OpenAI | **Automatic, zero-config** | **50%** | ≥1,024 token prefix; GPT-4o/5-family ([docs](https://openai.com/index/api-prompt-caching/)) |

Headline for the book: **Google 90% automatic > Anthropic 90% opt-in > OpenAI 50% automatic.** OpenAI's smaller discount is often missed.

### Context Windows (Honest Version)

| Model | Advertised | NoLiMa effective | Note |
|-------|-----------|------------------|------|
| GPT-4o | 128K | ~8K | |
| GPT-4.1 | 128K | ~16K | |
| GPT-5.1 Chat | 128K | — | |
| GPT-5.1 Codex / 5.2 | 400K | — | |
| GPT-5.4 / 5.4 pro | **1.05M** (opt-in) | — | Prompts >272K priced 2x input, 1.5x output ([docs](https://developers.openai.com/api/docs/models/gpt-5.4)) |
| Claude 3.5 Sonnet | 200K | ~4K | |
| Claude Sonnet 4.5/4.6 | 200K (1M beta) | — | |
| Gemini 1.5 Pro | 1M | ~2K | |
| Gemini 2.5 Pro | 1M | — | Google-reported 99.7% recall at 1M (vendor claim, not independent) |

Treat advertised figures as marketing and effective figures as what to design for.

### MCP Adoption Timeline

- **Nov 2024**: Anthropic announces Model Context Protocol
- **May 2025**: OpenAI adds remote MCP server support to the Responses API, building on MCP support in the Agents SDK ([announcement](https://openai.com/index/new-tools-and-features-in-the-responses-api/))
- **May 2025**: Microsoft announces broad first-party MCP support across GitHub, Copilot Studio, Dynamics 365, Azure AI Foundry, Semantic Kernel, and Windows 11 ([announcement](https://news.microsoft.com/source/asia/2025/05/20/microsoft-build-2025-the-age-of-ai-agents-and-building-the-open-agentic-web-en/))
- **Dec 2025**: Google Cloud announces official MCP support for Google services ([announcement](https://cloud.google.com/blog/products/ai-machine-learning/announcing-official-mcp-support-for-google-services))
- **Dec 2025**: MCP donated to Linux Foundation's Agentic AI Foundation ([announcement](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation))

MCP is now the cross-vendor protocol for giving LLMs tools and context. AGENTS.md is the cross-vendor format for giving them instructions. These two standards, more than any single tool feature, define the 2026 context landscape.

### Tool-Specific Quick Reference

**ChatGPT / OpenAI**
- Rules: Custom Instructions (per-account), Projects (per-project with own memory), Custom GPTs (shareable)
- Assistants API deprecated Aug 26, 2025; **shutdown Aug 26, 2026**. Responses API is the successor. ([deprecations](https://developers.openai.com/api/docs/deprecations))
- Context windows: GPT-5.1 Chat 128K; GPT-5.1 Codex / 5.2 400K; GPT-5.4 1.05M opt-in

**Gemini / Google**
- GEMINI.md three-level hierarchy; `/memory show` prints assembled context
- Context caching default-on for Gemini 2.5+
- NotebookLM: 50 sources/notebook free, 300 Plus, 600 Ultra; 500K words per source ([FAQ](https://support.google.com/notebooklm/answer/16269187))

**Cursor**
- `.cursor/rules/*.mdc` with four rule types
- `@`-mentions for files, folders, docs, git refs, web pages
- Memories GA in 1.2; Background Agents for longer-horizon remote work

**GitHub Copilot**
- `.github/copilot-instructions.md` + path-scoped `.github/instructions/*.instructions.md`
- Reads AGENTS.md (Aug 2025+)
- Spaces bundle curated context sets for chat; Coding Agent GA Sep 2025 (issue-to-PR async)

**Windsurf (Cognition)** — acquisition status: Google paid ~$2.4B for license + CEO/co-founder mid-2025; Cognition bought remaining operating business. Product still ships. Reconfirm before print.

**Aider** — `/read CONVENTIONS.md` marks read-only + cache-eligible; `/add` brings file into editable set. Repo map tree-sitter-based, default 1K-token budget.

### Obsidian / PKM Integrations

- **Obsidian plugins**: Smart Connections (local embeddings, 100+ providers), Copilot for Obsidian (cloud-first, vault-wide RAG, agentic actions)
- **MCP servers for Obsidian**: iansinnott/obsidian-claude-code-mcp (WebSocket + HTTP/SSE), MarkusPfundstein/mcp-obsidian (via Local REST API plugin)
- **Local-first PKM with LLM**: Reor (Obsidian-compatible markdown, LanceDB vectors, local Ollama or OpenAI-compatible endpoint)
- **Multi-provider native**: Heptabase (OpenAI/Gemini/Anthropic at card/canvas level), Tana (schema-aware AI via supertags)
- **Flag for caution**: Logseq development cadence visibly slowed (community perception); mem.ai trajectory contested

([Smart Connections](https://github.com/brianpetro/obsidian-smart-connections), [Obsidian Copilot](https://github.com/logancyang/obsidian-copilot), [Reor](https://github.com/reorproject/reor), [agents.md](https://agents.md/))

### Counter-intuitive Findings Worth Highlighting

- **Long-context ≠ solved context**. Even at 1M tokens, "lost in the middle" degradation persists across all frontier models. Dumping a full Obsidian vault into context measurably loses to reranked RAG ([RAGFlow 2025 review](https://ragflow.io/blog/rag-review-2025-from-rag-to-context)).
- **Chunking strategy dominates raw capacity**. Snowflake finance-RAG work: chunking and retrieval ordering matter more for output quality than raw window size ([blog](https://www.snowflake.com/en/engineering-blog/impact-retrieval-chunking-finance-rag/)). Contextual retrieval (Anthropic 2024) and late chunking (Jina AI) both beat naive chunking on independent evals.
- **Recency placement wins**. Placing retrieved chunks at the *end* of the prompt exploits the recency half of the U-curve and measurably outperforms middle placement. Practical consequence: put crucial instructions right before your ask, not at the top.
- **No frontier model is free of middle-drift**. Ms-PoE, "Found in the Middle" calibration, and retrieval reordering reduce but don't eliminate the effect on independent benchmarks.
