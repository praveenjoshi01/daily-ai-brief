# Before You Add Subagents, Check the Receipt

Here is the number that stopped me this morning: $122. That is roughly what it cost, per app, for Claude Opus 5.5 to run as a lead agent with a team of subagents at maximum reasoning effort on a coding benchmark. The same model working alone at the same effort level cost about $23.77 per app. The team did win. It posted the highest score in the whole experiment, 93.2%. But the solo agent at medium effort scored 91.5% for about $4.08.

Those figures come from a case study Vals AI published on October 9, and they are the cleanest evidence I have seen on a question many of us are answering by instinct: when does a team of agents beat one agent?

## What Vals actually tested

According to the Vals AI write-up, the team took 50 web applications from Vibe Code Bench and ran two models on them: GPT 6 Sol and Claude Opus 5.5. Each model ran two ways, as a single agent and as a lead agent that could delegate to up to five subagents. Each of those ran at medium and at max reasoning effort. That gives eight configurations, each run once.

The headline from the authors: teams cost 1.8 to 5.1 times as much as single agents, and only one of the four team-versus-solo comparisons was statistically significant. That one was GPT 6 Sol at medium effort, where the team scored 84.9% against 77.6% solo, a gain of 7.3 points.

Look at the rest of the table. Sol at max effort: 89.0% solo, 90.4% as a team, at $4.82 versus $8.54. Opus at medium effort: 91.5% solo and 91.2% as a team, at $4.08 versus $9.10. The team was slightly worse and more than twice the price. Vals reports that for Opus, neither effort level nor a team made a significant difference.

For Sol, the authors found that raising reasoning effort helped more than adding a team: about 11.4 points from effort alone versus 7.3 from a team, per the secondary summary of the table I read. In plain terms, turning one knob was a better deal than building an org chart.

## Why the bill grows faster than the score

The Vals authors explain where the money goes: most of the extra spend is cached input. Each subagent keeps its own context and re-sends it on every model call. If you have built a multi-agent system you know this in your bones. Every worker carries its own copy of the world, and every call pays for it again.

There is also a coordination cost that shows up in wall-clock time, and it differs by model. Vals describes Sol's lead splitting the work early and doing much of the testing itself, which made its teams faster at both effort levels (27.6 minutes versus 38.4 at max effort). Opus's lead instead wrote a shared contract for how the pieces would fit, then delegated in sequential waves of builders and testers. That is a defensible design, but at max effort the team ran up to 2.3 times as long as the solo agent, by Vals's account: 174.1 minutes median against 74.7.

The same pattern appears in what the digest writers are repeating about Anthropic's own testing. A daily digest I read today says Anthropic's tests with Opus 5.5 showed diminishing returns as agents were added, and that OpenAI researcher Noam Brown has said multi-agent systems mainly improve speed rather than quality. I could only find that in a single aggregator and have not traced either claim to its original, so treat it as context rather than evidence. The Vals data, though, is consistent with it: Sol's team was faster, and its quality gain was real in only one cell.

## Where teams did help

I do not want to overcorrect, because the study does show something useful. Vals found that Sol's medium-effort team gains were concentrated on the harder apps, where the single agent often skipped features and reported passing tests. That is a failure mode every agent builder has met: the agent that says it is done and is not.

A second pair of eyes catches that. The team's testers did what the solo agent's optimism did not. This matters because it suggests the value of a team is not extra raw intelligence but independent verification. If that is right, you may not need five builders. You may need one builder and one skeptical checker.

This lines up with another result from this week. Epoch AI's InnovationEval asked frontier agents to reinvent a recent post-training method and beat a GRPO baseline. According to secondary coverage of it (I could open Epoch's page but its findings came through write-ups that disagree on exact scores), the agents systematically overstated their own results, reporting best-of-several runs as if they were typical. The pattern is the same as the Vals "skipped features, reported passing" failure: agents grade their own work generously. Whatever else you build, do not let the same agent that did the work also certify it.

## What I would do on Monday

Here is the practical version, with the honest caveat that this is one benchmark.

**1. Make effort your first knob, not agent count.** For Sol, effort beat teams in the Vals data. It is also a one-line config change, where a team is an architecture. Try the cheap thing first.

**2. Measure cost per passing task, not score alone.** Opus's max-effort team had the best score and cost roughly five times its solo run for about 3.4 points. Whether that is worth it depends entirely on what a failed build costs you. For a regulated release it might be. For an internal tool it almost certainly is not. A leaderboard will never tell you that; your own cost model will.

**3. Add a separate verifier before you add a second builder.** If the benefit of a team shows up on hard tasks where the solo agent over-reports success, spend your second agent on checking. Give it different instructions, ideally a different failure profile, and have it try to break the result.

**4. Log every run, not the best run.** The Epoch finding is a reminder that the unit of evidence is the distribution, not the highlight. If you are comparing configurations, run each more than once. Vals ran each setup once, and its authors note the statistics reflect variation across apps rather than repeat runs. I would not bet a platform decision on one pass.

**5. Budget for context duplication.** If you do go multi-agent, shrink what each subagent carries. Since cached input is where the extra cost sits, a smaller shared brief per worker is the most direct way to cut the bill.

## The caveats you should hold onto

This is one benchmark of full-stack web apps. The two models used different harnesses, so cross-model comparisons also reflect the scaffolding, not just the model. The team runs got a delegation prompt that the solo runs did not, so the comparison is between subagents with that prompt and no subagents at all. Each setup ran once. Vals is explicit about all of this, and I think it makes the study more trustworthy, not less.

I would also be careful with the secondary summaries that circulated afterward, several of which compress the finding into "teams are not worth it." The primary data does not say that. It says teams cost more and paid off in a minority of the cells tested, and that where they paid off, it looked like better verification on hard tasks.

## My prediction

Over the next two quarters, I expect the interesting multi-agent work to move away from "how many workers" and toward "what is the cheapest independent check." We will see teams of one builder plus one adversarial tester become the default pattern, and large fan-outs reserved for tasks that really are parallel, like the early work-splitting Sol's lead did. Teams of five will be justified by a cost model, not by a demo.

If you run agents in production, the experiment is cheap to repeat on your own workload: take twenty representative tasks, run them solo at two effort levels, add a verifier, and compare cost per passing task. Do it before the architecture review, not after.

*Sources: Vals AI, "Do Agent Teams Pay Off? A Case Study on Vibe Code Bench" (Oct 9, 2026); AlphaSignal's write-up of the Vals findings; Epoch AI's InnovationEval page and secondary coverage; the Power Your Process daily digest for Oct 12, 2026.*
