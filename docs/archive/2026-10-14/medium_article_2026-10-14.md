# The Cheapest Model Isn't the Cheapest Model: Reading Haiku 5.5's Price Table Like an Engineer

Last week Anthropic shipped Claude Haiku 5.5 with a headline number that every finance-minded engineering lead will quote in the next planning meeting: about 75% cheaper to run than Haiku 4.5. It's a good model release. It's also a good excuse to stop thinking about LLM cost the way most of us still do.

Here is the short version of what I'd tell my own team: the price per million tokens is now the least informative number on the page.

## What actually shipped

According to Anthropic's announcement on October 7, Haiku 5.5 is its "cheapest, fastest, and most capable small model" to date, aimed at high-volume work like summaries, compaction, database queries and classification. The rate card is tiered by prompt size. Up to 100K prompt tokens, input costs $0.10 and output $0.50 per million tokens, against $1 and $5 for Haiku 4.5. Above 100K, it is $0.50 and $2.50, still half of the old price, but five times the lower tier. Cache reads are $0.01 in the lower tier.

Three other details in the same announcement matter more than the discount:

- Haiku 5.5 is the first Haiku-class model with an adjustable effort setting, from Low to Max.
- Anthropic says Sonnet 5.5 and Opus 5.5 remain the better choice for complex agentic coding, and positions Haiku 5.5 as a good fit for narrowly scoped tasks and as a subagent. Its own table backs that up: on Terminal-Bench 4.0, Anthropic reports 39.2% for Haiku 5.5 against 70.6% for Sonnet 5.5.
- In the same post, Anthropic halved Sonnet 5.5 cache-read pricing to $0.10 per million, which it says makes Sonnet 5.5 about 20% cheaper on most agentic work.

Those benchmark figures are Anthropic's own. Independent evaluation is thinner so far, which I'll come back to.

## Where the 75% comes from, and where it doesn't

The 75% claim is described by Anthropic as an average, and a footnote says it also accounts for differences in how many tokens each model needs to do the same work. That is an honest caveat, and it is the whole story.

An independent analysis on Braindetox tried to reproduce the figure from the published rates and couldn't, because the weighting, input/output split and request sizes aren't disclosed. Its arithmetic: if the same text cost the same number of tokens, the lower tier would be 90% cheaper. Factor in the new tokenizer, which Braindetox says Anthropic's model docs and migration guide describe as producing roughly 30% more tokens for the same text, and the lower tier lands near 87% cheaper. Weight by a mix of requests that includes some over the 100K line, and it drops to roughly 82%. So the announced 75% is more conservative than the analyst's own math, not less. Another write-up, from MetricNexus, frames the effective saving as closer to 75% than 90%. Same conclusion from the other direction: the number depends on assumptions you can't see.

That's not a complaint about Anthropic. It's the point. A per-token discount is a statement about a unit that your bill doesn't use. Your bill uses tokens consumed per completed task, and three things in this release change that quantity independently of the rate card:

1. **The tokenizer.** The same prompt now counts as about 30% more tokens. Your `max_tokens` limits, your budgets and your cost estimates were all calibrated on the old count. Per Braindetox, Anthropic's migration guide tells developers to recompute them.
2. **The 100K cliff.** A fivefold price step at a prompt-size boundary means a RAG pipeline that sometimes stuffs 90K tokens and sometimes 110K has a cost curve with a discontinuity in it. Averages hide that.
3. **The effort dial.** A model whose reasoning budget you can turn up has no single price. It has a price per effort level.

## What independent data says about task cost

The best third-party signal so far is Artificial Analysis, as relayed by MetricNexus (I'm reading it secondhand, not from Artificial Analysis directly). It reports an Intelligence Index of 43 for Haiku 5.5 at max effort, about 162,000 output tokens used per task, which it describes as roughly three times GPT-6 Luna, and a cost of $0.21 per task at max effort versus $0.12 at xhigh.

Do the arithmetic yourself: 162,000 output tokens at $0.50 per million is about eight cents of output alone. That is my calculation from the published rate, not a figure from the source, but it makes the point that a "cheap" model that thinks a lot is still a model that thinks a lot. Dropping one effort level cut the reported task cost by roughly 40%. That is a bigger lever than the difference between most vendors' rate cards.

The same MetricNexus summary reports mixed accuracy characteristics: lower factual accuracy than Luna on one benchmark (36% versus 44%) but a lower hallucination rate (40% versus 77%), plus one benchmark score it flags as unreliable because of an over-refusal bug, with a re-run planned. Treat all of it as preliminary. One analysis I read says an Epoch AI evaluation is still pending, and the agentic scores in Anthropic's table are self-reported.

## What I'd change on Monday

If you run a pipeline with a small-model tier, here is what I'd do before switching anything.

**Measure cost per passing task, by effort level.** Not cost per request, not cost per million tokens. Log input tokens, output tokens (including thinking tokens, which count toward `max_tokens` according to the MetricNexus summary) and a pass/fail from your own evals. Then compare Haiku 5.5 at Low, Med and High with whatever you run today. The winner will often be a surprise in both directions.

**Put prompt size on your dashboard.** If any meaningful share of your traffic is near 100K tokens, you have a routing problem, not a pricing problem. Either trim context, split the request, or send big prompts to a model whose tiering suits them.

**Use the small model where its published strengths are.** Anthropic's own guidance points to classification, extraction, summarization and subagent work. MetricNexus adds a caution that independent testing found weaker results on creative or open-ended visual tasks. Both match the intuition that cheap models earn their keep on well-specified work. Don't let a price drop talk you into using one as your planner.

**Recompute budgets after the tokenizer change.** This one is boring and will bite someone. A hard `max_tokens` cap that was comfortable on Haiku 4.5 is effectively 30% tighter in text terms.

## The bigger shift

For a couple of years, we compared models on two axes: capability and price per token. Haiku 5.5 is a clear sign that a third axis, effort, has moved from a research curiosity to a production parameter, and it arrives with a tokenizer change and a tiered price. Each of those is individually reasonable. Together they mean a rate card no longer lets you predict a bill.

My prediction, and you can hold me to it: for small models, the comparison that practitioners argue about over the next quarter won't be dollars per million tokens. It will be dollars per solved task at a stated effort level, and the teams that already log tokens per task by effort will be able to answer in an afternoon what everyone else needs a month of production traffic to learn.

Price cuts are easy to announce and hard to verify. Task cost is the opposite: hard to publish, easy to measure on your own workload. Measure it.

## Sources

- Anthropic, "Introducing Claude Haiku 5.5" (October 7, 2026): anthropic.com/claude-haiku-5-5
- Braindetox, analysis of the Haiku 5.5 price table: braindetox.kr/en/posts/claude_haiku_5_5_release_pricing_2026.html
- MetricNexus, "Claude Haiku 5.5: Benchmarks and Real Cost Math" (relaying Artificial Analysis): metricnexus.ai/blog/claude-haiku-5-5-benchmarks-pricing
