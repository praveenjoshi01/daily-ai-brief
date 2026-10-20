One refinement step took GLM-5 from 59.6% to 71.4% on a legal-agent benchmark. The model's weights never changed.

Google Cloud AI Research's Harness² (arXiv 2610.14224, code under Apache 2.0) lets an agent edit its own harness: prompt, guardrails, skills, tool guidance and four more files.

For builders: the weaker model gained more. On WorkBuddy-Bench, GLM-5 gained 11.5 points in one step; Gemini 3.5 Flash gained 5.1.

How it works, in its sharpest form:
- Run the task once under the current harness as a reference
- An editor proposes two edits, each is run on the same task, and a composer merges, revises or rejects them using the behavioral difference
- Lessons from adopted edits go into a library the next task starts with

Caveats: preprint, authors' own numbers, no verifier anywhere in the loop, nine regressions in the appendix, and one editable file is the guardrails.

Question for you: if an agent edited its own skills folder overnight, which files would you let it touch without review?

Full breakdown with my redrawn diagram: [link to Medium article]

#AIEngineering #AIAgents #AgentHarness
