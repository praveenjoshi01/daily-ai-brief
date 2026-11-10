A wiki-based agent memory went from 13% to 48% of graded criteria over 128 "dreaming" sessions, and still trailed plain search (53%).

The model didn't change. The system that maintains its memory did.

Anthropic's Nov 6 engineering post on agent memory is worth reading if you build agents. The result that matters for builders: a wiki plus search scored 61% and saved about 20,000 tokens per question.

The mechanism in its sharpest form:
- Transcripts are ground truth; notes are just claims about them
- Dreaming is an offline pass that re-reads transcripts, fixes wrong notes and rebuilds wiki pages
- Sharding by task kept 57 of 57 contract facts; one shared table kept 41 of 57

Caveat: these are Anthropic's own evaluations on Claude models, and the best-known example is a single run.

Question for you: do you re-validate agent notes against transcripts today, or trust whatever was written last?

Full breakdown with a redrawn diagram: [link to Medium article]

#AIEngineering #AIAgents #LLM #AgentMemory
