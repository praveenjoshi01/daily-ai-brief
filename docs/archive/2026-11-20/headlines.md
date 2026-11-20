# Daily AI Brief — 2026-11-20

Lead story marked. Grounding labels show source strength.

## Frontier Labs

### Anthropic prices IPO at $83; 980M shares on Nasdaq as ANT
*Grounding: Primary (Anthropic news page, fetched). First-day close ($97.17) is a single secondary source (Latent Space). Valuation figures vary by share count across outlets.*

Anthropic's page states 980,000,000 Class A shares at $83.00 (956,351,354 from the company), trading Nov 19 on Nasdaq Global Select, expected closing Nov 20. Latent Space reports a $97.17 close and an $81.3B raise; a search did not confirm either.

**Why it matters:** Mostly business news, but it sets the funding backdrop for model pricing and roadmap pace.

Sources: [Anthropic: IPO pricing](https://www.anthropic.com/news/anthropic-prices-initial-public-offering) · [Latent Space AINews](https://www.latent.space/)

### Gemini 4 Neon independent evals: Cognition FrontierCode 2.0 at 46.2%, about 1/3 the cost of Opus 5.5
*Grounding: Single secondary source (Latent Space relaying third-party posts). Launch itself was covered Nov 19.*

Latent Space lists Artificial Analysis scores of 27 (Hydrogen low, $0.29/task) to 61 (Neon xhigh, $6.44/task), and a Vals RSI Index run costing $475 vs $1,536 for Fable 5.2. A commentator criticized that index as 4 tasks, single runs.

**Why it matters:** Cheap near-frontier coding is real on some boards; check noise before routing production traffic.

Sources: [Latent Space AINews](https://www.latent.space/)

### Genie 4: sources conflict on API availability
*Grounding: Primary (DeepMind post, fetched) vs. Latent Space. Treat the API claim as unconfirmed.*

DeepMind's Oct 27 post describes a research preview for trusted testers, with Google AI Ultra via Project Genie next and early-access Gemini API partners later. Latent Space says a Genie 4 API is live with 720p, 24fps and WebRTC; a search found no published API pricing or developer endpoint.

**Why it matters:** Don't plan around a Genie API yet; get on the waitlist if relevant.

Sources: [DeepMind: Genie 4](https://deepmind.google/blog/genie-4-a-new-generation-of-world-simulation/) · [Latent Space AINews](https://www.latent.space/)

## Research

### [LEAD] Hugging Face harness-hub: harness-adapted LoRAs lift Qwen3.8-27B from 39.2% to 64.7% on SWE-bench Pro hard-51 (pi harness)
*Grounding: Primary (both model cards fetched) + AIWeekly + Latent Space. Self-reported, small sets, no independent replication found.*

AsyncGRPO LoRA (r=32) trained inside the target agent. Pi adapter: Terminal-Bench 2.1 39.5% to 55.8%; median generated tokens on SWE-bench Pro 48.8k (base with thinking) vs 9.4k. OpenCode adapter: 35.3% to 51.0% (p = 0.057). With xhigh thinking, base and adapter tie at 74.5%. The pi card corrected its first numbers after an infrastructure failure (29.4% to 62.7% became 39.2% to 64.7%).

**Why it matters:** If your agent exhausts its step budget, fit between model and harness may matter more than model choice; re-run on your own tasks first.

Sources: [Pi adapter card](https://huggingface.co/harness-hub/Qwen3.8-27B-pi-adapted) · [OpenCode adapter card](https://huggingface.co/harness-hub/Qwen3.8-27B-opencode-adapted) · [AIWeekly](https://aiweekly.co/alerts/harness-hub-ships-qwen38-27b-pi-adapted-lora-hits-647-on-swe-bench-pro-hard-and)

### arXiv: "What Does a Harness Buy? Tokens, Mostly" finds harness swaps move pass rates about as much as reruns
*Grounding: Primary (arXiv abstract page, fetched). v2 dated Nov 18, 2026.*

Liu and Han ran seven models through Claude Code, mini-SWE-agent and OpenCode. No harness led across models; where the gap could be bounded it was 2 to 5 points. OpenCode trailed by 8 to 9 points on one model and led by 14 on another; cost gaps ranged from under 10% to 3-4x.

**Why it matters:** Report a rerun baseline next to any harness comparison, and treat single-pairing results with suspicion.

Sources: [arXiv 2610.04433](https://arxiv.org/abs/2610.04433)

### Google GUARD reports 80.8% on 43 SDK tasks, +6.28 over Meta-Harness with 54.5% fewer tokens
*Grounding: Single secondary source (Latent Space relaying a social post). Paper not located in this run; unverified.*

Latent Space lists GUARD under self-improving harnesses. Only the figures above were reported; the method was not described in what I read.

**Why it matters:** Another claim that harness search can cut tokens; wait for the paper before acting.

Sources: [Latent Space AINews](https://www.latent.space/)

### OpenAI publishes AI-for-research transparency numbers: experiments per experimenter up ~1.68x
*Grounding: Single secondary source (Latent Space summarizing reactions). OpenAI's post was not fetched.*

Latent Space reports a ~1.68x gain in experiments per experimenter and a 35% unassisted job-launch success rate, with commentators disputing which metrics matter.

**Why it matters:** Useful as a reality check on 'agents accelerate research' claims; read the primary post before quoting.

Sources: [Latent Space AINews](https://www.latent.space/)

## Engineering & Tooling

### OpenAI dev guidance: append Responses API history rather than editing it to preserve reasoning items
*Grounding: Single secondary source (Latent Space quoting OpenAIDevs). Docs not fetched.*

Per Latent Space, editing earlier turns can discard reasoning items; appending preserves them.

**Why it matters:** If your agent loop trims or rewrites history, check whether it is silently dropping reasoning state.

Sources: [Latent Space AINews](https://www.latent.space/)

### AutoRLBench: agents detect unhealthy RL runs 82.6% of the time but find the root cause only 28.2%
*Grounding: Single secondary source (Latent Space). Paper not located.*

Reported as an ML-engineering-agent benchmark result; no methodology details were available in what I read.

**Why it matters:** Agent monitoring is easier than agent debugging; keep a human in the diagnosis loop for now.

Sources: [Latent Space AINews](https://www.latent.space/)

## Industry

### Microsoft MAI Code 2 claims conflict between sources
*Grounding: Conflicting: Microsoft's page (fetched in the Nov 19 run) said 98% of GPT-6.1 Sol quality at 40% of the price; Latent Space cites a social post saying 96% of Opus 5.5 at 5% of cost. Not re-fetched today.*

The two framings use different comparison models and cost bases, so they cannot both be summarized as one number.

**Why it matters:** Wait for independent tests before treating either as a price/quality fact.

Sources: [Microsoft AI: Ignite 2026](https://microsoft.ai/news/microsoft-ignite-2026/) · [Latent Space AINews](https://www.latent.space/)
