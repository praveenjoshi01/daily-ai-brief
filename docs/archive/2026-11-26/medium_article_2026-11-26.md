# Title options

1. **Paradigm 3's swarm study: why one agent, restarted eight times, beat a team of eight** *(recommended)*
2. You (probably) don't need an agent swarm: what 1,100 runs say about stale context
3. Agent swarms explained: the missing baseline between one agent and eight

**Subtitle:** On the same 32M-token budget, a team of eight scored 93.2%, a single long-running agent 83.7%, and a single agent with eight fresh starts 97.0%.

---

If you've left a coding agent on a long task, you've probably watched it get worse. It re-reads files it already read. It defends a plan it made three hours ago. The usual fix on offer this year is more agents. [PRAVEEN: 1-2 sentences, optional: have you seen a long agent session degrade in your own work, and what did you do about it?]

Paradigm 3 published a study on November 24 that tests that fix at equal cost. The number I'd keep is **97.0%**. That's what a single agent scored on a hard porting task when its budget was split into eight fresh sessions. A coordinated team of eight, on the same budget, scored 93.2%. One long session scored 83.7%.

The team didn't beat the agent. It beat the agent's stale context.

## Where to find it

"Swarms do not yet raise the roof," by Niccolò Zanichelli and Gavin Leech, Paradigm 3, dated November 24, 2026. Data and code are public (the repo is `paradigm-3-institute/raising-the-roof`). TLDR AI summarised it on November 25. I found no independent technical commentary yet, so every result below is the authors' own.

## What this post covers

- **The problem:** swarm results rarely hold the token bill constant
- **How the study works:** budgets, team types, tasks and three baselines
- **The diagram:** three ways to spend the same budget, on one time axis
- **The bridge:** replicas and restarts
- **What the evidence says:** four findings, ranked
- **Three limitations,** including two in the source itself
- **What to try this week**

## The problem: more agents also means more tokens

Most swarm results compare a team with one agent and report that the team did better. The team also spent several times as many tokens. So you can't tell whether coordination helped or the extra compute did.

This study fixes the bill. Every team is compared with a single agent that gets the same total budget.

**Takeaway: a swarm result without a matched-budget baseline is a spending result.**

## How it works

### Part 1. The budget

Budgets are counted in weighted tokens: output at 100%, unique input at 23%, total input at 2%. That roughly tracks cost, since cached input is far cheaper than fresh output. Most runs had 8M weighted tokens, split evenly across the team. A subset had 32M.

Why it's interesting: the weighting stops a team from looking cheap just because its agents re-read the same cached files.

### Part 2. The teams

Teams of 2, 4 and 8 (and 16 and 32 on one task) came in three kinds. Protocol teams follow a fixed prompt that assigns distinct approaches and sharing rules. Self-organized teams get a shared goal and a message channel. Orchestrated teams have one lead agent directing helpers. A team is scored on its best submission.

### Part 3. The tasks

Four tasks: porting git to Zig (scored on 743 git tests, from FrontierSWE), two AtCoder heuristic contests, and Anthropic's performance take-home. The models were Claude Opus 5.5, Claude Sonnet 5.5, GPT-6.1 Sol and GPT-6.1 Terra, all at high reasoning effort. In total: more than 1,100 runs and more than 80 team configurations.

### Part 4. The three baselines

This is the part I'd copy.

- **Single agent:** one session, whole budget.
- **No-talk team:** the same agents, working independently. This measures how much of a team's score is just extra attempts.
- **Restarted single agent:** the budget is split into eight sequential sessions. Each starts with an empty context and keeps only the files the last one left on disk.

The third baseline isolates one variable. It has the team's fresh contexts with none of its coordination.

**Takeaway: the study's contribution is the control group.**

## The diagram

