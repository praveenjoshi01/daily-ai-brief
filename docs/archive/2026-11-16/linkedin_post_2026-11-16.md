31.1% of agent runs that counted as successes still failed at least one harness check.

If your evals only score the final answer, they can't see that.

An arXiv preprint from Oct 23 benchmarks four agent harnesses (Claude Code, Codex, OpenClaw, DeepSeek) across 95 tasks, 9 model groups and 3,420 runs. Its main point: the harness (context, tools, permissions, retries) is a system you can grade on its own, separately from task success.

The mechanism, sharpest form:
- Each harness's logs are normalized into one event schema, and ambiguous tool-call matches stay unlinked instead of being guessed.
- Each judge sees only its own evidence packet, and the agent's verdict is finalized before the harness is judged.
- Failure attribution proposes a mechanism chain, and a person reviews it before calling it causal.

The numbers that stuck with me: only 8.4% of runs pass every criterion, and the harness with the best task pass rate is not the one with the best harness reliability.

Caveats I'd name: the authors built the benchmark and its judge, the judge's accuracy isn't reported, and I found no independent replication.

Reader question: if a third of your "successful" runs had a broken layer underneath, which of those would your current evals have caught?

Paper and code are linked in the full write-up: [link to Medium article]

#AIEngineering #AgentEvaluation #LLMOps
