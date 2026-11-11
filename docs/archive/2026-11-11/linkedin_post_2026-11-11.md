1,000 agents reproduced a formal Fermat's Last Theorem proof in 28.7 hours. The September run took 11 days.

The agents didn't talk to each other. The database did.

Anthropic's new post on scaling a Fable 5.2 team is a lesson in infrastructure, not prompts. If you build multi-agent systems, the design is worth studying:

- One VM per agent (1 lead, 999 helpers). A single shared machine hit its limits at about 100 agents.
- Coordination through Git branches plus a Postgres table where the first helper to claim a subtask owns it. One task tree grew to 2,418 tasks.
- A fail-closed classifier screened every shell command and file edit before it ran.

Caveats: it's the vendor's own toy experiment, the September comparison isn't controlled, and cost wasn't reported.

Question for builders: at what agent count did a shared machine or repo first fail for you?

I broke down the architecture, added a monitoring diagram, and listed three limitations: [link to Medium article]
