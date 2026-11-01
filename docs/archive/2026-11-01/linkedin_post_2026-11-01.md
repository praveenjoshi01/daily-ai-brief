Zero benchmarks. One idea worth stealing: stop prompting your agent to behave, and enforce it at the network boundary.

David Cramer's write-up of Sentry's open-source Junior agent (Oct 29) describes a proxy that every sandbox request passes through. The model didn't change. The wiring around it did.

If you build coding agents, the useful part is how little the prompt does:

• The sandbox holds no tokens. The proxy injects credentials after checking policy.
• Disallowed actions get a 403 written for the model: "use the PR tool instead." The error message becomes the instruction.
• CI failures and review comments are injected back as messages, so the agent doesn't poll.

Caveats I'd flag: the post has no metrics, the author says the guard can be bypassed, and the repo is tagged non-production. Treat it as a hypothesis you can test in a day.

Question for you: which rule would you move from a prompt to an enforced boundary first, and how would you measure compliance?

Full breakdown with a redrawn diagram: [link to Medium article]

#AIEngineering #AIAgents #LLMOps
