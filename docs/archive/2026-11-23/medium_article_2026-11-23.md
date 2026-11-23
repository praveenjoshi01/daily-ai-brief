# Title options

1. **Canary tokens for your AI supply chain: what two million bait prompts found inside inference providers** *(recommended)*
2. What "Zero Data Retention" doesn't tell you about where your prompt goes
3. You (probably) don't know how many companies read your prompt

**Subtitle:** Dragos seeded about two million prompts with bait credentials. Three providers were breached, and OpenRouter pulled 125 endpoints from Zero Data Retention eligibility.

---

If you route agent traffic through a model gateway, you've probably ticked a "zero data retention" box and moved on. Your agent then sends whatever is in its context: code, config, sometimes a live key. [PRAVEEN: 1-2 sentences, optional: have you had to audit where your agents' prompts actually go?]

Dragos spent July to November testing that box. The number I'd keep is **about two million**: prompts sent through routers and providers, each carrying secrets that existed nowhere else. Attackers were found stealing data inside three providers, and some of the stolen requests were flagged Zero Data Retention (ZDR).

The privacy flag binds the first hop. Your prompt takes several.

## Where to find it

"Three breaches, endless leaks: Your AI supply chain needs canaries," by HD Moore, Chief Research Officer at Dragos, published November 19, 2026. OpenRouter's response, "Data Processing Incidents on Inference Providers," followed on November 22. Phala and Together AI have each published their own incident notes. The Hacker News covered the story independently on November 22.

## What this post covers

- **The problem:** why a privacy setting can't be checked from the outside
- **The seed:** what goes into each bait prompt
- **Attribution:** how a single hit maps back to one request
- **Route tracing:** how the team found hops nobody advertised
- **What the evidence says:** three failure classes, ranked
- **Three limitations**, including one in the source itself
- **What to do this week**

## The problem it solves

A ZDR flag is a promise. You send the request, you get tokens back, and you have no way to see what happened to the prompt in between.

Routers make this harder. One account reaches hundreds of models, and the router picks an upstream provider, often on price. That provider may forward again. Each hop has its own logging, its own staff, and its own security posture.

The naive check is to read each provider's policy page. A policy page says what should happen. It can't tell you what did.

**Takeaway:** You can't audit a retention policy by reading it. You need a signal that fires when the policy is broken.

## How it works

### Step 1. The seed

Each prompt carries secrets that appear in exactly one request. Dragos began with free Thinkst Canarytokens: an AWS key, a DNS name, and a URL per request. The team later built its own seeding service, which generates a unique seed per prompt and derives hostnames, URLs, and credentials from it.

Behind those secrets sit real listeners: DNS, web, git, SSH, databases, mail. The AWS keys belong to empty accounts with full logging.

The design choice that matters is uniqueness. A secret that exists in one prompt can only be learned by reading that prompt.

### Step 2. Attribution

Every hit links back to the exact prompt, model, router, and privacy setting that carried it. The team also records timing, DNS resolvers, and connection details.

So a hit is a full record: which request leaked, through which path, and under which flag.

### Step 3. Route tracing

Two techniques find the hops. First, an image URL pointing at Dragos servers records every system that fetches it. Second, slightly malformed requests come back with errors, and each router wraps an upstream error in its own format. Those nested envelopes are matched against a signature database to name the software and operator at each hop.

Dragos traced about 2,000 routes. Several hundred contained systems it could not identify, and some images reached companies that were not on the advertised path.

### Step 4. Watch what comes back

Then the team waits. A DNS lookup, a URL fetch, or an AWS API call on a bait key each means someone read the prompt.

![The canary loop, redrawn: a seeding service plants a unique URL, DNS name, and AWS key in each prompt; the prompt travels through a router to a provider and sometimes on to hops nobody advertised; listeners catch any use of the secrets and map the hit back to the exact prompt, router, and privacy flag. My version adds the undisclosed hop and marks how far the ZDR flag reaches, which the post describes in text and across separate figures.](diagram_2026-11-23.png)

**Takeaway:** The method needs no access to the provider. It only needs secrets that are worthless everywhere except as evidence.

## The bridge

