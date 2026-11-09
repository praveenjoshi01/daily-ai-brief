At 10M tokens, choosing which keys to read took ~98% of one attention layer's prefill time. A new paper (Latent Sparse Attention, arXiv 2610.42147) reports a 22.7x faster prefill for that layer.

The attention kernel didn't change. The index did.

For anyone building long-running agents: once attention is sparse, the selector becomes the bottleneck, so latency is decided by the system around the model.

How it works, in short:
- Keys are clustered by content (Ward's method, ~8 keys per bucket) and never re-clustered
- A query scores cluster centroids, not every key; a tree variant needs only ~log T centroid scores
- Selected clusters expand to keys, plus sink tokens and a recent window, then normal attention runs

Caveats I put in the article: the 72x headline compares against full attention on a different model; end-to-end first-token gains are 2.2x (GLM) and 9.2x (Qwen vs full attention); on GLM it trails its baseline by up to 8 RULER points at 2M-5M tokens; and the KV cache still grows linearly.

Question for you: would you trade a few long-context accuracy points for a 2x faster first token?

Full breakdown with a redrawn diagram: [link to Medium article]

#AIEngineering #LLM #AIAgents #MachineLearning
