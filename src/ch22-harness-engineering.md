# Chapter 22 — Harness Engineering

The field has had, in rough approximation, three recognizable eras in the last five years.

The first was **prompt engineering** — roughly 2022 through 2024 — when the question was *how do I write the single instruction that produces a good result?* Essays were written. Guides were published. Entire job titles were minted around the art of the well-wrought prompt.

The second was **context engineering** — which dominated 2025 and is the subject of most of this book — when the question shifted from *the prompt* to *the environment*. Not just what you say, but what the model has access to when you say it. Rules files, retrieval patterns, memory systems, MCP.

The third, emerging through 2026, goes by the provisional name **harness engineering**, and it asks a different kind of question again. ([one of several attempts to name it](https://www.epsilla.com/blogs/harness-engineering-evolution-prompt-context-autonomous-agents))

*What systems surround the agent? What do you block? What do you measure? What do you repair?*

The shift is subtle on the surface and significant underneath.

## What a harness is, and why it matters

A harness is the set of scaffolding and controls that surround a model as it does its work. It is the difference between letting a model run unbounded — *here is a task, here are your tools, go* — and running it inside a structured environment where certain things are constrained, certain outputs are checked, certain failures are caught and recovered from.

The word was chosen, I think, to evoke the climbing sense: something that holds you in place while you do work that would otherwise be dangerous. The harness doesn't stop you from climbing. It stops you from falling past the point at which falling becomes irrecoverable.

This matters because, as models get more capable and agents more autonomous, the failure modes change. Not every agent failure in 2026 is *the model said something wrong and the user noticed.* Some failures are *the agent ran for forty minutes, made a hundred tool calls, and ended up in a state the user did not expect and cannot easily unwind.* Some are *the agent produced plausible output that passed a casual review and turned out to be wrong in ways that did damage.* The more autonomy you grant, the more important it becomes to build structure around what the agent can and cannot do, and how you would know if something went wrong.

Harness engineering is the discipline of building that structure.

## Three families of harness

In practice, harnesses consist of three kinds of machinery, roughly in the order most teams adopt them.

**Blocks** are the things the agent cannot do. Permission systems that refuse certain tool calls. Validation that rejects certain outputs. Guardrails that prevent certain categories of action. *The agent may not delete files without explicit confirmation. The agent may not make external network calls outside this allowlist. The agent may not produce output containing PII in plaintext.* Blocks are the safety lines: they define the space within which the agent can freely operate.

**Measurements** are the things you observe about the agent's behavior without necessarily acting on them. Traces of tool calls, token usage, response quality scores, latency, user-satisfaction signals, drift over time. Measurements tell you what is happening; they do not, by themselves, change what happens. But you cannot fix what you cannot see, and most agents in production in 2026 are running with shockingly little observability. Better measurement is, for most teams, the cheapest improvement available.

**Repairs** are what the harness does when something goes wrong. Retry logic for failed tool calls. Fallback strategies when a model is unavailable. Checkpointing that lets you resume from a known-good state. Rollback for agent actions with side effects. Human-in-the-loop handoffs when confidence drops below a threshold. Repairs are how you make agent failures recoverable rather than catastrophic.

The three tend to be adopted in that order, because each depends on the previous one. You cannot measure without first blocking your way out of pure chaos. You cannot repair without first measuring what went wrong.

## Evaluation and monitoring, briefly

Two specific pieces of the harness deserve their own mention.

**Evaluation** — *evals*, in the house style of the field — is the practice of running agents against deliberately-constructed test cases and measuring how they do. The mature teams in 2026 run two kinds. **Unit evals** target specific behaviors with deterministic pass/fail criteria: *does it refuse this unsafe request? does it produce the right output format?* **Holistic evals** measure broader properties — response quality, helpfulness, style adherence — usually with an LLM-as-judge scoring against a rubric. Neither is sufficient alone; the standard practice is to run both, at different frequencies, with at least a few evals that reflect the exact use cases that matter most to your users.

**Monitoring** is the same discipline, but continuous, in production. Tracing captures the sequence of model calls and tool uses for each run. Logging records what happened at each step. Metrics aggregate across runs. Alerting surfaces anomalies. The difference from traditional software observability is that the traces are more valuable: an agent run is a dense and interesting artifact — dozens of tool calls, many model responses, a visible reasoning chain — and when things go wrong the trace is usually sufficient to explain why, provided the trace was captured well. Several vendors compete in the space — LangSmith, Helicone, Arize, Braintrust — offering varying combinations of tracing, evals, and monitoring. The general recommendation is: even a thin layer of tracing beats none. Even bad tracing is better than no tracing.

## Where this connects to the rest of the book

This chapter feels, at first, like it has left the context-fundamentals thread behind. I want to argue that it hasn't.

Everything we have covered — rules files, shaped commands, directed reconnaissance, MCP, curated context — is, in a sense, a *harness* applied at the prompt level. A well-maintained `AGENTS.md` is a block: it prevents classes of mistakes by stating the invariants. Shaped commands are blocks and measurements combined: they constrain the ask, and their structure makes it easier to tell whether the output was right. Just-in-time retrieval is a repair: it avoids the failure mode of dumping too much context into the window.

The distinction between context engineering and harness engineering is, in practice, blurry. The tools overlap. The techniques graduate from one into the other. A prompt becomes a skill. A skill accumulates blocks and retries. The whole thing eventually becomes a production service with evals and monitoring around it. There is no clean boundary.

What is useful about the harness framing is that it foregrounds *what you measure and what you repair*, rather than just what you instruct. *How would I know if this agent started doing something wrong? What would I do about it?* These are the questions that separate prototypes from systems.

## For Monday

Two habits, for those running anything beyond personal use.

First, **add a trace to whatever agent you are building**. Even the simplest logging — capturing the prompt, the response, the tools called — is dramatically better than nothing. You will need it the first time something goes wrong and you are asked to explain what happened.

Second, **write three evals**, even if they feel like overkill. Pick three behaviors your agent should reliably exhibit. Capture the inputs and the expected outputs. Run them every time you change something. This is the smallest-useful evaluation practice, and the hardest to skip once adopted. Most teams I know who started with three evals are now running three hundred.
