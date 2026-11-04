Up to 33% cheaper and 20% faster, with no model change. That's Framer's claim for its new agent harness. The post gives no baseline, so read it as directional.

The model didn't get smarter. The harness stopped waiting for it to finish.

Why it matters to builders: most agent latency is round trips, not thinking. Each command goes out, the result comes back into the prompt, the model reasons again.

The mechanism, per Framer's write-up:
- The agent writes one JavaScript program per workflow instead of one command per turn
- Complete statements run in a Web Worker while the code is still streaming
- A terminal error or "nothing to do" cancels the rest of the stream, while soft errors are collected and reported at the end

A related paper (arXiv 2604.00491) reports hiding 83-100% of execution time behind generation in a controlled Python setting. Different setting, same idea.

Question for you: if your agent streams code, which errors should cancel the run and which should only warn?

Full breakdown with a redrawn diagram and three limitations I'd name: [link to Medium article]

#AIEngineering #LLMAgents #DeveloperExperience
