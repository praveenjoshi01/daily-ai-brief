Same loss as MXFP8 training for about 2% extra compute, with a 4-bit forward pass.

That's the claim in Thinking Machines' new post on training Inkling 2 Small. NVIDIA's earlier work found that fully NVFP4 models diverge, so the format wasn't the breakthrough. The recipe was.

For builders: low-precision training is an allocation problem. You decide where error is cheap and where it compounds.

The mechanism, sharpest form:
- Forward pass of the MoE experts runs in NVFP4. Backward pass stays in MXFP8 with stochastic rounding, because noise averages out but bias accumulates.
- A 32-dim Hadamard transform plus an 8-bit format cuts combine communication from 16 to 8.25 bits per value.
- Reported gains in the largest jobs: about 8% faster pretraining, 20% faster RL versus MXFP8.

Caveats: lab's own results, no downstream benchmarks in the post, and the backward pass is not 4-bit yet.

Question for you: where in your stack does bias accumulate while noise averages out?

Full write-up with a redrawn diagram: [link to Medium article]

#AIEngineering #MLSystems #LLMTraining
