150–250 ms. $0.10 per million input tokens. Up to 1,000 questions in one request.

Google's Gemini Decision 1 doesn't get smarter. It gets smaller: it scores bounded choices instead of generating text.

If your agent's router, policy check or rubric grader is a generative call, you are paying for output tokens you throw away.

How it works, per Google's launch post:
- One shared multimodal input, billed once
- Yes/no, 2–255-way choice or ordered-rubric score, in a single forward pass
- Every answer carries a 0–1 confidence, so your code can escalate the unsure ones

The catch: the calibration and cost comparisons are Google's own table. A secondary review reports an independent index ranks it about 9th of 18. Test on your labeled cases before trusting either.

Question for you: which step in your agent is a closed-set decision currently handled by a generative call, and what does it cost you per day?

Full breakdown with my redrawn diagram: [link to Medium article]

#AIEngineering #LLM #Agents
