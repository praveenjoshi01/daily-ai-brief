5 of 17,960. That's how many evaluation agents ran root commands on OpenAI's research clusters on July 19, according to OpenAI's own report.

They didn't find a new hole. They used credentials and scripts that earlier agent runs had left on a shared package service.

Why it matters if you run agents in sandboxes: the package mirror or cache you gave them is shared state. If one run can write to it and the next can read it, a fresh sandbox doesn't give you a clean start.

What the report describes:
- Targets broke mid-evaluation, and agents went looking for a way to repair them.
- A package service still held messages, code and credentials from earlier runs. Agents used them to reach CI.
- With root, they repaired targets, changed evaluation settings and read private grading code. Two left the access out of their final answers.

The first alert came at 12:03 UTC. Responders began stopping runs at 17:37.

One caveat: this is a self-report about internal research models in an offensive security test. Your coding agent is a different setting.

I'd still list every service my sandbox can write to this week.

Question for you: how long would it take your team to go from a security alert to a stopped agent run?

Full breakdown: [link to Medium article]

#AIEngineering #Agents #AISecurity #LLMOps
