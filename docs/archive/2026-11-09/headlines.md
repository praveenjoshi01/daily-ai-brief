# Daily AI Brief — 2026-11-09

Sources: inbox editions (AlphaSignal Nov 8, Luiza Nov 8, Refactoring Nov 9, TLDR AI Nov 6) plus primary pages fetched this run. No TLDR edition dated Nov 7-9 had arrived.


## Frontier Labs

1. **Thinking Machines' Inkling 2 Small: 594B MoE (17B active), open weights promised 'next week'** — Announced Nov 5; available via Tinker with closed weights for now. Apache 2.0 release is planned after external safety testing. The post says it trails some closed models on its alignment evals and sometimes picks suboptimal tools. Sources: [Thinking Machines (primary)](https://thinkingmachines.ai/news/inkling-2-small/). *[Vendor primary only; release not yet confirmed.]* *Why it matters: Wait for the actual weights before planning around it; benchmarks shown are the lab's own.*

2. **OpenAI GPT-6 Cyber and Google Gemini Omni 1.2 Flash announced (Nov 6 TLDR)** — TLDR summarizes GPT-6 Cyber as a model for finding and validating exploitable vulnerabilities within researcher-defined boundaries, and Gemini Omni 1.2 Flash as faster and cheaper with longer clips. I did not retrieve either primary post. Sources: [TLDR AI, Nov 6 (inbox)](https://tldr.tech/ai). *[NEWSLETTER SUMMARY ONLY.]* *Why it matters: Check the primary posts for access terms before evaluating.*


## Research

3. **★ LEAD — Latent Sparse Attention: 22.7x faster prefill at 10M tokens by clustering keys instead of scanning them** — Paper (arXiv 2610.42147, Oct 30, v2 Nov 3) says that at 10M tokens the key-selection step dominates sparse attention. LSA clusters keys in a learned space so queries score centroids. Reported: 22.7x prefill / 4.6x decode over GLM-5.3-Flash's sparse attention for one layer; 2.2x end-to-end first-token gain on GLM and 9.2x on Qwen vs full attention. Gains shrink at shorter context. Sources: [arXiv 2610.42147 (primary)](https://arxiv.org/abs/2610.42147) · [GitHub README (primary)](https://github.com/Prefrontal-AI/latent-sparse-attention) · [AlphaSignal, Nov 8 (inbox)](https://alphasignal.ai/news/eth-zurich-s-lsa-slashes-10-million-token-ai-processing-by-72x). *[Primary x2 (paper, repo README) + AlphaSignal newsletter. Speedups are authors' own.]* *Why it matters: Long-running agents make selection cost, not attention, the latency lever; code and weights are Apache-2.0.*

4. **METR: Anthropic's R&D progress on well-specified tasks likely ~2x the Mar 2024-Oct 2025 rate** — METR's Nov 5 assessment (engagement Aug 12-Oct 29) estimates ~2x acceleration, with a plausible range of 1.3x-3x, and guesses ~80% is due to AI. It says Anthropic had unilateral redaction rights and removed most of the most informative evidence, and METR lacked query access to unreleased models. Sources: [METR, Nov 5 (primary)](https://metr.org/blog/2026-11-05-anthropic-ai-rd-acceleration-assessment/) · [TLDR AI, Nov 6 (inbox)](https://tldr.tech/ai). *[Primary (METR) + TLDR AI and Luiza's newsletter. Evidence is partly redacted.]* *Why it matters: Strong evidence-quality caveats; read it before repeating the headline number.*

5. **'Sovereign Agents' paper (Hayum) separates persistent from sovereign loss-of-control states** — Per Luiza Jarovsky's newsletter, the paper defines seven sovereignty capabilities and seven prevention routes, each with stated limitations, and argues no single route is robust. I did not retrieve the paper itself. Sources: [Luiza's Newsletter, Nov 8 (inbox)](https://www.luizasnewsletter.com/p/preventing-irreversible-loss-of-control). *[SINGLE SECONDARY SOURCE (newsletter); paper not retrieved.]* *Why it matters: A useful threat-model vocabulary for agent infrastructure (compute, payment, cybersecurity gating).*


## Engineering & Tooling

6. **DX Q3 report: heavy-AI orgs wait 105% longer for a first PR review** — DX's State of AI Impact (500+ companies; review data Jul-Sep 2026) reports median time to first review from 40 min (20-40% AI code) to 82 min (80%+), and weekly PR throughput up 75.5% over four quarters. Refactoring's Nov 9 newsletter cites DX saying PRs are over twice the size and wait over twice as long. Sources: [DX Q3 report (primary)](https://getdx.com/report/state-of-ai-impact-in-engineering-q3-report/) · [Refactoring Monday Ideas, Nov 9 (inbox)](https://refactoring.fm/p/customer-work-answers-and-readings). *[Primary (DX report page) + Refactoring newsletter. PR-size figure only in the newsletter's sponsor text.]* *Why it matters: Authoring got faster; review capacity is the new constraint. Budget for review tooling.*

7. **Devin Review 2.0: cost per PR down 82% since August, typical $0.25-$0.75** — Cognition's Nov 5 post credits a better model mix and harness optimizations, and says bugs found per PR rose from 1.22 to 1.32. No baseline, sample size or methodology is given. Sources: [Devin blog (primary, vendor)](https://devin.ai/blog/devin-review-2). *[Vendor primary only; self-reported.]* *Why it matters: A data point that harness work, not just model price cuts, drives agent unit economics.*


## Industry

8. **Linear CEO: teams and agents ship changes faster than leaders can understand them** — Per Refactoring's reading list, Karri Saarinen argues companies are losing the ability to steer, and that something working doesn't mean it belongs in the product. I did not retrieve the essay. Sources: [Refactoring Monday Ideas, Nov 9 (inbox)](https://refactoring.fm/p/customer-work-answers-and-readings). *[SINGLE SECONDARY SOURCE (newsletter blurb).]* *Why it matters: Review and product judgment, not generation, is the scarce resource.*
