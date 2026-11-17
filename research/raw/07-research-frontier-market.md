# 07 — Research Frontier, Engineering Patterns, Market & Funding

*Agent 7 of 7. Compiled 2026-11-17.*

## Read this first: evidence quality and limits

This run was **badly constrained**, and you should know how before relying on any number below.

- **Network:** `arxiv.org` and `aclanthology.org` do not resolve from this container, so I could not read primary PDFs. I stopped trying other hosts after those two failed, as the environment instructs.
- **Search budget:** about 14 web searches in, the shared per-turn search budget ran out (200 calls, shared across all 7 parallel agents). The research half (Part A) is fairly well grounded. **Part B (market and funding) rests mostly on model recall up to about mid-2026, and none of it was re-checked this session.**

Every claim carries one of these labels:

| Tag | Meaning |
|---|---|
| **[verified]** | Confirmed this session from search results quoting the primary source (abstract, proceedings page) |
| **[claimed]** | An author's or company's own claim, seen this session, not independently checked |
| **[inferred]** | My own reasoning or arithmetic |
| **[recall]** | From model training knowledge (cutoff about mid-2026). **Not re-verified this session.** Treat it as a lead to check, not a fact. |

**Recommended follow-up:** allow `arxiv.org` and `aclanthology.org` in the session's network settings, then re-run a narrow verification pass. Main targets: the Part B funding table, the Planner-R1 and DeepTravel numbers, and the TravelEval, Trip+ and GroupTravelBench metrics.

---

# PART A — Research & Engineering Frontier

## A1. Benchmarks: what exists and how far the SOTA has moved

### A1.1 The benchmark landscape (2024 → 2026)

| Benchmark | Venue / date | What it tests | Key point | Tag |
|---|---|---|---|---|
| **TravelPlanner** (Xie et al.) | ICML 2024 (arXiv 2402.01622) | Multi-day US trips over a sandbox of ~4M records. Tests hard constraints (budget, room type, cuisine, transport) and commonsense constraints. Two modes: two-stage (tool use + planning) and sole-planning. | GPT-4-Turbo got **0.6% final pass rate** in two-stage mode. It is still the canonical benchmark. | [verified] |
| **TravelPlanner+** | EMNLP 2024 Industry | Personalisation on top of TravelPlanner, using user profiles (pet, cuisine, home city), judged by an LLM-as-judge | Personalised plans preferred over generic ones in up to 74.4% (validation) and 87.3% (test) of cases. Note this is a win rate, not a feasibility rate. | [verified] |
| **Flex-TravelPlanner** (KAIST) | ICLR 2025 Workshop (arXiv 2506.04649) | Constraints added one by one over several turns, plus explicitly prioritised constraints that compete | GPT-4o and Llama-3.1-70B **wrongly favour newly added, lower-priority preferences** over earlier hard constraints | [verified] |
| **NATURAL PLAN** (Google DeepMind) | 2024 | Trip planning, meeting planning, calendar scheduling | Trip-planning exact match was in the low 30s% for the best models of 2024 (Gemini 1.5 Pro ~35%) | [recall] |
| **ChinaTravel** (Nanjing U.) | arXiv 2412.13682, v5 Apr 2026 | Open-ended Chinese travel queries from 1,154 humans, with a DSL for checking compositional constraints | Neuro-symbolic agents reach **27.9% (v2) → 37.0% (v4, Sept 2025)** constraint satisfaction on human queries, about 10× pure-neural (2.6%). The authors argue TravelPlanner's templated queries are **near saturation** for solver methods. | [verified] |
| **TripCraft** (IIT Bhubaneswar + Microsoft India) | ACL 2025 main | Real public-transit schedules, events, attraction categories, personas. Five continuous metrics: Temporal Meal, Temporal Attraction, Spatial, Ordering, Persona. | Moves scoring from pass/fail to continuous quality metrics. Adding parameter info raised Temporal Meal Score from 61% to 80% on 7-day trips. | [verified] |
| **ITINERA** | EMNLP 2024 Industry; Best Paper, KDD UrbComp 2024 | Open-domain urban itinerary planning (OUIP) from natural-language preferences | **LLM + spatial optimisation**: decompose the request → retrieve candidate POIs → cluster-aware spatial ordering → LLM writes the itinerary. Deployed system. LLM-only plans are "circuitous" and impractical. Code is public. | [verified] |
| **TripTailor** (Fudan) | ACL 2025 Findings (arXiv 2508.01432) | Real data: 500k+ POIs, ~4k real itineraries (China), single-turn | SOTA LLMs remain **below human standard** on feasibility, rationality and personalisation | [verified] |
| **TravelAgent** (Fudan) | arXiv 2024 | Modular personalised assistant (tool, recommendation, planning, memory) | Early modular reference design | [recall] |
| **TravelBench** | arXiv 2512.22673 (Dec 2025) | Multi-turn, single-turn and **unsolvable** subsets. GPT-4.1 acts as the user simulator. | Tests whether agents detect impossible requests, which matters for accountability | [verified] |
| **TravelEval** | arXiv 2606.01046 (Jun 2026) | Six-dimension evaluation, data sandbox, simulation-based global evaluation | Reports a **non-linear performance collapse as user preferences accumulate** | [verified, abstract-level] |
| **Trip+** | arXiv 2606.21169 (Jun 2026) | Interactive, minute-level itineraries revised as events unfold. An LLM simulator rates **experiential quality** (e.g., fatigue). | 18 LMs evaluated; a **consistent gap in experiential quality** | [verified, abstract-level] |
| **GroupTravelBench** | arXiv 2605.25200 (May 2026) | 650 multi-user, multi-turn tasks with real profiles, POIs and ticket prices. The simulator withholds preferences until they come up in dialogue. | Scores elicitation, coordination and group planning separately | [verified, abstract-level] |
| **AI Tour Meeting** | arXiv 2607.18806 (Jul 2026) | LLM agents act as proxies for group members negotiating a trip | Group-preference aggregation via agents | [verified, abstract-level] |
| **MobilityBench** | arXiv 2602.22638 (Feb 2026) | Route-planning agents in real mobility scenarios | Spatial and transit side | [verified, title-level] |
| **PlanningBench** | arXiv 2605.20873 (May 2026) | Scalable, verifiable planning data for evaluation **and training** | A source of RL training data | [verified, title-level] |
| **τ-bench / τ²-bench** (Sierra) | 2024 / 2025 | Airline customer-service agent with a simulated user and policy compliance; pass^k reliability metric | The best template for post-booking change and cancel flows. Pass^k shows reliability falls sharply over repeated trials. | [recall] |

