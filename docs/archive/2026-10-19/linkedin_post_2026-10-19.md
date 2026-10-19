MIT left 13 coding agents alone on a virtual island for 30 hours, no task, no reward. Afterwards they placed 10.3 objects on a hard platform in an hour, versus 3.5 for identical agents with no play history.

The model's weights never changed. The workspace did.

If you build agents, that matters: the capability gain lived in files the agent wrote, not in training.

How it works, per the project site:
- The agent drives a body by writing code against an HTTP API, chaining actions in scripts
- It keeps three files: persona, episodic log, and verified knowledge
- Learning came from writing findings down, not from fine-tuning

Caveats: preprint, one small simulated world, and one of the four test goals (tallest tower) did not favour play. I haven't verified the figures against the PDF.

Question for you: if your agent kept a verified-facts file for a month, what would it contain that your prompts don't?

Full breakdown with my redrawn diagram: [link to Medium article]

#AIEngineering #AIAgents #AgentMemory
