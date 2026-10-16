30,000 merged changes a day. In May it was about 2,500.

That is what Anthropic says happened to its monorepo between May and September, and git stopped being the right tool.

Git assumes clients go offline. Agents and CI jobs never do. Anthropic built Scion around that flip and, by its own numbers, moved the repo off git in five months.

If you are rolling out coding agents, the useful part is the mechanism:

- Commits, rebases and merges happen on the server, so there is nothing to push
- Clients request only the objects they will read; immutable requests mean any cache can answer (99%+ hit rates reported)
- Refs are one contended row; everything else is lock-free

Reported results: ~200x less CPU and memory than the old git mirrors, and checkouts down from minutes to seconds. These are Anthropic's own figures, and it says Scion is not a general git replacement.

The model did not change. The pipeline around it did.

My question: at what daily change volume did your CI checkout or merge queue become the slowest step?

Full breakdown with a redrawn diagram: [link to Medium article]
