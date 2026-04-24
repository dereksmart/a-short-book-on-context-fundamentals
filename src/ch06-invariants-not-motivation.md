# Chapter 6 — Invariants, Not Motivation

If you were given the task of writing a manual for a newly-hired, brilliant, and slightly underinformed colleague, there are certain things you would put in it.

You would not put in: *be a good colleague.* You would not put in: *write clean code.* You would not put in: *care about the user.* These are things your new hire, being brilliant, already knows and quite agrees with. They are also, for the most part, what large language models already know and agree with, having read most of the internet's thoughts on the subject several times over.

What you *would* put in the manual is everything your new hire cannot reasonably figure out on their first day. You would put in the build command that only works if you run it from a specific directory. You would put in the fact that the deploy script, despite its name, does not actually deploy — it only queues a deploy for later, a thing the previous person in this role learned the hard way at seven o'clock on a Friday. You would put in the name of the test that, against all reason, is expected to be flaky and is safe to retry. And you would, if you were being thorough, put in the one file in the repository that must not be edited directly, no matter what the linter suggests.

These are **operational invariants**: things that are true in your world and nowhere else, and that someone stepping in fresh could not possibly deduce. They are what belongs in a rules file. Almost everything else is either public knowledge (which the model already has) or task-specific (which belongs in the current command, not the standing orders).

This chapter is about the difference.

## The new-hire test

There is a single question worth keeping in your pocket whenever you consider adding something to a rules file:

**Would I tell a brilliant new hire on day one because I know they'll make expensive mistakes without it?**

That is the test. It is not the only test, but it is the first one, and the one that catches the most noise.

Consider three candidates that pass.

A product manager writes: *never mark a feature as ready-to-ship without a user-impact note and a rollback path.* It passes — specific to this team's definition of "ready," reflects a real incident, the kind of thing a new PM would get wrong in week one.

A designer writes: *use published design tokens; do not invent new colors or spacing values without approval.* It passes — the model cannot know which tokens are published unless told, and left to itself will confidently produce a five-color palette that nobody asked for.

An engineer writes: *run targeted tests before commit — not the full suite, which is flaky and slow.* It passes. The tests being flaky is not a universal truth about testing; it is a fact about this repository.

And three that don't.

*Care deeply about code quality.* The model already cares, as much as a model can care, and will produce code proportional to what is asked of it. This line costs tokens and buys nothing.

*Be rigorous.* A disposition, not an invariant.

*Communicate clearly.* See above, twice.

These are what I will insist on calling **motivation**, as opposed to invariants. They are the kinds of things organizations love to put on posters. They are not what a model needs from you, and they actively dilute the rules that matter. A rules file full of motivation is a rules file in which the one line about the flaky test sits deep in the middle of a long document, and which — by the physics of the last few chapters — the model will skim past.

## Write it literally

A small thing about voice, regardless of tool or role.

Models read rules literally. If you write *try to avoid hardcoded paths*, the model hears *try, if convenient.* If you write *never hardcode paths*, the model hears *never*. If you write *MUST NOT hardcode paths*, the model hears, well, the same thing, but louder.

The practical recommendation, which most professional rules files converge on, is to use strong verbs for strong rules. *MUST*, *NEVER*, *ALWAYS*, *DO NOT*. Reserve these for genuine invariants, because they lose their force through overuse. If everything MUST be done, nothing MUST. Use softer phrasing — *prefer*, *generally*, *when possible* — for guidance that is really a preference.

## What belongs, by role

The invariants look different across disciplines, because the mistakes a new hire can make look different.

**Engineering.** Build and test commands that are non-obvious. The repo's top-level architecture in two or three sentences, so the model doesn't have to infer it from file names. Which tests are flaky. The file that must not be touched without review. The one or two conventions your team has chosen that contradict what the model would otherwise assume.

**Product** needs the spec template, the definition of "done," and the kinds of scope creep the team keeps fighting. **Design** needs published tokens, the handoff checklist, and the brand violations the team keeps catching late. **Writing and editorial** needs voice constraints, banned phrases, and the preferred term for the thing the brand has three terms for.

Each of these lists, you will notice, is short. That is deliberate. The best rules files I have seen tend to be startlingly brief — fifty or eighty lines, not eight hundred. We will come to the mathematics of why two chapters from now. For the moment, trust the instinct: if your rules file is long, most of it is probably motivation.

## A note on human origin

A good rule is **human-produced** — written from an actual experience of the model getting it wrong, not generated by an AI pretending to know what your team cares about, not copied from a template, not included because it seemed like the sort of thing a rules file ought to have.

The temptation to ask an AI to write your rules file for you is strong, and the output looks convincing. But the model does not know what your team does. Its best guess is a synthesis of the public internet's average opinion on what a rules file should contain — which is to say, motivation. The result passes a casual read and fails the new-hire test at almost every line.

The rules file that saves you from real mistakes is the one written by the person who has made those mistakes.

## For Monday

Two exercises.

First, open your rules file today. Read each line out loud and ask: *would I tell a brilliant new hire on day one, because without it they will make an expensive mistake?* Anything that cannot pass this test is a candidate for removal. Be brave. Most rules files lose forty percent of their lines and get better for it.

Second, think of two corrections you have given your AI this week — specific ones, not general ones. Write each as an invariant. Use MUST or NEVER. Add them to the file, at the top, where the model's attention is sharpest.
