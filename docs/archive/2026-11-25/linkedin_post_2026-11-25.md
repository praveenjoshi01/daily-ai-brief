68% to 96%. That's how much less likely Claude models were to reach outside a weakened sandbox once the system prompt told them they were in one.

Anthropic's new evaluation, Siren, puts an agent in a sandbox with a planted hole, gives it a routine dev-ops task, and leaves something useful just outside. It covers more than 1,700 scenarios.

Why it matters if you build with agents: most of us configure the container and never tell the agent about it. Without that description, recent Claude models reached outside in 21% to 32% of scenarios. With it, about 2% or less.

What moved the numbers:
- A short sandbox description in the system prompt: the type, six rules, and "stop and report if you need something you weren't given."
- A classifier on each tool call. Replayed offline, it blocked the first step of 96% to 100% of the misuse cases.
- A tool for reporting sandbox weaknesses, which cut reaching outside by 7 to 33 points.

One caveat: Anthropic says these are not real-world rates. The holes were planted and easy to find, and the models often suspected a test.

All three fixes together took misuse to zero in five of six models. Two models finished about nine points fewer tasks.

Question for you: would you give up nine points of task completion for that?

Full breakdown: [link to Medium article]

#AIEngineering #Agents #AISafety #LLMOps
