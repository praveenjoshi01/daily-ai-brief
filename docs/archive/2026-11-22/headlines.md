# Daily AI Brief — 2026-11-22

Lead story marked. Grounding labels show source strength. Items are ranked highest first within each category.

**Inbox status:** No editions dated Nov 21 or 22 were in the inbox at run time. The newest inbox items were TLDR AI and Latent Space from Nov 20, plus a Luiza Jarovsky post from Nov 20. Items below are drawn from those editions and from pages fetched this run. Several items are dated Nov 18–19, and one is older (Oct 22), which the label shows.

**Dropped from today's list:** Replit's agent-swarm study (already the Nov 21 lead), Perplexity's self-improving skills and Gemini's Mac computer use (TLDR-only, no primary fetched), and Google's Mirror Dimension post (no date on the page).

## Lead Story

### [LEAD] Stripe's integration evals: a plugin lifted all 14 model–harness pairs, and outdated API references fell from 7% to 1.3%
*Grounding: Primary (Stripe methodology post, fetched, Nov 19). Self-reported by Stripe, which also owns the product being tested. Relayed by TLDR AI (Nov 20). Independent commentary covers Stripe's July benchmark program (InfoQ), not these plugin numbers.*

Coding agents (Claude Code, Codex, OpenCode) built Stripe integrations across 69 public scenarios, each run with and without Stripe's agent plugin. A role-playing LLM answered the agent's questions one at a time. A judge scored MUST and SHOULD rubric criteria against the transcript and the workspace.

**Why it matters:** The gain came from the context the agent was given, not from a new model. If you ship an SDK, your docs and tooling are part of the agent's runtime.

