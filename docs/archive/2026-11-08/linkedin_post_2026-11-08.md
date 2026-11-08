Google says agents spend 90-95% of their time waiting. Scale-to-zero then costs 20+ seconds to wake them. Agent Substrate targets under 500 ms.

The model didn't get faster. The Pod stopped being the unit of an agent.

If you run agents in production, this changes the cost question: it isn't compute per second, it's compute held while the agent waits on a tool call or a human.

How it works, in short:
- An "Actor" holds the session's memory, files and identity
- A pre-warmed "Worker" sandbox (gVisor or a microVM) is borrowed per turn, then freed
- A gateway injects credentials at egress, so the agent never holds the key

Caveats I put in the article: every number (500 ms, 10x density, 500+ activations/s) is Google-reported with no published methodology, and the GA story differs between two Google posts.

I also wrote about why snapshot-restore deserves a security review, using this week's Firecracker CVE-2026-122192 as the example.

Question for you: what share of your agent sessions' wall-clock time is actually idle?

Full breakdown with a redrawn diagram: [link to Medium article]

#AIEngineering #Kubernetes #AIAgents
