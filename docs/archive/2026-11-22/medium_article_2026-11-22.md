# Title options

1. **Stripe's integration evals, explained: the missing layer between the model and the docs** *(recommended)*
2. What the docs don't tell your coding agent
3. You (probably) don't know what your coding agent is looking up

**Subtitle:** Outdated API references fell from 7% to 1.3% across 14 model–harness pairs. The models stayed the same. The harness changed.

---

If you've watched a coding agent write a payment integration, you've probably seen it use a parameter that was deprecated last year, with complete confidence. You fix it by hand, and the next task does it again. [PRAVEEN: 1-2 sentences, optional: have you hit a stale-API failure from an agent in your own work?]

Stripe just measured that failure mode. The number I'd keep is **7%**: the share of API parameter references that were outdated when agents wrote integrations without help. With Stripe's agent plugin loaded, it dropped to **1.3%**.

The model didn't learn anything new about Stripe. The agent got a current map.

## Where to find it

Stripe's methodology post, "Stripe integration evals," was published on stripe.dev on November 19, 2026. The results are Stripe's own, and Stripe also sells the product being tested. I'll mark which numbers come from where.

## What this post covers

- **The scenarios:** 69 public cases, and what they ask agents to build
- **The role-playing developer:** why the agent gets questions instead of a complete spec
- **The harnesses:** the 14 model-and-harness pairs, with and without the plugin
- **The judge:** MUST and SHOULD criteria, and the difference between a headline score and a strict pass
- **What changed with the plugin:** the 3–8 point gains, the 96% drop in searching, and the stale-reference rate
- **Three limitations**, including the one that matters most for production

## The problem it solves

Most code benchmarks give a model a complete task and check the output. A real integration doesn't start that way. The request is vague, the developer doesn't know which API version is current, and the agent has to find out what the customer actually needs.

Stripe's baseline shows what happens without help. Agents ran about 1.26 web searches per eval, and 7% of the API parameters they referenced were outdated. Searching the web is how an agent tries to fix a stale memory, and it is slow, noisy, and sometimes wrong.

The naive fix is to paste the docs into the prompt. Stripe's approach is different: it ships a plugin that gives the agent current references, and it measures whether that changes the outcome.

**Takeaway:** If the agent is searching the web to answer basic API questions, its memory is out of date, and that is a harness problem before it is a model problem.

## How it works

The eval has four moving parts. I've redrawn the loop below, because the post describes the pieces but not the feedback path between them, and that path is where the design is interesting.

