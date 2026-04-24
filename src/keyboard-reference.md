# Keyboard Reference

A condensed reference for the major AI-developer tools covered in this book. All shortcuts verified against official docs where possible; where a tool's docs are thin, the listed shortcuts are the ones reported reliably by users and not contradicted by the vendor.

On macOS, `Cmd` is the canonical name for what the docs often call `Meta` or the command key. On Linux and Windows, the same binding usually maps to the `Super` or `Win` key; check your tool's keybindings settings if it doesn't respond as expected.

---

## Claude Code

All verified against [code.claude.com/docs/en/keybindings](https://code.claude.com/docs/en/keybindings).

### Core editing

| Shortcut | Action |
|---|---|
| `Ctrl+G` | Open system text editor for the current prompt (`chat:externalEditor`) |
| `Ctrl+J` | Insert a newline without sending (`chat:newline`) |
| `Ctrl+S` | Stash the current prompt temporarily (`chat:stash`) |
| `Shift+Tab` | Cycle through permission modes: Normal → Auto-Accept → Plan (`chat:cycleMode`) |
| `Meta+T` / `Cmd+T` | Toggle extended thinking (`chat:thinkingToggle`) |
| `Meta+O` / `Cmd+O` | Toggle fast mode (`chat:fastMode`) |

### Interface

| Shortcut | Action |
|---|---|
| `Ctrl+O` | Toggle verbose transcript view (`app:toggleTranscript`) |
| `Ctrl+T` | Toggle task list visibility (`app:toggleTodos`) |
| `Ctrl+B` | Background a running bash command (`task:background`) |

### Agent teams (v2.1.32+, in-process mode)

| Shortcut | Action |
|---|---|
| `Shift+Down` | Cycle through teammates |

### Notes

- All keybindings are customizable via `~/.claude/keybindings.json`. Run `/keybindings` to create or open the file.
- Changes are auto-detected without restarting the CLI.
- The `/context` and `/memory` slash commands show what's currently loaded — invaluable for debugging.

---

## Cursor

Cursor's keybindings inherit most defaults from VS Code. The shortcuts below are the Cursor-specific ones most relevant to AI workflow.

| Shortcut | Action |
|---|---|
| `Cmd+K` / `Ctrl+K` | Inline edit / chat with the editor |
| `Cmd+L` / `Ctrl+L` | Open chat panel |
| `Cmd+I` / `Ctrl+I` | Open Composer (multi-file agent edits) |
| `Tab` | Accept inline completion suggestion |
| `Esc` | Dismiss inline completion |
| `Cmd+Enter` / `Ctrl+Enter` | Accept suggestion and continue |
| `@` (in chat) | Open the context picker (files, folders, docs, git refs, web) |

---

## VS Code + GitHub Copilot

| Shortcut | Action |
|---|---|
| `Tab` | Accept inline completion |
| `Alt+]` / `Option+]` | Next suggestion |
| `Alt+[` / `Option+[` | Previous suggestion |
| `Ctrl+Enter` | Open Copilot suggestions panel |
| `Cmd+I` / `Ctrl+I` | Open inline chat |
| `Cmd+Alt+I` / `Ctrl+Alt+I` | Open Copilot Chat panel |
| `/` (in Copilot Chat) | Invoke slash commands (`/explain`, `/fix`, `/tests`, etc.) |
| `#` (in Copilot Chat) | Reference files, symbols, or Spaces as context |

Copilot's agent mode and Coding Agent are primarily interface-driven; no canonical keyboard shortcuts as of this writing.

---

## Gemini CLI

The Gemini CLI is a terminal-resident tool; most of its interface is slash commands rather than keyboard shortcuts.

| Command | Action |
|---|---|
| `/memory show` | Print the assembled GEMINI.md context (genuinely useful for debugging) |
| `/help` | List available commands |

---

## Aider

| Command | Action |
|---|---|
| `/add <file>` | Add a file to the editable set |
| `/read <file>` | Add a file as read-only (cache-eligible) reference |
| `/drop <file>` | Remove a file from the working set |
| `/clear` | Clear conversation history |
| `/undo` | Undo the last edit |
| `/diff` | Show diffs of uncommitted changes |
| `/commit` | Commit uncommitted changes |
| `/ls` | List files in the chat |
| `/tokens` | Show current token usage |

---

## ChatGPT (claude.ai and chatgpt.com, web interface)

These tools are primarily mouse-driven. The shortcuts that do exist:

| Shortcut | Action |
|---|---|
| `Cmd+Shift+O` / `Ctrl+Shift+O` | New chat |
| `Cmd+Shift+S` / `Ctrl+Shift+S` | Toggle sidebar |
| `Cmd+K` / `Ctrl+K` | Search chat history |
| `Cmd+Shift+;` / `Ctrl+Shift+;` | Copy last code block |
| `Shift+Esc` | Focus the chat input |

Custom GPTs, Projects, and Gems are invoked by typing their name in the composer (preceded by `@` in ChatGPT); there is no dedicated shortcut for invocation.

---

## Claude (claude.ai)

| Shortcut | Action |
|---|---|
| `Cmd+K` / `Ctrl+K` | Search conversations |
| `Cmd+/` / `Ctrl+/` | Show keyboard shortcuts |
| `Cmd+Shift+O` / `Ctrl+Shift+O` | New conversation |
| `Cmd+Enter` / `Ctrl+Enter` | Submit message |
| `Shift+Enter` | New line without sending |

---

## A note on customization

Every tool in this reference supports some degree of keybinding customization. The serious users of any of these tools all, eventually, tune their keybindings to fit their hands and habits. This is worth doing. The default bindings are reasonable compromises; your bindings, customized, are the ones you'll actually use.

The rule of thumb: if you find yourself reaching for a specific menu item or command more than once a day, give it a keybinding. The cumulative saving over months is considerable, and the muscle-memory, once formed, transfers usefully across tools (especially if you standardize the keys themselves — `Cmd+K` for "the main command-y thing" tends to work everywhere).
