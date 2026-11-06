Median time to first token fell about 35% for 500k–1M token requests. Token usage didn't change.

The model didn't get faster. The request got smaller.

Anthropic's new "message threads" (public beta, Nov 2) stops long agent sessions from re-sending the whole conversation every turn. If you run coding or computer-use agents, this is where latency actually hides.

How it works:

• First request sends the full conversation and starts a thread.
• Every later request sends only the new messages plus the previous response ID.
• Threads expire after 5 minutes idle, so your app must keep its own history and be able to replay it.

Caveats worth knowing: the 35% is Anthropic's own median from Claude Code usage, in one context-size bucket. Claude still reads everything each turn, so you save time, not money.

Question for builders: if a thread expired mid-task, would your harness recover silently or fail loudly?

Full breakdown, with a diagram of the replay path: [link to Medium article]

(Tip: put the link in the first comment.)

#AIEngineering #LLM #AIAgents
