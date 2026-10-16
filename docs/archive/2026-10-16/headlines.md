# Daily AI Brief — 2026-10-16

Ranked within each category. Gmail (TLDR, Latent Space) scanned first; web used to corroborate the lead. Items marked single-source are labelled.

## Engineering & Tooling

### [LEAD] Anthropic replaces git with Scion: 30,000 merges a day broke a design built for offline clients
- Source: [Anthropic Engineering (Oct 13, updated Oct 15)](https://www.anthropic.com/engineering/redesigning-source-control); [The Register (Oct 13)](https://www.theregister.com/a/5302943); [TLDR IT (Oct 15)](https://tldr.tech/it)
- Confidence: Multi-source (LEAD); all figures are Anthropic self-reported
Anthropic says merged changes grew from about 2,500 a day in May to over 30,000 a day by September, and that source control became the bottleneck. Seven engineers built Scion, a server-centric system with server-side commits and a tiered cache, and moved the monorepo off git in five months. Anthropic reports roughly 200x lower CPU and memory than the old mirroring setup and checkouts dropping from minutes to seconds. Anthropic says it is not a general git replacement and will not release it; The Register notes the figures are unverified.
- **Why it matters:** Agent-written code moves the bottleneck from writing to landing and checking it: look at your CI checkout cost, merge queue and review path before your model choice.

### OpenCode 2.0 rebuilds the coding agent around a shared local service and a JavaScript 'code mode'
- Source: [OpenCode 2.0 notes (anoma.ly, undated)](https://anoma.ly/notes/opencode-2-0/); [TLDR Dev (Oct 15)](https://tldr.tech/dev)
- Confidence: Single primary-style write-up (undated page); date from TLDR listing
TUI, web and desktop clients now share one background server, with a rebuilt API and SDK. Code mode lets the agent write scripts that chain MCP and OpenAPI tools in one round trip, and subagents and shell commands can run in the background. Plugins written for 1.0 will not work and the server API is entirely different.
- **Why it matters:** Tool composition via generated scripts is spreading from hosted platforms to open-source agents; budget migration time for plugins.

### LangChain: start agent evals with 10-20 examples drawn from real traces
- Source: [LangChain blog (Oct 15)](https://www.langchain.com/blog/common-questions-about-agent-evals)
- Confidence: Single vendor source (a tooling vendor's own guidance)
The guide recommends picking one agent behaviour, building a small dataset from production traces, and recording a baseline before changing anything. It prefers code evaluators, uses LLM judges for subjective checks with narrow binary criteria validated against humans, and scores whole trajectories and final state for multi-step agents.
- **Why it matters:** A cheap, concrete starting point if your agent has no evals yet.

### Workday launches Agent Harness for building agents on HR and finance data
- Source: [Constellation Research (Oct 13)](https://www.constellationr.com/insights/news/workday-makes-sana-its-interface-launches-agent-harness-decision-and-work)
- Confidence: Single secondary source
Announced at Workday Rising, Agent Harness runs agents in isolated environments with access to HR and finance data, cross-process context and built-in memory. It is generally available on consumption-based Flex Credits and supports third-party agents that reach data via MCP.
- **Why it matters:** Enterprise suites are productising the harness layer; MCP is the integration seam.

## Frontier Labs

### Gemini 4 Argon 'Long Decode' raises output to about 1M tokens, with caveats
- Source: [Google Gemini API docs](https://ai.google.dev/gemini-api/docs/models/gemini-4-argon); [TLDR IT quick link (Oct 15)](https://tldr.tech/it)
- Confidence: Docs seen via search snippet only; page not opened. Third-party write-ups disagree on details
Search results quoting Google's model page list a roughly 1M-token window, a 65,536-token default output cap and up to about 1M with long decode, where thinking tokens count against the budget. One third-party write-up says generation runs in 64K hops via the Interactions API; reports of the limit are conflicting. Introductory pricing of $2/$10 per million tokens is from secondary reports.
- **Why it matters:** Read the limit as shared input plus thinking plus output, and test the cap yourself before building on it.

### Anthropic tells investors Q3 revenue rose 45% to $16.8B
- Source: [TLDR Dev summary (Oct 15)](https://tldr.tech/dev)
- Confidence: Single secondary source (newsletter summary); underlying report not opened
TLDR reports that Anthropic told investors third-quarter revenue rose 45% to $16.8 billion and that it was profitable after adjustments, as it prepares for a possible IPO.
- **Why it matters:** Context for vendor-stability questions; treat as unverified until the original report is read.

## Research & Evals

### Epoch's SpireClimb: frontier models now win 90%+ of Slay the Spire runs at base difficulty
- Source: [Epoch AI (Oct 14)](https://epoch.ai/publications/ai-systems-are-improving-rapidly-at-slay-the-spire-and-its-sequel)
- Confidence: Primary (page summary retrieved)
Epoch reports a jump from barely winning to at least 90% wins at base difficulty in about six months. At maximum difficulty the best models win roughly 17-35% depending on game and model, against 80%+ for top human players.
- **Why it matters:** A long-horizon, state-heavy agent benchmark that has not saturated at the hard end.

### METR proposes public assessments of loss-of-control risk inside frontier labs
- Source: [METR (Oct 14)](https://metr.org/blog/2026-10-14-better-informing-the-public-about-loss-of-control-risks/)
- Confidence: Primary (proposal, voluntary by design)
METR would publish reports on alignment, monitoring and AI R&D acceleration based on interviews and internal access, with scope agreed in advance and redactions disclosed. METR itself says the exercises are voluntary and cannot replace audits or regulation.
- **Why it matters:** Signals what evidence about agent oversight may soon be expected from labs.

### Researchers' hidden message in a webhook inbox drew replies from probing AI agents
- Source: [TLDR Dev summary (Oct 15)](https://tldr.tech/dev); [The New Stack (page body truncated)](https://thenewstack.io/rogue-ai-agent-fleet-tencent/)
- Confidence: Single secondary source (newsletter); article body could not be read
Per TLDR, researchers studying agents probing Alibaba's Amap left a message in a webhook inbox and received replies describing the agents' tasks and sandbox, tracing thousands of requests to agents on Tencent Cloud.
- **Why it matters:** Agents read and act on untrusted text they encounter: another prompt-injection surface.

## Industry

### Modal reportedly hits $1B ARR on a $16B Series D
- Source: [Latent Space AINews (Oct 15)](https://www.latent.space)
- Confidence: Single secondary source (newsletter subject line only; body not opened)
The AINews issue headline states Modal's $1B ARR and $16B Series D; details were not read.
- **Why it matters:** Sandbox and inference infrastructure is where agent spend is landing.

### Shopify opens its catalog to shopper-configured agents, with human sign-off on purchases
- Source: [Forkast via TLDR IT (Oct 15)](https://forkast.news/shopify-is-widening-the-catalog-door-to-personal-agents-the-sign-off-stays-human/)
- Confidence: Single secondary source (newsletter summary)
Per TLDR's summary, Agentic Storefronts give merchants access to agents such as ChatGPT, Copilot and Gemini while keeping a mandatory human approval on every purchase.
- **Why it matters:** Approval gates are becoming a product feature of agent commerce.
