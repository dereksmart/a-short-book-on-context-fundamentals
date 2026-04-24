# Chapter 11 — Letting the Model Ask

There is a myth, surprisingly persistent, that the best prompts are the ones written by prompt engineers — long, precisely worded, comma-controlled incantations, polished to a high finish before they are delivered to the model.

This is wrong. Or rather, it is often wrong. A great deal of real AI work is not produced by the careful execution of a perfect instruction. It is produced by a conversation that begins, as most useful conversations do, with the model asking a few questions.

You are, generally speaking, allowed to let the model ask.

## The unfinished command

Most of the prompts people send to AI tools are, strictly speaking, under-specified. This is not a criticism. Most requests people make of each other in real working life are under-specified. The PM who says to a designer *can you take another pass on the sign-up flow* is not handing over a completed specification; they are starting a conversation. The designer sensibly replies with clarifying questions: *which pass? The whole flow or just the form? By when?*

An AI can do the same thing, given permission. And you will find, once you start giving it permission, that the quality of the work improves in a way that is, initially, startling.

## When to declare, when to ask

The previous chapter was about how to write a complete command. This chapter is about what to do when you cannot — or would rather not — write one up front.

You should declare when you know exactly what you want. The command is clear in your head. You know the job, the anchors, and the return. Writing it out takes a minute. The model does the work. You get the result.

You should ask when the job is fuzzy. You have a sense of what you want but not the specifics. There are decisions you haven't made. Constraints you haven't thought of. Background you haven't supplied. In these cases, a front-loaded command is guesswork dressed up as precision. You're going to be wrong about something, and the model, faithfully executing your wrong command, will produce something that misses.

Most work, if you are being honest, sits in the second camp.

## How to invite questions

The mechanics are, refreshingly, simple. You ask.

*Before you start, what would help you do this well?*

*Ask me up to three clarifying questions before you begin.*

*I'm not sure about some of the details — what would you need to know?*

These prompts work across every frontier tool. Claude tends to take them particularly earnestly, asking thoughtful questions that surface real ambiguities. ChatGPT will ask, sometimes with a tendency to ask more than you wanted; capping the number ("three questions, then proceed") is useful. Gemini will ask if prompted but charges ahead more readily; explicit invitations help.

A useful variant, especially for longer work, is to have the model propose a plan before it executes. *Draft a short plan first — don't start yet — and let me confirm or correct before you begin.* This catches the expensive errors early. It costs a minute. It saves, on a medium-sized task, somewhere between a few minutes and a whole afternoon.

## What good questions look like

Not every question from a model is a useful one. The ones that add value tend to be of three kinds.

**Scope questions.** *Am I editing only the component itself, or also the tests?* Questions about where the work begins and ends. They often reveal places where you had a fuzzy sense of scope you hadn't articulated.

**Constraint questions.** *What version of the SDK am I targeting? Is this replacing the current implementation or running alongside it?* Hidden requirements that would otherwise collide with the first draft.

**Context questions.** *Who is the reader of this document? Who signs off on pricing?* Questions about the world outside the immediate task — often the most useful clarifications, because they are the ones you are least likely to have included.

When a model asks you a bad question — one whose answer doesn't change what it should do — that is feedback. The model has not understood the task well enough to know what matters. Either provide better framing, or reconsider whether you have the right command in mind.

## The Socratic inversion

There is a larger point buried here, worth saying plainly.

The common mental model of AI use is AI as oracle: you type a short clear request, and the AI produces a complete answer. Ask, and receive.

The more useful model, for the kind of work most people actually do, is AI as collaborator. You do not hand over a finished problem and receive a finished answer. You start with an underspecified problem, and you and the model make it specific together. You bring domain knowledge, judgment, and taste. The model brings speed, breadth, and the patience to iterate.

Letting the model ask is how you enable the collaboration mode. If you only ever declare — front-loading every prompt, accepting whatever comes back — you are using the oracle mode, and leaving most of the tool's value on the table.

## When not to ask

Two situations where inviting questions is the wrong move.

First, when the task is genuinely small and well-understood. *Format this list as JSON. Fix the typo in the README. Translate this paragraph into French.* Inviting questions here is friction.

Second, when the same fuzzy command is going to run many times on similar inputs — say, processing a batch of documents — figure out the right command once, write it precisely, and run it. Save the collaborative mode for one-off creative work, which is what it is best suited for anyway.

For everything else, which is most things, ask.

## For Monday

Two habits.

First, for your next non-trivial task, try opening with: *Here's the task in one sentence. Ask me up to three clarifying questions before you begin.* See how often the questions surface something you hadn't thought of. Most people find they're under-specifying their requests somewhere between half and three-quarters of the time.

Second, when a model's first response misses what you wanted, don't just correct it and try again. Pause and ask: *was the prompt complete, or was I hoping the model would infer something I hadn't said?* If the latter, the fix is not a longer prompt. The fix is starting over with *ask me what you need to know.*
