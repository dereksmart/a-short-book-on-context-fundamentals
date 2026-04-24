# Chapter 13 — Directed Reconnaissance

Imagine that you are the senior partner in a firm, and you have given a research task to a new associate. You could hand them the entire filing cabinet and tell them to find what's relevant. Or you could say: *start with the 2023 correspondence, then check the regulatory filings from that quarter, and ignore the trial transcripts — they're from a different matter.*

The first approach is thorough. It is also, in practice, a way of throwing away the associate's time and arriving at a worse answer. The associate will spend hours doing the thing you could have spared them, end up with a great pile of unsorted material, and — being new and eager — bring you something that is comprehensive in exactly the wrong direction.

The second approach is directed. It tells them where to start, what to ignore, and how to proceed. It acknowledges that you know things about the shape of the problem that they do not. It frees them to do the *research* part of the task instead of the *orientation* part, which was never a useful use of their time.

What you want, as a senior partner — and as someone working with an AI — is not thoroughness. It is **directed reconnaissance**.

## The third layer

Rules are what the model should know, always. Commands are what the model should do, now. Knowledge is what the model *learns* while working — the files it opens, the tool results it pulls, the patterns it infers from the code it reads.

This third layer gets the least deliberate attention and, depending on the task, does more work than the other two combined. A model asked to refactor a component does not work from the rules and the command alone. It reads the component. It reads the tests. It reads adjacent files. It pulls in utilities. It consults type definitions. By the time it proposes an edit, it has assembled, on its own, a working picture of the codebase. That picture is what the answer is actually built on.

You cannot, as the user, directly control what the model notices during this process. What you *can* do is shape the path — aim it toward the right material, bound it away from the wrong material, and, for the recurring kinds of tasks, encode the path into something reusable.

## Three moves

### Aim

Aiming is telling the model where to start. It is not the same thing as listing the anchors in your command (that, from Chapter 10, is the static context — the files you explicitly attach). Aiming is about the *exploration*. Where should the model look first? Which direction is productive?

*Start in the `checkout/` package.* *Begin by reading the PRD and the two most recent customer interviews.* *Look at the previous migration at `db/migrations/2026_04_*` before proposing the new one.*

A good aim gives the model a head start on the territory. Without it, the model's first move is usually a broad scan — reading everything that sounds relevant, including much that isn't. A narrow aim collapses that step. The model starts where the useful material already is.

The analogy, if you want one, is to the cartographer who hands you a map with "X marks the spot" drawn on it. The map is better than no map. The X is what makes the map useful.

### Bound

Bounding is the more important move, and the one most people skip.

A bound tells the model what *not* to do. What to ignore. When to stop. Where the edges of the task are.

*Ignore the archived mocks in `design-explorations/`.* *Don't scan the whole repository — only the modified files.* *Use the current research doc only; don't go back through old Slack threads.* *Stop at the planning stage; don't write any code yet.*

Every bound is, in a loose sense, a negative anchor: a specific thing the model should treat as off-limits. The effect of a good bound is almost always to improve quality, because it eliminates the wrong material from the working set. A model that reads fewer files reads them better, for all the Part I reasons. A model that knows when to stop produces cleaner output, because it doesn't drift past the task.

The bound most people forget is the *stopping* one. Agents, particularly the newer ones, will happily keep going — reading more, proposing more, touching more — long past the point where the task was done. *Propose the plan; don't execute it.* *Refactor the function; don't touch the tests.* *Answer the question; don't generate follow-ups.* These bounds are worth their weight in model-hours.

### Encode

The third move is the one that pays off over time.

If a particular pattern of aiming and bounding is always true — *on this project, AI tasks always start by reading `AGENTS.md`, `README.md`, and the closest relevant test* — then it belongs in the rules file. Write it there once. Every task inherits it.

If the pattern applies to a specific recurring task — *when auditing a PRD, the model should read the PRD, the team's checklist, and the linked spec docs, in that order, and ignore past versions of the same PRD* — then it belongs in a skill. The pattern becomes part of the reusable unit.

What you should *not* do, having discovered a good pattern, is keep retyping it into every new prompt. The rules file and the skill exist precisely so that patterns encode themselves out of your daily friction.

## Across roles

The three moves apply identically across disciplines; only the names of the files change.

**Engineering.** *Aim:* start in the affected package; read the tests adjacent to the change. *Bound:* don't touch the migration files; don't run the full test suite. *Encode:* put the test discipline in `AGENTS.md`.

**Product** aims at the latest research and the PRD template; bounds away from archived versions and internal Slack; encodes the sources list into a PRD-drafting skill.

**Design** aims at the current Figma frame and the token set; bounds away from archived explorations; encodes the design-system reference into a critique skill.

**Editorial** aims at the latest draft and review notes; bounds away from older drafts and resolved comments; encodes the style guide as a read-only reference.

The specifics differ. The mental model is identical. Aim, bound, encode.

## A note on tool-specific conveniences

Most modern AI tools offer features that amount to aiming devices — Cursor's `@`-mentions, Claude Code's file references, ChatGPT's file uploads, Aider's `/read` and `/add`. These reduce the friction of attaching specific material to a conversation. They are not, however, quite the same as directed reconnaissance. They attach *static context*; directed reconnaissance is about shaping the *process* the model takes through the work. The tool features help; they don't replace the instruction.

## For Monday

Two small exercises.

First, for your next non-trivial task, include one explicit *ignore* or *don't* instruction. Something the model should *not* do, read, or touch. Notice the effect on the output. You will often find the result is tighter than you expected, for reasons you wouldn't have predicted.

Second, when the model completes a task well, pause and ask yourself: *was that path of exploration worth encoding?* If yes — if you're likely to want the same path next week — take three minutes and promote it. To the rules file if it's general. To a skill if it's task-specific. The encoding compounds; the raw instruction does not.