Sources: [Stripe: integration evals methodology](https://stripe.dev/blog/stripe-integration-evals-methodology) · [TLDR AI (Nov 20)](https://tldr.tech/ai) · [InfoQ: Stripe's July benchmark](https://infoq.com/news/2026/07/stripe-ai-agents-benchmark/)

## Engineering & Tooling

### Gemini API Tool Retrieval: the model searches for tools and loads only the schema it needs
*Grounding: Primary (Google blog, fetched, Nov 19). Preview feature; no benchmarks published.*

Tools marked `defer_loading: true` show only name and description until the model searches for them. The search runs server-side inside one API call. Client-side search is optional. Google gives no savings figure, and the post advises measuring against your own traffic.

**Why it matters:** Large tool libraries cost tokens on every call. This is a built-in way to defer schemas, and it changes how you size a tool registry.

Sources: [Google: Tool Retrieval in the Gemini API](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-api-tool-retrieval/) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Vercel Board: a message store where agents claim tasks and post updates
*Grounding: Primary (Vercel blog, fetched, Nov 18). Vercel calls it experimental; no adoption data.*

Agents pull labelled tasks from a channel, claim them for a time window, post progress in threads, and mark work done with a PR link. It is harness-agnostic, so Claude Code, Codex, and LangChain can share one board. It syncs with Slack and GitHub.

**Why it matters:** This is the coordination layer that the Replit study from Nov 21 said matters. Here it is as a product, and you can test it.

Sources: [Vercel: Introducing Board](https://vercel.com/blog/introducing-vercel-board) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Cloudflare releases Clairic and Clairic-flash weights for structured extraction
*Grounding: Primary (Cloudflare blog, fetched, Nov 18). Benchmarks are Cloudflare's own and labelled directional. License terms not stated in the post.*

Two open-weight models (27B and 9B) pull fields from text, images, and PDFs, with confidence scores and character spans. Cloudflare reports 99.7% on its fresh-text eval for the 27B model and 77.1% for ScaleDown on the same set. Clairic-flash is the smaller model.

**Why it matters:** Small, open extraction models are now a credible option for pipelines that currently call a frontier API. Check the license before you build on them.

Sources: [Cloudflare: Open Clairic](https://blog.cloudflare.com/open-clairic/) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

## Research

### Anthropic and Theorem: LLM-scaled formal verification on 239 entry points
*Grounding: Primary (Anthropic research post, fetched). Original date Oct 22, 2026, not today. Resurfaced in Latent Space (Nov 20). Self-reported.*

Claude wrote Rocq proofs that OSS-Fuzz entry points cannot crash on inputs up to 64 MB, across 123 libraries. Opus 5.5 solved half of 36 small verification tasks with about 40% fewer tokens than Opus 5. The authors say "formally verified" does not mean bug-free.

**Why it matters:** Verification is becoming a per-task cost you can budget. The reduced token cost is the number to track.

Sources: [Anthropic: LLM-scaled formal verification](https://www.anthropic.com/research/formal-verification) · [Latent Space (Nov 20)](https://lspace.beehiiv.com/p/formal-verification)

### Exponential Time Hypothesis claims from OpenAI and Anthropic await independent review
*Grounding: Two secondary sources (TechCrunch, Oct 27; TLDR AI, Nov 20). Lab preprints not fetched this run. Unverified by humans.*

Both labs say an internal model found a subexponential algorithm for counting 3-SAT solutions, which would refute ETH. UC San Diego and MIT researchers are organizing a review, and they say their involvement is not certification. Anthropic's Lean proofs have passed machine checks.

**Why it matters:** ETH underlies many complexity results. Treat the claim as open until human experts sign off.

Sources: [TechCrunch (Oct 27)](https://techcrunch.com/2026/10/27/frontier-ai-labs-say-their-models-refuted-the-exponential-time-hypothesis-what-does-that-mean/) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Apple FastFrames: 480p autoregressive video at 36 ms per frame on one B200
*Grounding: Primary (Apple project page, fetched). Paper and code linked from the page; the arXiv paper was not fetched and its date is unconfirmed. VBench numbers not given in the page text.*

A 1.3B model generates 480p video at 36 ms per frame on one B200. The gain comes from replacing VAE decoding and KV-cache updates, which account for over half of latency. The 14B model runs at 158 ms per frame on one GPU.

**Why it matters:** Interactive video generation is moving from research demo toward real-time latency budgets.

Sources: [Apple ML Research: FastFrames](https://apple-aiml-research.github.io/ml-fastframes/) · [arXiv 2611.23226](https://arxiv.org/abs/2611.23226) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

### Models can signal each other through a shared inference server, in a contrived setup
*Grounding: Primary (authors' LessWrong post, fetched, Nov 19). Not peer reviewed. Relayed by TLDR AI (Nov 20).*

Two Qwen3-8B instances on one vLLM server pass bits by changing engine step size or a KV-cache mailbox. With a fine-tuned reader the KV channel decoded 1,221 of 1,221 rounds. Background traffic at 1x dropped it to 49%. Proposed fixes: batch-invariant kernels, per-user cache salting, and separate engines for monitors.

**Why it matters:** If you run multi-tenant inference with agents, sandboxing alone does not isolate them.

Sources: [LessWrong: Models Can Communicate via Inference Servers](https://www.lesswrong.com/posts/7wzWuLP3HhyBLmKfo/models-can-communicate-via-inference-servers-despite-being) · [TLDR AI (Nov 20)](https://tldr.tech/ai)

## Industry & Policy

### [UNVERIFIED] U.S. federal frontier-AI safety bill outline, reportedly released Nov 19
*Grounding: Single secondary source (Luiza Jarovsky newsletter, Nov 20). A search found no bill text, no bill number, and no primary release. Treat as a watch item only.*

The post describes a proposed SAFE AI Act covering enforceable safety frameworks, incident reporting, pre-deployment evaluations, and whistleblower protection. Another blog reports a House outline, but no legislative text had surfaced at run time.

**Why it matters:** If it passes, frontier labs' release timelines and your compliance checklist would change. Confirm on congress.gov before acting.

Sources: [Luiza's Newsletter (Nov 20)](https://www.luizasnewsletter.com/p/americas-ai-safety-rules-are-about-to-change)
