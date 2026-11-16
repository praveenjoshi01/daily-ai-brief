# Daily AI Brief — 2026-11-16

Quiet day. No AI-engineering editions from today's inbox had arrived when this ran: the newest relevant inbox items are from Nov 14–15, and the TLDR AI / Latent Space editions cited in recent digests did not appear in a Gmail search for the last two days. The lead is a slow story that is new to this archive, not a fresh release. Five items cleared the bar. Engineering & Tooling had nothing that met it today.

Grounding labels show source strength. Vendor benchmarks are labeled as such.

## Research

1. **[LEAD] Trial by Trace: a benchmark grades agent harnesses separately from task success; 31.1% of successful runs still failed at least one harness criterion.** Submitted to arXiv Oct 23, 2026. Four harnesses (Claude Code, Codex, DeepSeek Harness, OpenClaw) and nine model groups across 95 tasks and 3,420 runs. Harness macro scores range from 59.8% to 72.0%, while the best task-pass rate (Claude Code, 44.0%) is not the best reliability score. Only 8.4% of runs pass every criterion in both layers.
   Sources: [arXiv:2610.32285](https://arxiv.org/abs/2610.32285) · [TraceTrial-Bench repository (MIT)](https://github.com/TraceLite-AI/TraceTrial-Bench) · secondary write-ups on hyper.ai and mer.vin (search snippets, not opened)
   *[Primary (arXiv HTML and abstract, fetched; repository fetched). Benchmark authors' own results; no independent replication found. The judge is a fixed model with no reported agreement figures.]*
   *Why it matters: Outcome-only evals can count broken harness runs as wins. Log tool calls and grade them, and treat the harness as a separate system.*

2. **AlphaProof Code: DeepMind agents wrote about six million lines of Lean to formally verify key security properties of Signal's code (covered as the Nov 12 lead).** Human experts approve the specifications. Lean checks the proofs, and agents flag about 1% of the codebase for human review. Verification took four weeks, with a head start from earlier Signal verification work. DeepMind reintroduced two previously fixed bugs, and the proofs marked both buggy versions as insecure.
   Sources: [DeepMind: Introducing AlphaProof Code](https://deepmind.google/blog/introducing-alphaproof-code/) · [Let's Data Science](https://letsdatascience.com/news/google-deepminds-alphaproof-code-formally-verifies-key-signa-a2c50019) (which cites WIRED)
   *[Primary (DeepMind post, fetched; the linked paper PDF could not be read) + Let's Data Science (secondary, cites WIRED). Authors' claims; no cost reported.]*
   *Why it matters: The trust sits in the specification and the checker, not in the agents. Line counts differ across reports (six million vs 6.5 million), so use the approximate figure.*

## Frontier Labs

3. **Claude Fable 5.2 and Mythos 5.2: the per-token price fell, but Artificial Analysis puts cost per task at about 2.6× Opus 5.5 at max effort.** Released Nov 9 (amended Nov 11). Fable 5.2 is $8 / $40 per million input / output tokens, about 20% below Fable 5.1, with Mythos restricted to verified organizations. Artificial Analysis reports cost per task of about $26.5 at max versus $10.0 for Opus 5.5. SemiAnalysis reports GDPx cost per task up 31%. Anthropic reports Fable at High matching Opus 5.5 at Max for about half the cost per task. The three numbers disagree, so measure on your own tasks. Already covered in the Nov 10, 11 and 14 digests; this item is about cost per task.
   Sources: [Anthropic: Claude Fable 5.2 and Mythos 5.2](https://www.anthropic.com/claude-fable-and-mythos-5-2) · [Latent Space AI News, Nov 10 (inbox, reports Artificial Analysis, SemiAnalysis and Arena figures)](https://latent.space/p/ainews-fable-5-2-retakes-world-1-llm-spot-as-ant-ipo-roadshow-begins/)
   *[Primary (Anthropic page, fetched; system card linked, not read). Artificial Analysis and SemiAnalysis numbers are secondhand via Latent Space; the Artificial Analysis page returned 403. Vendor-reported figures are labeled.]*
   *Why it matters: Per-token price is not your bill. Compare configurations by cost per completed task, and note that the effort setting changes that cost a lot.*

## Industry

4. **Anthropic launches the roadshow for its proposed IPO of Class A common stock.** Dated Nov 10 on Anthropic's news index.
   Sources: [Anthropic: roadshow launch](https://www.anthropic.com/news/roadshow-launch)
   *[Primary headline and date from Anthropic's news index; the post body was not read. Title-level only.]*
   *Why it matters: Context for item 3's pricing and access story; no direct engineering impact.*

5. **NVIDIA's CEO transition: Jensen Huang resigned as President, CEO and director, effective immediately; CFO Colette Kress is interim CEO; Q3 FY27 results are due Nov 17.** The 8-K is dated Nov 11, and the press release Nov 12. An NVIDIA statement on Nov 8 had said Huang would stay on, so the timeline matters.
   Sources: [NVIDIA Form 8-K (SEC EDGAR, via search listing)](https://www.sec.gov/Archives/edgar/data/0001045810/000104581026000082/nvidiaannouncesceotransiti.htm)
   *[Primary SEC filing surfaced by search; the filing body was not opened. Stated facts come from the search summary and need checking against the filing.]*
   *Why it matters: Leadership change at the main accelerator supplier, with earnings on Nov 17. Watch the call for supply and roadmap signals.*

## Engineering & Tooling

No item met the bar today.

## Not included

Left out on purpose: an unverified personal-conduct claim about NVIDIA's former CEO (reported in newsletters, not confirmed by the filing), and secondary-only tracker entries on Claude Code and Google ADK releases (no primary opened).
