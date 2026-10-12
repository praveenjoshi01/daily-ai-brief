# Your Model Isn't the Bottleneck Anymore. Your Merge Queue Is.

Here is a number that should change how you plan your next quarter: according to CloudBees' State of Code Abundance survey, 67% of enterprise technology leaders saw a significant increase in code volume over the past year, but only 52% saw higher output in the form of shipped features and pull requests. The code is piling up faster than it is turning into product.

That gap is the most useful story I read this week, and it is the one I think AI engineers should be talking about, because it describes a problem our own tools created and our own tools are not yet solving.

## What the data says

CloudBees surveyed 213 IT leaders and published the results in May 2026. DevOps.com covered the findings, and CloudBees' own event recap lays out the headline figures. AI writes or assists with about 61% of the average enterprise codebase. Yet 70% of respondents say maintaining their test suite is now a heavier burden than writing code. More leaders now name the post-code stages (review, testing, deployment) as their main bottleneck. Costs followed: 54% reported a significant rise in CI/CD infrastructure spend.

Then there is the trust paradox. 93% report productivity gains, and 81% report more production issues tied to AI-generated code. Meanwhile 92% said they were confident the code was production-ready before it shipped. Both can be true at once only if confidence is not being calibrated against outcomes.

The governance numbers are thin. Only 12% of organizations have a dedicated AI governance team, and when something breaks, 46% say responsibility defaults to the CTO or VP of Engineering. Only 31% can tie AI spend to specific business outcomes.

A caution on provenance: this is one vendor's survey, and the vendor sells delivery tooling. Treat the specific percentages as directional. What gives me more confidence is that independent voices describe the same shape. A LeadDev piece published this week cites the CloudBees survey and reports that 57% of respondents named reviewing, testing and deploying as the delivery bottleneck against 35% who named writing code. (LeadDev dates that survey to September while CloudBees' own materials date the report to May, so I am relying on CloudBees' dates.) A CIO essay from August by Vittesh Sahni, a senior director of AI engineering at Coherent Solutions, argues that AI has moved the bottleneck from generation to review, and cites GitHub's Octoverse 2025 figure of 43.2 million pull requests merged per month, up 23% year over year.

## Why this is an engineering problem, not a management one

It is tempting to read this as a process story for engineering managers. I think it is more specific than that. It is an architecture story.

When generation was the scarce resource, we optimized for generation: better prompts, better models, better autocomplete. Review was a human activity that scaled linearly with team size, and that was fine because humans were also the ones writing code. Now one engineer with an agent can open several pull requests an hour, and the reviewer pool did not grow. Sahni notes that AI-authored diffs tend to be larger, and that reviewers who skim large diffs focus on style and miss security and correctness problems. That matches what I see: the failure mode is not that review disappears, it is that review quietly degrades into a rubber stamp.

The data on trust points the same direction. Sahni cites the Stack Overflow 2025 developer survey, where developer trust in AI output fell from 40% to 29% and 66% described the output as "almost right, but not quite." Almost right is the most expensive kind of wrong, because it passes a glance and fails in production.

## The obvious fix has a catch

The obvious response is to point AI at review. Some teams are making it work. CloudBees' recap mentions that at Intercom, a PR review agent auto-approved 19.2% of pull requests. Sahni reports, anecdotally, that agent findings in his pilots start at roughly 35-40% acceptance and climb past 60% as context improves.

I am for this, with one structural warning, and it comes from an unrelated source. Sakana AI published a project this week called MASS, where a single open-weights 27B model acts as solver, workflow optimizer and evaluator, then trains on its own best results. The numbers are interesting (win rate on three held-out synthetic tasks rose from 53.9% to 69.9% after two rounds), but the passage that stuck with me is the authors' own caveat: when one model family plays every role, shared blind spots can be reinforced across updates, so self-evaluation needs independent checks.

Apply that to code review. If the same model family writes the code and reviews it, the reviewer shares the author's blind spots. The bugs a model is likely to write are exactly the bugs it is likely to approve. An AI reviewer from the same lineage as your coding agent is closer to a spell checker for your own typos than to a second pair of eyes.

Satya Nadella made a related argument in a post covered by The Decoder on October 11. He argues for treating AI models like insider threats, separating intelligence from control, using multiple models rather than one, logging every action, auditing independently, and keeping a human off-switch. The Decoder rightly points out that Microsoft has competitive reasons to say this. The engineering content stands on its own regardless of motive: the most trustworthy system is the one that requires the least trust in any single model.

## What I would do on Monday

Based on the evidence above, here is how I would change my team's setup.

**1. Measure the review queue, not just generation.** Track time-in-review, diff size, and post-merge defect rate alongside tokens used and PRs opened. CloudBees found 36% of organizations track AI spend with no ROI measurement at all. Don't be in that group.

**2. Split review into separate jobs.** Sahni's suggestion is to separate a requirements check (did we build what the ticket asked?) from a quality check (security, error handling, architecture, tests), with findings limited to changed lines. Different questions deserve different checkers, and a single comment thread sorted by type is easier to act on.

**3. Diversify the reviewer.** Use a different model family, a static analysis tool, or a human for the checks where correlated errors would hurt most. Independence matters more than raw capability here.

**4. Expand autonomy only on evidence.** Sahni's rule is a good one: increase the AI reviewer's scope only when the acceptance rate rises and the post-merge defect rate holds flat or falls. If only one of those moves, treat it as a warning.

**5. Put verification in the budget.** LeadDev's piece recommends including review, dependency control, sandboxing and auditability costs in the strategy from the start and keeping an assumption register for major bets, with a signal and an owner for each. I would add test maintenance to that list, given the 70% figure.

## My prediction

Within a year, the differentiating skill for AI engineers will not be getting an agent to write a feature. That is becoming table stakes. It will be designing the verification layer: the tests, sandboxes, independent reviewers and audit trails that let you trust code you did not write and did not fully read.

The teams that treat the merge queue as a first-class system, instrumented and budgeted like production infrastructure, will convert code volume into shipped product. The teams that keep measuring tokens and pull requests opened will keep seeing the gap in the CloudBees numbers widen: 67% more code, 52% more output, and a growing pile of almost-right changes waiting for someone to look at them.

If your dashboard shows how fast you generate code but not how fast you can trust it, you are watching the wrong gauge.

---
*Sources: CloudBees State of Code Abundance 2026 (event recap and DevOps.com coverage, May 2026); LeadDev (Oct 2026); CIO, "The code review crisis" (Aug 11, 2026); Sakana AI, MASS project page; The Decoder (Oct 11, 2026).*
