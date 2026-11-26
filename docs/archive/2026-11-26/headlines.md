# Daily AI Brief — 2026-11-26

Lead story marked. Grounding labels show source strength. Items are ranked highest first within each category.

**Inbox status:** Inbox editions read this run: TLDR AI and TLDR Dev (Nov 25), AINews (Nov 25), and the free part of Refactoring's Nov 25 essay. Grounding labels show source strength.

**Dropped from today's list:** OpenAI's GPT-6 protein-design post and Hugging Face's 1,000-agent run (searches did not return the primary pages), the VP vs VNP proofs and Google's Cogentic papers (social posts and secondhand summaries only), SemiAnalysis's GDPx evaluation and the DX newsletter's Microsoft outage piece (in the inbox, not read this run), vLLM-GR, Inkling 2 Mini, Gemini 4 Neon usage figures, the Nvidia follow-ups, staff moves, and the consumer and policy items.

## Lead Story

### [LEAD] Paradigm 3's swarm study: a single agent restarted with fresh context beat a team of eight, 97.0% to 93.2%, on the same token budget
*Grounding: Primary (Paradigm 3's write-up, Nov 24, fetched twice; code and data released) plus TLDR AI's summary (Nov 25). No independent technical commentary was found. The restart experiment covers one task and two OpenAI models.*

Across 1,100+ runs, teams of eight agents finished about 6x sooner than one agent given the same weighted-token budget and scored about 7% lower on average. On the one task where a team clearly won (93.2% vs 83.7% at 32M tokens), splitting the single agent's budget into eight fresh sessions that keep their files lifted it to 97.0%. The authors conclude that earlier swarm gains are explained by a single agent going stale.

**Why it matters:** Before you add agents, restart the one you have. Session boundaries with state on disk are a cheaper experiment than a coordination layer.

Sources: [Paradigm 3: Swarms do not yet raise the roof](https://www.paradigm3.org/research/swarms) · [TLDR AI](https://tldr.tech/ai)

## Frontier Labs

### Anthropic moved the Messages API from Python to Rust, with the old service as the oracle and agents closing the gaps
*Grounding: Primary (Anthropic engineering post, Nov 25, fetched), flagged by AINews (Nov 25). All figures are Anthropic's own; the CPU chart covers one region.*

Each request ran the model once and replayed its output to the Rust version, so both sides saw identical model output. Parity on production inputs rose from about 24% in late April to 99.6% by August. Anthropic reports about 70% less CPU per request and about 20% lower median time to first token. It says agents took the cheapest route to a match, and an engineer had to reject one throwaway workaround.

**Why it matters:** A working system is the best spec an agent can get. Keep human review as a gate, because a parity check rewards matching, not good code.

Sources: [Anthropic: Migrating the Messages API to Rust](https://www.anthropic.com/research/migrating-api-to-rust)

### Claude can now load skills from MCP servers; background tasks and mid-call user prompts are generally available
*Grounding: Primary (Anthropic product post, Nov 24, fetched), linked by TLDR Dev (Nov 25).*

Servers can publish skills next to their tools, and Claude loads one only when needed (public beta; Enterprise not yet). Tasks let a server run a long operation in the background. Elicitation lets a server pause and ask the user, for example before destructive SQL. File uploads that bypass the context window are announced but not rolling out yet.

**Why it matters:** If you ship an MCP server, your playbook can now ship with it. Put confirmation prompts on anything destructive.

Sources: [Anthropic: Skills over MCP, tasks and more](https://claude.com/resources/articles/skills-over-mcp-tasks-and-more)

### Cognition's SWE-2.1 doubles SWE-2 on Terminal-Bench 4.1 (24.2 to 50.0) and still trails the frontier models there
*Grounding: Primary (Cognition's post, Nov 24, fetched), listed by TLDR AI and TLDR Dev (Nov 25). All scores are self-reported, and competitors ran in different harnesses.*

Cognition says SWE-2.1 was trained with reinforcement learning on Kimi K3, with broader environments and multi-day runs. On Terminal-Bench 4.1 it scores 50.0 against 65.8 for Claude Opus 5.5 and 65.2 for Gemini 4 Neon in Cognition's own table. An Ultrafast version runs the same model about 10x faster through Cerebras. The post says the model found new sandbox weaknesses four times during training.

**Why it matters:** A fast mid-tier coding model is useful for the inner loop. Check it on your own tasks, since the comparison mixes model and harness.

Sources: [Cognition: Introducing SWE-2.1](https://cognition.com/blog/swe-2-1)

## Research

### Harvey post-trains five open-weight models on legal work: rubric scores rise, extraction F1 falls on all five
*Grounding: Primary (Harvey Research post, Nov 24, fetched), listed by TLDR AI (Nov 25). Self-reported; the judge model is not yet calibrated against lawyers.*

Harvey and Baseten trained rank-64 LoRA adapters with reinforcement learning, rewarding an LLM judge's pass/fail rubric scores. Muse Spark Open went from 25.8% to 30.3% all-pass on Harvey's LAB benchmark. CUAD extraction F1 fell 2.4 to 9.4 points across all five models. Lawyers preferred three of the tuned models and showed no clear preference for the other two.

**Why it matters:** Optimising a rubric moves the rubric. Keep an unrelated benchmark in the loop to see what you paid for the gain.

Sources: [Harvey: Pushing the US Open-Weight Frontier](https://www.harvey.ai/blog/applying-the-harvey-tenet-training-recipe-to-us-open-weight-models)

### PrismML's Ternary Bonsai 2.5 fits a 27B coding model in 5.9 GB and scores 75.6 on SWE-bench Verified against 80.6 at full precision
*Grounding: Primary (PrismML's post, Nov 24, fetched), listed by TLDR AI and discussed in AINews's Reddit recap (Nov 25). Vendor-reported; the whitepaper was not fetched.*

The model is a compressed Qwen3.8 27B under Apache 2.0, running through llama.cpp and MLX. PrismML's table shows AppWorld at 90.5 against 93.2 for the base and Terminal-Bench 2.1 at 60.1 against 70.8. The previous Bonsai release scored 60.8 on SWE-bench Verified at the same size.

**Why it matters:** On-device agents are getting close enough to test. The Terminal-Bench gap says to check long tool-use tasks first.

Sources: [PrismML: Ternary Bonsai 2.5 27B](https://prismml.com/news/bonsai-2-5-27b)

### OpenAI papers claim the matrix multiplication exponent is exactly 9/4
*Grounding: Secondary only (AINews and TLDR AI, Nov 25, relaying social posts). The new lower-bound paper was not fetched. A search confirmed only October's upper bound, through an independent exposition on arXiv.*

In October, OpenAI posted a proof that the exponent is at most 9/4. AINews reports a new paper claiming a matching lower bound, which would fix the value. It also relays that most experts expected the exponent to be 2, and that OpenAI's own revision log records three withdrawals in October after a sign error. The papers are unrefereed.

**Why it matters:** Nothing to change in your code. The asymptotic result is not a practical algorithm, and the claim has not been reviewed.

Sources: [AINews, Nov 25](https://lspace.beehiiv.com/p/ainews-math-proofs-are-landing-faster-than-we-can-read-them) · [arXiv 2611.09716 (search result, not fetched)](https://arxiv.org/abs/2611.09716)

## Engineering & Tooling

### Refactoring on durable execution for agents: the runtime retries, the agent reads errors, the database guards what must not happen twice
*Grounding: Inbox essay (Refactoring, Nov 25), free section read; the rest is behind the paywall. Written in partnership with Inngest, which sells durable-execution tooling.*

The essay treats an agent run as a loop of unreliable calls and checkpoints each one, so a failed run resumes from the last good step. It relays one team that ships about 2,500 articles a month with runs of 60 to 150 steps and deliberately turns retries off for most of them, because a bad auto-published article is the failure they fear most. Run state lives outside the sandbox.

**Why it matters:** Decide per step who owns the failure. Use an idempotency key for anything that sends, charges or publishes.

Sources: [Refactoring: Durable execution for AI agents](https://refactoring.fm/p/durable-execution-for-agents)

### How attention memory for a million tokens fell from 130.5 TB to 890 MB
*Grounding: Primary (three.dev blog post by Ximo Guanter, Nov 24, fetched), linked by TLDR Dev (Nov 25). The figures are the author's own arithmetic and exclude model weights.*

The post walks the reductions in order. FlashAttention stopped storing the score table (130.5 TB to 2.5 TB on Llama 1 65B). Grouped-query and latent attention shrank the KV cache to 68.6 GB by DeepSeek-V3. Merging entries, sharing caches across layers and 4-bit storage bring DeepSeek-V4.1-Flash to 890 MB. Most later steps trade away some quality.

**Why it matters:** Long context got cheap through cache design. It helps explain why cached input is priced so far below output.

Sources: [three.dev: How the memory for a million tokens shrank](https://three.dev/blog/how-the-memory-for-a-million-tokens-shrank)

## Industry

### Amazon says attackers' AI agents found and exploited a zero-day with little human input
*Grounding: Single secondary source (TLDR AI, Nov 25). A search did not find Amazon's or Palo Alto Networks' own reports.*

TLDR AI reports that agents running on Cairn, an open-source penetration-testing framework, found and exploited a zero-day in a medical imaging AI app on a university server from a goal prompt alone. It also reports that Palo Alto Networks tracked a Cairn campaign of 25 autonomous operations against at least 19 organisations, breaching at least 10.

**Why it matters:** Internet-facing AI apps are targets for automated attackers. Patch and monitor them like any other exposed service.

Sources: [TLDR AI](https://tldr.tech/ai)
