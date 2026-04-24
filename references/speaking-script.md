# Context Fundamentals — Practice Script

This is a rehearsal script, not a transcript. Use it to practice the flow, then let the exact words loosen once the beats feel natural.

**Format:** 60 min for the PED Immersive cohort (Day 1, 2:00 PM, ~50 people, skewed Design and Product).
**Target shape:** ~42 min speaking, ~12 min exercises, ~6 min room conversation and handoff.
**Slide count:** 34.

**Timing map:**

- Slides 1-12: why sessions drift + Exercise 1 (~17 min)
- Slides 13-23: Rules + Exercise 2 (~24 min)
- Slides 24-29: Command (~9 min)
- Slides 30-34: Knowledge + close (~10 min)

Conversation hooks are marked `[HOOK]`. Stage directions are in italics.

---

## Slide 1 — Title

*Walk on. Let the title sit for a beat. Don't read it. Don't introduce yourself yet.*

"Quick question before I start. By show of hands: how many of you, this week, had an AI tool go off the rails on something you were sure it could do?

Doesn't have to be dramatic. Just the moment where you went, 'wait, why did you do that?'"

*Wait for hands.*

"Okay. Most of the room. That's what this hour is about.

My job for the next sixty minutes is to give you a clean explanation for why that happens, and three concrete things you can change before demos this afternoon."

---

## Slide 2 — A Familiar Failure

"These three quotes are from your pre-survey. Verbatim. Different people, different roles, same underlying failure."

*Read each one slowly.*

"It drifts.

It repeats mistakes you've already corrected.

It doesn't know your world.

If any of those felt familiar a minute ago, you're in the right room. And I want to take one thing off the table right away: this is not proof that you're using the tools wrong, and it's not proof that the tools are useless.

It's a recognizable, fixable failure mode. There's a mechanism behind it, and there are a few moves that make it much less common."

---

## Slide 3 — What You'll Leave With

"Three promises for the hour.

One: you'll be able to explain why your sessions drift in a single sentence.

Two: you'll know the three layers every good AI session needs.

Three: you'll leave with a working habit you can reuse for the rest of this workshop, and honestly anywhere you work with LLMs after that.

Not a trick prompt. A habit: how you set the system up before asking it to work."

---

## Slide 4 — The One Idea

*Let the slide land before speaking.*

"Here's the whole talk in one line:

Drift is a context problem, not a model problem.

If that's true, the fix is not begging the model harder, switching tools every time something goes wrong, or writing a longer and longer prompt. The fix is changing what surrounds the task.

So first I'll defend the sentence. Then we'll turn it into a working framework."

---

## Slide 5 — Why Sessions Drift

"This first section is the mechanism.

We're going to look at what the model can see, what happens when that space fills up, and why good sessions suddenly go sideways.

Once this clicks, the rest of the framework becomes much more obvious. This is the load-bearing part."

---

## Slide 6 — Brilliant New Hire

"The mental model I want you to hold is this:

An LLM is a brilliant new hire who joined five seconds ago.

Capable, fast, eager, broadly knowledgeable, but brand new to your world. It doesn't know what your team decided last quarter. It doesn't know which design patterns are sacred. It doesn't know the thing everyone avoids because the last attempt broke something important.

So the question is not only, 'is this model smart enough?'

The better question is: 'what would I tell a brilliant new hire on day one so they stop making avoidable mistakes?'

That question is going to come back in every layer."

---

## Slide 7 — Without Context

"Without context, the model defaults to the internet average.

That means a generic PRD that doesn't know your customers. A generic design critique that ignores your system. A generic implementation that follows generic conventions instead of yours.

And the dangerous part is that generic output often looks polished. It can pass a first read. It just doesn't fit your actual world."

---

## Slide 8 — One Window

"Here's the mechanism. Everything the model sees has to fit in one window.

Rules. Files. Tool results. Conversation history. Your current prompt. All of it lives in a single buffer.

Two things matter.

First: if it's not in the window, it doesn't exist. There's no hidden place where your team's context is magically available.

Second: every turn, the model is effectively re-reading this whole window from scratch. So everything you load competes with everything else for attention.

That sounds abstract until you look at what actually fills the window."

---

## Slide 9 — Everything Competes

"This is the slide I want you to remember.

The advertised window is like a very large library with one small reading lamp. The shelves are there. The question is what is actually lit well enough to use.

Start with your prompt. What you type might be five hundred tokens. It barely registers.