### A1.2 Best published results on TravelPlanner, and what moved them

| Approach | Technique | Final pass rate | Tag |
|---|---|---|---|
| Original baselines (2024) | ReAct / CoT, GPT-4-Turbo | **0.6%** (two-stage) | [verified] |
| LLM-Modulo (Kambhampati group, 2024) | LLM proposes, **external critics** (format, hard constraints, commonsense) send feedback, up to 10 iterations | **20.6%** vs 4.4% baseline (GPT-4-Turbo). A follow-up reports GPT-4o 8.3% → 23.9% and Claude-3.5-Sonnet 4.4% → 25%. | [verified] |
| ATLAS (Google Research; ICLR 2026) | Multi-agent: **dynamic constraint management + iterative plan critique + adaptive interleaved search** | **44.4%** with Gemini-2.5-Pro vs 23.3% for the best alternative (PMC) and 20.6% for ReAct. With Claude-Sonnet-4: 23.3% vs 14.4% (PMC). Reaches **84%** in a separate live-search, multi-turn setting (ReAct 59%, monolithic agent 27%). | [verified] |
| Agentic RL: Planner-R1 (2509.25779), DeepTravel (2509.21842), TourPlanner (2601.04698, constraint-gated RL) | RL with shaped rewards on Qwen3-8B/32B, SFT cold start + RL with experience replay | The papers report big gains for **small open models**. I could not retrieve the exact numbers. My recall puts Planner-R1-32B in the mid-50s% and 8B in the high-30s%, **unverified**. | [verified existence] / numbers [recall] |
| A "source code agent" style method (2025/26) | Plans as executable code | 35.6% on the 1,000-task test set, claimed +97.6% over ATLAS on the same backbone. The paper's own baseline numbers for ATLAS don't match the ICLR paper. | [claimed] |
| **Formal verification / SMT** (Hao, Chen, Zhang, Fan — MIT; NAACL 2025) | LLM translates the request into a **constraint satisfaction problem → Z3/SMT solver**. If the solver says UNSAT, the LLM reads the unsat core and proposes **relaxations to the user**. | **93.9% final pass rate** (93.3% validation). Other citations say 97% vs 4% for LLM-only. | [verified] |
| TTG "To the Globe" (Meta, 2024) | LLM → symbolic spec → **MILP** solver; returns a guaranteed-optimal plan in about a second | ~91% exact on their benchmark | [recall] |
| LLMFP (Hao et al., ICLR 2025) | General LLM → formal optimisation formulation | Generalises the SMT idea beyond travel | [recall] |

