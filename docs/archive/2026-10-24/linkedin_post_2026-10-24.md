One customer's agent ran about 2x faster after Anthropic folded its subagents into a single loop. A separate AI21 study cut code-review cost per PR from $0.589 to $0.0135 by changing the harness, not the task.

The model isn't the lever. The system around it is.

If you're running router + planner + specialist agents, this is worth an afternoon. Anthropic's Applied AI team says single agents with skills often beat both one-prompt and subagent designs on quality, at lower cost and latency (their numbers are thin, so test it yourself).

How the fold works:
- Routing and planning move into the loop: the model writes and revises its own plan
- Specialists become skills; hard limits and approval gates become tools
- Evals come first, and you fold one subagent at a time (one fold sped things up and silently broke a shipping-date rule)

Caveat: the 2x figure is one unnamed customer, and AI21 tuned and scored on the same 50 PRs.

Question for you: which of your subagents exist because of a real context limit, and which because of your org chart?

Full breakdown with a redrawn diagram: [link to Medium article]

#AIEngineering #AIAgents #LLM