Now compare that to tool results. One Figma MCP response can be thousands of tokens. A transcript can be ten thousand. A few docs can be twenty thousand before you've said anything new.

[[slnc 400]]

So when a session suddenly forgets something it had been tracking, that's often not random. That's pressure. The model can hold a lot more than it can attend to evenly. The important detail got pushed toward the edges or compressed away.

The punchline is the line at the bottom: can hold is not the same as can use, and the right fifty lines outperform five thousand lines of everything."

---

## Slide 10 — History Gets Compressed

"This is where drift becomes visible.

Think screenshot of a screenshot. Each pass preserves the gist and loses precision.

Start on the left. The original constraint is crisp: use existing components only.

Then the window fills and history gets summarized the first time.

Look at the first summary. What survived? The topic. Component guidance discussed.

What disappeared? The specific constraint that mattered.

Now the session keeps going. More files, more tool results, more back-and-forth. The window fills again, and the summary gets summarized.

Look at the second summary. At this point, it may remember that the user wanted UI polish. But it may no longer know how you started, what you were protecting, or why the constraint existed.

Now move right. The user asks for polish, and the model confidently makes the exact thing you were trying to avoid.

That's the whole failure mode in one visual: specific constraints become a vague summary, then an even vaguer summary, and the model confidently optimizes the wrong thing.

Drift isn't the model being dumb. Drift is the window being lossy."

---

## Slide 11 — Fighting Context Rot

"There are five moves that help. I'm going to name them now, and we'll come back to most of them through the framework.

Rules survive. Anything that must persist belongs in a rules file, because rules are re-injected every turn.

Start fresh. If a long session is going sideways, a new window is often cheaper than fighting an overloaded one.

Restate anchors. When a detail matters, say it again close to the ask. Repetition at the tail is not inelegance. It is arithmetic. Don't assume the summary preserved it.

Compact with focus. If you compact, tell the model what to keep: 'summarize, but preserve the pricing constraints.'

And leave breadcrumbs. Before a break, reset, or compaction, write a short scratchpad: what's done, what's next, open questions, key files. That's session state. It belongs in notes, not in rules.

For now, just know there are fixes. Now let's make the problem visible in your own setup."

---

## Slide 12 — Exercise 1

"Two to three minutes.

Open Claude Code and run `/context`. Look at what's loaded. How much of your window is used? What's in there?

If you're not in Claude Code, use whatever AI tool you have open. Look at attached files, conversation length, and anything else the model is carrying.

You're not fixing anything yet. Just notice whether the window feels empty, healthy, or crowded. Go."

*Wait 2-3 minutes. Walk the room. Look for surprise.*

[HOOK — 60 seconds] "Two or three quick callouts. What did `/context` show you? Just one observation."

*Take 2-3 callouts. Don't solve yet.*

"Good. That's the Box. You've seen yours. The next part is about what belongs in it."

---

## Slide 13 — Three Things Every Session Needs

"Now that we've seen the failure mode, here's the framework.

Every strong AI session has three layers. Skip any one and quality drops fast.

The useful part is that you can name all three in three words."

---

## Slide 14 — Framework

"Rules. Command. Knowledge.

That's the whole framework.

Rules are the durable invariants: the things that should be true every time.

Command is the job you're asking for right now.

Knowledge is what the agent learns while working: files, rules, tool results, and patterns it discovers.

Keep the new-hire metaphor running. If I gave a new hire no handbook, no clear assignment, or no way to learn the local context, I would expect them to struggle. Same here.

We're going to spend the most time on Rules, because that's the biggest gap for this room. Then we'll move through Command and Knowledge more quickly."

---

## Slide 15 — Rules

"Layer One: Rules.

This gets the most time because it's the biggest unlock. Rules are how you stop solving the same problem in every conversation."

---

## Slide 16 — Rules: The Invariants

"Rules are durable invariants: things that should stay true across tasks.

They are not the task itself. They're the standards and guardrails around the task.

The test is simple: would I tell this to a brilliant new hire on day one because I know they'll make expensive mistakes without it?

Look at the three examples.

'Never call this ready without user impact and rollback path.' That's a product and risk invariant.

'Use published tokens before inventing new UI.' That's a design-system invariant.

'Run targeted tests before commit.' That's an engineering invariant.

Different artifacts, same structure. Each one tells the agent something specific it could not reliably infer on its own."

---

## Slide 17 — Every Tool Has a Rules File

