OpenAI says Codex stops for human approval about 200x less often with Auto-review. A red-team just found 11 ways around it.

The surprise: the approver model wasn't the weak point.

If you're letting a model decide what your coding agent may run, the weak points are the seams around it:
- Persistent trust rules on scripts and hooks. Swap the contents later and the trust still holds.
- Agent-written text that reads like a user turn, so it carries user-level authority.
- Time-of-check vs time-of-use: approval reflects the state at review time, not at execution.

Caveats worth stating: the attacks were hand-written, replayed against one pinned commit, and the per-attack success rates are only in a private report. OpenAI says it has fixed several, and calls Auto-review a compromise, not a guarantee.

My takeaway: an approver model is a smoke detector, not a deadbolt. Put the deterministic controls where the model can't be argued with.

A question for you: which allow rules in your agent setup execute code you don't control, and would you notice if one of those files changed?

Full breakdown with a redrawn control-flow diagram: [link to Medium article]
