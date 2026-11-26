97.0% vs 93.2% vs 83.7%. Same task, same model, same 32M-token budget.

The 83.7% is one agent in one long session. The 93.2% is a coordinated team of eight. The 97.0% is one agent whose budget was split into eight fresh sessions that share only the files on disk.

That's from Paradigm 3's new study of agent swarms: 1,100+ runs, every team compared with a single agent on the same token budget.

Why it matters if you build with agents: the team's win over the long session came from fresh context. Coordination wasn't needed to get it.

What the study found:
- Teams of eight finished about 6x sooner and scored about 7% lower on average at matched tokens.
- Talking helped where work splits cleanly (16 to 53 points on a git port) and cost points on optimisation contests.
- Bigger teams didn't help. A team of 32 scored below the single agent.

One caveat: the restart test was run after the fact, on one task with two OpenAI models, at budgets far below what the labs use.

Before adding agents, I'd try restarting the one I have.

Question for you: how long do your agent sessions run before quality drops, and have you measured it?

Full breakdown: [link to Medium article]

#AIEngineering #Agents #LLMOps #DeveloperExperience