"Quick aside: rules files are not a Claude Code thing.

Claude Code reads `CLAUDE.md`. Cursor and Codex read `AGENTS.md`. Copilot reads `.github/copilot-instructions.md`. Gemini reads `GEMINI.md`.

Different filenames. Same idea: persistent guidance injected into the session.

Pick the tool you actually live in and start there."

---

## Slide 18 — Write the Rules Once

"The scalable move is to write the rules once.

At Automattic, the convention is to keep `AGENTS.md` as the source of truth and have the other tool files reference it.

So `CLAUDE.md` can be one line: `@AGENTS.md`.

One file. Every tool reads it. Update once, everyone benefits.

The Field Guide link at the bottom has the full Automattic pattern."

---

## Slide 19 — What Goes In

"So what belongs in a rules file?

Commands and workflows. Architecture. Conventions. Non-obvious patterns. Common pitfalls.

Notice what's not on the list: motivational posters. 'Write clean code.' 'Care about quality.' 'Be a good collaborator.' The model already knows public principles.

Rules are for the things it cannot infer.

For engineering, that might be build commands, repo layout, test expectations, and traps.

For product, it might be the spec template, the prioritization framework, the definition of done, and the kinds of scope creep your team keeps fighting.

For design, it might be critique checklists, handoff templates, token usage, file organization, and recurring brand violations.

The context each role provides is different. The principle is the same: include what's hard for the agent to figure out on its own."

---

## Slide 20 — Key Principles

"Four short principles.

Human produced: tell it things the public internet doesn't already know. Operational invariants, not public values.

Strong phrasing: MUST, NEVER, CRITICAL. The model reads rules literally, so write them that way.

Update regularly: every repeated correction is a candidate rule.

Don't split too early: one root file is reliable up to around two hundred lines. Split only when the file actually gets hard to use."

---

## Slide 21 — Red Flags

"When I look at a rules file, these are the smells.

Think of the kitchen wall sign in an office that has been there too long. It started with one useful instruction: wash your dishes. Then came the additions. Use this soap. Not that sponge. The dishwasher note from a manager who left two years ago. Eventually nobody reads it; worse, the wrong parts are still there.

Commands that would fail. References to deleted files. Template text nobody customized. Generic advice. Stale TODOs. Duplicate guidance across files.

The line at the bottom is the mindset: a stale rule is worse than no rule.

No rule leaves empty space. A stale rule actively misleads the agent with high confidence."

[HOOK — 30 seconds] "Quick check. Who has a rules file right now that you're a little worried might be stale?"

*Wait. Count loosely. Don't moderate.*

"Good. Exercise Two is for you."

---

## Slide 22 — Three Scopes of Memory

"One quick orientation before the exercise.

There are three places rules and memory live.

Project memory: `AGENTS.md`. Team rules, in source control.

User memory: your personal `~/.claude/CLAUDE.md`. Your preferences, loaded across projects.

Auto memory: Claude's notes from your corrections.

Run `/memory` if you want. Ten seconds. Just see what's loaded."

---

## Slide 23 — Exercise 2

"Three to four minutes. This is the big one.

If you have a Claude Code repo open, install the audit plugin and ask it to audit your `CLAUDE.md` files.

If you don't have a rules file yet but you do have a codebase, run `/init`.

If you don't have a codebase open, start a plain `AGENTS.md` and write three invariants from your team's working norms. Real ones. Things you'd tell a new hire on day one. Use words like MUST, NEVER, ALWAYS.

Pick the path that matches your situation. Three to four minutes. Go."

*Walk the room. Look especially for Product and Design examples.*

[HOOK — 90 seconds] "One designer, one PM, one engineer: what did you write, or what did the audit tell you?"

*Take three quick callouts from different disciplines.*

"Notice how different the artifacts are. The structure is the same. That's the layer."

---

## Slide 24 — Command

"Layer Two: Command.

This is lighter today because tomorrow goes deep on Skills. For now, I want the instinct:

Shape the job. Anchor it to something real. Let the model clarify what's fuzzy. If the command repeats, save it."

---

## Slide 25 — Command: The Job Right Now

"Command is the job you're asking for right now.

Not forever. Not your whole team culture. This task, in this session.

The anatomy is simple.

First: the job. Compare the current PRD, latest mockup, and implementation notes. Quick test: underline the verb. If you can't find one, it is not a command yet.

Second: what to anchor to. Point at the actual artifacts.

