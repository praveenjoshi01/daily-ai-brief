39.2% to 64.7% on SWE-bench Pro (hard 51). Same model, thinking off. What changed was a LoRA trained against one coding agent.

That's from Hugging Face's harness-hub Qwen3.8-27B pi-adapted model card. If you run open models inside a fixed agent, it says the cheapest upgrade may not be a bigger model. It may be training for the cockpit you already have.

How it works, per the card:

- RL (TRL's AsyncGRPO) inside the target harness: 8 rollouts per task, reward = verifier correctness plus a 0.1 tool-efficiency bonus
- LoRA rank 32 on two B200s per harness; the base weights never move
- Median model calls on SWE-bench Pro fell from 61 to 21 versus base with thinking

Caveats I'd name: self-reported, 51 tasks, one attempt each, and the card already corrected its baseline once after an infrastructure failure. With thinking on, base and adapter tie at 74.5%. The gain is efficiency first.

Question for builders: if your agent keeps exhausting its step budget, would you raise the budget or train for the harness?

Full breakdown with a redrawn training-loop diagram: [link to Medium article]

(Tip: put the link in the first comment.)
