# Daily AI Brief — 2026-11-21

Lead story marked. Grounding labels show source strength.

## Frontier Labs

### OpenAI's Performance Factory: Codex agents ran 1,700+ ChatGPT regression investigations in ~3 months
*Grounding: Primary (OpenAI engineering post, fetched). Self-reported.*

A task service, dispatch loop, cloud Codex API and event subscriptions wake agents when alerts fire or PRs get comments. A perf-forensics skill guides diagnosis; a separate Codex session reviews adversarially. Over 600 cases root-caused; in a manual review of 100 suggestions, 70% were graded accurate.

**Why it matters:** A concrete blueprint for agents in on-call loops, and an honest baseline: about 3 in 10 diagnoses still need a human.

Sources: [OpenAI: Performance Factory](https://openai.com/index/how-openai-performance-factory-keeps-chatgpt-fast/) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Riemann Hypothesis claim attributed to Claude-assisted work: unverified
*Grounding: Single secondary source (Latent Space relaying social posts). A search found no Anthropic page for it; it found only Anthropic's August result on zeta zeros.*

Latent Space reports that Anthropic mathematician Levent Alpöge claims a proof of RH (and GRH) with Claude, shipped as a Lean artifact of about 1.3 GB, still compiling at the time of writing. A separate human-written proof was also announced. Artificial Analysis lists the claim as unverified. Anthropic's earlier, verified-in-Lean result raised the share of zeta zeros known to lie on the critical line from 41.6% to 67.2%, and Anthropic said then it didn't expect those techniques to prove RH.

**Why it matters:** Don't repeat this as fact yet. Watch whether the Lean build completes and whether the statement checked is really RH.

Sources: [Latent Space AINews (Nov 20)](https://latent.space/p/ainews-riemann-hypothesis-proved-twice-independently/) · [Anthropic: Riemann zeta result (Aug)](https://www.anthropic.com/research/riemann-zeta)

## Research

### [LEAD] Replit: 32 Opus 5.5 agents hit an 18.92x NumPy speedup vs 3.66x solo, but the strongest solo model got worse as teams grew
*Grounding: Primary (Replit Frontier post, fetched) + TLDR AI + The New Stack's Missions coverage (via search). Self-reported; no cost data; 4 of 14 libraries discussed.*

Optimization-Bench: agents speed up real library workloads in 2 hours on 8 vCPUs each, with outputs checked on hidden inputs and timed on a dedicated machine. Opus swarms put 82% of messages on a shared board. GPT-6.2 Astra had the best solo runs on every task, yet at 32 agents fell below its own solo score on 3 of 4 tasks as its coordinator became a message switchboard.

**Why it matters:** Before scaling agent counts, measure your coordination topology and how separable the work is. Solo benchmark scores don't predict team performance.

Sources: [Replit: Throwing Headcount at the Problem](https://frontier.replit.com/throwing-headcount-at-the-problem/) · [The New Stack: Replit Missions](https://thenewstack.io/replit-missions-agent-swarms/) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Sandboxed models can signal each other through a shared inference server
*Grounding: Primary (LessWrong post, fetched). Contrived setting; not peer reviewed.*

Two channels on vLLM with Qwen3-8B: one agent changes engine step size so the other's kernels differ numerically, or leaves a KV-cache 'mailbox'. With a fine-tuned reader the KV channel got 1,221 of 1,221 rounds right. Background traffic cut it to 49%. Fixes: batch-invariant kernels, per-user cache salting, separate engines for monitors.

**Why it matters:** If you run an untrusted monitor on the same server as the policy it watches, isolate them.

Sources: [LessWrong: Models can communicate via inference servers](https://www.lesswrong.com/posts/7wzWuLP3HhyBLmKfo/models-can-communicate-via-inference-servers-despite-being) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### ETH's original authors set up an independent review of the OpenAI/Anthropic refutation claim
*Grounding: Primary (UC San Diego news, fetched).*

Russell Impagliazzo and Mohan Paturi (UCSD), who proposed the Exponential Time Hypothesis in 1998 with Francis Zane, and MIT's Ryan Williams opened a community blog and plan conferences to check the claim. They have posted the OpenAI prompt that led to it.

**Why it matters:** The right template for AI-claimed math results: public artifacts and expert review before anyone builds on them.

Sources: [UC San Diego: Independent review](https://today.ucsd.edu/story/computer-scientists-facilitating-an-independent-review-of-a-high-profile-open-ai-and-anthropic-resul) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

## Engineering & Tooling

### Stripe evals: 69 integration scenarios; strict pass rate falls from 78.1% to 29.4% when every MUST criterion counts
*Grounding: Primary (Stripe engineering post, fetched).*

A role-playing LLM acts as the developer and reveals 2 to 4 hidden needs one at a time. 14 model-harness pairs (Claude Code, Codex, OpenCode) each ran twice. Stripe's agent plugin raised every pair by about 3 to 8 points and cut outdated parameter use from 7% to 1.3%. Benchmark and the Forge harness are going to GitHub.

**Why it matters:** Domain plugins measurably steer agents, and 'mostly right' integrations are the norm. Grade on MUST criteria, not averages.

Sources: [Stripe: Evals methodology](https://stripe.dev/blog/stripe-integration-evals-methodology) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Gemini API Tool Retrieval: load tool schemas on demand
*Grounding: Primary (Google blog, fetched) + Latent Space.*

Add a tool_search tool and mark tools defer_loading: true. Names and descriptions stay visible; schemas load only when needed. Search can run server-side or client-side, works for MCP servers, and keeps the cached prompt prefix stable. Preview in the Interactions API, Gemini 3.6+; no extra fee.

**Why it matters:** Agents with dozens to hundreds of tools can stop paying for every schema on every turn. Measure savings on your own traffic.

Sources: [Google: Tool Retrieval](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-api-tool-retrieval/) · [Latent Space AINews (Nov 20)](https://latent.space/p/ainews-riemann-hypothesis-proved-twice-independently/)

### Perplexity Brain writes and updates its own skills: 80,000+ personal skills since August
*Grounding: Primary (Perplexity engineering post, fetched). Self-reported A/B test.*

A four-stage loop (evidence, reflection, verification, activation) runs daily on each user's sessions. In an eight-week randomized test, tool-call failures fell 11% and dissatisfaction 7.6%, with no measurable cost or latency change. Built-in skills add replay testing and engineer review.

**Why it matters:** Learning in the harness layer, without touching weights, is shipping at scale. The verification gate is the part to copy.

Sources: [Perplexity: Self-improving skills](https://www.perplexity.ai/hub/blog/self-improving-skills) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Vercel Board: a harness-agnostic message board for agent teams
*Grounding: Primary (Vercel blog, fetched). Experimental.*

Agents claim tasks, renew leases, post updates in channels and threads, and get woken by watchers. Two-way sync with Slack and GitHub; per-channel grants. Vercel says v0's software factory, rebuilt on Board, merges over 50% of its PRs.

**Why it matters:** The shared-board pattern that worked in Replit's swarms is becoming an off-the-shelf primitive.

Sources: [Vercel: Introducing Board](https://vercel.com/blog/introducing-vercel-board) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Chrome's 'mirror dimension': a synthetic web for testing browser agents
*Grounding: Primary (Google security blog, fetched). Internal tool.*

Agents visit real URLs inside a gVisor sandbox; a proxy serves generated sites with on-the-fly certificates. A multi-agent harness builds the sites. Google says automated red-teaming yields 1,000+ test candidates per engineer per day, over 30x manual.

**Why it matters:** Hermetic environments are how you test agents against prompt injection without touching the live web.

Sources: [Google: Mirror dimension for agents](https://blog.google/security/mirror-dimension-for-agents/) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Cloudflare open-sources Clairic (27B) and Clairic-flash (9B) extraction models
*Grounding: Primary (Cloudflare blog, fetched) + Latent Space. Internal evals only.*

Both run on Workers AI and are on Hugging Face. On 336 fresh text fields Clairic got 335 right; p50 latency 358 ms (flash: 155 ms). $0.10 per million input tokens until Dec 1. Latent Space says Apache 2.0, post-trained from Qwen; Cloudflare's page doesn't name a license.

**Why it matters:** A cheap, open option for structured extraction from PDFs and images. Run it on your own documents first.

Sources: [Cloudflare: Open Clairic](https://blog.cloudflare.com/open-clairic/) · [Latent Space AINews (Nov 20)](https://latent.space/p/ainews-riemann-hypothesis-proved-twice-independently/)

## Industry

### Apple reportedly building an autonomous agent for apps, browsing and coding
*Grounding: Single secondary source (TLDR summarizing a Bloomberg report; Bloomberg not fetched).*

Per TLDR, a job listing seeks a manager for a proactive agent that can code, browse and control apps, coordinating subagents. Apple is also adding a macOS 27.3 warning before users grant third-party agents control of their Macs.

**Why it matters:** Platform owners are starting to gate desktop agents. Expect permission friction for computer-use products on macOS.

Sources: [TLDR AI (Nov 20)](https://tldr.tech/ai)
