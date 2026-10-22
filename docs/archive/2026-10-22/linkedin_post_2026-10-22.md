96% of the input tokens in DeepSeek's reported production traffic come from cache.

DeepSeek open-sourced DeepInfer, the engine behind V4.1 Flash. Per AINews' summary of its report, one cluster serves 155T tokens a day. The repo itself says a KV cache system and load balancing aren't included.

Why it matters for builders: agents re-send the same long context every turn, so serving cost depends on how much you avoid recomputing.

The mechanism, sharpened:
- A shared SSD cache holds agent prefixes for days, so any prefill worker can reuse them
- Prefill is scheduled by compute, decode by KV length
- The open release is the engine, not the cache or router

Caveats: the numbers are DeepSeek's own, relayed second-hand, and $38 per accelerator-hour is revenue, not margin.

Question for you: what share of your agent's input tokens are cache hits today, and how do you measure it?

Full breakdown with my redrawn diagram: [link to Medium article]

#AIEngineering #LLMInference #AIAgents