![Stripe's eval loop, redrawn: a role-playing developer answers the coding agent's questions one at a time; the agent runs in one of two arms (with or without the plugin); a judge scores each rubric criterion against the transcript and workspace. My version adds the arm split and the question-and-answer loop, which the post's text describes but does not draw.](diagram_2026-11-22.png)

*Caption: My redrawn version of Stripe's eval loop. The post names the parts; I've added the two-arm split and the question loop between the developer and the agent, since the design depends on both.*

### Module 1. The scenarios

The eval includes 69 public cases: 24 one-time payments, 26 subscriptions, and 19 Connect cases for marketplaces and platforms. Tasks include hosted checkout, metered billing, per-seat subscriptions, and splitting a payment across a marketplace.

The interesting design choice is what the scenarios are not. They aren't a spec sheet. They are the kind of request a developer would type into an agent.

### Module 2. The role-playing developer

A secondary LLM plays the developer. From the opening prompt, it derives a private list of two to four needs, up to six at most. Each turn, it asks about one unresolved need. It does not write code, it does not reveal its list, and it does not assume the agent knows Stripe. The run stops when every need is met or the turn limit is reached.

This turns requirements gathering into part of the test. An agent that asks the wrong question, or stops asking too early, loses points for reasons that have nothing to do with its code.

**Takeaway:** The eval measures whether the agent elicits requirements well, not just whether it writes valid code.

### Module 3. The harnesses

Coding agents ran headlessly in isolated workspaces: Claude Code, Codex, or OpenCode, across 14 model-and-harness pairs. Each pair ran each case with and without Stripe's plugin, twice per arm. That is 276 runs per agent. Runs that hit the 45-minute timeout counted as errors and were excluded from scores.

This is the design that matters for this newsletter's usual argument. Stripe holds the model fixed inside a pair and changes only what the agent is given. The comparison is apples to apples.

### Module 4. The judge

Every rubric criterion is labelled MUST or SHOULD, using the RFC 2119 meanings. A judge grades each criterion against the transcript and a snapshot of the workspace, and the model's reasoning is excluded.

Two metrics come out of this. The headline is the **mean criteria success rate**. The **strict pass rate** requires every MUST criterion to pass. The gap between them is where most of the story sits, and I come back to it below.

**The bridge:** The plugin is a current map handed to a driver who already knows how to drive. The role-playing developer is a passenger who answers only when asked. The judge is the inspector who checks that the car arrived, not how the driver read the route.

## What the evidence says

Here is what Stripe reports, ranked by how much each number should change what you do.

**1. Every pair improved, by roughly 3 to 8 points.** Across all 14 model-and-harness pairs, adding the plugin raised the score. The floor is a few points and the ceiling is around eight. That is a consistent direction across models, which is the strongest part of the result. Practical consequence: if you're deciding whether to add tooling to your agent, expect a gain in the single digits from reference context alone, and measure your own before you claim more.

**2. Outdated references fell from 7% to 1.3%.** This is the number I'd build a case on. A stale parameter in an integration is a runtime failure waiting to happen, and cutting the rate by more than five-sixths is the change that matters most in production.

**3. Web searches fell 96%.** Pooled searches per eval dropped from 1.26 to 0.05. Fewer searches mean less latency, fewer tokens spent on noisy results, and less exposure to whatever page the search engine happens to rank first.

**4. Strict grading takes the average from 78.1% to 29.4%.** This is the number a team leader should look at. A headline average of 78% sounds like a working agent. Under strict grading, where every required criterion has to pass, the post reports 29.4%. If your internal dashboards report the lenient number, they describe a different system than the one a strict reviewer would accept.

**5. Harness effects depend on the model.** Fable 5.1 made 53% more tool calls with the plugin. Gemini 3.8 Flash made 26% fewer. The same tool changes behaviour differently depending on what is running it. Measure per model, not once for the team.

**Which component carries the gain?** The post doesn't separate the reference data from the reduced searching, and it doesn't run an ablation. My inference, which the post doesn't test, is that the stale-reference drop and the search drop are the same mechanism seen from two sides: the agent gets current references and stops guessing. Treat that as a hypothesis for your own eval, not a finding.

**Takeaway:** The gain is consistent, and the strict number is the one to trust.

## Limitations I'd name

**1. The source grades its own product.** Stripe wrote the scenarios, the rubric, the plugin, and the post. The results are reproducible in principle, since Stripe describes the method in detail, but nobody has independently re-run them yet. An independent InfoQ article covers Stripe's earlier July benchmark, which had no plugin comparison, so it doesn't corroborate these numbers. Before you bet on the size of the effect outside Stripe's API, wait for a second team to run it.

**2. The judge and the developer share a model family.** The role-playing developer and the judge were both GPT 6.1 Sol. Stripe ran a probe using Opus as the judge and found no bias, only differences in how leniently each judge scored. That's a reassuring check, but it was one probe with one alternative judge.

**3. The benchmark checks specification, not execution.** The post says so directly: "The benchmark asserts correct specification, not correct execution." An integration can satisfy every rubric line and still fail at runtime. The eval also doesn't measure whether the agent recommends the right Stripe product, or how the code holds up when the API changes over months.

## Closing

The number that sticks is 7% to 1.3%, and the reason it matters is the one that sticks in my head too: the model's knowledge is frozen at training time, but what sits in its context is not. Stripe's result is a measurement of that gap.

For a builder, the action is concrete. If you maintain an SDK or an internal API, publish a machine-readable reference an agent can load, and measure your stale-reference rate the way Stripe did. Then report the strict pass rate, not the average.

## Now I want to hear from you

1. Which API you integrate with most has changed in the last twelve months, and would your coding agent have known?
2. When your team reports an eval, do you count MUST failures as failures, or average them into the score? Which one did your last report use?
3. If a plugin lifts a model, how much of the gain is reference data and how much is reduced searching? The post doesn't separate them. Would you run that ablation first?

## References

1. Stripe. (2026, November 19). *Stripe integration evals: methodology*. stripe.dev/blog/stripe-integration-evals-methodology
2. Stripe. (2026). *Can AI agents build real Stripe integrations? We built a benchmark to find out*. stripe.com/blog/can-ai-agents-build-real-stripe-integrations
3. InfoQ. (2026, July 15). *Stripe's AI agent integration benchmark*. infoq.com/news/2026/07/stripe-ai-agents-benchmark/
4. TLDR AI. (2026, November 20). Newsletter issue. tldr.tech/ai

Reference 2 is cited for its earlier benchmark; I did not fetch it this run, so I rely on InfoQ's summary of it. Reference 4 is the newsletter that relayed the methodology post.

---

**Further reading:** [link to hub article]

If this kind of breakdown is useful, follow along or subscribe to the newsletter: [newsletter link placeholder]
