# Title options (recommended first)

1. **Trial by Trace: the benchmark that grades the harness, not just the answer**
2. What the docs don't tell you about agent harnesses: a third of "successful" runs broke a check
3. Trial by Trace explained: the missing layer between task success and harness reliability

**Subtitle:** 31.1% of successful agent runs still failed at least one harness check. Here is how the benchmark measures it, and what it means for anyone shipping an agent.

---

If you've shipped an agent, you've probably checked its answer and moved on. The task passed. The ticket closed. Nobody read the retries, the approvals, or the tool calls that got it there.

[PRAVEEN: 1-2 sentences on a time an agent's answer looked right but a retry, permission or side effect was wrong in your own work. Delete this placeholder if you'd rather skip the personal hook.]

A new benchmark puts a number on that blind spot. Across 3,420 runs, **31.1% of runs achieved task success while failing at least one harness criterion.** An outcome-only benchmark would count every one of those as a clean win.

Outcome scores grade the agent. Nobody was grading the harness.

## Where to find it

"Trial by Trace: Benchmarking AI Agent Harnesses for Reliability and Failure Attribution," by Zhiyong Cao, Hengjie Zhu, Yongxin Wang and 20 others. Submitted to arXiv on October 23, 2026 ([arXiv:2610.32285](https://arxiv.org/abs/2610.32285), cs.AI). The benchmark, TraceTrial-Bench, is MIT-licensed on [GitHub](https://github.com/TraceLite-AI/TraceTrial-Bench). It is a preprint from the benchmark's own authors. I could not find an independent replication.

## What this post covers

- **The problem:** why outcome-only scoring hides harness failures
- **Module 1, Trajectory Tracing:** four harness logs become one schema
- **Module 2, Evidence Acquisition:** each judge sees only its own evidence
- **Module 3, Failure Attribution:** a harness failure linked to a task failure, with a human in the loop
- **The scoring rule** and the ordering that keeps it honest
- **What the evidence says**, and what it cannot say yet

## The problem: outcome scores check the return value

The paper defines a harness as the native layer that builds context, exposes tools, transports results and enforces permissions. The model sits inside it. The benchmark's authors argue that most agent benchmarks report model capability and final task success, and say little about the harness.

The gap shows up quickly in their table. Task success ("Agent Pass") runs from 35.8% for Codex to 44.0% for Claude Code. Harness reliability ("Harness Macro") runs from 59.8% for Codex to 72.0% for OpenClaw. The harness with the best task success is not the harness with the best reliability. If you pick a harness by one column, you have answered only half the question.

> An outcome benchmark is an integration test that asserts on the return value and never on side effects. It goes green while the job retried three times, wrote to the wrong path and skipped the approval step.

That is the bridge, and it is the reason the paper matters to anyone who has run an agent unattended.

## How it works

The benchmark has three modules. They run in order, and each one has a rule that stops it from overreaching.

### Module 1. Trajectory Tracing

Every harness writes logs in its own format. Claude Code emits stream-JSON plus a session record. Codex emits a JSON event stream. OpenClaw emits JSON plus session JSONL. The DeepSeek Harness emits a persistent JSON-RPC notification stream. Each has its own adapter.

The adapters map these records to one event schema with a sequence index. They keep the raw events, and they correlate each tool call with its result by native call ID. Ambiguous matches stay unlinked. The design choice I find most interesting is that the system refuses to guess. An unlinked event is an honest gap. A wrong link would quietly corrupt every judgment downstream.

### Module 2. Multi-source Evidence Acquisition

Each criterion gets a bounded evidence packet, built from declarative selectors: which event types, which fields, which keywords, and how many results to return. Full archives stay available for audit.

The rule that matters here is that each source is authoritative only for its own claim. Simulator state shows what happened. The model-facing result shows what the model could see. The gap between those two is where harness bugs live: a tool that returns the right data in a form the model cannot use looks correct to an outcome check and broken to this one.

### Module 3. Failure Attribution

Attribution uses predeclared mechanism chains. A failed harness criterion links to a failed agent criterion through a stated intermediate distortion. The system flags candidate links automatically, but a flag only means the conditions matched. Calling a link a propagation requires manual review of event order, observable distortion and competing explanations.

This is the module I'd copy first. It separates "the conditions matched" from "this caused that," and it keeps a person in the second step.

### The scoring rule

The benchmark covers seven harness components, with task counts in brackets: Context (15), Execution (27), Governance (9), Lifecycle (19), Observability (7), Tools (17) and Verification (1). Each run gets a score:

**Per-run score = 50 × (harness criteria passed ÷ harness items) + 50 × (agent items passed ÷ agent items)**

Two ordering rules make this honest. Infrastructure checks run first as an admission gate, so a broken container never gets scored at all. And agent results are finalized before the harness judge runs, so an agent's verdict cannot serve as evidence of a harness failure. Without that second rule, the two judges would grade each other's homework.

![Redrawn diagram of the TraceTrial-Bench pipeline: native harness records pass an admission gate, go through adapters into a shared schema, become evidence packets, then feed an agent judge (finalized first) and a harness judge, which together produce a per-run score and feed failure attribution. My addition: the admission gate and the agent-first ordering are drawn in, because they are easy to miss in prose and they decide whether the harness score can be trusted.](diagram_2026-11-16.png)

*My redraw of the pipeline from the paper's text. The original prose states the admission gate and the agent-first ordering, but a summary diagram usually drops them. I drew them in because they decide whether the harness score can be trusted.*

## What the evidence says

Here are the paper's per-harness results. All figures are percentages.

| Harness | Agent Pass | Harness Macro | Clean runs | Overall |
|---|---|---|---|---|
| Claude Code | 44.0 | 71.2 | 9.1 | 73.5 |
| Codex | 35.8 | 59.8 | 2.8 | 65.2 |
| DeepSeek Harness | 40.0 | 68.8 | 9.8 | 71.0 |
| OpenClaw | 38.2 | 72.0 | 11.7 | 71.8 |

*"Clean" means the run passed every criterion in both layers. The paper's headline says 8.4% of all runs do.*

What these numbers mean in practice:

- **Most runs have something to fix.** Only 8.4% of runs pass every criterion. For an unattended agent, that means a typical successful run still carries a harness problem you would not see in the output.
- **Task success and reliability can point in different directions.** Claude Code leads on Agent Pass. OpenClaw leads on Harness Macro and on clean runs. Codex is last on both, with 2.8% clean. If you only watch whether the task finished, you will choose the harness that is most likely to hide problems.
- **Budget for the judge.** The paper says its reported costs are token-based estimates and exclude judge calls. A replication costs more than the agent runs alone.
- **The paper does not rank components.** It tells you which harness criteria failed. It does not say which component, such as Governance or Lifecycle, most affects outcomes. That is the experiment I'd want next, and it is not in this paper.

## Limitations I'd name

1. **The source is the benchmark's own team.** The same group built the tasks, the trace adapters, the judge and the scoring. I found no independent replication. The repository says community runs are not official results, and that is the right way to read them.
2. **The LLM judge is not validated in the paper.** The judge is a fixed model, deepseek-v4-flash. The authors say their analysis does not estimate judge agreement, selector recall or link precision. The scores depend on a judge whose accuracy the paper has not measured.
3. **One run per cell, and a thin Verification layer.** Each of the 36 harness-model cells was run once, so repeatability is not estimated. The Verification component has a single task. The paper's own wording is that harness-criterion pass rates are "operational, not confirmed defect rates."

## The thesis, one more time

Outcome scores grade the agent. The harness needs its own grade. The 31.1% figure is the cost of skipping that step: nearly a third of the runs that looked like wins had a broken layer underneath.

The one insight to keep: **passing the task tells you the agent got there. It does not tell you the harness behaved.**

The action for this week: before you trust an agent unattended, log every tool call, and check that what the model was shown matches what your system says it was shown.

## Now I want to hear from you

1. If 31.1% of successful runs failed a harness check, which of those failures would your current evals have caught, and which would have passed silently?
2. The paper's clean-run rates range from 2.8% to 11.7%. What is your harness's clean rate today, and how would you measure it without a benchmark like this?
3. The judge here is a fixed model with no reported agreement numbers. How many runs would you need to hand-label before you trusted a judge on your own traces?

## References

1. Cao, Z., Zhu, H., Wang, Y., et al. (2026). *Trial by Trace: Benchmarking AI Agent Harnesses for Reliability and Failure Attribution.* arXiv:2610.32285 [cs.AI]. https://arxiv.org/abs/2610.32285
2. TraceLite-AI. *TraceTrial-Bench* [software repository, MIT license]. https://github.com/TraceLite-AI/TraceTrial-Bench

---

**Further reading:** [link to hub article]

If this kind of breakdown is useful, follow along for the daily AI engineering brief. [Newsletter / follow link]
