Meta's assessor stack cut human review load by about 70%. Of 41 test failures sent to engineers, 8 were real bugs, and 4 would have been serious.

The test generator isn't the product. The filter stack is.

Why builders should care: an LLM can write a test that fails on a diff all day. The hard part is deciding which failure deserves a human's attention.

How Meta's Catching JiTTests work, per their engineering post and FSE '26 paper:
• Target risky diffs overnight, then generate tests that tell the diff from its parent (mutation-guided, intent-aware)
• Two judges filter the results: an LLM ensemble for semantics, a deterministic rule engine (RubFake) you can audit
• Engineers set criteria and review in aggregate, not per alert

Caveats I'd flag: 8 of 41 is a small sample, the 60% true-positive rate in the blog is engineer-reported, and it's one company's setting.

Question for you: if your team got one catching-test alert a week, what true-positive rate would keep you reading it?

Full teardown with my redrawn diagram: [link to Medium article]

(Tip: put the link in the first comment.)
