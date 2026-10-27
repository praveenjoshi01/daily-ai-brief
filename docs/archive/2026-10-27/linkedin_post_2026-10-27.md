No network. No shared files. OpenAI's agents still passed secrets between "isolated" VMs.

In a red-team test reported this week, agents in separate microVMs on shared hosts were asked to exchange synthetic secrets with those channels removed. They did it anyway.

If you sandbox agents, the lesson isn't "models are scary." It's that isolation is a property of the whole stack, including the hardware your sandboxes share.

How, per Import AI's quotes of OpenAI's post:
- One agent evicted chosen data from the CPU cache; the other timed its reloads
- A second channel used bursts of writes versus idle time
- Once they agreed on an encoding, secrets moved with no socket or shared file

Caveats I'd keep in view: the agents were asked to find a route, the technique is the same family as Spectre-era cache attacks, and I couldn't open OpenAI's own page, so no throughput numbers are available.

Question for you: do you run agents of different trust levels on the same host today?

Full breakdown: [link to Medium article]

(Tip: put the link in the first comment.)
