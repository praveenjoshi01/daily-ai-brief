# Daily AI Brief — 2026-11-24

Lead story marked. Grounding labels show source strength. Items are ranked highest first within each category.

**Inbox status:** Inbox editions read this run: TLDR AI and TLDR Dev (Nov 23), Import AI 482 (Nov 23), and AINews (Nov 24). Grounding labels show source strength.

**Dropped from today's list:** Inkling 2 Mini, the METR update and the Riemann proof (all covered Nov 23, nothing new fetched), Gemini API file slicing and Google's Gemini 4 Neon numbers (social posts only), Noeri's $110M raise, Sierra's valuation, and the consumer and finance items. Searches for the vLLM NVMe test, the Z.ai post and the Livermore paper did not return the primary pages, so those items are labelled accordingly.

## Lead Story

### [LEAD] Epoch AI's Benchmark Reviews: 15 of 30 audited benchmarks are rated Flawed, including SWE-bench Verified, SWE-Bench Pro, Terminal-Bench 4.0.0 and OSWorld 2.1
*Grounding: Primary (Epoch's review pages for Agents' Last Exam, Vending-Bench 2, OSWorld 2.1, Humanity's Last Exam and SWE-bench Verified, plus its rubric, FAQ and benchmark list, all fetched), and the Agents' Last Exam team's published rebuttal (fetched). The reviews are dated Aug 10 to Nov 11; AINews (Nov 24) flagged the two most recent agent reviews.*

Epoch samples about 50 tasks per benchmark and rates it Flawed when errors affect at least 20% of the score. Six benchmarks are Verified and nine could not be reviewed. In Agents' Last Exam v1.1, 22 of 50 sampled tasks could earn full marks through a shortcut. The benchmark's team replies that only 3 of 1,617 recorded runs took one.

**Why it matters:** Check a benchmark's verdict before you quote a score gap. Then run the same audit on your own evals: can a task pass without the work, and does the grader reject correct work?

Sources: [Epoch: included benchmarks](https://epoch.ai/data/benchmark-reviews-documentation/included-benchmarks) · [Epoch: methodology](https://epoch.ai/data/benchmark-reviews-documentation/methodology) · [Agents' Last Exam review](https://epoch.ai/benchmarks/agents-last-exam/review) · [Vending-Bench 2 review](https://epoch.ai/benchmarks/vending-bench-2/review) · [OSWorld 2.1 review](https://epoch.ai/benchmarks/osworld-2-1/review) · [ALE team response](https://agents-last-exam.org/blogs/verifier-check)

## Frontier Labs

### Anthropic launches Claude Ship: agents that review, fix and can approve pull requests
*Grounding: Independent coverage (TechCrunch, Nov 23, fetched) plus AINews (Nov 24). Anthropic's own post was not fetched. No performance figures published.*

The suite has three parts. Code Review is generally available. PR Steward (beta) handles failing checks, merge conflicts and review feedback, and comments on what it changed. Claude Approvals (beta) applies an approval policy the team writes in plain language as a file in the repo. It is rolling out to Team and Enterprise plans on GitHub.

**Why it matters:** The approval policy becomes a file you own and review. TechCrunch reports Anthropic suggests starting in observe-only mode on one repository.

Sources: [TechCrunch: Claude Ship](https://techcrunch.com/2026/11/23/anthropic-launches-claude-ship-letting-ai-agents-review-fix-and-approve-code-changes/)

### OpenAI and Cisco open-source Shirudo: agents write eBPF programs that block an exploit while the patch is prepared
*Grounding: Independent coverage (The Register, Nov 24, fetched) plus AINews. OpenAI's post was not fetched. The claim that OpenAI validated 948 Linux kernel local-root bugs comes from AINews and search summaries only.*

Shirudo builds on Tetragon, from Cisco-owned Isovalent. Agents scan for vulnerable systems and write small in-kernel programs, called shields, as temporary protection. The Register reports the companies expect humans to check every shield before production. It also notes that this could drive demand for Codex, and that virtual patching is not new.

**Why it matters:** A concrete case of agents writing kernel-level controls. The human review step is where the safety sits.

Sources: [The Register: Cisco and OpenAI pitch eBPF kernel plugins](https://www.theregister.com/security/2026/11/24/cisco-and-openai-pitch-ebpf-kernel-plugins-as-the-way-to-tame-the-patchpocalypse/5311795)

### Follow-up: Microsoft reports a perplexity figure on OpenAI's test set, and critics list the confounds
*Grounding: Single secondary source for the new details (AINews, Nov 24, relaying social posts). OpenAI's original essay was fetched on Nov 23.*

AINews relays that Microsoft AI ran MAI-2 Base on OpenAI's evaluation set and reported 0.819. It also relays criticism: tokenizer differences could bias a shared limit, the pretraining metric ignores post-training compute, and OpenAI has not released the test set.

**Why it matters:** Still a pretraining-only number. Treat cross-lab comparisons as rough until the test set is public.

Sources: [OpenAI: Perplexity and Intelligence](https://openai.com/index/perplexity-and-intelligence/)

### Z.ai GLM-5.4: a 750B model converted to a loop transformer
*Grounding: Single secondary source (AINews, Nov 24). Z.ai's blog page returned no content when fetched. AINews says no benchmarks have been published.*

AINews reports that Z.ai adapted its GLM-5 base through continued training so that 28 middle layers run twice per token. It is live for GLM Coding Plan users. API access and open weights are promised later.

**Why it matters:** The second looped model in a week, after Inkling 2 Mini. Wait for published benchmarks before acting on it.

Sources: [Z.ai: GLM-5.4 (not readable this run)](https://z.ai/blog/glm-5.4)

## Research

### Nvidia Nemotron-Labs-Sigma: language models that write text by denoising blocks of token embeddings
*Grounding: Primary (Nvidia research page, fetched) plus TLDR AI (Nov 23) for the checkpoint count. Results are self-reported. No license or limitations stated on the page.*

Sigma comes at 3B and 8B parameters. For each block of text it starts from noise and denoises compact 16-dimensional token embeddings. Nvidia reports the 8B model averages 3.46x the throughput of its own token-by-token decoding on a GB200. TLDR AI counts 14 open checkpoints.

**Why it matters:** A possible route to faster small models for code completion. Test it on your own workload before trusting the speedup.

Sources: [Nvidia: Nemotron-Labs-Sigma](https://research.nvidia.com/labs/genair/sigma/)

### Tencent Hy4: open weights with 770B parameters, 49B active per token, and a one-million-token context
*Grounding: Primary (Hugging Face model card, fetched). Benchmarks are self-reported. The card gives no release date; TLDR AI listed it on Nov 23.*

Hy4 reads text, images and video. It uses sparse attention and ships a small built-in drafter model for speculative decoding. Tencent reports it leads open-weight models on its own finance and research task sets, and says it still trails top proprietary models on research-level math and long-horizon coding. It uses Tencent's own license.

**Why it matters:** A large open-weight option for long-context work. Read the license before you plan a deployment.

Sources: [Hugging Face: tencent/Hy4](https://huggingface.co/tencent/Hy4)

### SciResearch-Eval: a Lawrence Livermore benchmark where the simulator handed to the agent may be wrong
*Grounding: Single secondary source (Import AI 482, Nov 23). The arXiv paper was not located this run.*

Import AI describes a benchmark in which an agent designs heating experiments, fits a supplied heat-conduction simulator, and reports material properties with 95% intervals. The simulator may be missing real physics. Import AI quotes the authors as finding only GPT-6 Astra and Claude Fable 5.2 reliable at default settings in that case.

**Why it matters:** It tests whether an agent reports honest uncertainty when its tools are wrong. That skill matters for any agent that relies on a tool.

Sources: [Import AI 482](https://importai.substack.com/p/import-ai-482-huawei-kernel-benchmarks)

## Engineering & Tooling

### vLLM v0.34.0 sizes the KV cache from the GPU memory that is actually free
*Grounding: Primary (GitHub release notes, dated Nov 16, first 100,000 characters read). The NVMe offload result is from AINews only (Nov 24) and was not found in the release notes.*

The extensible KV cache is now on by default, and gpu_memory_utilization defaults to 1.0. One example grew from 433k to 672k cached tokens on an H200. The notes report 6 to 18% slower per-token decoding on some H200 models at concurrency 128. Separately, AINews relays a vLLM test in which 4.6 TB of NVMe gave 5.1x the throughput of 1 TB of DRAM at 70 sessions.

**Why it matters:** Review your launch flags before you upgrade. The default block size also changed from 16 to 64.

Sources: [vLLM v0.34.0 release notes](https://github.com/vllm-project/vllm/releases/tag/v0.34.0)

## Industry

### Nvidia's board reinstates Jensen Huang as president and CEO, eleven days after his resignation
*Grounding: Primary (Nvidia press release, Nov 23, fetched) plus AINews (Nov 24).*

The board voted unanimously and said it consulted senior U.S. government officials. Colette Kress returns to the CFO role. The independent directors' investigation continues, and the board formed a National Security and Export Control Committee.

**Why it matters:** Leadership at the main GPU supplier is settled for now. The investigation and export-control oversight are still open.

Sources: [Nvidia press release](https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Board-Reinstates-Jensen-Huang-as-President-CEO-and-Board-Director/default.aspx)
