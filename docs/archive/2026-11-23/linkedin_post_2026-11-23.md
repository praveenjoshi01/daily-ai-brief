About two million bait prompts. Three inference providers breached. 125 endpoints pulled from Zero Data Retention eligibility.

That's the outcome of Dragos's canary-token research (HD Moore, November 19) and OpenRouter's response on November 22. Some of the stolen requests carried the ZDR flag.

Why it matters if you build with agents: your agent sends whatever is in its context, and a privacy flag only binds the first company that receives it.

How the test works:
- Every prompt carries a unique URL, DNS name, and AWS key that exist nowhere else. Any use means someone read that prompt.
- Each hit maps back to the exact prompt, model, router, and privacy setting.
- Route tracing across about 2,000 paths found several hundred with systems the team could not identify.

Three failure classes came back: attackers inside providers, a lab whose systems fetched links from about two-thirds of ZDR-flagged requests, and marketplace resellers who simply logged what arrived.

Caveats: most providers are unnamed, and a canary only fires when someone uses the secret.

The fix lives in the harness. Pin your upstream providers, limit what agents put in context, and plant your own canary.

Question for you: if a canary key in your agent's context fired tomorrow, who gets paged, and what gets rotated?

Full breakdown: [link to Medium article]

#AIEngineering #LLMOps #AISecurity #Agents