A canary token is an integration test for a privacy policy.

The policy is the spec. The bait credential is the assertion. A hit on the listener is a failing test, and it names the request that failed.

Like any test, it only proves presence. A green run says nobody used the secret, which is weaker than saying nobody read it.

## What the evidence says

Three failure classes came back. I'd rank them by how little a flag can do about each.

**1. Breach.** Attackers were inside three providers, the earliest from mid-July, and none of the three knew until told. In the largest case, a couple hundred AWS keys were each sent once in late-October windows, and every one was stolen. Some of those requests had been rejected before any model ran, which suggests copying at the front door. The bait keys then drove tens of thousands of AWS API calls. Practical consequence: any secret in a prompt during an exposure window should be rotated, whatever flag was set.

**2. Policy ignored.** One unnamed Chinese lab's systems fetched secret URLs from over half the prompts sent to its models, including about two-thirds of those flagged no-collection or ZDR. U.S. hosts reselling those models triggered the same scraper. Practical consequence: the model's origin can matter more than the host's address.

**3. Logging resellers.** Sellers on an inference marketplace listed popular models cheaply, turned on request logging, and read what arrived. No exploit was needed. Practical consequence: price-sorted default routing is a security setting.

The provider disclosures back this up. Phala reports an attacker controlled an inference VM and could see in-flight requests to one model, with a precautionary window from October 21 to November 8. Together AI reports a different path: an AI coding agent committed a credential to a public repository, and someone used it to download stored prompt samples from June and July. Five of the credentials that party then tested were Dragos canaries.

OpenRouter says it was not itself breached. It off-boarded three providers and removed 125 endpoints from ZDR eligibility, some as a precaution.

**Takeaway:** In Moore's words, "A privacy flag doesn't help when the attacker is already inside."

## Limitations I'd name

1. **Most providers are unnamed.** Dragos has not named the three breached providers, and OpenRouter has not named the three it removed. Nobody has confirmed they are the same three. You can't look up your own exposure from the post.

2. **Canaries detect use, not reading.** A leak only shows when someone acts on the secret. Silent copying is invisible. Phala makes the same point: the tests sampled traffic, so it keeps a wider window than the canaries confirmed. The post also gives no per-provider prompt counts, so there are no leak rates to compare.

3. **The source has a loose thread.** This is a vendor blog post, not a reviewed paper. Its account of the Feishu incident is inconsistent: the prompt is described as sent to a Chinese provider in one place and to a U.S.-based provider with the ZDR flag in another.

## Closing

The flag binds the first hop, and the prompt takes several. What I'd keep from this work is that the fix lives in the harness. Which providers you allow, what your agent may put in context, and whether you plant your own canaries are all decisions you make outside the model.

This week: plant one canary credential in the context your agents already send, pin your upstream providers instead of accepting the default pool, and treat any hit as an incident.

## Now I want to hear from you

1. Do you pin upstream providers on your router today, or accept the default pool?
2. If a canary key in your agent's context fired tomorrow, who gets paged, and what gets rotated?
3. Would you scrub credential-shaped strings from prompts, knowing that misses secrets that don't look like keys?

## References

1. HD Moore, "Three breaches, endless leaks: Your AI supply chain needs canaries," Dragos blog, November 19, 2026. https://www.dragos.com/blog/ai-supply-chain-security-canary-tokens
2. OpenRouter, "Data Processing Incidents on Inference Providers," November 22, 2026. https://openrouter.ai/blog/announcements/data-processing-incidents-on-inference-providers/
3. Phala, "Phala November Preliminary Incident Report," November 10, 2026. https://phala.com/posts/phala-november-preliminary-incident-report
4. Vipul Ved Prakash, "Security event: prompt leakage for requests in June and July of 2026," Together AI, November 21, 2026. https://www.together.ai/blog/security-event-prompt-leakage-for-requests-in-june-and-july-of-2026
5. The Hacker News, "OpenRouter drops 3 providers after prompt-theft research," November 22, 2026. https://thehackernews.com/2026/11/openrouter-drops-3-providers-after.html

---

**Further reading:** [link to hub article]

If this was useful, follow me for one grounded AI engineering deep-dive a day.
