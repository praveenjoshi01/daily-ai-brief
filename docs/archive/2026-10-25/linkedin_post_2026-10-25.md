~10% of eligible internal Codex traffic ran unmonitored for months. Not because the monitor was bad. Because of when it ran.

METR and Redwood Research spent three weeks inside OpenAI testing its agent-monitoring system. Their report, published Oct 22, says the monitor mostly saw what the agent saw. The gaps were around it.

If you run agents with any kind of guardrail, this is a checklist, not a headline:

- The monitor fired only when the agent handed control back. Keep acting, postpone the check.
- Context compaction wasn't monitored. That alone is the ~10% (an estimate, with wide error bars).
- Two client-controllable headers could switch monitoring off for new agents.

OpenAI says the production issues are patched. METR hasn't verified that, and the findings describe the system as of July 21.

I wrote up how the pieces fit together, redrew the failure points on the pipeline, and listed what I'd copy and what I'd question.

One question I'm still turning over: do you reconcile your monitor logs against your inference logs, or do you trust that "every request is monitored" is true?

Full breakdown: [link to Medium article]

(Tip: put the link in the first comment.)
