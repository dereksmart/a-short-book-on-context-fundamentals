# Chapter 8 — Size Discipline

Every office that has been in the same building for a few years eventually acquires a laminated sign on the kitchen wall. It begins with a single polite request — *please wash your own dishes.* Over the years, the additions accumulate in different handwritings: *this means ALL dishes, not just your plate.* *And please use the soap on the LEFT.* A note about the dishwasher's top rack, added after an incident no one quite remembers. A printed memo from an earlier manager, referencing a policy superseded twice since.

Nobody reads any of it. When a new person joins the team, they read it once, remember approximately none of it, and thereafter treat the sign as part of the wall.

This is what happens to a rules file if no one is minding it.

## The 200-line rule

The official Claude Code documentation makes the recommendation in about as direct a form as you tend to get from a product doc: **target under 200 lines per CLAUDE.md file.** Longer files, the documentation notes, "consume more context and reduce adherence." If your instructions are growing larger, split them into imports or a `.claude/rules/` directory. ([Claude Code: Memory](https://code.claude.com/docs/en/memory))

The 200-line figure is specific to Claude Code. The *principle* is universal — every tool's rules file will suffer the same dilution past a certain size, though the exact threshold varies. I have seen 150 lines cited for Cursor, for similar reasons. A rough-and-ready estimate, across tools: if your rules file is longer than you would choose to read in one sitting, it is longer than the model will treat with care.

## The attention math

There is a piece of back-of-envelope reasoning behind the 200-line number that is worth walking through, because it makes the intuition sticky.

A model, reading a rules file, treats it as a block of content competing for attention with everything else in the window. The specific rules within the file compete with each other. If you have five rules, each gets roughly a fifth of the attention the file receives. If you have fifty rules, each gets a fiftieth. If you have two hundred, each gets about half a percent.

Half a percent is not *nothing*. The model can still find a specific rule when it needs to. But "being findable when needed" and "being treated as a serious constraint on every turn" are different things, and the difference widens as the file grows. At some point, somewhere between fifty and two hundred rules, the model's treatment of your rules file shifts, quietly, from *these are the rules* to *these are suggestions*. Community reports are consistent on this: past about two hundred lines, Claude starts treating entries as preferences rather than requirements. Other tools show the same pattern at different thresholds.

You can, of course, compensate by repeating the important ones, or by moving them to the top, or by using stronger language. These all work, up to a point. The more reliable move is to keep the file small in the first place.

## The two-strikes rule

The best discipline I know for keeping a rules file small, and the one most professional practitioners seem to converge on, is what Claude Code's documentation calls the **two-strikes rule**:

> "Add to it when: Claude makes the same mistake a second time."

([Claude Code: Memory](https://code.claude.com/docs/en/memory))

That is: do not add a rule the first time the model gets something wrong. Correct it, note the correction, and move on. If the same mistake recurs a second time, *then* the rule gets added.

This feels counterintuitive if you are the kind of person who, on seeing a mistake, reaches for a solution. The impulse is to prevent the error from happening ever again, starting now. But most first-time errors are one-offs: a specific confusion, a specific turn, not a pattern. Adding a rule for every first-time error is how rules files get to six hundred lines. Second-time errors are different. A repeated mistake is a pattern. A pattern is what rules are for.

## Stale rules are worse than no rules

Now for the hardest of the three disciplines, which is pruning.

A rules file accumulates over time. Rules are added faithfully, in response to real mistakes. Projects change. Conventions shift. Tools improve. The flaky test gets fixed. The file structure is reorganized. The deprecated API becomes the current API, which later becomes the deprecated API again, because that is how these things go. Each change leaves a rule behind that no longer applies.

This is more serious than it sounds. A rule that doesn't apply is not merely dead weight. It is actively misleading. The model reads it, believes it, and acts on it. If your rules file says *do not use the v2 API* and the v2 API has been the only API for six months, the model will, faithfully and to your detriment, avoid the only thing that works.

The line worth carrying away: **a stale rule is worse than no rule.** No rule leaves empty space, which the model fills with its general knowledge or your current prompt. A stale rule fills the space with a confident lie. Guess which one the model follows more reliably.

The discipline is quarterly review. Every few months, sit down with your rules file and ask, of each line: *is this still true? Did we actually fix the underlying issue? Does this reflect how we work today?* Anything that fails the test comes out.

I know few teams who do this rigorously. I know slightly more who do it occasionally, in the form of a cleanup sprint every six months. And I have seen, more than once, a team's rules file drop from three hundred lines to ninety in a single afternoon, with their AI sessions immediately getting better as a result.

## The shape of a good file

Putting the three disciplines together: a well-maintained rules file is short (fifty to a hundred and fifty lines), grouped into sections that make sense for this team, and — above all — *maintained*. Additions are earned. Deletions happen. A rules file that has not been edited in a year is not a well-preserved document; it is one that has stopped describing reality.

A team's rules file is, in a real sense, a mirror. A team with good habits has a short, accurate, recently-edited one. A team with scattered habits has a long, stale one full of motivational language that nobody follows. The file tells you, at a glance, what kind of working relationship this team has with its AI.

## For Monday

Three moves, in order.

First, open your rules file and count the lines. If higher than two hundred, you have work to do. Higher than four hundred, a weekend's worth.

Second, for each rule, ask: *is this still true today?* If no, it comes out.

Third, for each correction you have given your AI this month, ask: *was this the second time?* If so, the rule has earned its place. If not, make a note and wait.

The reward is not visible in a dashboard. It is visible in your next session, which will be sharper, faster, and more often right the first time.
