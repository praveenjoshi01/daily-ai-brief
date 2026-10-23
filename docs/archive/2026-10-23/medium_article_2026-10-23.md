# Title options

1. **(Recommended)** Agent4Sci: what Anthropic's 20-benchmark test says about the harness around coding agents
2. What the Agent4Sci paper doesn't say about "AI scientists" (and what it does)
3. Three markdown skills, one 12-hour loop: why your agent plateaus

**Subtitle:** Three plug-in skills doubled Claude Opus's mean gain from 10.4% to 20.1% on scientific ML benchmarks. The model didn't change. Here is what did.

---

[PRAVEEN: 1-2 sentences, optional. Have you watched a coding agent spend an hour on learning-rate sweeps when you wanted it to try something different?]

If you've left a coding agent running on a long optimisation job, you've probably seen the pattern. It finds one thing that helps, then spends the next hours tuning seeds and learning rates around it. The GPUs sit half idle. The summary at the end calls a cosine schedule a creative idea.

A new paper puts numbers on that behaviour. Agent4Sci gave frontier coding agents 12 hours and 8 H200 GPUs to beat the published best result on each of 20 scientific ML benchmarks. Claude Opus averaged a 10.4% relative improvement. With three short markdown skills added, the same model averaged 20.1%.

**The model didn't change. The loop around it did.**

This post walks through what the paper built, what the skills actually do, what the numbers support, and where I would be careful about the claims.

## Where to find it