![Three ways to spend the same 32M-token budget on the git-to-zig task with GPT-6.1 Sol. One long session, whose context goes stale, scores 83.7%. A team of eight in parallel with a message board finishes sooner and scores 93.2%. One agent restarted eight times, with only files on disk carried over, scores 97.0%. My version puts all three on one time axis, which the write-up's charts don't do. The axis is schematic.](diagram_2026-11-26.png)

*My redrawn view. The team is wide and short. The restarted agent is as long as the single session, with clean breaks.*

## The bridge

Think of it as service operations.

A swarm is horizontal scaling. More replicas give you more throughput, and you pay for the load balancer.

A long session is a process with a memory leak. It still runs. It just gets slower and stranger.

A restart with state on disk is a rolling restart against a database. The process is new. The data survives.

## What the evidence says

Ranked by how much I'd act on each.

1. **Restarts beat teams on the task where teams won.** At 32M tokens on git-to-zig, the restarted agent scored 97.0% (Sol) and 41.9% (Terra), against 93.2% and 32.0% for teams of eight. At 8M it was 62.1% and 28.0% against 55.0% and 17.8%. The authors conclude the earlier "swarm premium" is explained by a single agent going stale. They think compaction is the cause: each one is a guess about what will matter later. Consequence: session length is a setting you should be tuning.

2. **Teams buy time and pay in quality.** Teams of eight finished about 6x sooner and scored about 7% lower on average at matched tokens. They matched the single agent only where it was already near its ceiling. Consequence: a team is a latency purchase.

3. **Talking matters on separable work, and hurts elsewhere.** On git-to-zig, teams of four and eight scored 16 to 53 points above their no-talk versions. On the contest tasks, talking cost GPT teams 2 to 12 points. The authors note that on git-to-zig each agent claimed a part of git's functionality in the first minute and kept it. Consequence: coordination pays when the work splits cleanly.

4. **Bigger isn't better.** With Terra at 32M, a team of 16 scored 33.3% and a team of 32 scored 23.2%, below the single agent's 26.6%.

The authors compress this into one parameter, λ, borrowed from economics: N agents get as much done as one agent running N^λ times as long. Against the restarted baseline they estimate λ between 0.6 and 0.9 for teams of eight. By my arithmetic, at 0.9 that's about 6.5x sooner for about 1.2x the tokens. At 0.6 it's about 3.5x sooner for about 2.3x the tokens.

**Takeaway: at these budgets, a swarm made things faster. It didn't raise the ceiling.**

## Limitations I'd name

1. **The key experiment is narrow, and the source says so.** The restart baseline was run after the fact, on one task, with two OpenAI models. The authors say comparisons on the other three tasks may favor teams as a result.

2. **The budgets are small.** The authors put them at about 100x below some lab runs, and their team designs are simpler than the labs'. Teams that pay coordination costs early and pull ahead later can't be ruled out.

3. **The statistics are thin in places.** Most configurations ran three times. The all-task λ estimate is 0.235 with an interval from -0.39 to 0.86, which is why the authors fall back on one task. The Codex harness also had a compaction bug that they patched and re-ran on the best teams only.

## Closing

Stale context was the variable that moved the score most, and team size came second. This is a harness finding. The model, the task and the budget stayed the same, and where the session boundaries fell was worth 13 points.

Before you build a coordination layer, split your next long agent run into fresh sessions that hand off through files, and compare the result with one long session at the same budget.

## Now I want to hear from you

1. How long do your agent sessions run before quality drops, and have you measured it or just felt it?
2. If a team of eight gets you about 93% of the result in a sixth of the time, which of your tasks would take that trade?
3. What does your agent write to disk that a fresh session could pick up cold?

## References

1. Niccolò Zanichelli and Gavin Leech, "Swarms do not yet raise the roof," Paradigm 3, November 24, 2026. https://www.paradigm3.org/research/swarms
2. TLDR AI, November 25, 2026 edition (summary of reference 1). https://tldr.tech/ai

---

**Further reading:** [link to hub article]

If this was useful, follow me for one grounded AI engineering deep-dive a day.
