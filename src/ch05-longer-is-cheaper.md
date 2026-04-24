# Chapter 5 — Where Longer Is Cheaper

Here is a fact about working with modern AI that tends to produce a brief, puzzled silence when you first hear it.

Making your prompt *longer* can make it *cheaper*.

Not in any roundabout way. Not in the long run, or on average, or once you factor in reduced follow-up queries. Directly, mechanically, on the invoice that arrives at the end of the month. A prompt of five thousand tokens, properly arranged, can cost you less than a prompt of five hundred.

This runs against most of what anyone thinks they know about how these systems are priced, which is roughly: you pay for what you send, so more is more. In the simple case, that is still true. But the simple case is rarer than it looks. Most people, most of the time, are not sending one-off questions. They are working with an AI over a long conversation, or inside a tool that prepends a system prompt and a pile of rules to everything they say. All of that has to be re-sent, every turn. And all of it used to cost full price every turn — which, when you thought about it for more than about ninety seconds, was a bit mad.

The vendors, who after all do think about these things, noticed. The result is a feature called **prompt caching**, and it is one of those small technical shifts that turns out to quietly restructure how you should think about the whole enterprise.

## The mechanism, more or less

When you send a prompt, the vendor hashes the beginning of it. If that opening portion matches something they have seen recently from you, the model does not need to reread those tokens from scratch. It can pick them up from a cache, rather the way your browser picks up an image from a previous visit to a website. And because it does not need to read them, the vendor does not need to charge you full price — or rather, charges you a great deal less. On some vendors, ninety percent less.

There are three things to know about caching that will shape how you use it.

It is **strictly prefix-based**. The cache matches from the start of your prompt, token by token, until the match breaks. The moment your prompt diverges from a cached one — one comma different, one sentence added near the top — the cache is invalidated from that point onward. If you want the discount, the stable parts of your prompt must be at the top and the volatile parts at the bottom.

There is a **minimum**. The cache does not engage for tiny prompts; most vendors require around a thousand tokens of content before caching turns on. On the largest models, the floor has crept up to four thousand. Below that, ordinary arithmetic applies.

And there is a **time-to-live**. Cache entries do not persist forever. A typical default is five minutes — long enough for a burst of activity, short enough that stale prefixes don't clog the system. Some vendors offer longer TTLs at a premium.

Now the fun part: the three big vendors do this very differently, in ways that reward paying attention.

## A tour of the vendors

**Google**, on Gemini 2.5 and later, turns caching on by default. You do not ask for it. You do not configure it. You send a prompt, and if the same prefix has been through recently, the discount appears on your bill. The discount itself is approximately **ninety percent on cached input tokens** for the 2.5 family, and seventy-five percent on Gemini 2.0. ([docs](https://ai.google.dev/gemini-api/docs/caching)) This is an uncommonly generous default. A user who has never heard of caching is quietly getting most of the benefit anyway.

**OpenAI** also caches automatically. No flag, no configuration, engaging on prompts of at least 1,024 tokens across the GPT-4o and GPT-5 families. The discount is **fifty percent on cached input**. ([docs](https://openai.com/index/api-prompt-caching/)) Fifty percent is not nothing — it is a lot — but it is half of what Google and Anthropic offer, and since the rest of OpenAI's pricing tends to be comparable to its competitors', this is a real delta that widens as your prompts grow.

**Anthropic** takes a third path, which is the most finicky. Their caching is **opt-in** — you mark specific blocks of your prompt with a `cache_control` header in the API call, saying in effect: *please remember this bit; I'll be sending it again.* If you don't mark anything, nothing is cached. In exchange, the discount is **ninety percent on cached reads**, matching Google, with a small premium on the initial write: 1.25x the base price at the default five-minute TTL, or 2x at the hour-long TTL. Every read thereafter is at a tenth of normal pricing. ([docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching))

Why make users do the extra work? The charitable reading is that explicit control is a feature: users who mark their cache blocks tend to *organize* their prompts around cache boundaries, which produces more efficient caching than a system that just does its best in the background.

If you want a single sentence to carry out of this tour: **Google 90% automatic, Anthropic 90% opt-in, OpenAI 50% automatic.**

## The consequence nobody talks about

The unloved consequence of all this is that the rules file sitting at the top of your prompt — the one you write once and mostly leave alone — is one of the most valuable pieces of text in your working setup.

A good rules file — `CLAUDE.md`, `AGENTS.md`, `.cursor/rules/*.mdc`, `GEMINI.md`, whatever your tool calls it — is stable. It rarely changes. It sits at the top of every prompt your tool sends. Which means that from the very first turn of a session, it becomes a cache prefix. From the second turn onwards, it is essentially free. A carefully constructed hundred-line rules file that gets re-sent two hundred times a day is, after the first time, a rounding error on your bill.

The same applies to the system prompts inside tools you have built yourself. Any boilerplate that sits at the top of every request should live in the cache-friendly region. If it moves around turn to turn, you are leaving money on the table and, more importantly, asking the model to re-process work it has already done.

In practical terms, prompt caching inverts one of the older habits in prompting: the instinct, learned in the twitchy early days of pay-by-the-syllable APIs, to keep prompts short. That instinct is not quite dead, but it is wrong more often than it is right.

## Two habits for the desk

Two habits follow, and neither costs anything to adopt.

First, put the **durable at the top and the volatile at the bottom**. Your system prompt, your rules file, your non-changing reference — top of the stack. Your actual question, the thing that will be different every turn — bottom of the stack. This arrangement requires precisely the same amount of typing as the reverse and, on any vendor with caching, costs somewhere between ten and fifty percent less over any substantial session.

Second, **treat your rules file as an asset, not a document**. A well-written `CLAUDE.md` or `AGENTS.md` is the one chunk of your prompt that will be cached on nearly every turn. Investing in it pays down on every future interaction. The compound return is hard to beat.

We are going to spend the entire next Part on what belongs in that rules file. It is, as it happens, the single biggest unlock most people have available to them. Caching is the economic argument for it. The editorial argument — the more important of the two — comes next.

Onward.
