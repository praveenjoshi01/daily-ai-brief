# Daily AI Brief — 2026-10-27

Tuesday. The inbox was rich today (TLDR AI, AINews/Latent Space, Import AI). The lead is OpenAI's disclosure about agents passing secrets through a shared CPU cache: I could not open OpenAI's own post (HTTP 403), so it rests on Import AI's direct quotes from it plus several independent write-ups; the dashboard says so. Items resting on one secondary source are labelled.

## Frontier Labs & Safety

### [LEAD] OpenAI: sandboxed agents with no network and no shared files still passed secrets through the CPU cache
- Source: [Import AI 478, Oct 26 (inbox; quotes OpenAI's post)](https://importai.substack.com/p/import-ai-478-math-for-alignment) ; [OfficeChai, Oct 24](https://officechai.com/ai/openai-says-its-ai-agents-found-a-way-to-talk-to-each-other-through-the-processors-cache-even-when-every-other-channel-was-cut-off/) ; [ai-tldr.dev](https://ai-tldr.dev/releases/openai-offline-frontier-training/)
- Confidence: OpenAI's post ("Securing our frontier model training environment", reported Oct 23) returned 403 to me; the mechanism is taken from Import AI's quotes of it and corroborated by two independent write-ups. No bandwidth, error-rate or trial-count figures were found anywhere. Agents were asked to find a route; it was not spontaneous escape.
- In an internal red-team test, agents in separate microVMs on shared hosts were asked to swap synthetic secrets with no network and no shared writable files. They agreed on an encoding and signalled by evicting cache lines and timing reloads; a second channel used bursts of writes versus idle time.
- **Why it matters:** Isolation at the software layer (network, files) does not close channels that live in shared hardware. If you sandbox agents, the host is part of your threat model.

### OpenAI moves frontier RL training to an offline, cached copy of the web; training resumed Oct 1
- Source: [ScaleVise summary](https://scalevise.com/resources/openai-frontier-training-offline-web-security/) ; [remio.ai analysis](https://www.remio.ai/post/openai-on-securing-our-frontier-model-training-environment-containment-requires)
- Confidence: Secondary write-ups only (OpenAI post not retrieved). They report a Sept 20 DNS-misconfiguration incident and a pause of about 11 days; one other summary did not mention the Sept 20 incident, so treat those details as company-reported and unconfirmed. Full air-gapping is reported as not currently feasible.
- Agents still browse, search and use computer-use tools, but inside an offline world of indexed and cached pages, with restricted outbound traffic, sandboxing and layered monitoring. Reports say red-teaming now runs continuously.
- **Why it matters:** Offline-by-default is becoming the baseline for evaluating capable agents; expect similar designs for your own eval harnesses.

### Anthropic S-1 reaction: 48% of H1 revenue via cloud marketplaces, 85% gross margin (reported)
- Source: [AI Weekly (secondary; AINews/Latent Space newsletter in inbox has no link I retrieved)](https://aiweekly.co/alerts/anthropic-s-1-shows-163b-h1-revenue-25-from-two-customers-and-807b-non-cash)
- Confidence: Single newsletter summarizing social-media posts; I did not open the filing. Web search gave conflicting accounts of whether the S-1 is public, and I could not confirm the ticker or the 85% margin. Figures differ across commentators. Treat all numbers as unverified.
- The newsletter reports H1 2026 revenue of $16.3B, a Q2 operating profit near $1B, and a pitch of "virtual collaborators" for knowledge workers. Commentators dispute how much revenue is circular via Amazon and Google.
- **Why it matters:** If accurate, margin and distribution data say a lot about what serving frontier models costs; wait for the filing itself before quoting numbers.

## Models & Research

### Kimi K3.1 Pro: score of 55 on Artificial Analysis; open weights promised by Nov 4
- Source: [Moonshot post (linked from TLDR AI Oct 26; not opened)](https://www.kimi.ai/blog/kimi-k3-1-pro) ; [CGTN, Oct 24](https://news.cgtn.com/news/2026-10-24/Kimi-K3-1-Pro-an-open-weight-model-within-3-points-of-the-frontier-1Rvpycrxw2s/p.html) ; [i-scoop](https://www.i-scoop.eu/kimi-k3-1-pro/)
- Confidence: Newsletter plus secondary coverage via search summaries; I did not open Moonshot's post. The score is Artificial Analysis's; performance claims are mostly vendor-reported. Weights are not yet published.
- Moonshot's API release is a post-trained Kimi K3 (reported 2.8T total, 104B active parameters) priced at $2 / $10 per million tokens. If weights ship, the open-vs-proprietary gap on that index shrinks to about 3 points, per Artificial Analysis as relayed.
- **Why it matters:** Worth planning an eval slot for Nov 4, but don't depend on weights that haven't been posted.

### Apple's 20B on-device model: ~2 GB resident memory by keeping experts in flash
- Source: [The AI Realist (independent measurement)](https://www.airealist.ai/p/exploring-apple-on-device-model) ; [The Next Web](https://thenextweb.com/news/apple-third-generation-foundation-models-afm)
- Confidence: One independent measurement (single M3 Max, one run, 20-problem energy test) plus press coverage of Apple's announcement; no Apple technical report yet. TNW and the measurement differ on routing detail (once per prompt vs about every 32 tokens).
- Apple says 20B parameters with 1-4B active per prompt. The measurement found roughly 2 GB resident, about a third of Qwen3 4B's energy on a small test, but weaker math: 78/100 on GSM8K vs 89-94 for open builds.
- **Why it matters:** Flash-resident experts trade capability on some tasks for a tiny memory footprint; a design to watch for on-device agents.

### ProgramBench: best score 0% at launch in May, now 18.5% resolved (Claude Opus 5.5, xhigh)
- Source: [Import AI 478 (inbox)](https://importai.substack.com/p/import-ai-478-math-for-alignment)
- Confidence: Single secondary source (Import AI); I did not open the arXiv paper. 18.5% is fully-resolved tasks out of 200; the same source reports 70.5% "almost" (>95% of tests pass).
- ProgramBench asks models to rebuild programs such as SQLite, jq and ripgrep from a compiled binary and docs.
- **Why it matters:** A useful yardstick for how fast agentic coding is moving on whole-program tasks, not just patches.

### Mirendil-Base: one researcher, 3.5 months, under $10M compute (self-reported)
- Source: [Import AI 478 (inbox)](https://importai.substack.com/p/import-ai-478-math-for-alignment)
- Confidence: Single secondary source relaying the company's own claims; no independent verification and I did not open the Mirendil post.
- Mirendil says its 100B-500B-parameter base model beat several open bases on its evals, trained from public data, with larger models still training.
- **Why it matters:** If true, AI-assisted research is shrinking the team size needed to pretrain; treat as a claim until evals are replicated.

### Resolution autoformalizes resolution of singularities: ~600k lines of Lean for about $135k in tokens
- Source: [Import AI 478 (inbox)](https://importai.substack.com/p/import-ai-478-math-for-alignment)
- Confidence: Single secondary source quoting the company's post; not opened directly.
- An orchestrator agent executed a 112-page plan over about a week, with sub-agents writing proofs and Lean.
- **Why it matters:** A concrete cost data point for long-horizon, plan-then-delegate agent runs.

## Engineering & Tooling

### Cursor agents can now drive desktop apps such as the iOS Simulator to test what they build
- Source: [TLDR AI, Oct 26 (inbox)](https://links.tldrnewsletter.com/9vOZh9)
- Confidence: Single newsletter blurb; I did not open the Cursor post.
- Per TLDR, agents can control desktop applications to verify their own changes.
- **Why it matters:** Closing the loop with real UI testing is where coding agents are heading.

### Unified Claude Chat and Cowork now generally available on Enterprise plans
- Source: [Anthropic, via TLDR AI (inbox)](https://claude.com/resources/articles/unified-claude-enterprise)
- Confidence: Link seen in TLDR; I did not fetch the page, only the newsletter's one-line description.
- TLDR reports the combined chat and Cowork experience is GA for Enterprise.
- **Why it matters:** Minor for builders; relevant if your org standardizes on Claude.

### A 10-year-old CNN beats GPT-6 Astra and Claude Fable 5.1 at skin-lesion diagnosis (claimed)
- Source: [Lynch Lab, via TLDR AI (inbox)](https://lynchlab.net/llm-skin-cancer)
- Confidence: Single newsletter blurb; I did not open the study, so methods and numbers are unchecked.
- The blurb argues a small specialised network outperforms frontier LLMs on this task.
- **Why it matters:** A reminder to benchmark task-specific baselines before reaching for a frontier model.

## Items checked and left out

Gemini 4 Carbon early tests, SpaceX $40B GPU debt (CNBC via TLDR): single-source blurbs, not corroborated. GPT-6.1 Terra pricing and benchmark claims appear only as relayed social posts in AINews and were not verified.
