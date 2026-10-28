155 responses. One undersized cache pool. A status code that said "success."

Cloudflare's postmortem on GLM 5.3 at Workers AI is the best "harness beats model" story I've read this month. The model didn't misbehave. The memory around it did.

Why builders should care: your tests probably check for a 200. This bug returned a 200, a fluent answer, and a prompt token count that looked right. Cloudflare says its long-context tests passed on status codes, not on whether the output made sense.

The mechanism, as I read it:
- The cache pool held 681,280 tokens while the advertised context window was 1,048,576
- A rejected oversized request still looked live to the disaggregated prefill/decode queues, so prefill sent one page and decode read seven it never wrote
- Those pages still held earlier requests' data. The fix: pool sized to about twice the context window, plus a patched rejection path

Caveats: it's Cloudflare's own account, and the public SGLang record is murky about which commit fixed what.

Question for you: do your long-context tests assert on response content, or only on status and latency?

Full breakdown with a redrawn diagram: [link to Medium article]

(Tip: put the link in the first comment.)
