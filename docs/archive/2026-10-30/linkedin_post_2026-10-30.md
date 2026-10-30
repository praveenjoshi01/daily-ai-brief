$5.59 per task vs $11.42. That's what Artificial Analysis measured for GitHub's new Copilot Fusion against Claude Code with Opus 5.5 at max, for an overall score about two points lower.

The model didn't change. The decision about which model runs did.

Why builders should care: picking a model is becoming a runtime decision made by the harness, not a dropdown you manage by hand.

How it works, per GitHub's changelog:
• You choose an effort level (Standard, High, Max), not a model
• Cascade: a cheap model drafts, a quality check accepts or escalates to a stronger one
• Critique: one model drafts, another reviews, the first revises

Caveats I'd flag: AA tested only the Max setting in the CLI, reported no error bars, and Fusion trails by 5 points on FrontierCode even while leading Terminal-Bench 4.0.

Question for you: would you trust a cascade's quality check on your codebase, and what would you need to see in its logs?

I wrote up the full teardown, with my redrawn diagram: [link to Medium article]