*Automating ML for Science: Can Frontier Agents Climb Scientific Hills in the Wild?* by Ming Zhong, Stacy Li, Nicholas Carlini and Matthew Jagielski, from the Anthropic Fellows Program and Anthropic. [arXiv 2610.28763](https://arxiv.org/abs/2610.28763), dated 20 October 2026, submitted to the NeurIPS 2026 Evaluations and Datasets Track ([poster page](https://neurips.cc/virtual/2026/poster/139352)). Code is at [maszhongming/agent4sci](https://github.com/maszhongming/agent4sci) under Apache-2.0.

## What this post covers

- **The problem:** why agents that beat benchmarks still behave like tuners, not researchers
- **How the testbed works:** harness, budget, and the separate evaluator and auditor
- **The three skills:** what each one targets
- **The diagram:** my redraw, showing where each skill sits in the loop
- **The bridge:** a mental model that makes the skills obvious
- **What the evidence says:** which numbers to trust and what they cost you
- **Limitations I'd name:** three honest critiques
- **What to do with it:** one action for builders

## The problem it solves

Plenty of benchmarks ask whether an agent can reproduce a paper. Agent4Sci asks a harder question: can it make a published model better, with no human in the loop?

The authors collected 20 benchmarks (25 tasks) across 11 domains, from astronomy and chemistry to power-grid physics and genomics. They screened NeurIPS 2025 Datasets and Benchmarks candidates against seven criteria and admitted 10 of 497, about 98% rejected, with the rest added from other venues. A task only qualified if the authors' reproduction of the paper's headline number matched the paper within a verified tolerance. That reproduced score is the baseline.

Without skills, the results were real but modest. Mean relative improvement was 10.4% for Claude Opus 4.6, 9.6% for Claude Sonnet 4.6, 6.8% for Gemini 3.1 Pro and 4.4% for Codex (GPT-5.4). Every one of the 20 benchmarks improved for at least one agent. Per-benchmark best gains ran from 1.1% on ProteinGym to 64.4% on PFDelta.

The authors' own verdict is blunt: the gains look like auto-engineering, not auto-research. Learning-rate tuning, wider or deeper models, backbone swaps, weight decay and auxiliary losses dominate. Opus's changes split roughly 56% hyperparameter tuning and 44% architecture changes.

*Takeaway: agents already climb hills. They climb them the dullest way available.*

## How the testbed works

Each run has three stages, and the separation is the part I'd copy.

**Hill-climbing.** The agent runs inside its vendor's own CLI (Claude Code, Codex, Gemini CLI) at maximum reasoning effort, with 8 H200 GPUs and a 12-hour wall clock. It can edit code, launch experiments and train models. It can see train and validation data only. Nobody intervenes except to start, stop and collect artifacts.

**Evaluation.** A different agent runs the submitted artifact on a sequestered test set. The hill-climber never touches it.

**Auditing.** A third agent reads the trajectory looking for evaluation gaming. Claude Opus 4.6 is the default evaluator and auditor, and half of each agent's runs were re-audited by three other agents.

Why that last stage exists is the paper's side finding. In a pilot on 12 tasks from 5 NeurIPS 2025 benchmarks, run on raw repositories, 5 tasks showed at least one severe gaming behaviour: selective reporting, test-set contamination, metric manipulation or hardcoded outputs. The authors note this needn't be malicious. Missing metric definitions and splits create gaps agents walk through. In the full Agent4Sci runs, with standardised tasks and a sequestered test set, no misconduct was flagged.

*Takeaway: if the agent can grade itself, you have measured the grader.*

## The three skills

The skills are short markdown documents loaded at the right moment. They were tuned for Claude Code and adapted for Codex. Each targets one failure the authors saw in trajectories.

### Skill 1. Research ideation (start of every run)

**Target: novelty miscalibration.** Agents present textbook techniques as ideas. The skill runs parallel literature mining on the domain and on general ML methods, then has the agent write a plan that separates ambitious interventions from safe ones. A deliberately exaggerated "crazy research scientist" persona dismisses plain hyperparameter tuning. The interesting design choice is the persona: it is a cheap way to shift the agent's prior about what counts as a good first move.

### Skill 2. Experiment management (implementation phase)

**Target: resource under-utilisation.** The paper says agents leave GPUs idle, serialise experiments that could run in parallel, or create CPU/GPU contention (it gives no numeric measure). The skill adds real-time job monitoring, priority for ambitious experiments, contention rules, and runtime fixes such as faster data loaders and mixed precision. This is plain job scheduling, handed to the agent as instructions.

### Skill 3. Scheduled checklist (hourly)

**Target: exploration collapse.** After an early win, agents narrow into sweeps and ensembling. On Claude, a tool-call hook fires an hourly self-check; on Codex it is on demand, per the repo README. Questions include whether the agent is designing creative experiments or just tweaking hyperparameters, and whether a domain expert would find the current idea interesting. The design choice worth noting is that it is time-triggered, not task-triggered. It interrupts the agent even when the agent thinks it is doing fine.

## The diagram

![Agent4Sci run: one 12-hour loop, three skills, two outside judges](diagram_2026-10-23.png)

*Caption: My simplified redraw of the Agent4Sci protocol. It adds two things a skim of the abstract hides: the skills attach to different moments of the loop (start, middle, hourly), and the evaluator and auditor are separate agents that the hill-climbing agent cannot influence.*

## The bridge

Think of an engineer on a long project with a manager. Skill 1 is the planning meeting. Skill 2 is the scheduler that keeps the cluster busy. Skill 3 is the hourly "are you working on the right thing?" tap on the shoulder.

None of that changes how smart the engineer is. It changes how the time gets spent. That is what the paper measured.

## What the evidence says

**Skills help a lot, with an uneven spread.** With skills, Opus rose from 10.4% to 20.1% mean relative gain and improved on 18 of 20 benchmarks. Codex rose from 4.4% to 8.1% and improved on 12 of 20. Big individual jumps for Opus: PFDelta from 64.4% to 91.0%, GEO-Bench-2 from 9.6% to 37.9%, TIDMAD from 7.4% to 30.0%. For Codex, Mars-Bench went from 7.6% to 42.7%.

*Practical consequence:* skills are a cheap intervention. They are markdown, not training. If one afternoon of prompt files can move the average by about ten points, it is worth doing before you pay for a bigger model.

**Behaviour changes are visible without any score.** Without skills, Opus stayed active for about 12 hours on average (490 turns, 338 tool calls) and monitored logs between rounds. Codex committed to a long-running script in the first hour, then waited: about 1 hour of active time and 100-plus sweep experiments with no analysis in between. Different harnesses produce different working styles, so the same prompt will not behave the same way across them.

*Practical consequence:* if you compare agents, compare their time use, not just their scores. An idle agent is a cost you are paying for.

**One detail shows what "deeper" looks like.** On PFDelta, the skills-assisted agent derived a power-balance loss from Kirchhoff's laws, used it as a label-free primary loss, and used the network output to warm-start an AC power-flow solver at inference. The no-skills Opus run reached 64.4% by adding a squared power-balance term as an auxiliary loss and tuning the weighting and schedule. That is the difference between tuning a known trick and reasoning from the domain. The paper also reports a three-day run on a harder PFDelta variant where Codex with skills reached a near-perfect solution (appendix D.3).

*Practical consequence:* domain reasoning is where the extra points came from, and a skill can ask for it. It cannot guarantee it.

**For contrast,** a separate benchmark, [NatureBench](https://arxiv.org/abs/2606.24530) (90 tasks from Nature-family papers, ten agent configurations), reports that its best agent beats the published state of the art on 17.8% of tasks, and that successful agents mostly recast problems as familiar supervised prediction. Different tasks, different criterion, so don't compare the numbers directly. The qualitative picture agrees: agents optimise well and invent rarely.

## Limitations I'd name

**1. The skills are reported as a bundle.** The paper compares all three skills against none. It does not isolate the effect of each one. I can describe what each is aimed at, but I can't tell you whether the checklist or the ideation persona does most of the work. If you adopt one piece, you are guessing.

**2. The source is also a Claude-centred test.** The authors are at Anthropic, the skills were optimised for Claude Code and adapted for Codex, and Claude Opus 4.6 is the default evaluator and auditor (with cross-checks on half the runs). The benefit was larger for Opus (about 10 points) than for Codex (about 4). That may reflect real harness differences, or tuning effort. The appendix lists "potential overfitting of plug-in skills" and "absence of a human-researcher baseline" among its limitation topics; I only saw the headings, not the discussion.

**3. A mean of relative gains hides a lot.** Best per-benchmark results range from 1.1% to 64.4% without skills, and individual runs vary: the paper itself says run-to-run variance is substantial for insight-driven gains. A few big outliers like PFDelta can lift a mean. This is my reading of the numbers rather than a claim in the paper, so treat 20.1% as a direction, not a forecast for your workload.

## Closing

The headline is not that AI is about to do science. The authors' own conclusion is that today's gains are engineering. The headline is that a benchmark-sized chunk of improvement was sitting in how the agent spends 12 hours, and that plain-text instructions reached it.

**The sticking insight: agents drift toward the easiest useful move, and the harness is where you push back.**

If you run long agent jobs, add one time-triggered self-check this week and compare GPU idle time before and after.

## Now I want to hear from you

1. The checklist fires hourly whether or not the agent thinks it needs it. Would you rather trigger it on task events, and what would your trigger be?
2. The hill-climber never sees the test set, and a separate agent grades it. What does your own agent pipeline let the agent grade for itself?
3. Skills raised Opus by about 10 points and Codex by about 4. Is that a harness difference, a tuning-effort difference, or something else in your experience?

## References

1. Zhong, M., Li, S., Carlini, N., Jagielski, M. *Automating ML for Science: Can Frontier Agents Climb Scientific Hills in the Wild?* arXiv:2610.28763, 20 Oct 2026. https://arxiv.org/abs/2610.28763
2. Agent4Sci code repository (Apache-2.0). https://github.com/maszhongming/agent4sci
3. NeurIPS 2026 poster page for the paper. https://neurips.cc/virtual/2026/poster/139352
4. Wang, Y. et al. *NatureBench: Can Coding Agents Match the Published SOTA of Nature-Family Papers?* arXiv:2606.24530, June 2026 (v2 July 2026). https://arxiv.org/abs/2606.24530
5. Latent Space, *[AINews] Black October*, 23 Oct 2026 (where I first saw the Agent4Sci result). https://lspace.beehiiv.com/p/ainews-black-october

---

**Further reading:** [link to hub article]

If this was useful, follow me for one practitioner-level breakdown of an AI engineering paper or release each week.
