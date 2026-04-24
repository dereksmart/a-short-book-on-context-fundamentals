# Chapter 7 — The Rules-File Landscape

If you stand in the middle of a modern repository and look around, you may notice an unusual feature: the ground is littered with small markdown files that look vaguely like instructions.

There is `CLAUDE.md`. There is `AGENTS.md`. There may be `GEMINI.md`, or a `.cursor/rules/` directory, or `.github/copilot-instructions.md`, or a `.clinerules`, or several others. To the casual observer this looks like the usual software chaos — the aftermath of a format war that hasn't quite finished yet.

In fact, the situation is tidier than it looks. There are two layers at work. At the bottom, a **cross-vendor standard** that most of the major AI tools now read. On top, each tool's own format that adds capabilities the standard doesn't cover. Once you can see the two layers separately, the repository starts to look less like a battlefield and more like a stack.

This chapter is the map.

## The standard underneath: AGENTS.md

In late 2024 and early 2025, several of the major tool makers — Sourcegraph, OpenAI, Google, Cursor, and a handful of others — converged on a shared convention. They would read a file called `AGENTS.md` at the root of a repository, treat its contents as instructions, and otherwise leave the format flexible. No schema. No required frontmatter. Plain markdown, short or long, structured or prose.

The convention was formalized at [agents.md](https://agents.md/), and in late 2025 moved under the stewardship of the Linux Foundation's newly-formed Agentic AI Foundation. The list of tools that read the file is, by now, somewhere between long and comprehensive: **OpenAI Codex, Cursor, GitHub Copilot, Gemini CLI, Aider, Zed, Warp, Windsurf, Cline, Continue.dev,** and many others. ([agents.md](https://agents.md/), [agentsmd.io](https://agentsmd.io/)) The project's own count is more than sixty thousand repositories using one.

This is, for a field that routinely invents three incompatible standards before breakfast, an unusual outcome. It happened in part because markdown is the lowest-friction format — everyone reads it, everyone writes it, no parser to maintain — and in part because none of the adopters wanted to own the standard themselves. The Linux Foundation stewardship makes the neutrality explicit.

The practical consequence: if you are going to write one rules file, write it at `AGENTS.md`. It is the file most tools will find. It is the one that survives tool changes and team migrations. It is the durable layer.

## The layer on top

Above the standard, each tool adds its own format, which usually does one of three things: scopes rules to file paths, layers rules by priority, or integrates with tool-specific features. Five tools are worth taking in turn.

### Claude Code — CLAUDE.md with imports

Claude Code reads `CLAUDE.md`, with support for hierarchical loading: project-level, user-level, and enterprise-level files are all combined. The project-level file can include imports, which is the feature that makes the cross-vendor story work cleanly. Most Claude Code users I know keep their `CLAUDE.md` as a one-liner:

```
@AGENTS.md
```

And put all their actual rules in `AGENTS.md`, which every other tool also reads. One file is the source of truth. All tools see the same content. This pattern — the one-line import — is the simplest version of team-wide rules portability, and is strongly recommended unless you have a specific reason to keep Claude-specific content separate.

### Cursor — four types of rules

Cursor takes a more elaborate approach. Rules live in `.cursor/rules/*.mdc`, with YAML frontmatter declaring each rule's type. There are four, and the names do most of the explaining: **Always** rules get injected on every request, the classic behavior; **Auto Attached** rules activate only when the files you are working on match a glob pattern, so a Python-conventions rule loads when Python files are open and not otherwise; **Agent Requested** rules are consulted by name — the agent reads the rule's short description and decides whether to pull the body in — and **Manual** rules load only when you `@`-mention them explicitly in chat. ([Cursor rules docs](https://docs.cursor.com/context/rules))

The practical consequence is that Cursor users can keep a large library of rules without paying the attention cost of loading all of them every turn. A fifty-line rule about Rust memory safety doesn't land in your context when you are editing a CSS file. This is genuinely useful, and it is a feature the cross-vendor standard does not yet offer.

The trade-off is portability. Cursor `.mdc` files do not copy cleanly to Claude or Gemini. For teams on multiple tools, keep the core invariants in `AGENTS.md` for portability and use Cursor's type system for the tool-specific refinements.

### GitHub Copilot — path-scoped via frontmatter

Copilot reads two things: `.github/copilot-instructions.md` at the repository root, and `.github/instructions/*.instructions.md` for path-scoped rules. The path-scoped files use frontmatter with `applyTo` globs, much like Cursor's Auto Attached type. Copilot also, since August 2025, reads `AGENTS.md` from the repository root alongside its own files. ([GitHub Docs](https://docs.github.com/en/copilot/reference/custom-instructions-support))

### Gemini CLI — three-level hierarchy

Gemini CLI uses `GEMINI.md`, loaded in three levels: a global file at `~/.gemini/GEMINI.md`, any project files found by walking upward from the current directory to the git root, and any component-level files found by walking downward into subdirectories (respecting `.gitignore`). All files are concatenated, with more specific files overriding more general ones. ([Gemini CLI docs](https://geminicli.com/docs/cli/gemini-md/))

The `/memory show` command prints the fully-assembled context, which is a useful debugging feature the other tools could stand to copy.

### Aider — CONVENTIONS with a twist

Aider reads a `CONVENTIONS.md` file, loaded via `/read CONVENTIONS.md`. The twist is that `/read` is distinct from `/add` in Aider's model: `/read` marks a file as read-only and cache-eligible; `/add` makes it part of the editable working set. The conventions file lives as read-only reference. This is Aider's clean answer to the question of where invariants stop and working material begins. ([Aider docs](https://aider.chat/docs/usage/conventions.html))

### The rest, in brief

Windsurf reads `.windsurfrules`. Zed reads `.rules` and also picks up `CLAUDE.md` and `AGENTS.md` if present ([Zed docs](https://zed.dev/docs/ai/rules)). Cline reads `.clinerules` and `AGENTS.md`. Warp reads `AGENTS.md`. Continue.dev has a configurable context-provider system that includes a rules-file concept but doesn't impose a single filename. RooCode is a Cursor-family fork with per-mode rules and regex file matchers.

The common thread: every one of these tools reads some form of persistent markdown instructions. The details differ. The shape is the same.

## The practical recommendation

For the average team, the recommendation simplifies to two moves. **Write one set of rules in `AGENTS.md`.** If your primary tool is Claude Code, add a one-line `CLAUDE.md` that contains `@AGENTS.md`; the other major tools will read `AGENTS.md` directly or alongside their native format. Use your tool's path-scoping features on top of this, if they have them, for rules that genuinely benefit — but keep the cross-cutting invariants in `AGENTS.md` so the rest of your team can see them.

The effort is smaller than it looks. One source file. A few one-liners on top. Updated rarely, read constantly.

## For Monday

Two small moves.

First, check what your primary tool actually reads. Run its equivalent of *show me your loaded context* — `/memory`, `/context`, `/rules`, or whatever — and confirm.

Second, if you don't already have an `AGENTS.md`, create one, even if you are a Claude-only or Cursor-only shop today. Tools change. Teams expand. Rules that travel are rules that survive. The cross-vendor format costs you nothing.
