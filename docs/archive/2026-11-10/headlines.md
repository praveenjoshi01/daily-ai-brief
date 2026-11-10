# Daily AI Brief — 2026-11-10

Sources: inbox editions (Latent Space AINews Nov 10, TLDR AI Nov 9, AlphaSignal Nov 9, Import AI 480, others scanned) plus primary pages fetched this run. Lead chosen for primary source with mechanism and independent coverage. Labels show grounding strength.


## Frontier Labs

1. **Claude Fable 5.2 / Mythos 5.2: #1 on several leaderboards, but 31% more cost per task despite a 20% cheaper token price** — Per Latent Space's AINews roundup of third-party posts, Fable 5.2 lists at $8/$40 per 1M tokens versus $10/$50 for 5.1. SemiAnalysis reportedly paid $88.15 per task on GDPx versus $67.16, because the model wrote hundreds of tests where predecessors wrote about 20. Vals reportedly found High effort beating Max. I did not retrieve Anthropic's own announcement or the underlying posts, and a web search found no 5.2 page. Sources: [Latent Space AINews, Nov 10 (inbox)](https://www.latent.space/) *[SINGLE SECONDARY SOURCE (newsletter relaying tweets); primary not retrieved.]* *Why it matters: Per-token price is not per-task cost; measure cost per task at your own effort setting before migrating.*


## Research

2. **★ LEAD — Anthropic: 'dreaming' lifts a wiki-based memory score from 13% to 48% over 128 sessions, and still trails search alone (53%)** — Anthropic Engineering (Lance Martin, Nov 6) defines a four-layer agent memory stack (transcripts, notes, wiki-style representations, injected context) and an offline 'dreaming' pass that re-reads transcripts to fix notes and rebuild pages. Reported: CL-Bench mean reward 0.383 to 0.700 (Opus 4.7); wiki plus search 61% versus 53% for search alone; a per-task dreaming setup kept 57 of 57 contract facts versus 41 of 57 for a shared table. Sources: [Anthropic Engineering (primary)](https://www.anthropic.com/research/components-of-agent-memory) · [TLDR AI, Nov 9 (inbox)](https://tldr.tech/ai) · [Let's Data Science](https://letsdatascience.com/news/anthropic-details-how-claude-uses-dreaming-to-organize-agent-86d1704a) *[Primary (Anthropic post) + TLDR AI and Let's Data Science coverage. Vendor's own evals.]* *Why it matters: Memory is maintenance, not storage: build the audit-against-transcript pass before the wiki.*

3. **Ajeya Cotra: AI is now dramatically accelerating AI research at Anthropic** — Writing on Planned Obsolescence (Nov 6), Cotra argues Anthropic's own 'dramatically accelerated progress' threshold has likely been crossed, leaning on METR's report that progress about doubled over the past year. She estimates researchers are sped up roughly tenfold. She notes much of the supporting evidence is redacted. Sources: [Planned Obsolescence (primary)](https://www.planned-obsolescence.org/p/ai-is-dramatically-accelerating-ai) · [TLDR AI, Nov 9 (inbox)](https://tldr.tech/ai) *[Primary (author's post, fetched) + TLDR AI. It is an argument, not new data; evidence partly redacted.]* *Why it matters: Opinion built on a partly redacted assessment; useful framing, weak as a citation for hard numbers.*

4. **OpenAI releases BioBasicsBench: 100 routine wet-lab data-interpretation tasks** — TLDR describes a benchmark for how AI agents interpret raw experimental data across 100 routine wet-lab tasks; AlphaSignal lists a related OpenAI and Ligo release. I did not retrieve the primary post. Sources: [TLDR AI, Nov 9 (inbox)](https://tldr.tech/ai) · [AlphaSignal, Nov 9 (inbox)](https://alphasignal.ai/) *[TWO NEWSLETTERS, no primary retrieved.]* *Why it matters: Another domain-specific agent eval; check whether its tasks resemble your own data work.*

5. **PSI research system, using an Anthropic model, reportedly proves the Aaronson-Ambainis conjecture** — TLDR summarizes PSI's claim that its system resolved this open quantum-complexity problem, implying no exponential quantum speedup on random inputs. I did not retrieve the PSI page or any independent verification. Sources: [TLDR AI, Nov 9 (inbox)](https://tldr.tech/ai) *[SINGLE SECONDARY SOURCE (newsletter); unverified claim.]* *Why it matters: Treat as unverified until mathematicians weigh in.*


## Engineering & Tooling

6. **OpenRouter's new Auto Router and Auto Code: model chosen per request from eleven factors plus live price and provider health** — Announced Nov 6. A fast decision model rates each request, then routing weighs cost, health and cache status. The post claims up to 4x over the old router (methodology not given) and that Auto Code matches Opus 5.5 on five benchmarks at 74% lower cost. It stays on one model for nearly nine in ten agent turns to protect the input cache, and admits no router beats the best single model everywhere. Sources: [OpenRouter blog (primary)](https://openrouter.ai/blog/announcements/auto-and-auto-code-routers/) · [TLDR AI, Nov 9 (inbox)](https://tldr.tech/ai) *[Primary (OpenRouter, vendor claims) + TLDR AI.]* *Why it matters: Routing is now a harness decision; the cache-stickiness trade-off is the part to copy or test.*

7. **OpenCode Browse lets a coding agent drive your real, already-logged-in browser** — AlphaSignal says the tool controls your actual Chromium browser, records screenshots and network traffic, hands control back for logins and 2FA, and runs locally with MCP-compatible agents. Sources: [AlphaSignal, Nov 9 (inbox)](https://alphasignal.ai/) *[SINGLE SECONDARY SOURCE (newsletter).]* *Why it matters: Removes login scripting from auth-gated tests, but an agent in your signed-in browser needs tight permissions.*

8. **Nous Research's Arete-27B: Qwen3.8-27B fine-tune cuts a measured propaganda rate from 22% to under 1% with SFT only** — AlphaSignal reports 53M tokens of supervised fine-tuning, no RL, fact score 2.32 to 2.98 of 5, and general performance flat (65.60% vs 65.77% on Hermes Bench), with weights, evals and data on Hugging Face. I did not retrieve the model card. Sources: [AlphaSignal, Nov 9 (inbox)](https://alphasignal.ai/) *[SINGLE SECONDARY SOURCE (newsletter); figures are Nous's own per AlphaSignal.]* *Why it matters: If accurate, targeted SFT can remove a behavior without much capability loss; verify the eval yourself.*


## Industry

9. **OpenAI reportedly raises $11B at a $1.25T valuation, short of a $30B target** — TLDR, summarizing a TechCrunch report, says the round could reach $20B before closing. I did not retrieve the TechCrunch article. Sources: [TLDR AI, Nov 9 (inbox)](https://tldr.tech/ai) *[SINGLE SECONDARY SOURCE (newsletter summary of a report).]* *Why it matters: Funding pressure is a vendor-risk signal; keep your stack model-portable.*
