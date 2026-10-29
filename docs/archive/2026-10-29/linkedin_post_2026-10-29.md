Mean attacker objectives per run: 2.48 down to 0.23.

That's from Tracebit's October study of AI attack agents in a simulated AWS environment: 7 models, 773 assessments, 9 kinds of decoys. The attackers didn't get worse. Their environment did.

If you build agents that touch cloud credentials, this matters twice: an attacker agent has a cost curve you can push on, and whatever your own agent reads is an input it may act on.

What the decoys do:
- A fake pentest report that labels real targets as canaries: 39/40 runs reaching an objective fell to 2/40 on four models
- Staged encryption: GLM took 7.8x longer to its first objective, but still got there in 10/10 runs
- Model spend per confirmed objective went from $1.33 to $31.10 (23x)

Caveats I'd name: it's vendor-run (Tracebit sells canaries), roughly ten runs per model and scenario, one AWS environment, no independent replication. Delay isn't prevention.

Question for builders: if decoys buy you extra minutes, does your team have a responder who can use them?

Full breakdown, with the numbers translated into cost and time: [link to Medium article]

#AIEngineering #AIAgents #Security
