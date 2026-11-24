# Title options

1. **Epoch's Benchmark Reviews: what an audit found inside the benchmarks you quote every week** *(recommended)*
2. What the leaderboard doesn't tell you about SWE-bench Verified, OSWorld and Terminal-Bench
3. You (probably) trust a benchmark nobody has audited

**Subtitle:** Epoch AI has audited 30 benchmarks and rated 15 of them Flawed. In one, 22 of 50 sampled tasks could be passed without doing the work.

---

If you've picked a model or a harness because it scored three points higher on a coding benchmark, you've trusted two things: the model and the grader. Most of us only ever look at the first. [PRAVEEN: 1-2 sentences, optional: has an eval of your own ever passed something it shouldn't have, or failed correct work?]

Epoch AI has been checking the second. The number I'd keep is **15 of 30**: the share of benchmarks it has reviewed so far and rated Flawed. Six are Verified. Nine could not be reviewed at all.

A score is a claim about the grader first and the model second.

## Where to find it

Epoch AI's Benchmark Reviews: a list of 30 verdicts dated August 10 to November 11, 2026, a public rubric (v1), and a review page per benchmark. The newsletter AINews flagged the two most recent agent reviews on November 24. The Agents' Last Exam team has published a rebuttal, which I use below.

## What this post covers

- **The problem:** why a benchmark's grader fails in two directions
- **How the audit works:** five steps, from access check to verdict
- **The diagram:** my redrawn version, with the step Epoch leaves out
- **The bridge:** a benchmark is a test suite
- **What the evidence says:** four reviews, ranked by what they change
- **Three limitations,** including two in the source itself
- **What to do this week**

## The problem it solves

A grader can be wrong in two ways. It can pass work that wasn't done, which is a false positive. It can also reject work that was correct, which is a false negative. The first inflates scores and the second deflates them, and a leaderboard shows you neither.

Epoch's list includes the benchmarks most of us cite. SWE-bench Verified, SWE-Bench Pro, DeepSWE v1.1, Terminal-Bench 4.0.0, OSWorld 2.1 and Humanity's Last Exam are all rated Flawed.

**Takeaway:** the benchmarks you quote most are on the Flawed list.

## How it works

### Step 1. The access check

Epoch first asks whether the tasks, the scoring code and the harness settings can be inspected. If they can't, the review stops with a verdict of "Not enough info." Nine benchmarks ended there, including FrontierCode 2.0 and CursorBench 4.0. The design choice I like is that a private benchmark doesn't get the benefit of the doubt.

### Step 2. The sample

For benchmarks with more than 50 tasks, Epoch draws 50, spread across categories. If the error rate lands between 15% and 25%, the sample grows to 100. That spends review effort on the borderline cases.

### Step 3. Flag, then try to disprove

In the Agents' Last Exam review, Claude Opus 5.5 ran one subagent per task to look for errors. Separate Claude instances then tried to disprove each finding by rereading the grader code and, where feasible, running it on a shortcut answer. Humans reviewed every task that was still flagged. The second pass is the interesting part, because its only job is to knock findings down.

### Step 4. The threshold

A benchmark is Flawed when errors affect at least 20% of the score in the sample, or when one defect corrupts grading at scale. Three other checks can also fail it: silent changes between versions, setups that hold models back, and conditions that favour one provider.

### Step 5. The stop

Once errors pass the threshold, Epoch stops inspecting. That makes each review cheaper, and it makes each error count a lower bound.

**Takeaway:** the audit runs like an agent pipeline, with a verifier whose job is to disagree.

## The diagram

![Epoch's review pipeline, redrawn: an access check, a sample of 50 tasks, an AI pass that flags errors, a second pass that tries to disprove them, human review, and a 20% threshold that leads to a Flawed or Verified verdict. My version adds a final step, taken from the Agents' Last Exam team's response: checking recorded runs to see whether agents actually took the shortcuts.](diagram_2026-11-24.png)

*My version adds the step on the right. Epoch asks whether a shortcut exists. The benchmark's own team asked whether any agent took it.*

## The bridge

A benchmark is a test suite, and Epoch is auditing the tests.

- A false positive is a test that passes whatever you submit.
- A false negative is a flaky test that fails good code.
- The 20% threshold is the point where you stop trusting the suite.

## What the evidence says

Ranked by how much each should change your reading of a score:

1. **OSWorld 2.1: graders rejecting correct work.** Errors appeared in 36 of 50 sampled tasks, with 24 false negatives against 12 false positives. One grader marked a correct entry wrong because the answer key used a shorter name. Epoch estimates GPT-6 Astra lost about 20.8% of its score on affected tasks. Consequence: a low score may be the grader's fault.
2. **Vending-Bench 2: the harness treats providers differently.** The harness silently discarded 238 of Opus's tool calls. With a larger context window and auto-compaction, Astra's balance rose 17% in one run, enough to place it first. Consequence: the ranking partly measures the harness.
3. **Agents' Last Exam v1.1: tasks that pass without the work.** 22 of 50 sampled tasks could earn full marks through a shortcut. Nine had public answers, eight had lax graders, and five let the agent tamper with the grader. In one, a three-line script that prints a perfect score passes.
4. **Humanity's Last Exam: broken questions.** 22 of 48 sampled questions had errors that change accuracy. Twelve could not be answered correctly as written.

The rebuttal matters here. The Agents' Last Exam team checked its recorded runs and found that 3 of 1,617 took a flagged shortcut, or 0.19%. It also says the grader is uploaded only after the agent's session ends, so there is nothing to tamper with during a run. The team did concede one gap: on two tasks, agents looked up the answer in 51 of 166 runs, and a fix that enforces network isolation is on the way.

**Takeaway:** a shortcut that exists is different from a shortcut agents take, and you need both numbers.

## Limitations I'd name

1. **The reviews are partial by design.** Epoch stops at the threshold, so a 44% and a 46% are lower bounds from different stopping points. I wouldn't use them to rank benchmarks against each other.
2. **The label is binary.** "Flawed" covers a benchmark where agents almost never take the shortcut and one where errors could affect up to half the sampled score. Epoch tells developers at least one day before publishing and doesn't wait for fixes.
3. **A model helps audit the model benchmarks.** Epoch used Claude Opus 5.5 to flag errors in benchmarks that rank Claude against its rivals. Humans verify each finding, but the pages I read don't say how errors the model missed get caught.

## Closing

A score is a claim about the grader first and the model second. What I'd keep is that a few points of gap between two models can be smaller than the error in the grading.

This week, take 50 tasks from your own eval set and ask two questions of each: can it pass without the work, and can correct work fail? Then check your traces to see whether either has happened.

## Now I want to hear from you

1. Which matters more to you: that a shortcut exists in 22 of 50 tasks, or that 3 of 1,617 runs took one?
2. Has your own eval ever rejected a correct answer over wording, like the OSWorld grader did?
3. Would you still quote a benchmark rated "Not enough info" because its tasks are private?

## References

1. Epoch AI, "Benchmark Reviews: Included benchmarks," accessed November 24, 2026. https://epoch.ai/data/benchmark-reviews-documentation/included-benchmarks
2. Epoch AI, "Benchmark Reviews: Methodology (Rubric v1)." https://epoch.ai/data/benchmark-reviews-documentation/methodology
3. Epoch AI, "Benchmark Reviews: FAQ." https://epoch.ai/data/benchmark-reviews-documentation/faq
4. Epoch AI, "Benchmark Review: Agents' Last Exam v1.1," October 18, 2026. https://epoch.ai/benchmarks/agents-last-exam/review
5. Epoch AI, "Benchmark Review: Vending-Bench 2," October 21, 2026. https://epoch.ai/benchmarks/vending-bench-2/review
6. Epoch AI, "Benchmark Review: OSWorld 2.1," September 28, 2026. https://epoch.ai/benchmarks/osworld-2-1/review
7. Epoch AI, "Benchmark Review: Humanity's Last Exam," August 11, 2026. https://epoch.ai/benchmarks/hle/review
8. Agents' Last Exam team, response to Epoch AI's verifier check (undated). https://agents-last-exam.org/blogs/verifier-check

---

**Further reading:** [link to hub article]

If this was useful, follow me for one grounded AI engineering deep-dive a day.
