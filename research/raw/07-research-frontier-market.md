# 07 — Research Frontier, Engineering Patterns, Market & Funding

*Agent 7 of 7. Compiled 2026-11-17.*

## Read this first: evidence quality and limits

This run was **badly constrained**, and you should know how before relying on any number below.

- **Network:** `arxiv.org` and `aclanthology.org` do not resolve from this container, so I could not read primary PDFs. I stopped trying other hosts after those two failed, as the environment instructs.
- **Search budget (first pass):** about 14 web searches in, the shared per-turn search budget ran out (200 calls, shared across all 7 parallel agents). Part A was fairly well grounded, but Part B rested on model recall. *The gap-fill pass below has since verified most of Part B.*

Every claim carries one of these labels:

| Tag | Meaning |
|---|---|
| **[verified]** | Confirmed from search results quoting the primary source (abstract, proceedings page, company release, SEC filing) or from consistent reporting in reputable trade press, in either pass |
| **[claimed]** | An author's or company's own claim, seen this session, not independently checked |
| **[inferred]** | My own reasoning or arithmetic |
| **[recall]** | From model training knowledge (cutoff about mid-2026). **Not re-verified this session.** Treat it as a lead to check, not a fact. |

### Gap-fill verification pass (2026-11-17, second agent)

A second pass re-checked this report using **59 web searches** (the cap was 60). It did not fetch any primary PDFs: arXiv and ACL were still blocked, and WebFetch was not used. Raw notes with every source URL are in `/home/user/travel/research/notes/07-gapfill-notes.md`. What changed:

- **Part B is now mostly verified.** Funding, M&A, graveyard dates, FY2025 OTA financials, Phocuswright and GBTA sizing, and platform launches were checked against company releases, SEC filings and trade press (PhocusWire, Skift, TechCrunch).
- **Material corrections:**
  - **DeepTravel** is from **HKUST(GZ) and DiDi**, not Amap/Alibaba.
  - **Perk's** $200M Series E valued it at **$2.7B**, not $1.4B.
  - **Amex GBT–CWT** was **~$540M** and closed on 2 Sept 2025.
  - **Layla acquired Roam Around in Feb 2024**, not 2023.
  - **Mindtrip's** Amex, Capital One and United investments came in **Dec 2025**.
  - **TTG's ~91%** is translation accuracy, not plan accuracy.
  - **Fora's** big 2026 round is a **$60M Series D at $1B**.
- **Major new facts:**
  - **Expedia acquired Layla** (mid-2026).
  - **OpenAI acquired Odessia** and shut its product down (10 Nov 2026).
  - Travel VC fell for a second straight quarter in Q3 2026, and the number of AI rounds was cut in half (Skift).
- **Still unverified:** official affiliate rate cards (most sit behind logins, so the third-party figures are tagged [claimed]), OpenTable and World Nomads affiliate terms, Spotnana's 2024 Series C, funding for Axel, Stardrift and "Pilot", whether "Boardwalk" exists (not found), TravelEval's "collapse" wording, Planner-R1's 8B figure, τ-bench airline pass^8, and any published cost per itinerary. Items not re-checked keep their **[recall]** tag.

---

# PART A — Research & Engineering Frontier

## A1. Benchmarks: what exists and how far the SOTA has moved

### A1.1 The benchmark landscape (2024 → 2026)

| Benchmark | Venue / date | What it tests | Key point | Tag |
|---|---|---|---|---|
| **TravelPlanner** (Xie et al.) | ICML 2024 (arXiv 2402.01622) | Multi-day US trips over a sandbox of ~4M records. Tests hard constraints (budget, room type, cuisine, transport) and commonsense constraints. Two modes: two-stage (tool use + planning) and sole-planning. | GPT-4-Turbo got **0.6% final pass rate** in two-stage mode. It is still the canonical benchmark. | [verified] |
| **TravelPlanner+** | EMNLP 2024 Industry | Personalisation on top of TravelPlanner, using user profiles (pet, cuisine, home city), judged by an LLM-as-judge | Personalised plans preferred over generic ones in up to 74.4% (validation) and 87.3% (test) of cases. Note this is a win rate, not a feasibility rate. | [verified] |
| **Flex-TravelPlanner** (KAIST) | ICLR 2025 Workshop (arXiv 2506.04649) | Constraints added one by one over several turns, plus explicitly prioritised constraints that compete | GPT-4o and Llama-3.1-70B **wrongly favour newly added, lower-priority preferences** over earlier hard constraints | [verified] |
| **NATURAL PLAN** (Google DeepMind) | 2024 (arXiv 2406.04520) | Trip planning, meeting planning, calendar scheduling | Trip-planning solve rates (5-shot): **GPT-4 31.1%, Gemini 1.5 Pro 34.8%**. Accuracy falls to near 0% at 10 cities. Gemini many-shot reaches 39.9% at 800 shots. | [verified] |
| **ChinaTravel** (Nanjing U.) | arXiv 2412.13682, v5 Apr 2026 | Open-ended Chinese travel queries from 1,154 humans, with a DSL for checking compositional constraints | Neuro-symbolic agents reach **27.9% (v2) → 37.0% (v4, Sept 2025)** constraint satisfaction on human queries, about 10× pure-neural (2.6%). The authors argue TravelPlanner's templated queries are **near saturation** for solver methods. | [verified] |
| **TripCraft** (IIT Bhubaneswar + Microsoft India) | ACL 2025 main | Real public-transit schedules, events, attraction categories, personas. Five continuous metrics: Temporal Meal, Temporal Attraction, Spatial, Ordering, Persona. | Moves scoring from pass/fail to continuous quality metrics. Adding parameter info raised Temporal Meal Score from 61% to 80% on 7-day trips. | [verified] |
| **ITINERA** | EMNLP 2024 Industry; Best Paper, KDD UrbComp 2024 | Open-domain urban itinerary planning (OUIP) from natural-language preferences | **LLM + spatial optimisation**: decompose the request → retrieve candidate POIs → cluster-aware spatial ordering → LLM writes the itinerary. Deployed system. LLM-only plans are "circuitous" and impractical. Code is public. | [verified] |
| **TripTailor** (Fudan) | ACL 2025 Findings (arXiv 2508.01432) | Real data: 500k+ POIs, ~4k real itineraries (China), single-turn | SOTA LLMs remain **below human standard** on feasibility, rationality and personalisation | [verified] |
| **TravelAgent** (Fudan) | arXiv 2024 | Modular personalised assistant (tool, recommendation, planning, memory) | Early modular reference design | [recall] |
| **TravelBench** | arXiv 2512.22673 (Dec 2025) | Multi-turn, single-turn and **unsolvable** subsets. GPT-4.1 acts as the user simulator. | Tests whether agents detect impossible requests, which matters for accountability | [verified] |
| **TravelEval** (Weiyi Chen et al.) | arXiv 2606.01046 (Jun 2026) | Six dimensions: accuracy, compliance, temporal feasibility, spatial coherence, economic efficiency, practicality. Sandbox built on real transport and accommodation data. | Across 12 methods, LLMs are weak at spatiotemporal reasoning and budget management. **More elaborate agent strategies and advanced prompting give no consistent gain.** The first pass's "non-linear collapse as preferences accumulate" wording was **not re-found** in the gap-fill snippets, so check the PDF before quoting it. | [verified, abstract-level]; "collapse" [unverified] |
| **Trip+** (HKUST, Tencent Hy, HKUST-GZ) | arXiv 2606.21169 (Jun 2026) | 153 instances and 570 user turns. Interactive, minute-level itineraries revised as events unfold. An LLM simulator rates **experiential quality** (e.g., fatigue). | Across 18 LMs, models **"favor technically feasible but exhausting itineraries that diverge sharply from profiled traveler preferences."** | [verified, abstract-level] |
| **TRIP-Bench** (separate from Trip+) | arXiv 2602.01675 (Feb 2026) | Long-horizon interactive travel agent tasks | At most **50% success on the easy split and under 10% on hard subsets**, even for advanced models | [verified, summary-level] |
| **GroupTravelBench** (Xiang Cheng et al.) | arXiv 2605.25200 (May 2026) | 650 multi-user, multi-turn tasks in 3 difficulty levels, with real profiles, POIs and ticket prices. The simulator withholds preferences until they come up in dialogue. | **Even the strongest frontier agents produce a valid group plan less than 12% of the time.** Substantial weaknesses in preference coverage and group fairness. Third-party leaderboard figures (Qwen3-235B ~3% validity; DeepSeek-V4-Pro 64.5% preference coverage) are [claimed]. | [verified, abstract-level] |
| **AI Tour Meeting** | arXiv 2607.18806 (Jul 2026) | LLM agents act as proxies for group members negotiating a trip | Group-preference aggregation via agents | [verified, abstract-level] |
| **MobilityBench** | arXiv 2602.22638 (Feb 2026) | Route-planning agents in real mobility scenarios | Spatial and transit side | [verified, title-level] |
| **PlanningBench** | arXiv 2605.20873 (May 2026) | Scalable, verifiable planning data for evaluation **and training** | A source of RL training data | [verified, title-level] |
| **τ-bench / τ²-bench** (Sierra) | 2024 (arXiv 2406.12045; ICLR 2025) / 2025 | Airline and retail customer-service agents with a simulated user and policy compliance; pass^k reliability metric | GPT-4o function-calling agent: **pass^1 ~61% retail, ~35% airline**. Retail **pass^8 drops to ~25%**, about 60% below pass^1. The best template for post-booking change and cancel flows. The airline pass^8 value was not found. τ²-bench is [recall]. | [verified] (τ-bench) |

### A1.2 Best published results on TravelPlanner, and what moved them

