One fake policy took a prompt-injection classifier from catching 82.9% of attacks to catching 3.9%.

That's Datadog's result on Jev, a small structured-output model, across 4,643 attack samples. The classifier didn't get worse. The attacker's text was allowed to talk to the judge.

Why it matters if you gate agent tool calls with a model: the text you're judging is written by the person you're judging.

How it works, in three lines:
- Prepend a fabricated "policy" to the attack that dictates the verdict and redefines every attack category as harmless
- In a tool-gating test, the risk score fell from 0.893 to 0.290 (block threshold: 0.5) using only a user-editable profile field
- Plain "fake system message" injections barely moved the score, so a basic red team would have missed it

Caveats: the attack is hand-built for Jev, and it measures flagging, not full agent compromise. Lasso and HiddenLayer report weaknesses too, but Lasso sells a competing product.

My takeaway: keep the hard permission check outside the model, and treat the classifier as a second opinion.

Question for you: which user-controlled fields reach your classifier's prompt today?

Full breakdown with diagram: [link to Medium article]

#AIEngineering #AgentSecurity #PromptInjection
