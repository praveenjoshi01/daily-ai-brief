100+ organizations are working with NVIDIA's Open Agent Safety Platform. The part you can run today is an Apache 2.0 runtime, OpenShell, and its design is the lesson.

Don't ask the agent to behave. Build the room so misbehaving isn't possible.

Why this matters to builders: prompt-level rules are requests. A compromised or confused agent can ignore them. Rules enforced outside the agent can't be argued with.

The mechanism, sharply:
- Deny by default, with policy over files, network and processes, checked per binary, destination, method and path
- Agents never hold real credentials; they're added only for approved endpoints (per the README)
- The agent can propose a policy change, but a human approves it

Caveat I'd name: the sources publish no effectiveness benchmarks, and the claim that it could have stopped the Hugging Face breach is hedged by NVIDIA's own executive. Treat it as a reference architecture, not a guarantee.

A question for you: which action would you put behind human approval first, credential use, new network hosts, or file writes outside a workspace?

Full breakdown with a redrawn diagram: [link to Medium article]
