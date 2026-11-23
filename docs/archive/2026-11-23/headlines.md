# Daily AI Brief — 2026-11-23

Lead story marked. Grounding labels show source strength. Items are ranked highest first within each category.

**Inbox status:** No TLDR AI or Latent Space edition dated Nov 21–23 was in the inbox at run time. The only new AI-relevant edition was Peter Yang's interview post (Nov 22). Today's items come mostly from pages fetched this run, found through two daily roundups (The Neuron, AI Impact Hub) and Simon Willison's blog.

**Dropped from today's list:** Architect Labs' AI-designed CPU (pre-silicon, startup claim, primary not fetched), OpenAI MedChemBench (roundup only, primary not fetched), OpenAI Dots, and the consumer and finance items. Ars Technica's report on the lead story could not be fetched, so it is not cited.

## Lead Story

### [LEAD] Dragos canary-token study: about two million bait prompts found attackers inside three inference providers, and OpenRouter pulled 125 endpoints from ZDR eligibility
*Grounding: Primary (Dragos post by HD Moore, Nov 19, fetched), plus OpenRouter's announcement (Nov 22), Phala's and Together AI's incident notes (all fetched), and independent coverage by The Hacker News (Nov 22). Most providers are unnamed.*

From July to November, Dragos sent about two million prompts through routers and providers, each with a unique URL, DNS name, and AWS key. Attackers were stealing data inside three providers, including some requests flagged Zero Data Retention. One unnamed lab's systems fetched secret links from about two-thirds of ZDR-flagged requests. OpenRouter off-boarded three providers and says it was not itself breached.

**Why it matters:** A privacy flag binds only the first hop. Pin your upstream providers, keep secrets out of agent context, and plant your own canary credential.

