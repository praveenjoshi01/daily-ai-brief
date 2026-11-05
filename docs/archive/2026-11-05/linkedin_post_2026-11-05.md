0.016% of a model's weights edited. MATH-500 from 7.9% to 48.1%.

The model didn't learn more math. It stopped repeating itself.

MIT CSAIL researchers had GPT-6 Astra patch Qwen3.5-0.8B directly, with no gradient training. It's a real result, and the headline oversells it.

If you build with small models, here is what matters:

• The fix removed a repetition direction in two layers. Responses hitting the token limit fell from 93.0% to 33.1%.
• It wasn't "just reading raw weights." Astra had Python and ran the model on practice batches. The strongest attempt took 158 turns and 20.3 hours.
• It failed to help Gemma 3 270M, which rarely loops. Editing removes obstacles; it doesn't add abilities.

The capability lives in the loop around the edit, not in the weights.

Question for you: how much of your own eval gap is truncation and loops rather than wrong answers?

Full breakdown with my redrawn diagram and three limitations: [link to Medium article]

#AIEngineering #LLM #AppliedML