| Approach | Technique | Final pass rate | Tag |
|---|---|---|---|
| Original baselines (2024) | ReAct / CoT, GPT-4-Turbo | **0.6%** (two-stage) | [verified] |
| LLM-Modulo (Kambhampati group, 2024) | LLM proposes, **external critics** (format, hard constraints, commonsense) send feedback, up to 10 iterations | **20.6%** vs 4.4% baseline (GPT-4-Turbo). A follow-up reports GPT-4o 8.3% → 23.9% and Claude-3.5-Sonnet 4.4% → 25%. | [verified] |
| ATLAS (Google Research; ICLR 2026) | Multi-agent: **dynamic constraint management + iterative plan critique + adaptive interleaved search** | **44.4%** with Gemini-2.5-Pro vs 23.3% for the best alternative (PMC) and 20.6% for ReAct. With Claude-Sonnet-4: 23.3% vs 14.4% (PMC). Reaches **84%** in a separate live-search, multi-turn setting (ReAct 59%, monolithic agent 27%). | [verified] |
| Agentic RL: **Planner-R1** (LinkedIn, 2509.25779) | RL with shaped (dense, process-level) rewards on Qwen3-8B/32B | **56.9% final pass rate** on the TravelPlanner test leaderboard using **only 180 training queries**. That is about 2.7× the GPT-5 baseline of 21.2%. v1 attributes 56.9% to the 32B model. The 8B model is the most compute-efficient (one summary reports 3.5× less compute and 1.5× less memory) but depends more on dense reward shaping. Curriculum learning alone gave no benefit. Out-of-domain performance (Multi-IF, NaturalPlan, τ-bench) was maintained. The 8B pass rate was not retrieved. | [verified, abstract-level] |
| Agentic RL: **DeepTravel** (HKUST-GZ + **DiDi**, 2509.21842) | End-to-end agentic RL in a sandbox of cached transport, hotel and POI data. Hierarchical reward: trajectory-level spatiotemporal feasibility, then a turn-level detail check. Replay-augmented RL from a buffer of failures. | Qwen3-32B **outperforms o1, o3 and DeepSeek-R1** on the authors' travel tasks. **82% itinerary-generation accuracy in a 3-month online test in DiDi's enterprise app.** Not on TravelPlanner. | [verified abstract]; 82% is [claimed] |
| Agentic RL: TourPlanner (2601.04698, constraint-gated RL) | Constraint-gated RL | Numbers not retrieved | [verified existence] |
| A "source code agent" style method (2025/26) | Plans as executable code | 35.6% on the 1,000-task test set, claimed +97.6% over ATLAS on the same backbone. The paper's own baseline numbers for ATLAS don't match the ICLR paper. | [claimed] |
| **Formal verification / SMT** (Hao, Chen, Zhang, Fan — MIT; NAACL 2025) | LLM translates the request into a **constraint satisfaction problem → Z3/SMT solver**. If the solver says UNSAT, the LLM reads the unsat core and proposes **relaxations to the user**. | **93.9% final pass rate** (93.3% validation). Other citations say 97% vs 4% for LLM-only. | [verified] |
| TTG "To the Globe" (Da Ju, Arman Zharmagambetov et al.; EMNLP 2024 Demo; arXiv 2410.16456) | A fine-tuned LLM translates the request into a **MILP** spec. The solver is pluggable (SCIP, Gurobi) and returns an optimal plan, which is then rendered back to natural language. | Responds in **~5 s**. **~91% exact-match translation accuracy** (back-translation metric). This is *not* a plan pass rate; the first pass misstated it. The Meta (FAIR) affiliation is [recall] and was not confirmed in snippets. | [verified] |
| LLMFP (Hao et al., ICLR 2025) | General LLM → formal optimisation formulation | Generalises the SMT idea beyond travel | [recall] |

**What moved the numbers, in order of effect size:**