Third: what to return. Mismatches. Missing criteria. Open questions.

That's the pattern: what to do, what to use, and what to return."

---

## Slide 26 — Anchor the Command to Something Real

"This is the leverage point.

On the left: 'Check whether these are aligned.' That's a wish. The model has to guess what 'these' means, what 'aligned' means, and what kind of answer would help.

On the right: compare these three artifacts and return these three types of findings. Same intent, much clearer command.

The less the model has to guess, the better the result fits.

And this ties back to the earlier punchline: the right fifty lines outperform five thousand lines of everything. Anchoring is how you make the right fifty lines win."

---

## Slide 27 — Let the AI Ask You

"You don't always have to front-load the perfect command.

If the job is still fuzzy, let the agent ask before it starts.

In this example, it asks whether the tiers replace the current offer, who signs off, and where the latest research lives.

That's the model helping build the command with you.

Most AI work is not, 'I know exactly what I want, type it for me.' Most of it is, 'help me think this through, but don't go generic.'

Questions are how you get there."

---

## Slide 28 — Save Repeated Commands

"Once a command works and you keep using it, save it.

A skill is a saved command with a name. Frontmatter names it. The body is the instruction.

It can grow scripts, file dependencies, and tool restrictions later. But the seed is simple: a command you got tired of retyping.

Tomorrow goes deep on this. Today I just want you to recognize the moment: the third time you type the same instruction, give it a name."

---

## Slide 29 — Iterate and Teach

"Last move in this layer: normalize iteration.

The first response isn't sacred. Roll back, re-anchor, try again.

'That's close, but not quite' is a valid prompt. Corrections are part of the conversation.

And here's the connection back to Rules: every repeated mistake is a candidate rule.

If you've corrected it twice, stop solving it in every conversation. Write it down once."

---

## Slide 30 — Knowledge

"Layer Three: Knowledge.

This is not what you ask for. That was Command.

Knowledge is what the agent learns while it works: files it opens, rules it discovers, tool results it pulls in, and patterns it infers.

Your job is to shape that discovery path."

---

## Slide 31 — Knowledge: Directed Reconnaissance

"Agents do not only use what you attach up front. They build working context as they move.

Walk the rows.

Files it opens: specs, modules, tests, mocks, transcripts.

Rules it discovers: nested AGENTS.md, READMEs, package notes, local conventions.

Tool results it pulls: Figma frames, Linear issues, Slack or P2 threads, browser state.

Patterns it infers: implementation shape, design-system usage, prior decisions.

That gathered context can help. But it also competes for the window.

So the active move is not 'dump more context.' The active move is directed reconnaissance.

Don't hand a smart new hire the entire filing cabinet and call that support. Shape where the agent looks."

---

## Slide 32 — Directed Reconnaissance

"Command is what you ask. Knowledge is what the agent learns while doing the work.

Your active move is to shape the discovery path: aim, bound, encode.

Aim it. Tell it where to start and what to inspect. Start in the checkout package. Read the PRD, the current Figma frame, nearby AGENTS.md, and relevant tests.

Bound it. Tell it what to ignore and when to stop. Ignore archived mocks. Don't scan the whole repo. Use current research only. Stop before editing.

Encode it. If that discovery path is always true, put it in AGENTS.md. If it's a named recurring task, make it a skill.

Don't dump context. Design the path it takes through the work.

Another way to say this is: pointers, not payloads. A map to the right three documents usually beats the full archive dumped into the window.

That's the image: compass, not encyclopedia. The point is not to load everything. The point is to make the next few moves obvious."

---

## Slide 33 — The Shift

*Let the quote sit. Then read it.*

"Your job shifted from making the artifact alone to assembling the right context and declaring clear intent.

That's the mindset shift under the whole framework.

Drift is a context problem because the job itself is now context assembly.

That doesn't reduce your judgment. It changes where your judgment shows up: less in typing every word yourself, more in setting up the system to do useful work with you."

---

## Slide 34 — Your Afternoon

*This stays up during Q&A. These are the last spoken words.*

"This is your contribution slide.

Pick one and do it before the four-thirty demos.

If your AI keeps violating something important, write the rule down.

If you keep typing the same workflow, save it as a skill.

If the agent needs to learn its way through the work, shape the discovery path.

That's enough for one afternoon.

Drift is a context problem. You now have three verbs for fixing it. Choose the compass, not the encyclopedia."

*Pause. Don't say "questions." Leave the slide up and let the room come to you.*