**What moved the numbers, in order of effect size:**

1. **Taking the combinatorial search away from the LLM.** Solver hybrids (SMT, MILP) reach 90%+ against single digits for prompting-only methods. This is the biggest lever by far. ChinaTravel explains why: TravelPlanner's templated constraints are exactly what solvers handle well, so the benchmark is close to "solved" for neuro-symbolic systems. The open problem is **open-ended, preference-laden, real-data** queries, where the best neuro-symbolic systems drop to about 37% (ChinaTravel v4).
2. **External verification loops** (LLM-Modulo critics, ATLAS's critique agent): roughly 3–5× over baseline.
3. **Explicit constraint tracking as state** (ATLAS's constraint manager). Flex-TravelPlanner shows models forget or down-rank earlier constraints, so constraints must live in a structured store rather than only in the context window.
4. **Agentic RL on verifiable rewards.** It lets small models compete, which cuts inference cost. It still trails solver hybrids on hard constraints.
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

> Caveat: almost all of this is **[recall]**, because the search budget ran out before I could verify vendor engineering posts. Companies rarely publish cost per itinerary. None of the companies below has published a full architecture.

| Company | What is publicly known about the build | Tag |
|---|---|---|
| **Booking.com** | AI Trip Planner launched in 2023 on OpenAI models over Booking's own inventory, ML ranking and recommendations. Launch partner for OpenAI Operator (Jan 2025) and for **apps in ChatGPT** (OpenAI DevDay, Oct 2025). Pattern: the LLM is a conversational front end; ranking, inventory and pricing stay in proprietary systems. | [recall] |
| **Expedia** | ChatGPT plugin (2023) → in-app assistant → **Romie** (2024, group-chat travel buddy) → Expedia app inside ChatGPT (Oct 2025). Public statements stress a mix of OpenAI and in-house models, with Expedia's data science platform doing ranking. "Trip Matching" turns Instagram reels into itineraries. | [recall] |
| **Kayak** | ChatGPT plugin (2023), "Ask Kayak", later an AI-mode style conversational search over Kayak's price data | [recall] |
| **Airbnb** | AI customer-service agent rolled out in 2025. Chesky described it as built on **many models (~13)**, not one, with a stated aim of moving toward a trip-planning concierge. Pattern: model routing and heavy policy grounding. | [recall] |
| **Navan** | "Ava" assistant for corporate travel support and booking. Its edge is policy-aware booking with its own inventory and merchant-of-record operations. | [recall] |
| **Mindtrip** | Consumer planner with a curated place database, maps-first UI and group-planning features. Uses frontier LLM APIs plus its own place and knowledge graph. Has added B2B/partner deals and booking integrations. | [recall] |
| **Layla** (absorbed Roam Around in 2023) | Chat planner monetised through affiliate booking links plus a subscription. Founding team includes a Skyscanner co-founder. | [recall] |
| **Google** | Gemini trip planning, then **AI Mode** with canvas-style trip planning and **agentic booking** (restaurants first, then flights and hotels through partners), and AI "Flight Deals" (2025). Google's moat: Maps POI graph, reviews, live hours, Flights/Hotels price data. | [recall] |
| **Alibaba/Amap (Gaode)** | DeepTravel (arXiv 2509.21842) is an end-to-end agentic-RL travel agent. My recall is that it comes from Amap and was deployed there (not verified). This is the clearest public **production-RL** travel agent. | [verified paper] / affiliation [recall] |
| **Google Research** | ATLAS (above) is the most detailed public multi-agent travel architecture from a hyperscaler | [verified] |

**Common production pattern** [inferred from the above]:
- A frontier LLM handles conversation and intent.
- The company's own ranking and recommendation stack picks inventory. The LLM does not pick inventory from its own knowledge.
- Live supplier APIs supply prices and availability.
- A thin itinerary composer sits on top.
- Distribution increasingly runs **through** the assistants (ChatGPT apps, Gemini, Perplexity) rather than against them.

**Nobody publicly claims solver-backed feasibility guarantees.** That is a gap.

### Open-source reference implementations [recall]
- **Google ADK `travel-concierge` sample** (google/adk-samples). Multi-agent: inspiration → planning → booking → pre-trip → in-trip → post-trip. Uses mock tools, and its booking is stubbed. A good *orchestration* template. Its weakness: no real feasibility checking, so data quality is only as good as Google Search and Places grounding.
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

> **Warning:** the search budget ran out before Part B. Everything here is **[recall]** or **[inferred]** unless tagged otherwise. Verify every figure before using it in a pitch or plan.

## B1. Market size (with skepticism)

| Figure | Value | Tag / comment |
|---|---|---|
| Booking Holdings gross bookings | ~$165B (2024), revenue ~$24B, so a revenue take of ~14–15% | [recall] |
| Expedia Group gross bookings | ~$110B (2024), revenue ~$13.7B | [recall] |
| Airbnb gross booking value | ~$80B (2024) | [recall] |
| Global online travel (gross bookings) | Commonly quoted at ~$600B–$1T+, depending on definition | [recall], wide variance |
| Global corporate travel spend (GBTA) | ~$1.4–1.5T forecast for 2024/25 | [recall] |
| "AI in travel" / "AI trip planner" market reports | Range from hundreds of millions to tens of billions of dollars, with CAGRs of 15–30% | [recall]. **Low credibility.** These are paywalled syndicated reports with inconsistent definitions. Don't anchor on them. |

**Skeptical framing** [inferred]:
- "AI trip planning" is not a market of its own. It is a **front-end** to a large but mature booking market whose economics are already split among OTAs, metasearch, Google and suppliers.
- The money available to a new entrant is the **share of distribution margin** it can capture: affiliate fees, merchant-of-record margin, or subscription.
- The most useful sizing is bottom-up: (number of planned trips) × (booking value influenced) × (commission per vertical).

## B2. Funding, M&A and the graveyard (2023–2026)

### Funding and exits [all recall — verify]

| Company | Category | Funding events (as recalled) | Notes |
|---|---|---|---|
| **Navan** (ex-TripActions) | Corporate travel and expense | **IPO on Nasdaq, Oct 2025** (ticker NAVN). Priced at about $25, valuation ~$6B+, below its 2022 private valuation of $9.2B. Shares traded down after the debut. | Even the category leader IPO'd below its peak private value, and public investors were cautious about travel tech. |
| **Perk** (ex-TravelPerk) | Corporate travel | ~$200M Series E (Jan 2025), valuation ~$1.4B. Rebranded to Perk in 2025. | |
| **Spotnana** | Travel-as-a-service infrastructure (B2B) | $75M Series C (2022). Total raised >$100M. | The infrastructure ("picks and shovels") play |
| **Mindtrip** | Consumer AI planner | Launched 2024. Seed ~$7M, then a strategic round of ~$12M (late 2024) with Amex Ventures, Capital One Ventures and United Airlines Ventures; ~$20M+ total by end-2024. | Strategic investors from card and airline companies point to **distribution through partners** |
| **Layla** | Consumer AI planner | Absorbed **Roam Around** (2023). Small seed rounds. | Roam Around (viral 2023 GPT itinerary generator) was folded into Layla, an early sign of consolidation |
| **Fora** | Travel-advisor host agency + software | Series A $13.5M (2022), Series B ~$20M (2023), **Series C ~$60M (2025)**, reportedly led by Thrive | Human advisors plus software. Monetised through supplier commissions (~10–15% luxury hotels) shared with advisors. |
| **Airial** | Consumer AI planner (ex-Meta founders) | ~$3M seed (2025) | |
| **Tern** | Software for travel advisors | Seed / Series A (amount not recalled) | B2B to advisors |
| **Boardwalk** | — | **Couldn't find or recall reliable funding data** | |
| **Otto** | AI assistant for business travel | Seed-stage (amount not recalled) | |
| **Amex GBT** | TMC | Acquired **CWT** (~$570M, closed 2025 after DOJ review) | Corporate-travel consolidation |

**Platform moves 2025–2026** [recall]:
- OpenAI **Operator** launch partners included Booking.com, Tripadvisor and Priceline (Jan 2025).
- **Apps in ChatGPT** with Booking.com and Expedia (Oct 2025).
- **Perplexity** hotel booking through Tripadvisor content and Selfbook.
- **Google AI Mode** agentic booking and trip-planning canvas (late 2025).
- Microsoft Copilot travel actions.

Implication: the general assistants are becoming the **default free trip planner** and are integrating OTA inventory directly.

### The graveyard and pivots [recall unless noted]

| Company | Era | Outcome | Lesson |
|---|---|---|---|
| **Google Trips** | 2016–2019 | Shut down, folded into Search and Maps | Even Google couldn't sustain a standalone planning app. Planning is low-frequency and gets absorbed into search. |
| **Hipmunk** | 2010–2020 | Acquired by SAP Concur (2016), shut down (2020) | Great UX did not overcome metasearch economics |
| **Lola** (Paul English) | 2015–2021 | Consumer AI and human chat travel agent → pivoted to **corporate travel** → acquired by Capital One (2021) | **Consumer chat travel-agent economics failed**: human-in-the-loop cost, low frequency. The pivot went to B2B. |
| **Mezi** | 2015–2018 | Acquired by Amex | Chat concierge absorbed by a card issuer (a loyalty and retention use) |
| **Pana**, **Native**, many 2016–2018 travel chatbots | | Shut down or acquired | The first "AI travel agent" wave died on cost, frequency and NLU limits |
| **Utrip**, **Inspirock**, **Triptile**, etc. | 2010s | Faded, shut down or acquired | Itinerary generators without booking revenue couldn't monetise |
| **Roam Around** | 2023 | Viral GPT itinerary site → folded into Layla | Demand for a free novelty tool doesn't equal a business |
| **Hopper** | 2020s | Layoffs; pivot toward **B2B (Hopper Technology Solutions)** and fintech add-ons | Consumer app CAC and margins pushed it to B2B. Fintech add-ons (price freeze, cancel-for-any-reason) had better margins than bookings. |
| The 2023–2024 wave of "GPT wrapper" planners | 2023–2025 | Many went dormant or were acqui-hired (specific post-mortems **not found**) | [inferred] Commoditised by ChatGPT, Gemini and Perplexity. No proprietary data. Affiliate revenue per user below LLM cost plus CAC. |

**Recurring causes of death** [inferred from the pattern]:
1. Travel is **low-frequency** (1–3 leisure trips a year for most people), so retention and LTV are weak.
2. Paid **CAC** in travel is dominated by Google and Booking/Expedia's large ad budgets.
3. **Affiliate economics are thin**: a few dollars per hotel night, near zero on flights.
4. Planning is valuable but **unpaid**, because the booking captures the value and booking happens at the OTA.
5. **Commoditisation** by general assistants.

## B3. Business models and commission rates

### Typical commission and take rates by vertical [recall; ranges vary by programme and volume]

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
| **Human-advisor hybrid** (Fora, Tern) | Luxury and complex trips. 10–15% commissions plus perks. AI raises advisor throughput. | Mass market | **Proven** unit economics. AI is a productivity multiplier. |
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

Named from recall and **not re-verified this session** (search for primary sources before citing): NATURAL PLAN (DeepMind 2024); TTG "To the Globe" (Meta 2024); LLMFP (ICLR 2025); τ-bench / τ²-bench (Sierra); Vansteenwegen et al. 2009/2011; Gavalas et al. 2014; Lim et al. PersTour; Masthoff group recommender strategies; Kaminskas & Bridge 2016; Google ADK travel-concierge sample (github.com/google/adk-samples); CrewAI trip_planner example; Navan IPO (Oct 2025); TravelPerk/Perk Series E; Fora Series C; Mindtrip rounds; Layla/Roam Around; Airial seed; Amex GBT–CWT; OpenAI Operator and ChatGPT apps travel partners; Google AI Mode agentic booking; Hopper HTS pivot; Lola→Capital One; Mezi→Amex; Google Trips shutdown; Hipmunk shutdown; Booking Holdings and Expedia 2024 financials; affiliate commission rates.