1. **Taking the combinatorial search away from the LLM.** Solver hybrids (SMT, MILP) reach 90%+ against single digits for prompting-only methods. This is the biggest lever by far. ChinaTravel explains why: TravelPlanner's templated constraints are exactly what solvers handle well, so the benchmark is close to "solved" for neuro-symbolic systems. The open problem is **open-ended, preference-laden, real-data** queries, where the best neuro-symbolic systems drop to about 37% (ChinaTravel v4).
2. **External verification loops** (LLM-Modulo critics, ATLAS's critique agent): roughly 3–5× over baseline.
3. **Explicit constraint tracking as state** (ATLAS's constraint manager). Flex-TravelPlanner shows models forget or down-rank earlier constraints, so constraints must live in a structured store rather than only in the context window.
4. **Agentic RL on verifiable rewards.** It lets small models compete, which cuts inference cost. Planner-R1 reaches 56.9% with 180 training queries, against 21.2% for GPT-5. It still trails solver hybrids (90%+) on hard constraints.
5. **Better base models** helped, but less than any of the above. Note that ATLAS with Claude-Sonnet-4 scores about half of ATLAS with Gemini-2.5-Pro, so the backbone still matters inside agentic scaffolds.

**Where research says pure LLMs fail** (consensus across papers):
- Holding many hard constraints at once (budget plus room plus cuisine plus dates).
- Arithmetic over budgets.
- Spatial coherence: routes are "circuitous" (ITINERA).
- Temporal feasibility: opening hours, transit schedules (TripCraft).
- Prioritising constraints across turns (Flex-TravelPlanner).
- Accumulating preferences (TravelEval's "collapse").
- Spotting unsolvable requests (TravelBench).
- Experiential realism such as fatigue and pacing (Trip+).
- Fusing group preferences (GroupTravelBench).

### A1.3 Classic (pre-LLM) literature that should be reused, not reinvented [recall]

- **Tourist Trip Design Problem / Team Orienteering Problem with Time Windows (TOPTW).** Choose the subset of POIs that maximises total "score" under a time budget, opening-hour windows and travel times. The problem is NP-hard, but city-day instances (20–60 candidate POIs) are solved near-optimally in milliseconds to seconds. Methods: iterated local search (Vansteenwegen et al., 2009), CP-SAT/MILP, or OR-Tools routing with time windows. Surveys: Gavalas et al. 2014 on tourist trip design; Vansteenwegen et al. 2011 on orienteering.
- **Personalised tour recommendation.** Lim et al.'s PersTour (IJCAI 2015 / KAIS 2018) learns POI interest from geotagged photo histories and plugs it into orienteering. Time spent at a POI is personalised by interest level. **This is how to turn implicit signals into solver weights.**
- **Group recommender aggregation** (Masthoff). Strategies: average, least misery, most pleasure, average-without-misery, fairness over a sequence. For multi-day trips, **sequence fairness** works well (a different member's favourite each day). Recent LLM group benchmarks (GroupTravelBench, AI Tour Meeting) bring this back.
- **Beyond-accuracy metrics** (Kaminskas & Bridge, ACM TiiS 2016): diversity, novelty (inverse popularity), serendipity (relevant *and* unexpected), coverage. These are the standard ways to **measure "non-generic-ness."**
- **Preference elicitation.** Conversational recommender systems literature: critiquing-based recommenders, and choosing questions by value of information. The 2026 benchmarks (GroupTravelBench, Trip+) now score elicitation explicitly.

## A2. Engineering patterns in production travel agents

> Caveat: the gap-fill pass verified launches and some architecture details from talks and trade press. **No company has published a full architecture or a cost per itinerary.** Rows tagged [recall] were not re-checked.

| Company | What is publicly known about the build | Tag |
|---|---|---|
| **Booking.com** | **AI Trip Planner** talk by Moran Beladev (PyData Tel Aviv 2025): speculative decoding with **Medusa-1 gave a 1.8× inference speedup**; production evaluation uses **LLM-as-judge** (including dialogue quality). Booking runs an **orchestration layer that lets teams switch between models**. It pairs **small travel-specific models (fast, cheap) with large LLMs (reasoning)**: classify the query → RAG → call APIs or specialist models. A partner guest-messaging agent was evaluated by LLM-as-judge plus human review for failure modes. Arize is used for observability. **Apps-in-ChatGPT launch partner (DevDay, 6 Oct 2025)**, with checkout on Booking's own site. CFO (Mar 2026): LLM referral traffic is **<1% of room nights**, and AI cut **customer-service cost per booking ~10% YoY**. | [claimed] talk/trade press; ChatGPT app and CFO remarks [verified] |
| **Expedia** | **Romie** launched May 2024 (group-trip "travel buddy") on a **mix of in-house and OpenAI models** (TechCrunch). **Romie has since been retired.** CPO Shilpa Ranganathan (Skift Data + AI Summit, 2026): early booking chatbots stalled; the fix was **rebuilding the evaluation framework and data plumbing so the assistant answers from live inventory**; "AI is an organizational problem before a technological one." Expedia app in ChatGPT (6 Oct 2025). **Acquired Layla (2026).** CFO: AI compute costs rising in H2 2026, funded by cuts elsewhere, and not disclosed as a line item. | [verified] trade press |
| **Kayak** | **AI Mode launched 15 Oct 2025**: natural-language search that combines Kayak's price data with ChatGPT. It graduated from the Kayak.ai testbed (Apr 2025). The CEO said agentic checkout was planned. | [verified] |
| **Tripadvisor** | Three-year **Perplexity** alliance (1B reviews, plus Viator's 300k+ experiences); Tripadvisor app in ChatGPT (Nov 2025). No in-house assistant architecture published. | [verified, headline-level] |
| **Airbnb** | On the Q2 2025 call, Chesky said the AI customer-service agent is **built on 13 models**, trained on tens of thousands of conversations, and will be brought into search and trip planning. By **Q1 2026 it resolved >40% of inquiries** (up from ~1/3). Cost per booking fell ~10% YoY (another report says ~16%). Pattern: model routing plus heavy policy grounding. | [verified] trade press |
| **Navan** | **Ava** handles **~60% of customer interactions (Q2 FY27)**, up from 50–54% earlier, at about **8,000 support conversations a day** with a CSAT of 78. It performed well during the CrowdStrike outage (Jan 2025 Skift interview). Its edge is policy-aware booking with Navan's own inventory and operations. | [claimed] company investor materials |
| **Mindtrip** | Free to travellers. Revenue comes from **affiliate links plus B2B "Mindtrip for Business"** sold to tourism boards, agencies, airlines and hotels. Viator is a partner. Uses a curated place DB, a maps-first UI and group chat (launched with the Sep 2024 round). Revenue estimated at ~$3.6M for 2025 (Latka estimate). LLM cost per user **not published**. | [verified] model; revenue [claimed estimate] |
| **Layla** (acquired Roam Around Feb 2024; **acquired by Expedia 2026**) | Berlin-based conversational planner founded 2023 (CEO Saad Saeed). Monetised by affiliate booking links plus a subscription; it continues to operate under Expedia. Skyscanner co-founder link is [recall]. | [verified] except as noted |
| **Hilton** | A Claude-based trip planner shows slightly higher conversion. The CIO describes the backend cost as "tokenomics" that the company watches closely. | [claimed, secondary summary of Skift] |
| **Google** | **AI Mode (17 Nov 2025):** a trip-planning **Canvas** built from live flight and hotel results, Maps reviews and web content (US desktop, Labs). **Agentic restaurant reservations** for US users. Event tickets and local appointments in Labs. **Flight and hotel agentic booking was previewed** with Booking.com, Expedia, Marriott, IHG, Choice and Wyndham, without a launch date at the time. **Flight Deals** is available in 200+ countries. Google had also shelved a planned AI trip planner in Mar 2025 (secondary). Google's moat: the Maps POI graph, reviews, live hours, and Flights/Hotels price data. | [verified] |
| **DiDi (HKUST-GZ)** — *corrected from "Alibaba/Amap"* | DeepTravel (arXiv 2509.21842) is an end-to-end agentic-RL travel agent deployed in **DiDi's enterprise app**, with 82% itinerary accuracy in a 3-month online test. This is the clearest public **production-RL** travel agent. | [verified abstract] |
| **Google Research** | ATLAS (above) is the most detailed public multi-agent travel architecture from a hyperscaler | [verified] |
| **OpenAI** | **Acquired Odessia** (an AI travel agent from Sonder founder Francis Davidson) on 10 Nov 2026 and shut down its standalone product, so this looks like an acqui-hire. It signals that OpenAI is building travel agent capability in-house, alongside the ChatGPT apps. | [verified] |

**Common production pattern** [inferred from the above]:
- A frontier LLM handles conversation and intent.
- The company's own ranking and recommendation stack picks inventory. The LLM does not pick inventory from its own knowledge.
- Live supplier APIs supply prices and availability.
- A thin itinerary composer sits on top.
- Distribution increasingly runs **through** the assistants (ChatGPT apps, Gemini, Perplexity) rather than against them.

**Nobody publicly claims solver-backed feasibility guarantees.** That is a gap.

### Open-source reference implementations [recall unless noted]
- **Google ADK `travel-concierge` sample** (google/adk-samples, `python/agents/travel-concierge`) **[verified exists]**. A root coordinator over **6 sub-agent groups** (inspiration, planning, booking, pre-trip, in-trip, post-trip), **20+ agents**, the largest ADK sample. Tools: **Places API, Google Search grounding, an MCP server**. It also ships as a Google Workspace add-on tutorial. That booking is stubbed or mocked is [recall]. A good *orchestration* template. Its weakness: no real feasibility checking, so data quality is only as good as Google Search and Places grounding.
- **CrewAI `trip_planner`** example. Role-play agents (city expert, local guide, planner) with web search. Typical failure: generic web-scraped "top 10" content, no constraint checking, high token use.
- **LangGraph** customer-support tutorial (travel and airline tools, human-in-the-loop interrupts on sensitive actions). Shows the **approval-gate pattern** needed before booking.
- **OpenAI** customer-service agents demo (airline triage, seat, cancellation agents with guardrails). **Sierra τ-bench** for policy-compliant airline agents.
- **ITINERA** (github.com/YihongT/ITINERA) is the most useful *research* reference for LLM + spatial optimisation.
- **TripTailor**, **ChinaTravel** and **TravelPlanner** sandboxes can serve as regression test suites.

Shared limitation of all the demos: no ground-truth data layer, no verification, no evaluation harness, no handling of supplier booking state (holds, payments, cancellations).

### Cost per itinerary [inferred]
A fully agentic multi-day itinerary typically involves:
- 20–60 tool calls (search, places, routing, prices),
- 100k–400k input tokens (mostly re-read context),
- 5k–15k output tokens.

At frontier mid-tier prices (about $1–3 per million input and $5–15 per million output, 2026), that costs **about $0.20–$1.50 without caching**. Prompt caching, small-model routing for tool steps, and solver offload can bring it to **about $0.05–$0.30**. Add maps and places API costs: Google Places and Routes calls can each cost a few cents, and an itinerary can need dozens of them, so **mapping data can cost as much as the LLM**.

**Gap-fill check:** no travel company has published a cost per conversation or per itinerary. The closest public evidence:
- Booking.com and Expedia both describe **small-model routing and orchestration to control cost** [claimed].
- Expedia's CFO says AI compute costs are rising but are not broken out [verified].
- Hilton's CIO talks about watching "tokenomics" [claimed].
- HRS forecasts blended inference falling from ~$15 to ~$6 per million tokens [claimed forecast].
- Airbnb and Booking report **support cost per booking down ~10% YoY from AI** [verified].

So far, the documented savings are in **customer service**, not planning.

---

## A3. Hard sub-problems and SOTA approaches

| Sub-problem | Why LLMs fail | SOTA / recommended approach |
|---|---|---|
| **Temporal and spatial feasibility** (opening hours, transit, durations) | No grounded clock or map; arithmetic errors; zig-zag routes (ITINERA, TripCraft) | Formulate as **TOPTW**. Get a travel-time matrix from a routing API or OSRM/GTFS; time windows from verified hours; visit durations from priors or personalisation. Solve with CP-SAT/MILP or ILS. The LLM only proposes the candidate set and utilities, then writes the narrative. |
| **Budget constraints** | Arithmetic and the tendency to forget constraints | Hard linear constraint in the solver. Use live prices only, with price-freshness timestamps. |
| **Multi-turn constraint drift** | Recency bias toward new, lower-priority asks (Flex-TravelPlanner); collapse as preferences pile up (TravelEval) | A **typed constraint store** (hard/soft, priority, source turn, confidence) kept outside the context window, re-checked every turn (ATLAS-style constraint manager) |
| **Unsatisfiable requests** | Hallucinated "solutions" (TravelBench's unsolvable subset) | SMT/MILP **unsat cores → minimal relaxation suggestions** ("drop the 4-star requirement *or* add $180"), as in Hao et al. This is the foundation for accountability. |
| **Group preferences** | Tends to average everyone into blandness | Elicit per member. Aggregate with average-without-misery plus sequence fairness. Make trade-offs explicit and attribute them by member ("Day 2 lunch is Maya's pick"). Benchmark: GroupTravelBench. |
| **Re-planning under disruption** | Full regeneration loses commitments and churns the plan | **Repair, don't regenerate.** Freeze booked or non-refundable items as fixed constraints and re-solve the rest with minimal-change objectives (penalise edits to the existing plan). Trip+ evaluates exactly this. τ-bench-style policy tests cover change and cancel flows. |
| **Explainability** | Post-hoc rationalisation | Explanations generated *from solver state*: which constraint is binding, what each choice traded off, data provenance (source, last verified date). |
| **Non-generic-ness / serendipity** | LLM priors over-represent the popularity head; this is the cliché problem | Measure **novelty** (e.g., −log of a POI's popularity rank, or the share of picks outside the top-N tourist list), **intra-list diversity**, and **serendipity** (rated relevant *and* outside the user's expected set). Fix it through **retrieval from long-tail local sources plus popularity-debiasing in the solver objective**, not prompting. Report a "cliché rate" against a reference list such as the top-20 Tripadvisor attractions. |
| **Personalisation from implicit signals** | Context-window "memory" is shallow | PersTour-style learned interest vectors (past trips, saves, dwell time, map interactions) → per-POI utility and per-POI duration in the solver |
| **Experiential quality** (fatigue, pacing, meal timing) | Not modelled (Trip+, TripCraft) | Soft constraints: daily walking km, a cap on consecutive "heavy" activities, meal windows, buffer time, jet-lag day-1 rules. Score with TripCraft-style continuous metrics. |
| **Evaluation validity** | LLM-as-judge has position, verbosity and self-preference bias; TravelPlanner+ relies on an LLM judge | **Programmatic checks for anything checkable** (feasibility, budget, hours, distance). Use LLM judges only for subjective dimensions, with pairwise and position-swapped comparisons, calibrated against a human-labelled set (report agreement). Run user-simulation evaluation (τ-bench, GroupTravelBench style) and report pass^k for reliability. |

---

## A4. Recommended "best-in-class" architecture

```
┌──────────────────────── Conversation layer (frontier LLM) ────────────────────────┐
│ Intent + elicitation (value-of-information questions) · group member threads      │
│ Narration of plan · explanations from solver state · provenance citations         │
└──────────────┬─────────────────────────────────────────────────────▲──────────────┘
               │ typed TripSpec (JSON)                               │ plan + trace
┌──────────────▼───────────────┐   ┌──────────────────────┐   ┌─────┴──────────────┐
│ Constraint & Preference Store│──▶│ Candidate generation │──▶│  SOLVER            │
│ hard/soft, priority, owner,  │   │ retrieval over POI   │   │ CP-SAT/MILP TOPTW  │
│ provenance, turn, confidence │   │ graph + long-tail    │   │ + SMT for UNSAT    │
│ (persisted, re-validated)    │   │ local sources; LLM   │   │ cores → relaxations│
└──────────────────────────────┘   │ scores utility/fit   │   │ repair mode (min-  │
                                   └──────────┬───────────┘   │ change re-solve)   │
                                              │               └─────┬──────────────┘
┌─────────────────────────────── Data layer ──▼─────────────────────▼──────────────┐
│ POI knowledge graph: hours (with last-verified ts), durations, price levels,     │
│ seasonality, accessibility; local-expert/creator content w/ attribution;         │
│ travel-time matrices (routing API / OSRM / GTFS); live price/availability via    │
│ supplier APIs (cached w/ TTL); popularity stats for debiasing                    │
└──────────────────────────────────────┬───────────────────────────────────────────┘
┌──────────────────── Verification loop (independent of planner) ──────────────────┐
│ Programmatic critics: feasibility, hours, budget, distance, pacing; freshness    │
│ check (re-fetch anything older than TTL before showing/booking); link/entity     │
│ existence check; LLM critic only for subjective fit → back to solver             │
└──────────────────────────────────────┬───────────────────────────────────────────┘
┌──────────── Booking / action layer: human-approval gates, holds, MoR or ─────────┐
│ affiliate deep links, post-booking monitoring & disruption re-plan triggers      │
└──────────────────────────────────────────────────────────────────────────────────┘
Eval harness: TravelPlanner/ChinaTravel/TripCraft regression · in-house real-city
sandbox · user simulator (multi-turn, group, unsolvable cases) · pass^k · cliché/
novelty/serendipity metrics · human-calibrated pairwise LLM judge · prod telemetry
(edit rate, booking rate, on-trip deviations, complaint/refund rate)
```

**Design principles, with the research behind each:**
1. **Planner/solver split.** The LLM never does combinatorics or arithmetic. Evidence: 0.6% → 93.9% on TravelPlanner with SMT; ITINERA's spatial optimiser.
2. **Constraints as persistent typed state**, not context. Evidence: Flex-TravelPlanner, ATLAS, TravelEval.
3. **UNSAT is a feature.** Explain infeasibility and offer minimal relaxations. Evidence: Hao et al.; TravelBench's unsolvable subset.
4. **Every fact carries provenance and a freshness timestamp.** Re-verify before display or booking. This addresses stale data, hallucination and accountability.
5. **Optimise against the popularity head.** Put novelty and serendipity terms in the objective, tunable per user ("first-timer classics" vs "local-only"), and measure a cliché rate. This addresses generic recommendations.
6. **Repair, don't regenerate**, for disruption. Use minimal-change re-solve.
7. **Use RL for small, cheap models** on the tool-calling and orchestration steps (Planner-R1, DeepTravel) once the eval harness exists, to cut cost.
8. **Evaluation ladder:** programmatic critics, then a user simulator, then a human-calibrated judge, then production outcomes.

---

# PART B — Market, Funding, Business Models

> **Status after the gap-fill pass:** most figures below are now **[verified]** against company releases, SEC filings or reputable trade press. Affiliate rates remain mostly **[claimed]** by third parties because the official rate cards sit behind logins. Rows still tagged [recall] were not re-checked.

## B1. Market size (with skepticism)

| Figure | Value | Tag / comment |
|---|---|---|
| Booking Holdings FY2025 | **Gross bookings $186.1B (+12%)**, revenue **$26.9B (+13%)**, so a revenue take of **~14.5%**. Room nights 1,235M (+8%). Merchant $130.0B vs agency $56.1B, as Booking shifts to merchant. 68M airline tickets ($16.8B GB). Adj. EBITDA >$9.9B. | [verified] 10-K, Q4 release |
| Expedia Group FY2025 | **Gross bookings $119.6B (+8%)**, revenue **$14.7B (+8%)**. Adj. EBITDA ~$3.5B. FCF $3.11B. 2026 guidance: GB $127–129B, revenue $15.6–16.0B. | [verified] 8-K |
| Airbnb FY2025 | **GBV ~$91.3B (+12%)**, revenue ~$12.2B (+10%), 533M nights and seats (+8%). Q4 GBV $20.4B (+16%). | [verified] Airbnb release |
| Trip.com Group FY2025 | Net revenue **RMB62.4B (~US$8.9B, +17%)**. Accommodation RMB26.1B (+21%); transport RMB22.5B (+11%); packaged tours RMB4.7B; corporate RMB2.8B. Net income was inflated by RMB19.9B of investment gains. Trip.com reports revenue, not gross bookings. | [verified] company release |
| Global travel gross bookings (Phocuswright, Dec 2025) | **~$1.67T in 2025**; **online ~$1.07T (+8%)**; OTAs ~$408B. Online is expected to be ~65% of the total by 2026, and APAC is 36% of OTA sales. An earlier (Jan 2025) forecast had online at $1.2T by 2026. | [verified] secondary coverage of Phocuswright |
| Global business travel spend (GBTA BTI, Jul 2025) | **$1.57T in 2025 (+6.6%)**; 2024 revised to $1.47T; expected to pass $2T by 2029. US $395.4B, China $373.1B. Still ~14% below pre-pandemic, inflation-adjusted. | [verified] GBTA release |
| "AI in travel" / "AI trip planner" market reports | Range from hundreds of millions to tens of billions of dollars, with CAGRs of 15–30% | [recall]. **Low credibility.** These are paywalled syndicated reports with inconsistent definitions. Deliberately not re-searched. Don't anchor on them. |
| LLM-referred travel demand | Booking CFO (Mar 2026): LLM referral traffic is **<1% of room nights** | [verified] Skift |
| Travel startup VC | Travel startups raised **$3.4B in 2025 (+11% vs 2024)** [secondary]. **2026: $2.2B across 302 rounds Jan–Sep** (Crunchbase, secondary). Skift tracker: **110 rounds in Q1 → 75 in Q2 → 57 in Q3 2026**. AI-native companies took 12 Q3 rounds (21%), and **AI rounds were cut in half**. Phocuswright Europe 2026 called startup funding a "decade low". | [verified] Skift / PhocusWire; Crunchbase totals [secondary] |

**Skeptical framing** [inferred]:
- "AI trip planning" is not a market of its own. It is a **front-end** to a large but mature booking market whose economics are already split among OTAs, metasearch, Google and suppliers.
- The money available to a new entrant is the **share of distribution margin** it can capture: affiliate fees, merchant-of-record margin, or subscription.
- The most useful sizing is bottom-up: (number of planned trips) × (booking value influenced) × (commission per vertical).
- The verified numbers support this. The four largest OTAs alone process **~$400B+ of gross bookings**, at a **~12–15% revenue take**. That take is the pool an AI front end competes for, and LLM-referred bookings are still under 1% of Booking's volume [inferred from verified figures].

## B2. Funding, M&A and the graveyard (2023–2026)

### Funding and exits [verified unless tagged]

| Company | Category | Funding / exit events | Notes | Tag |
|---|---|---|---|---|
| **Navan** (ex-TripActions) | Corporate travel and expense | **IPO priced 29 Oct 2025 at $25** (range $24–26) and began trading on Nasdaq (NAVN) on 30 Oct. It raised **~$923M**: 30M new shares for $750M, plus ~6.9M secondary shares. Valuation at pricing was **~$6.2B** (Reuters), or a $6.9B market cap per Renaissance. The stock **opened at $22 and closed day one ~$20 (−20%), about $4.7B**. **Nov 2026:** ~$25 per share, **~$6.3–6.9B market cap**, 52-week range $8.11–$30.88, TTM revenue ~$0.8B, TTM net loss ~$348M (aggregator data). | Even the category leader IPO'd well below its 2022 private value of $9.2B and dipped as low as ~$8. It has since recovered to around the IPO price. | [verified]; current market cap [claimed, aggregators] |
| **Perk** (ex-TravelPerk) | Corporate travel | **$200M Series E, 28 Jan 2025, at $2.7B post-money**, led by Atomico with Sequoia, EQT Growth, General Catalyst and Kinnevik. It also **acquired Yokoy** (expense) in an all-equity deal. Its prior round was a $104M Series D (Jan 2024, SoftBank) at $1.4B. Rebranded to Perk. | **Corrects the first pass's $1.4B.** | [verified] |
| **Spotnana** | Travel-as-a-service infrastructure (B2B) | $34M Series A (2021); **$75M Series B (Jul 2022, Durable Capital)**. One aggregator lists a **$75M Series C (Dec 2024) at $1.2B** led by ICONIQ and Madrona. | The infrastructure ("picks and shovels") play | Series B [verified]; Series C [claimed, aggregator only] |
| **Mindtrip** | Consumer AI planner | **$7M seed (2023, Costanoa)**; **$12M (Sep 2024, Forerunner + Costanoa)**, launched alongside group chat; **Dec 2025: strategic investments from Amex Ventures, Capital One Ventures and United Airlines Ventures** (amount undisclosed; CB Insights calls it a Series B). Total ~$19M+ per CB Insights, and the company says >$20M. | Card and airline strategic investors (Dec 2025, **not** 2024 as first stated) point to **distribution through partners**. Monetises through affiliate plus B2B. | [verified] |
| **Layla** | Consumer AI planner (Berlin, founded 2023) | Seed of ~€3M (PhocusWire), or ~€5M total (Crunchbase via Skift), from First Minute Capital and M13. **Acquired Roam Around in Feb 2024.** **Acquired by Expedia Group in mid-2026**, terms undisclosed. Layla keeps operating. | An OTA buying an AI planner shows that **acquisition by incumbents is the realistic exit** for consumer planners | [verified] |
| **Fora** | Travel-advisor host agency + software | **Series D $60M at $1B post-money (16 Jul 2026)**, led by Forerunner and Tactile Ventures. **~$138.5M raised in total.** **>$3B in bookings and >15,000 advisors.** Funds go to the **Via** AI advisor assistant and to expanding into cruise, flights and enterprise. The first pass's rounds (A $13.5M 2022, B ~$20M 2023, C ~$60M 2025, Thrive) are [recall] and not re-checked. | Human advisors plus software. Monetised through supplier commissions shared with advisors. **The only new travel unicorn of 2026 found.** | Series D [verified]; earlier rounds [recall] |
| **Tern** | Software for travel advisors | **$13M Series A (May 2025)**, led by Viewpoint Ventures and Haystack with Upfront. $17M raised in total (company figure). Later **acquired Lucia** (advisor services) and launched agentic AI for advisor workflows. | B2B to advisors | [verified] |
| **Airial** | Consumer AI planner (ex-Meta founders Archit Karandikar and Sanjeev Shenoy) | **$3M seed (Jun 2025)**, led by Montage Ventures with South Park Commons and Peak XV. Turns social-media travel content into bookable trip plans. | | [verified] |
| **Odessia** | Consumer AI travel agent (Francis Davidson, ex-Sonder) | ~$6M pre-seed/seed led by **Sequoia**; product launched mid-2026. **Acquired by OpenAI on 10 Nov 2026**, terms undisclosed. **The standalone product was shut down the same day**, which looks like an acqui-hire. | A foundation-model lab bought a travel agent team; the platforms are moving in-house | [verified] |
| **Hopper** | Consumer OTA/fintech + B2B (HTS) | Series G $175M (2021) at $3.5B; PitchBook valued it at $5B (2022). In Jan 2025 the CEO discussed a future TSX/Nasdaq listing at $5–10B. **No 2025–26 priced round found.** Restructured with job cuts twice in a year (Nov 2024). B2B was reported as ~two-thirds of revenue (2024). **Mar 2026: RBC travel rewards partnership, replacing Expedia.** **FTC $35M settlement over hidden fees (2 Jul 2026)**. | Shift to B2B; the regulatory risk of fee-heavy fintech add-ons is now concrete | Mostly [verified]; FTC item [secondary]; B2B share [claimed] |
| **Otto** | AI assistant for unmanaged business travel | **$6M seed (Aug 2024)**, led by Madrona with Direct Travel. CEO Michael Gulmann (ex-Expedia/Egencia). Conceived with Steve Singh (Concur founder). Integrates Spotnana and Direct Travel. | | [verified] |
| **BizTrip.AI** | Corporate travel "without the search bar" | **$1.5M pre-seed** (Q1 2026 roundup). Pilots with Moderna and Cain Travel. | | [verified] |
| **Vuelo** | AI-native booking + BNPL (London, FCA-regulated, founded 2025) | **£56M (25 Mar 2026): £6M equity** (Backed VC, Play Ventures) **+ £50M debt** (Viola Credit) | The headline is mostly debt to fund instalment lending | [verified] |
| **Holiwise** | AI travel agency, premium (London) | **€1.45M pre-seed (Aug 2025)**, for an AI agent, dynamic packaging and concierge | | [verified] |
| **Stippl** | Social travel planner (Amsterdam) | €575k pre-seed (Apr 2024, Marbruck, Volve). PhocusWire reports a later round (amount not seen). | | [verified] 2024 round |
| **Stardrift** | AI planner for frequent flyers (YC S24, founder Leila Clark) | ~$500K pre-seed per a single aggregator | | [claimed] |
| **Axel** | AI agent offering private travel rates, built by **Gordian Software** (YC W19) | Gordian: $25M Series A (Jul 2022, ~$200M valuation). Axel-specific: Dealroom lists a $125k seed. | | Gordian [verified]; Axel [unverified] |
| **HeyMax** | Loyalty/rewards travel (PhocusWire Hot 25 2026) | $11M Series A (Q1 2026) | | [verified, roundup] |
| **Amex GBT** | TMC | **Closed the CWT acquisition on 2 Sep 2025, at ~$540M** cash-free/debt-free (announced Mar 2024). Expects ~$155M in run-rate synergies. | Corporate-travel consolidation. **Corrects the first pass's ~$570M.** | [verified] |
| **Amadeus** | GDS | Acquired **SkyLink** (Hot 25 2026 startup) in Q1 2026 | | [verified, roundup] |
| **Pilot** | — | **No funding data found** | | [unverified] |
| **Boardwalk** | — | **No AI travel startup by this name found** in two passes, so it likely doesn't exist under this name. Similar names: Boop (social recommendations → bookable itineraries, Nov 2025), Walk.AI. | | [not found] |

**Platform moves 2025–2026:**
- **Apps in ChatGPT** (OpenAI DevDay, **6 Oct 2025**, Apps SDK): Booking.com and Expedia were launch partners (with Spotify, Figma, Coursera, Zillow, Canva). Checkout happens on the partner's site. A Tripadvisor app followed in Nov 2025. [verified]
- **Google AI Mode (17 Nov 2025):** trip-planning Canvas; agentic restaurant reservations; flight and hotel agentic booking previewed with Booking.com, Expedia, Marriott, IHG, Choice and Wyndham. [verified]
- **Kayak AI Mode** (15 Oct 2025), powered by ChatGPT. [verified]
- **Tripadvisor–Perplexity** three-year alliance (reviews plus Viator inventory). [verified headline]
- **OpenAI acquired Odessia** (Nov 2026). **Expedia acquired Layla** (2026). [verified]
- OpenAI **Operator** launch partners (Jan 2025), Perplexity hotel booking via Selfbook, Microsoft Copilot travel actions. [recall, not re-checked]

Implication: the general assistants are becoming the **default free trip planner** and integrate OTA inventory directly. In 2026 both the OTAs (Expedia–Layla) and the labs (OpenAI–Odessia) started **buying** AI-planner teams. Meanwhile VC for AI travel rounds halved (Skift Q3 2026). The realistic outcomes for a consumer AI planner are a **strategic acquisition** or a **B2B/embedded pivot**.

### The graveyard and pivots [verified unless tagged]

| Company | Era | Outcome | Lesson | Tag |
|---|---|---|---|---|
| **Google Trips** | 2016–2019 | Shutdown announced Jun 2019; **app support ended 5 Aug 2019**. Features moved to Maps, Search and google.com/travel. No official reason given. | Even Google couldn't sustain a standalone planning app. Planning is low-frequency and gets absorbed into search. | [verified] |
| **Hipmunk** | 2010–2020 | Acquired by SAP Concur (2016). **Consumer Hipmunk and Concur Hipmunk were both retired on 23 Jan 2020.** Co-founders Adam Goldstein and Steve Huffman offered to buy it back and were refused. Concur's stated reason: its integrated T&E approach had "evolved". | Great UX did not overcome metasearch economics. The acquirer had no use for a consumer brand. | [verified] |
| **Lola** (Paul English) | 2015–2021 | Consumer AI-plus-human chat travel agent → pivoted to **corporate travel** → **announced it was ceasing operations (late Sep 2021)** → Capital One acquired the team and technology (Oct 2021, undisclosed). English, Mike Volpe and 50+ staff went to Capital One's **B2B payments** unit. | **Consumer chat travel-agent economics failed.** The exit was an acqui-hire into a bank, not a travel business. | [verified] |
| **Mezi** | 2015–2018 | **Acquired by Amex in early 2018**. AI travel assistant for Card Members. | Chat concierge absorbed by a card issuer (a loyalty and retention use) | [verified] |
| **WayBlazer** (Terry Jones + ex-IBM Watson GM Manoj Saxena) | 2014–2018 | B2B AI travel search and discovery. Raised $8.7M, the last round in May 2017. **Closed with no reason given.** | Even B2B "AI travel search" on Watson-era NLU couldn't find a sustainable buyer base | [verified] |
| **Utrip** | 2010s–2019 | **Shut down in 2019 after a critical deal fell through** (GeekWire; Skift "What Utrip's tragic final year can teach") | Itinerary generators without booking revenue depend on one partner deal | [verified] |
| **Pana**, **Native**, Yahoo travel chatbot (killed Dec 2016), many 2016–2018 travel chatbots | | Shut down or acquired | The first "AI travel agent" wave died on cost, frequency and NLU limits | Yahoo [verified]; others [recall] |
| **Inspirock**, **Triptile**, etc. | 2010s | Faded, shut down or acquired | | [recall] |
| **Tripnotes** | 2023 | ChatGPT-based planner. Acquired by **Dorsia**, then **shut down in Dec 2023**. Skift: "won't be the last to shut down". | A GPT wrapper with no booking revenue has little standalone value | [verified] |
| **Roam Around** | 2023–2024 | Viral GPT itinerary site (FLYR-backed) → **acquired by Layla on 12 Feb 2024** (not 2023). Founder Shie Gabbai became Layla's COO and the brand was phased out. | Demand for a free novelty tool doesn't equal a business. Consolidation, then Layla itself was bought by Expedia in 2026. | [verified] |
| **App in the Air** | –2024 | Trip-management app **shut down on 19 Sep 2024** | In-trip utility alone did not sustain a consumer business | [verified] |
| **Journera** (Jeff Katz) | ~7 years | "Connected trip" data startup **shut down** | Even well-connected founders couldn't sell connected-trip infrastructure | [verified headline] |
| **HeyHaddock** | –2025 | AI travel tool, **shut down 1 Sep 2025**; the team moved to AI hardware and dev tools | | [claimed, directory] |
| **Tripify** | –2025 | Shut down 3 Jul 2025 after ~10 years | | [claimed] |
| **Odessia** | 2026 | Launched mid-2026 → **acquired by OpenAI and shut down on 10 Nov 2026** | The best outcome for a 2026 consumer AI agent was an acqui-hire by a platform | [verified] |
| **Romie** (Expedia) | 2024–2025/26 | Expedia's group-planning AI assistant, **retired** | Even an OTA's own chatbot stalled until evaluation and live-inventory plumbing were rebuilt | [verified, trade press] |
| **Hopper** | 2020s | Layoffs (Oct 2023; twice in a year to Nov 2024); pivot toward **B2B (HTS)**, which is reported at ~two-thirds of revenue; FTC $35M hidden-fee settlement (Jul 2026) | Consumer app CAC and margins pushed it to B2B. Fintech add-ons drew regulatory risk. | [verified]; B2B share [claimed] |
| The 2023–2024 wave of "GPT wrapper" planners | 2023–2025 | Many went dormant, were acqui-hired, or **were bought by incumbents** (Tripnotes→Dorsia, Roam Around→Layla→Expedia) | Commoditised by ChatGPT, Gemini and Perplexity. No proprietary data. Affiliate revenue per user below LLM cost plus CAC. | [inferred] from verified cases. **No founder-written post-mortem from this wave was found.** |

**Recurring causes of death** [inferred from the pattern]:
1. Travel is **low-frequency** (1–3 leisure trips a year for most people), so retention and LTV are weak.
2. Paid **CAC** in travel is dominated by Google and Booking/Expedia's large ad budgets.
3. **Affiliate economics are thin**: a few dollars per hotel night, near zero on flights.
4. Planning is valuable but **unpaid**, because the booking captures the value and booking happens at the OTA.
5. **Commoditisation** by general assistants.

## B3. Business models and commission rates

### Affiliate programme evidence found in the gap-fill pass

Official rate cards for Booking.com and Expedia sit behind partner logins. Everything here except the Expedia help-centre details is from third-party affiliate guides and network blogs, so it is **[claimed]**.

| Programme | Reported rate | Cookie / notes | Tag |
|---|---|---|---|
| **Booking.com** | A share of *Booking's own commission*: tiered **~25–40%** (≈ 4–6% of booking value at a 15% hotel commission). **Since Jun 2025, applicants are routed through the CJ network**, and listings show "up to 4%". | Session-based; tiered by monthly volume and country | [claimed] |
| **Expedia Group** (Travel Creator / affiliate) | Hotels.com "up to 4%" (programme pages). A reseller lists hotels up to 6% and flights and packages up to 1%. | **7-day, last-click** cookie. Rates vary by product, not by country (EG help centre). | cookie [verified]; rates [claimed] |
| **Agoda** | Up to ~5% | **1-day cookie** | [claimed] |
| **Viator** | **8%** (Travelpayouts lists 10%) | 30-day cookie | [claimed] |
| **GetYourGuide** | ~**8%** (reports range 5.25–10%) | | [claimed] |
| **Klook** | Tiered: **4% (<50 bookings/month) to 7% (>999)** | | [claimed] |
| **Kayak** | **50% of Kayak's revenue** (not of booking value) | ~30-minute cookie | [claimed] |
| **Skyscanner** | ~20% of Skyscanner's revenue (up to 50%) | Varies by country | [claimed] |
| **Omio** | **6%** | 30-day cookie | [claimed] |
| **12Go** | Conflicting: 50% of revenue share vs 2–2.75% of booking value | | [claimed, conflicting] |
| **Airalo** (eSIM) | Affiliate **10% per sale**, 30-day cookie; the consumer referral scheme pays $3 credit | | [claimed] / referral [verified] |
| **SafetyWing** (insurance) | ~10% recurring, for up to ~1 year of payments | | [claimed] |
| **VisitorsCoverage** (insurance) | $1–100+ per sale, or up to 15% on higher-value plans | 45-day cookie | [claimed] |
| **OpenTable**, **World Nomads** | **Not found** in this pass | | [unverified] |
| **Advisor commissions** | Hotels **10% standard, 15% at preferred partners**; cruise ~**15%** (forum anecdote); a typical Virtuoso independent-contractor split is **70/30**, while hosts advertise 75–100% splits | | [claimed, low quality] |

Takeaway [inferred]: hotel affiliate income through the big OTAs works out to **~3–6% of booking value**. Flights are effectively **~0–1%**. Activities pay a clean **~8%**. Metasearch (Kayak, Skyscanner) pays a **share of its own CPC revenue**, which means cents per click. The insurance and eSIM attach (~10%) is high-margin but small-ticket.

### Typical commission and take rates by vertical [recall, cross-checked with the claimed rates above; ranges vary by programme and volume]

| Vertical | OTA / merchant take | What an **affiliate** typically earns | Travel-advisor commission |
|---|---|---|---|
| Hotels | 15–25% (Booking/Expedia merchant or agency commission) | ~3–6% of booking value (e.g., a share of the OTA's commission) | 8–10% standard, 10–15%+ in luxury consortia (Virtuoso, Fora, etc.) |
| Vacation rentals | Airbnb ~14–16% combined fees | ~1–3%, or flat bounties | Low |
| Flights | GDS/NDC fees, ~$0–10 per ticket in commission | **~$0–5 per booking**, or ~0.5–1.5% via networks such as Travelpayouts. Effectively near zero. | ~0–1% (sometimes service fees) |
| Tours & activities | 20–30% (GetYourGuide, Viator) | ~8% (GetYourGuide/Viator affiliate) | ~10% |
| Car rental | 10–20% | ~3–6% | 5–10% |
| Cruises / packages | — | 3–6% | **10–16%+** (the highest-value advisor vertical) |
| Travel insurance / eSIM | — | Often 10–30%+ | — |
| Restaurants | OpenTable/Resy cover fees | Small per-cover bounties | — |

### Business model scorecard [inferred]

| Model | Works when | Fails when | Verdict |
|---|---|---|---|
| **Affiliate** | High intent, low LLM cost per session, attach-rate on hotels and activities | Free users run expensive agentic sessions and book elsewhere; cookie or attribution loss | Necessary but **insufficient** on its own |
| **Consumer subscription** | Frequent travellers, high-value features (monitoring, disruption help, concierge) | Low-frequency travellers churn after a trip; ChatGPT is "free" | Niche. Works for a power-user and frequent-traveller segment. |
| **Merchant of record / packaging** | Dynamic packaging (hotel + activities) earns 15–25% gross margin; you own the customer service | Requires payments, servicing, liability, licences (ATOL/IATA in some jurisdictions) | **Highest margin**, highest operational load. It also pays for accountability. |
| **Human-advisor hybrid** (Fora, Tern) | Luxury and complex trips. 10–15% commissions plus perks. AI raises advisor throughput. Fora has **>$3B in bookings, >15k advisors and a $1B valuation (Jul 2026)**; Tern raised a $13M Series A and bought Lucia [verified]. | Mass market | **Proven** unit economics, and the category that is actually raising money in 2026. AI is a productivity multiplier. |
| **B2B white-label** (DMOs, airlines, card issuers, hotels) | Buyer pays a SaaS fee. DMOs want visitor dispersion away from overtouristed spots, which **lines up with anti-cliché recommendations**. | Long sales cycles, small DMO budgets | **Durable revenue**, aligned with the hyperlocal thesis |
| **Embedded / loyalty** (card issuers, airlines; cf. Mindtrip's investors, Mezi→Amex, Lola→Capital One) | Partner funds it as a retention and engagement tool | Dependence on a single partner | Historically the most common **exit path** |
| **Sponsored placement / ads** | Scale | **Trust cost**: undermines the "honest local knowledge" positioning | Use carefully. Label it clearly, and never let it enter the solver's objective without disclosure. |

### Unit-economics sketch for a consumer planner [inferred, illustrative]

- **Per itinerary session:** LLM cost $0.05–1.50 plus maps and places API cost $0.05–0.50, so ≈ **$0.10–2.00**.
- **Booking conversion:** if 5–10% of sessions lead to a tracked hotel booking of ~$600 at a 4% affiliate rate, that is **$1.20–2.40 revenue per session**, *before* activity bookings and before any CAC.
- **Consequences:**
  - A naive agentic design with no caching or solver offload can **lose money per session**.
  - Paid acquisition at typical travel CAC ($20–80+) needs several booked trips per user to pay back, but users travel 1–3 times a year.
  - Viable consumer entrants must have: (a) cost per plan below $0.20 through solver offload, caching and small-model routing; (b) high attach-rate on high-commission verticals (activities ~8%, packages, insurance); and (c) organic or partner distribution, not paid CAC.

**Benchmarks found in the gap-fill pass** (weak sources; use as orders of magnitude only):
- **Retention:** travel apps retain **~18% of users on day 1 and ~2.8% on day 30** (Business of Apps) [claimed]. That fits the low-frequency thesis.
- **Paid installs:** Meta-ads cost per install in "Recreation & Travel" swung from **~$29 (Jul 2025) to ~$7 (Dec 2025)** (benchmark tool, methodology undisclosed) [claimed]. No authoritative travel CAC per *booking* was found. Vendors advise measuring CAC per confirmed booking, not per install.
- **Revenue scale of a leading consumer AI planner:** Mindtrip, the best-funded at ~$20M raised, is estimated at **~$3.6M revenue in 2025** (Latka estimate, [claimed]).
- **Distribution signal:** LLM referrals are **<1% of Booking.com room nights** (Mar 2026) [verified]. Assistant-driven demand is still tiny at OTA scale.

---

# Strategic implications

## Defensibility and moats (ranked) [inferred]
1. **Proprietary, fresh, hyperlocal data with provenance.** Verified hours, long-tail local-expert content, closures, seasonality, and "locals actually go here" signals. General assistants are weakest here, and this is what fixes clichés and staleness.
2. **Verified feasibility as a product guarantee.** Solver-backed "this plan works: hours, transit and budget checked, as of time T." No major consumer player publicly claims this, and the research shows it is achievable (90%+ on templated constraints).
3. **Booking and servicing operations** (merchant of record, holds, disruption repair). Hard to build, so it is a moat once built, and it is the basis of accountability.
4. **Evaluation infrastructure and preference data**: real-city sandboxes, user simulators, labelled serendipity. This compounds over time.
5. **Distribution partnerships** (card issuers, airlines, DMOs, ChatGPT and Gemini app surfaces). Probably more important than the model itself.

Not a moat: prompt engineering, choice of frontier model, generic multi-agent orchestration.

## Constraints a new entrant must design around
- LLM plus maps cost per plan must stay below expected affiliate revenue per session. Target **< $0.20 per plan**.
- Flights earn almost nothing. Monetise hotels, activities, packages, insurance, and B2B fees.
- Low trip frequency means retention comes from **in-trip and disruption value** and **group and social virality**, not repeat planning.
- General assistants are the default. You will likely need to **be inside them** (ChatGPT/Gemini apps, MCP) as well as standalone.
- Ads conflict with the trust positioning, so keep the objective function clean and disclosed.

## Top gaps and opportunities
1. **Feasibility-guaranteed itineraries.** An LLM + CP-SAT/SMT planner with UNSAT explanations and minimal relaxations, plus a published "verified as of" stamp. Research has shown this works (93.9% TravelPlanner, ITINERA in production). Consumer products haven't shipped it visibly.
2. **Measurable anti-cliché personalisation.** Novelty and serendipity terms in the solver objective, popularity debiasing, long-tail local sources, and a public cliché-rate metric. Nobody reports such a metric. DMOs will pay for visitor dispersion.
3. **Persistent constraint and preference state with group fairness.** Fixes the documented multi-turn failures (Flex-TravelPlanner, TravelEval "collapse") and the group gap (GroupTravelBench), using least-misery plus sequence fairness and attributed trade-offs.
4. **Repair-mode replanning with booking state** (frozen commitments, minimal-change re-solve, policy-aware change and cancel, τ-bench-style reliability testing). This is the accountability and in-trip retention play.
5. **A cost-efficient stack via agentic RL and solver offload.** Small fine-tuned models (Planner-R1 / DeepTravel style) for tool orchestration, frontier models only for elicitation and narration. This is what makes affiliate economics work, combined with B2B white-label distribution (DMOs, card issuers, airlines, advisors).

---

## Sources

Verified this session through search results (primary pages listed; full text not fetched because arxiv.org and aclanthology.org were blocked):

- TravelPlanner — https://www.alphaxiv.org/overview/2402.01622
- Hao et al., LLMs Can Solve Real-World Planning Rigorously with Formal Verification Tools (NAACL 2025) — https://aclanthology.org/2025.naacl-long.176 ; https://arxiv.org/abs/2404.11891v3 ; https://sites.google.com/view/LLM-rwplanning
- LLM-Modulo travel case study — https://arxiv.org/abs/2405.20625v1 ; follow-up https://www.arxiv.org/pdf/2411.14484
- ATLAS (ICLR 2026) — https://iclr.cc/virtual/2026/poster/10007591 ; https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c78ae0c1140902bf3a430b1725bcc4e-Abstract-Conference.html ; https://research.google/pubs/atlas-constraints-aware-multi-agent-collaboration-for-real-world-travel-planning/ ; https://www.themoonlight.io/review/atlas-constraints-aware-multi-agent-collaboration-for-real-world-travel-planning
- ChinaTravel — https://arxiv.org/html/2412.13682v4 ; https://huggingface.co/papers/2412.13682
- TripCraft (ACL 2025) — https://aclanthology.org/2025.acl-long.834 ; https://arxiv.org/abs/2502.20508v1
- ITINERA — https://arxiv.org/abs/2402.07204 ; https://aclanthology.org/2024.emnlp-industry.104 ; https://github.com/YihongT/ITINERA
- TripTailor — https://arxiv.org/abs/2508.01432v1 ; https://aclanthology.org/2025.findings-acl.503
- TravelPlanner+ — https://aclanthology.org/2024.emnlp-industry.37
- Flex-TravelPlanner — https://arxiv.org/html/2506.04649v1 ; https://mlanthology.org/iclrw/2025/oh2025iclrw-flextravelplanner
- Planner-R1 — https://arxiv.org/html/2509.25779v2
- DeepTravel — https://arxiv.org/html/2509.21842
- TourPlanner — https://arxiv.org/pdf/2601.04698
- TravelBench — https://arxiv.org/html/2512.22673v1
- TravelEval — https://arxiv.org/pdf/2606.01046
- Trip+ — https://arxiv.org/abs/2606.21169
- GroupTravelBench — https://arxiv.org/html/2605.25200v3
- AI Tour Meeting — https://arxiv.org/pdf/2607.18806
- MobilityBench — https://arxiv.org/pdf/2602.22638
- PlanningBench — https://arxiv.org/pdf/2605.20873
- FBOS-RL — https://arxiv.org/pdf/2605.20256
- Blueprint First, Model Second — https://arxiv.org/html/2508.02721v2

### Added in the gap-fill pass (2026-11-17; search-result level, full pages not fetched)

**Research and benchmarks**
- NATURAL PLAN — https://huggingface.co/papers/2406.04520 ; https://arxiv.org/html/2406.04520v1
- TTG — https://arxiv.org/pdf/2410.16456 ; https://aclanthology.org/2024.emnlp-demo.25.pdf
- τ-bench — https://export.arxiv.org/pdf/2406.12045 ; https://sierra.ai/blog/benchmarking-ai-agents
- Planner-R1 — https://huggingface.co/papers/2509.25779 ; https://arxiv.org/html/2509.25779v1
- DeepTravel — https://huggingface.co/papers/2509.21842 ; https://arxiv.org/abs/2509.21842v1
- GroupTravelBench — https://huggingface.co/papers/2605.25200 ; https://benchmarklist.com/benchmarks/grouptravelbench/
- TravelEval — https://chatpaper.com/paper/289564
- Trip+ — https://huggingface.co/papers/2606.21169
- TRIP-Bench — https://api.emergentmind.com/papers/2602.01675
- Google ADK travel-concierge — https://developers.google.com/workspace/add-ons/samples/travel-concierge ; https://docs.langdb.ai/guides/building-agents/building-travel-concierge-with-google-adk

**Engineering and company AI**
- Booking.com — https://cfp.pydata.org/pydata-tel-aviv-2025/talk/FZEQUJ ; https://www.phocuswire.com/more-ai-in-travel-how-businesses-choose-right-model ; https://www.hospitalitynet.org/external/4130183/bookingcom-built-agentic-ai-before-agents-existed-heres-how-it-scaled-with-small-models-for-speed-big-models-for-trust ; https://www.zenml.io/llmops-database/genai-agent-for-partner-guest-messaging-in-travel-accommodation
- Expedia — https://techcrunch.com/2024/05/14/expedia-starts-testing-ai-powered-features-for-search-and-travel-planning ; https://www.hospitality.today/article/expedia-learned-where-ai-breaks-it-wasnt-the-model ; https://www.phocuswire.com/expedia-group-ai-lessons-experimentation-chatbot ; https://www.geekwire.com/2026/expedia-group-sees-reward-and-risk-in-the-rise-of-ai-powered-travel/
- Airbnb — https://www.customerexperiencedive.com/news/airbnb-ai-assistant-resolves-customer-inquiries/ ; https://aiweekly.co/alerts/airbnb-ai-cleared-40-of-routed-q2-tickets-cut-support-cost-16
- Navan Ava — https://investors.navan.com/static-files/a1d7946a-fe2e-4768-98be-278b75ced15a ; https://navan.com/intelligence ; https://skift.com/2025/01/07/navan-exec-on-how-ai-chatbot-came-through-during-crowdstrike-outage
- Kayak AI Mode — https://techcrunch.com/2025/10/16/kayak-launches-an-ai-mode-for-travel-questions-search-and-bookings/
- Tripadvisor–Perplexity — https://www.pymnts.com/artificial-intelligence-2/2025/seamless-journeys-ais-rising-role-in-coordinating-consumer-travel/
- Apps in ChatGPT — https://www.techcrunch.com/2025/10/06/openai-launches-apps-inside-of-chatgpt ; https://www.expedia.com/newsroom/smart-trip-planning-new-expedia-app-in-chatgpt-to-plan-your-trip
- Google AI Mode — https://blog.google/products/search/agentic-plans-booking-travel-canvas-ai-mode/ ; https://www.seroundtable.com/google-ai-mode-adds-travel-ai-features-40441.html
- LLM cost commentary — https://skift.com/2026/03/03/booking-cfo-the-ai-threat-isnt-really-a-risk-at-all/ ; https://www.cfodive.com/news/booking-uses-ai-to-slash-customer-service-costs-cfo-says/812624/ ; https://letsdatascience.com/news/travel-industry-faces-two-sided-ai-cost-squeeze-d71822ba ; https://www.businesstravelnewseurope.com/QA/HRS-AI-could-cut-corporate-travel-task-costs-by-75-per-cent

**Market sizing**
- Booking Holdings FY2025 — https://www.sec.gov/Archives/edgar/data/1075531/000107553126000009/bkng-20251231.htm ; https://www.phocuswire.com/booking-holdings-q4-full-year-2025-earnings
- Expedia FY2025 — https://www.sec.gov/Archives/edgar/data/1324424/000132442426000005/earningsrelease-q42025.htm
- Airbnb FY2025 — https://news.airbnb.com/airbnb-q4-2025-financial-results/
- Trip.com FY2025 — https://ctripcominternationalltd.gcs-web.com/news-releases/news-release-details/tripcom-group-limited-reports-unaudited-fourth-quarter-and-5
- Phocuswright — https://www.phocuswright.com/Travel-Research/Research-Updates/2026/Travel-Forward-Data-Insights-and-Trends-for-2026 ; https://eglobaltravelmedia.com.au/2025/12/13/travels-1-67tn-surge-revealed-in-new-2026-phocuswright-report/ ; https://www.travelpulse.com/news/features/online-travel-bookings-to-reach-1-2-trillion-by-end-of-2026
- GBTA — https://www.businesswire.com/news/home/20250721167781/en ; https://www.gbta.org/research/2025-business-travel-index-outlook-bti/

**Funding and M&A**
- Funding trend — https://skift.com/2026/10/23/travel-vc-funding-fell-for-the-second-straight-quarter-rounds-for-ai-companies-cut-in-half/ ; https://www.phocuswire.com/news/startups/travel-startup-funding-acquisitions-q1-2026 ; https://www.hospitality.today/article/travel-startup-funding-hit-a-decade-low-the-scarce-input-moved-to-distribution
- Navan — https://www.renaissancecapital.com/IPO-Center/News/114574/corporate-travel-software-provider-navan-prices-ipo-at-25-midpoint ; https://www.thestar.com.my/tech/tech-news/2025/10/30/travel-tech-firm-navan039s-ipo-raises-about-923-million ; https://builtin.com/articles/navan-ipo-nasdaq-debut-20251031 ; https://stockanalysis.com/stocks/NAVN
- Perk — https://www.perk.com/press-release/travelperk-raises-200m-and-acquires-yokoy/ ; https://sifted.eu/articles/general-catalyst-travelperk-200m-raise-news
- Spotnana — https://salestools.io/report/spotnana-raises-75m-series-c (aggregator)
- Mindtrip — https://www.businesswire.com/news/home/20251208469469/en ; https://www.phocuswire.com/mindtrip-ai-travel-planning-capital-one-ventures-united-airlines-ventures ; https://www.phocuswire.com/mindtrip-secures-12m-funding-launches-group-chat ; https://www.phocuswire.com/mindtrip-ai-travel-b2b-destination-marketing ; https://getlatka.com/companies/mindtrip.ai
- Layla — https://ir.expediagroup.com/news-and-events/news/news-details/2026/Expedia-Group-acquires-Layla-accelerating-its-AI-powered-trip-planning-and-booking-strategy/default.aspx ; https://www.skift.com/expedia-acquired-ai-trip-planner-layla-exclusive ; https://www.phocuswire.com/expedia-group-acquires-ai-travel-planning-app-layla ; https://techcrunch.com/2024/02/12/travel-startup-layla-acquires-flyr-backed-ai-itinerary-building-bot
- Fora — https://www.foratravel.com/newsroom/fora-announces-series-d-funding ; https://skift.com/2026/07/16/fora-travel-the-unicorn-it-raised-60-million-at-a-1-billion-valuation/
- Tern — https://www.phocuswire.com/tern-raises-13-million-dollars-series-a ; https://www.tern.travel/post/tern-acquires-lucia-expanding-support-for-travel-advisors
- Airial — https://techcrunch.com/2025/06/30/former-meta-engineers-airial-travel-tool-helps-travelers-solve-logistics-planning-with-ai
- Odessia — https://skift.com/2026/11/10/a-year-after-sonders-collapse-francis-davidson-sells-his-ai-travel-startup-to-openai/ ; https://www.phocuswire.com/news/startups/openai-acquires-ai-travel-agent-odessia ; https://thenextweb.com/news/openai-acquires-odessia-ai-travel-agent
- Hopper — https://thelogic.co/briefing/hopper-raises-us175m-in-series-g-funding-nearly-doubling-its-valuation ; https://skift.com/2025/01/21/are-hoppers-ipo-plans-imminent/ ; https://skift.com/2024/11/22/hopper-restructures-with-job-cuts-for-the-second-time-in-a-year ; https://betakit.com/?p=380147 ; https://en.wikipedia.org/wiki/Hopper_(company)
- Otto — https://techcrunch.com/2024/08/22/ex-expedia-execs-startup-using-ai-to-solve-business-travel-gets-backing-from-madrona
- BizTrip.AI — https://skift.com/?p=761267
- Vuelo — https://fintech.global/2026/03/25/vuelo-raises-56m-to-launch-ai-native-travel-booking-platform/
- Holiwise — https://tech.eu/2025/08/26/holiwise-raises-eur145m-pre-seed-to-reinvent-premium-travel/
- Stippl — https://tech.eu/2024/04/02/social-travel-app-raises
- Stardrift — https://ycombinator.com/companies/stardrift
- Axel and Gordian — https://www.ycombinator.com/companies/axel-travel ; https://skift.com/2022/07/19/gordian-software-raises-25-million-for-airline-cross-selling-tools/
- Boop — https://techcrunch.com/2025/11/18/boops-new-app-turns-social-recommendations-into-bookable-itineraries
- Amex GBT–CWT — https://www.businesswire.com/news/home/20250902624882/en ; https://www.nasdaq.com/press-release/amex-gbt-completes-acquisition-cwt-2025-09-02

**Graveyard**
- Google Trips — https://www.engadget.com/2019/08/05/google-shuts-down-trips-app/ ; https://searchengineland.com/google-discontinues-trips-mobile-app-320376
- Hipmunk — https://www.phocuswire.com/sap-concur-shutters-hipmunk ; https://techcrunch.com/2020/01/14/hipmunks-co-founders-tried-to-buy-it-back-before-the-shutdown/
- Lola — https://skift.com/2021/10/08/lola-exits-travel-with-acquisition-by-capital-one ; https://www.travelweekly.com/Travel-News/Corporate-Travel/Capital-One-acquires-Lola-team-and-technology
- Mezi — https://www.fintechfutures.com/ai-in-fintech/amex-acquires-ai-travel-aide-mezi
- WayBlazer — https://www.phocuswire.com/Wayblazer-shutting-down
- Utrip — https://www.geekwire.com/2019/seattle-travel-planning-startup-utrip-will-shut-critical-deal-falls/ ; https://skift.com/2019/06/25/what-utrips-tragic-final-year-can-teach-other-travel-startups
- Tripnotes — https://skift.com/2024/01/02/tripnotes-a-buzzy-chatgpt-based-trip-planner-was-acquired-and-shut-down/
- App in the Air — https://alternativeto.net/news/2024/9/app-in-the-air-to-shut-down-on-september-19-2024-users-advised-to-export-their-data-now
- Journera — https://www.travelweekly.com/Travel-News/Travel-Technology/Journera-shuts-down-after-seven-years
- Yahoo travel chatbot — https://fortune.com/2016/12/20/yahoo-just-killed-its-travel-assistant-chatbot/

**Affiliate and unit economics (third-party; [claimed])**
- Booking.com affiliate — https://track360.io/blog/booking-com-affiliate-partner-program-operator-teardown-2026
- Expedia Group affiliate — https://help.creator.expediagroup.com/hc/en-us/articles/15187327581591-What-commission-will-I-earn
- Viator and GetYourGuide — https://track360.io/blog/viator-getyourguide-affiliate-programs-operator-teardown-2026 ; https://tourscanner.com/blog/tours-travel-activities-affiliate-programs/
- Flight and metasearch affiliates — https://travelpayouts.com/blog/best-flights-affiliate-programs/
- Airalo — https://www.airalo.com/blog/the-airalo-affiliate-program-everything-you-need-to-know
- Insurance affiliates — https://atlas.hellosafe.com/travel-insurance-affiliate-program/best-programs/
- Advisor commissions — https://www.foratravel.com/join/resources/travel-agent-commission ; https://hostagencyreviews.com/blog/ptn-q3-2025
- App retention — https://www.businessofapps.com/?p=97743
- Cost per install — https://www.superads.ai/facebook-ads-costs/cost-per-app-install/recreation-and-travel

### Still named from recall and not re-verified
Search for primary sources before citing any of these:
- **Research:** LLMFP (ICLR 2025); τ²-bench; Vansteenwegen et al. 2009/2011; Gavalas et al. 2014; Lim et al. PersTour; Masthoff group recommender strategies; Kaminskas & Bridge 2016.
- **Open-source examples:** CrewAI trip_planner example; LangGraph and OpenAI customer-service demos.
- **Funding:** Fora Series A–C details.
- **Platform launches:** OpenAI Operator travel launch partners (Jan 2025); Perplexity–Selfbook; Microsoft Copilot travel actions.
- **Other:** Layla's Skyscanner co-founder link; Pana and Native; Inspirock and Triptile; the TravelEval "collapse" wording; OpenTable and World Nomads affiliate terms.
