# Daily AI Brief — 2026-10-30

*Sources: inbox (TLDR AI 2026-10-29, TLDR IT 2026-10-29) plus primary-source fetches this run. The 2026-10-30 TLDR AI edition had not arrived; stories are from Oct 27–28. Items marked "single secondary source" were not independently verified.*

## Engineering & Tooling
1. **★ LEAD — GitHub Copilot Fusion goes GA: a router/orchestrator over models** — [GitHub changelog](https://github.blog/changelog/2026-10-28-route-and-orchestrate-models-with-github-copilot-fusion/) · corroborated by [Artificial Analysis](https://artificialanalysis.ai/articles/github-copilot-fusion-orchestrates-anthropic-and-openai-models-to-balance-performance-and-cost). Three workflows (single, cascade, critique) and three effort levels. AA measured $5.59/task vs $11.42 for Claude Code + Opus 5.5 Max, a couple of index points lower. *Why it matters:* model choice is becoming a runtime decision made by the harness.
2. **Microsoft Copilot harness now on Foundry** — [Microsoft blog](https://blogs.microsoft.com/blog/2026/10/28/introducing-the-microsoft-copilot-harness-unlocking-the-potential-of-truly-multi-model-agentic-work/) (primary; no benchmark numbers in the post). GitHub-built agent loop + sandbox, 20+ models, BYO key, runtime ported to Rust. *Why it matters:* the vendor is selling the harness, not the model.
3. **Vercel CI (beta)** — [Vercel](https://vercel.com/blog/introducing-vercel-ci). Runs only affected tasks via Turborepo graph; Vercel reports 2–6x faster push-to-pass on its own repos. *Why it matters:* CI built for agent-volume PRs. (Vendor-reported.)
4. **Decagon: inference stack that improves itself** — [TLDR AI summary](https://links.tldrnewsletter.com/3vHagX) *(single secondary source; original not retrieved)*. Reported up to 2.5x throughput with human-approved production changes.

## Frontier Labs
5. **Anthropic Frontier Red Team: vulnerability discovery with an unreleased model** — [Anthropic](https://www.anthropic.com/research/discovering-vulnerabilities-with-claude). Parallel scanner agents, verification pipeline; Chrome chain across 62 CVEs patched in Chrome 156; Linux MPTCP zero-click RCE. No false-positive rates or cost disclosed. *Why it matters:* scaffold diversity and test-time compute drive results.
6. **Google Gemini 4 Carbon** — [Google](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-carbon/). Claims #1 on AA Intelligence Index v5 (59); access limited to a subset of cyber defenders at first; vendor-reported benchmarks.
7. **OpenAI: text your Dot agent via iMessage/RCS (US Pro)** — [Engadget via TLDR](https://www.engadget.com/2300235/openai-now-lets-you-text-your-dot-agent/) *(single secondary source; not fetched)*.

## Research & Open Models
8. **NVIDIA Nemotron 3.5 Transcribe + Granary v2** — [Hugging Face blog](https://huggingface.co/blog/nvidia/nemotron-transcribe-granary). ~30B total / ~4B active, 40 languages, 5.33% English avg WER on Open ASR (as reported). License not stated in post.

## Industry
9. **Artificial Analysis v5 and the benchmarker's dilemma** — [Interconnects](https://www.interconnects.ai/p/artificial-analysis-v5-and-the-benchmarkers). Argues for more indices with different biases; notes hidden test prompts remove community scrutiny.
10. **Anthropic launches AI-spend reporting for enterprises** — [TechCrunch](https://techcrunch.com/2026/10/28/anthropic-just-launched-tools-to-show-companies-what-their-ai-spending-is-buying/). Team-level cost/output reports; Jellyfish survey: spend on Anthropic-model tools up 10x YTD, ~2% of engineering cost.
