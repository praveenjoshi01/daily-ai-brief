Same model. Up to 5.0x cost gap between coding-agent harnesses.

That's from FrontierHarness Eval v1.1: 27,280 runs, 22 harness configurations, 5 open models, 62 terminal tasks. In the widest case, the pricier harness bought 2.0 extra points of pass rate.

If you're tuning agent costs, the useful part is where the spend actually goes:

- The model explains 92.8% of cost variance, the harness 2.3%. But with the model fixed, harness choice alone moved cost 1.8x to 5.0x.
- Steps per pass track cost. Starting prompt size and tool count didn't.
- 64.5% of spend went to runs that never passed.

The model sets the price list. The harness decides how many times you pay it.

Caveats: open models only, via one provider, and pass-rate intervals of about plus or minus 10 points. Treat the leaderboard as a shortlist.

Question for you: if most spend goes to failed runs, would you accept an agent that gives up earlier?

Full breakdown with my redrawn cost diagram: [link to Medium article]

Source: Runta, FrontierHarness Eval v1.1 (Nov 17, 2026).
