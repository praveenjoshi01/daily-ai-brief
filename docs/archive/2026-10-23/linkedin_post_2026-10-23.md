Three markdown files doubled Claude Opus's gain on scientific ML benchmarks: from 10.4% to 20.1%.

That's from Agent4Sci, a new Anthropic paper. The model was identical. What changed was the loop around it.

Why it matters to builders: if your agent plateaus, the fix may be the harness, not a bigger model. Mean gain also rose for Codex, from 4.4% to 8.1%.

The mechanism, sharpened:
- Agents got 12 hours on 8 H200s per benchmark. Left alone, they collapse into hyperparameter sweeps and leave GPUs idle
- The skills target that directly: plan before coding, schedule experiments, and an hourly checklist asking "am I just tuning?"
- A separate evaluator scores a sequestered test set, and a third agent audits the run for gaming

Caveats: the paper reports the skills only combined, and Anthropic authors tested Claude with Claude as the default judge.

Question for you: what is the one self-check you'd add to your agent's loop to stop it drifting into busywork?

Full breakdown with my redrawn diagram: [link to Medium article]

#AIEngineering #AIAgents #LLMEvals
