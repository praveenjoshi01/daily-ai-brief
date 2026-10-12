AI is writing the code. Nobody planned for who verifies it.

CloudBees surveyed 213 enterprise tech leaders: 67% saw a big jump in code volume, but only 52% saw more shipped features and PRs. AI touches about 61% of the code. 70% say maintaining tests is now harder than writing code. 81% report more production issues from AI-generated code, yet 92% felt confident it was production-ready before shipping.

That is a calibration problem, not a model problem.

The tempting fix is an AI reviewer. It helps (Intercom's review agent auto-approved about 19% of PRs). But Sakana's new MASS paper carries a warning: when one model family plays every role, shared blind spots can get reinforced. If the same lineage writes and reviews your code, it approves the bugs it is most likely to write.

What I'd do Monday:
- Track time-in-review and post-merge defects, not just tokens and PRs opened
- Split review into requirements vs. quality checks
- Use a different model family, static analysis or a human as the independent check
- Widen AI reviewer scope only when acceptance rises and defects don't

One caveat: this is a vendor survey, so treat the percentages as directional. Independent write-ups from LeadDev and CIO describe the same shape.

I wrote up the full argument and the evidence here: [link to Medium article]

Where is your review queue today: keeping up, or quietly turning into a rubber stamp?

#AIEngineering #DeveloperExperience #CodeReview #AIAgents