Sources: [Dragos: Your AI supply chain needs canaries](https://www.dragos.com/blog/ai-supply-chain-security-canary-tokens) · [OpenRouter announcement](https://openrouter.ai/blog/announcements/data-processing-incidents-on-inference-providers/) · [Phala incident report](https://phala.com/posts/phala-november-preliminary-incident-report) · [Together AI security notice](https://www.together.ai/blog/security-event-prompt-leakage-for-requests-in-june-and-july-of-2026) · [The Hacker News](https://thehackernews.com/2026/11/openrouter-drops-3-providers-after.html)

## Frontier Labs

### Thinking Machines Inkling 2 Mini: an open-weights looped transformer that fits in about 20 GB
*Grounding: Primary (lab post, Nov 20, fetched). Benchmarks are self-reported. License not stated on the page.*

The model has 26.4B total parameters and 3.4B active per token. Its two middle blocks of layers run three times per token. The lab reports 48.2% on DeepSWE v1.1 and 71.6% on Terminal Bench v2.1, behind Qwen3.8-27B at 73.0%. It says the model is weaker on multi-turn chat and multi-constraint instructions.

**Why it matters:** A coding model that runs on a 32 GB Mac through Ollama is a real option for local agents. It also removes the third-party hop in today's lead story.

Sources: [Thinking Machines: Inkling 2 Mini](https://thinkingmachines.ai/news/inkling-2-mini/)

### OpenAI publishes its internal perplexity numbers and proposes shared limits
*Grounding: Primary (OpenAI post by Jakub Pachocki, Nov 22, fetched). An opinion piece; figures are OpenAI's own and unverified.*

Pachocki reports log-perplexity on a held-out internal codebase: about 0.99 for GPT-3.5 and 0.91 for GPT-4. He says capabilities in mathematics and cybersecurity emerged below 0.8. He proposes that labs agree common limits tied to such measures. He also notes perplexity does not measure any task directly.

**Why it matters:** This is a pretraining-only metric. It says nothing about the harness, which is where most teams get their gains.

Sources: [OpenAI: Perplexity and Intelligence](https://openai.com/index/perplexity-and-intelligence/)

## Engineering & Tooling

### AWS DevOps Agent can now take directed write actions in five third-party services
*Grounding: Primary (AWS "What's new" documentation, entries dated Nov 20–22, fetched).*

Customers can let the agent create and update pull requests, retry pipelines, and roll back deployments in GitHub, GitLab, and Azure DevOps, and update incidents in ServiceNow and PagerDuty. On Nov 21, the Sandbox was extended to custom agents, with read-only AWS access and a network allowlist.

**Why it matters:** The agent moves from investigating incidents to changing systems. Your permission and approval design now carries the risk.

Sources: [AWS DevOps Agent: What's new](https://docs.aws.amazon.com/devopsagent/latest/userguide/whats-new.html)

### Google Agent Compute Engine: microVM sandboxes that keep credentials outside the agent
*Grounding: Single secondary source (InfoQ, Nov 22). Google's own deep dive was not fetched. Not yet available; no pricing.*

InfoQ reports a managed service that runs agents in isolated microVMs with checkpoint and resume. API keys and OAuth tokens stay outside the sandbox, and an external gateway injects them. A critic quoted by InfoQ notes the deep dive gives no boot time, price, or density figures.

**Why it matters:** Keeping secrets out of the sandbox is the same lesson as today's lead, applied to compute. Watch for the preview.

Sources: [InfoQ: Google Agent Compute Engine](https://www.infoq.com/news/2026/11/google-agent-compute-engine/)

### Gemini 4 Neon in Antigravity CLI scores level with Claude Code at under half the cost per task
*Grounding: Single secondary source (The Neuron, Nov 20), reporting Artificial Analysis figures. The Artificial Analysis pages were not fetched.*

The Neuron reports that Neon in Google's Antigravity CLI scored 59 on the Artificial Analysis Coding Agent Index, against 58 for Claude Fable 5.2 in Claude Code. Cost per task was $6.86 against $15.47. The cost figures depend on token prices that change on December 1.

**Why it matters:** The comparison is between model-plus-harness pairs. Check cost per task on your own workload before switching.

Sources: [The Neuron: Gemini 4 Neon vs Claude Code](https://www.theneuron.ai/news/gemini-4-neon-claude-code-benchmark-cost/)

## Research

### METR: frontier time horizons near 40 hours, doubling about every 3.6 months, and harder to measure
*Grounding: Primary (METR post, Nov 20, first 100,000 characters read; appendices not reviewed). Secondary: The Decoder (Nov 22).*

METR puts the 50% time horizon at 40 hours for GPT-6 Astra and 39 hours for Opus 5.5, with very wide confidence intervals. The pooled doubling time is about 3.61 months. Human data directly informs only about 9% of its time estimates. Models do worse where feedback is slow or unclear.

**Why it matters:** Long-horizon agent work is getting more feasible. The error bars are wide enough that you should test on your own tasks.

Sources: [METR: Q4 2026 capability update](https://metr.org/blog/2026-11-20-q4-2026-capability-update/) · [The Decoder](https://the-decoder.com/ai-is-getting-better-faster-than-experts-can-reliably-test-whether-new-systems-are-safe-metr-warns/)

### [UNVERIFIED] A Claude-assisted Riemann hypothesis proof compiles in Lean; mathematicians are still reviewing it
*Grounding: Two secondary sources (TechCrunch, Nov 20; Simon Willison's quotation posts, Nov 20). The proof document was not fetched. Not accepted by the mathematical community.*

Anthropic mathematician Levent Alpöge says he found a proof working with Claude. TechCrunch reports that several people, including MIT's Andrew Sutherland, confirmed it compiles in Lean. A separate human-written proof of the generalized hypothesis, by Alessandro Masullo, was announced the same day and has not been formalized.

**Why it matters:** A compiled proof shows the formal statement holds. Whether that statement is the intended theorem is the open question. Treat it as open.

Sources: [TechCrunch (Nov 20)](https://techcrunch.com/2026/11/20/ai-claimed-a-solution-to-the-167-year-old-riemann-hypothesis-and-a-human-did-too/) · [Simon Willison: Alpöge](https://simonwillison.net/2026/Nov/20/levent-alpoge/) · [Simon Willison: Vakil](https://simonwillison.net/2026/Nov/20/ravi-vakil/)

## Industry

### OpenAI now requires approval for gateways and routers that resell its models
*Grounding: Single secondary source (Semafor, Nov 20). OpenAI's policy page was not fetched; the effective date comes from a roundup only.*

Semafor reports that third-party gateways and routers need OpenAI's review and approval before offering access to its models. It names OpenRouter as the most prominent example. The stated background is distillation through resellers that hide the end user.

**Why it matters:** With today's lead, this is a second sign that the routing layer is tightening. Check that your gateway is approved.

Sources: [Semafor (Nov 20)](https://www.semafor.com/article/11/20/2026/openai-tightens-grip-on-model-resellers)

### Microsoft's Charles Lamanna: engineers write less code and manage agents on a token budget
*Grounding: Single source (Peter Yang's newsletter, inbox, Nov 22). An interview recap; team-size figures are as relayed, not verified.*

Lamanna, Microsoft's EVP for Copilot and Agents, says his strongest engineers now focus on architecture, testing, and running agents. Yang relays that Copilot Cowork was built by 11 engineers.

**Why it matters:** One view of how engineering roles shift when code is cheap. It is an opinion, not data.

Sources: [Peter Yang: What Should Engineers Do When AI Writes All the Code](https://creatoreconomy.so/p/what-should-engineers-do-when-ai-writes-all-the-code-charles-lamanna)
