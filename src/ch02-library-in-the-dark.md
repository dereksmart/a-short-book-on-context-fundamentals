# Chapter 2 — The Library in the Dark

There is a small ceremony that plays out every few months now in Silicon Valley, in which a company unveils a new large language model and announces, with the solemn confidence of a physicist reporting a new particle, that it can hold a million tokens in memory.

A million! You are invited to picture this. Since a token is roughly three-quarters of a word, a million tokens is something in the order of seven hundred and fifty thousand words. *War and Peace*, twice, with room left for a receipt. The entire Harry Potter series, most of it unopened. Every email you have ever written, probably several times over.

And this, the announcement implies, is the room your AI now has to think in.

Well. Not quite.

The trouble is that "can hold" and "can use" turn out to be two rather different things. A model with a million-token context window is, on inspection, a bit like a vast and beautifully appointed Victorian library which, you only notice later, has a single small reading lamp on the desk in the middle of it. You are welcome to shelve as much as you like. Whether anyone actually reads the books on the top shelf, at the far end of the north wing — that is another matter entirely.

This chapter is about the gap between what the brochure says and what the library actually lights up.

## Lost in the middle

In 2023, a group of researchers at Stanford, UC Berkeley, Samaya AI, and Meta's FAIR lab — Nelson Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, and Percy Liang, if you want the full cast — published a paper with a title that now sounds like prophecy: *Lost in the Middle: How Language Models Use Long Contexts*. ([TACL, 2023](https://aclanthology.org/2024.tacl-1.9/))

Their setup was disarmingly simple. They gave a variety of models a passage containing a question and its answer, surrounded by other passages that did not contain the answer. Then they moved the useful passage around. If the model could really *use* all of its context, the position of the answer shouldn't matter. A thousand tokens in, five thousand tokens in, fifty thousand — it's all the library, isn't it?

It was not all the library. Accuracy was highest when the answer sat at the beginning of the context, nearly as high when it sat at the end, and slumped noticeably when it was buried in the middle. Plotted out, the shape was a U, and a pronounced one. For some models, being in the middle was almost worse than being absent altogether, because the model would confidently retrieve something *else* from the neighborhood and present it with every appearance of conviction.

This is an unsettling result, if you stop to think about it. It suggests the model is not reading uniformly. It is paying close attention at the two ends and drifting somewhat through the middle.

## A tour of the benchmarks

Since then, the benchmarks have grown more ingenious and, on the whole, more unkind.

The original *needle in a haystack* test, devised in 2023 by Greg Kamradt, hid a short, odd sentence inside an ever-longer pile of essays by Paul Graham. Could the model find it? Mostly yes, eventually. The test has since come to be regarded the way physicists regard a high school pendulum experiment: charming, but not really telling you what you want to know. The needle was too distinctive — the model could spot it by sheer vocabulary, the way you can find your car in an airport parking lot by being the only person looking for a red one. ([Kamradt, 2023](https://github.com/gkamradt/LLMTest_NeedleInAHaystack))

Which brings us to **RULER**, a benchmark published in 2024 by a team at NVIDIA led by Cheng-Ping Hsieh. ([paper](https://arxiv.org/abs/2404.06654)) RULER is needle-in-a-haystack's grown-up cousin — thirteen different tasks, scaling up to 128,000 tokens and beyond. The team's headline, stated with admirable plainness: only half of the seventeen tested models maintain satisfactory performance at 32K tokens. A great many models advertising 128K windows were already wobbling by 32K. Command-R+ and Qwen2-72B, both boasting 128K on the box, turned out to have an *effective* context of around 32K. GPT-4 and Llama 3.1 managed roughly 64K.

This was, to put it mildly, not the story the marketing had been telling.

And then it got worse.

In early 2025, a group at Adobe Research published **NoLiMa**, which stands for *No Literal Matching*. ([paper](https://arxiv.org/abs/2502.05167)) The insight is easy to state and hard to fake: when you ask a model a question whose answer involves a keyword that also appears in the relevant passage, the model can cheat by matching the keyword. So NoLiMa strips the overlap out. The question and the passage share meaning but not words. You have to actually *infer* which passage is relevant.

The results, tested across thirteen models all claiming at least 128,000 tokens of context, were — and there is no kind way to put this — a bloodbath. Eleven of the thirteen fell below half their short-context performance by 32K. Per-model *effective* lengths — the size at which the model still holds about 85% of its baseline — came out like this:

- GPT-4o: about 8,000 tokens.
- GPT-4.1: about 16,000 tokens.
- Claude 3.5 Sonnet: about 4,000 tokens.
- Gemini 1.5 Pro: about 2,000 tokens.

These are models whose packaging proudly reads "128K" or "1M" on the side.

A third benchmark, **BABILong**, puts the matter about as plainly as it can be put: popular LLMs effectively use only ten to twenty percent of their context, and performance declines sharply as reasoning complexity rises. ([paper](https://arxiv.org/abs/2406.10149)) The library is not merely dim at the edges. It is dim almost everywhere, and grows darker the moment you ask it for something slightly difficult.

## The practical headline

If you remember nothing else from this chapter, remember this: **the effective context window is somewhere between four and ten times smaller than the advertised one**, as a practical synthesis of what RULER, NoLiMa, and BABILong each show in different ways. ([RULER](https://arxiv.org/abs/2404.06654), [NoLiMa](https://arxiv.org/abs/2502.05167), [BABILong](https://arxiv.org/abs/2406.10149))

A model that says it can handle a million tokens can be reasonably trusted, in practice, with somewhere between a hundred thousand and a quarter of a million. A model that says 128K is often genuinely useful up to around 16K to 32K on a hard task. The bigger the claim, the bigger the gap tends to be — partly because the benchmarks are hardest at the extremes, and partly because marketing is unconstrained by benchmarks.

The honest engineering posture is to assume a useful window of perhaps 16,000 to 64,000 tokens, and to let measured benchmarks, not billboards, earn you any more. Design your prompts so the information that matters most sits near the ends, not the middle. Keep what the model must not forget *close to where it is about to speak*.

That is the honest engineering posture: measure the window you can actually use, and keep what the model must not forget close to where it is about to speak.
