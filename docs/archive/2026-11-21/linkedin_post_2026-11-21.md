3.66x to 18.92x. Same model, same two hours. The only change: 32 agents instead of one.

That's Replit's new Optimization-Bench study on NumPy with Claude Opus 5.5. The more useful finding is the other one: GPT-6.2 Astra had the best solo run on every task, and at 32 agents it fell below its own solo score on 3 of 4 libraries.

If you're scaling agents, the solo leaderboard won't tell you who wins as a team.

What separated them, per Replit:

- Opus swarms put 82% of messages on a shared board, with per-workload threads and file claims
- Astra workers sent about 15 direct messages each to the coordinator, which became a switchboard
- Separable work scaled (NumPy); shared files didn't (Git's 7 workloads touch the same 15 files)

Caveats: Replit's own benchmark, 4 of 14 libraries discussed, no cost or total-compute numbers.

Question for builders: in your multi-agent setups, does work flow through a shared log or through a coordinator's inbox, and did you pick that or did the model?

Full breakdown with a redrawn topology diagram: [link to Medium article]

(Tip: put the link in the first comment.)
