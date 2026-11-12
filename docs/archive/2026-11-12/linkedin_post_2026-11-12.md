6.5 million lines of machine-checked proof. About 26,000 lines you have to trust.

That's the ratio in DeepMind's AlphaProof Code paper, which proved key security properties of Signal's compiled code. Teams of 40 to 80 agents wrote the proofs. Five humans directed the work in four weeks.

The proofs got cheap. The specification didn't.

For anyone running agents on work that matters, the design is the lesson:

- The spec is held out. No agent can write to it, and the gatekeeper checks every proof against that copy.
- A critic agent decides on spec amendments, and it never sees the proof attempts.
- Only the gatekeeper can declare a goal done. The orchestrator and the provers can't.

The authors say most of their effort went into specifications, not proofs.

Caveats: one-to-one sessions only, crypto primitives treated as trusted contracts, and no dollar cost reported.

My question: in your agent workflows, what is the equivalent of the held-out spec, and can the agent write to it today?

Full breakdown with my redrawn diagram: [link to Medium article]

#AIEngineering #AIAgents #FormalVerification
