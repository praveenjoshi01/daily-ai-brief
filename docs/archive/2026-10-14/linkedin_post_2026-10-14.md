Your LLM rate card stopped predicting your bill.

Claude Haiku 5.5 shipped last week at $0.10 / $0.50 per million tokens (up to 100K prompt tokens), versus $1 / $5 for Haiku 4.5. Anthropic's headline: about 75% cheaper on average.

But read the fine print:

- The new tokenizer produces roughly 30% more tokens for the same text, per an independent analysis of Anthropic's docs
- Above 100K prompt tokens the price jumps 5x
- It's the first Haiku with an adjustable effort setting, so there is no single price, only a price per effort level

An independent analysis couldn't reproduce the 75% from the published rates, because the request mix isn't disclosed. A third-party summary of Artificial Analysis data reports about 162K output tokens per task at max effort, and $0.21 per task versus $0.12 one effort level down.

My takeaway: stop comparing small models on price per token. Track cost per passing task, by effort level, on your own evals. Watch your prompt sizes against the 100K line. Recompute max_tokens after the tokenizer change.

My prediction: over the next quarter, "dollars per solved task at a stated effort" becomes the number engineers argue about for small models.

Full breakdown, with sources, in the article: [link to Medium article]

What does your team measure today: tokens, requests, or tasks?
