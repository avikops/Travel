# 06 — The Voice of the Traveller: Reviews, Complaints, Demand Data and What Users Want from AI Trip Planning

*Research agent 6 of 7. Compiled 2026-11-17. Scope: the user side. Reviews and complaints, demand and adoption data, jobs-to-be-done, personalisation, workarounds.*

---

## 0. Read this first: method, evidence quality and gaps

**Evidence labels.** **[verified]** means the figure or quote appeared in a search result attributed to the named primary source or its press release. **[claimed]** means it appeared only in secondary coverage, competitor marketing or an aggregator, or the sources conflict. **[inferred]** means it is my analysis or domain reasoning, not a sourced user statement.

**Hard limits on this run (please read before relying on it):**
- **WebFetch was blocked.** `phocuswright.com`, `trustpilot.com` and `colemanconcierge.com` all failed with DNS errors because they are outside this session's allowed network domains, so I could not read primary pages. Every quote below is text that the search tool pulled from the named URL. I did not load the page itself. To read primary sources, these domains (and reddit.com, apps.apple.com, play.google.com and producthunt.com) need to be allowed in the session's network settings.
- **The shared web-search budget ran out after about 22 searches.** The limit is 200 per turn across all 7 parallel agents. So I did **not** gather data for: Kayak AI mode, Expedia Romie, Booking.com's AI Trip Planner, GuideGeek, iMean, Airial, Stippl, Holiwise, Wonderplan, Trip Planner AI or Gemini. I also have no App Store or Google Play star ratings for most tools, no Hacker News threads, no direct Reddit threads, and no NYT, WSJ, Verge, Wired or CNET hands-on tests. Those gaps are listed in §11 for a follow-up pass.
- What I did get is strong on **demand and trust data** (about 10 large surveys plus Adobe traffic data), moderate on **Layla, Wanderlog and ChatGPT complaints**, and thin on everything else. Rankings in §10 weight evidence accordingly.

---

## 1. Executive summary

1. **Usage is mainstream but shallow.** In 2025–26 roughly a quarter to over half of travellers used AI for some part of trip planning, depending on wording. Use is concentrated at the **inspiration and research** end. Deloitte found the top AI travel tasks were researching activities (67%), destinations (56%) and accommodation (54%) **[verified]**.
2. **There is a huge gap between saying and doing on booking.** Sponsor-run "readiness" surveys report that up to ~60% of US travellers are "ready" for AI-booked travel (Accenture) **[claimed]**. In other surveys only **8%** are comfortable booking through an AI platform (Expedia/YouGov, 2026), **6%** fully trust AI (Booking.com, 37k respondents), and **3%** trust it enough to pay by card (Booking.com Oceania) **[verified/claimed]**. Actual behaviour: LLM traffic is **"significantly below 1%" of Booking.com room nights** (Booking Holdings Q2 2026 call) **[claimed, via secondary coverage]**.
3. **Trust is cooling among the youngest users.** YouGov found US 18–24s comfortable with AI trip planning fell from **47% to 34%** in one year, while comfort among those 55+ rose from 16% to 20% **[verified]**. Women remain more sceptical: 44% are not comfortable, against 36% of men **[verified]**.
4. **Complaint evidence matches the brief's four problems, with additions.** Hallucinated or stale facts (closed or non-existent places, wrong opening hours) and generic, over-packed itineraries show up repeatedly. "No accountability" shows up in surveys as "I always fact-check" and "I want human oversight", not as a named complaint. **New problems not on the list:** (a) **subscription and billing dark patterns** are the #1 complaint in Trustpilot data for both Layla and Wanderlog; (b) **revision drift** and poor editing; (c) **unrealistic pacing and geography**; (d) **unreliable import and organisation** of bookings already made; (e) **opaque monetisation** and possible sponsored bias.
5. **Where AI planners earn praise:** an end-to-end draft in minutes, budget tweaking, beautiful maps-first UI (Mindtrip), and a **human expert in the loop** (Layla). The pattern is "AI drafts, human verifies or decides".

---

## 2. Demand and adoption data (2024–2026)

### 2.1 Adoption: who uses AI for travel planning

| Source (date, sample) | Headline metric | Notes | Label |
|---|---|---|---|
| Phocuswright, *Chat, Plan, Book: GenAI Goes Mainstream* (Jul 2025; US + Europe) | ~1 in 3 travellers use GenAI to plan or enhance trips | Full report paywalled (US$595) | [verified – preview] |
| Phocuswright, *Search Slips, AI Surges* (2025, US) | ~40% of US travellers use AI, **+11 pts YoY** | | [verified – summary] |
| Phocuswright Research Roundup 2H25 (US) | 58% of active US travellers use AI for something; **39% use it for travel** | | [verified – summary] |
| Phocuswright, *Travel Forward 2026* | **56%** used AI for at least one trip in the past 12 months, up from 43% | Baseline year for the 43% reported inconsistently | [claimed] |
| Phocuswright "From hype to habit" (2025) | **78%** say GenAI improves trip planning; only ~1/3 fully trust responses | | [verified – headline] |
| Skift US Travel Tracker (Jun 2025, n≈1,000+) | **30% use AI extensively** (13% in 2024); 25% occasionally; 13% considered; 21% open; 11% not interested | Most consistently cited Skift number | [verified – via Skift chart description] |
| Skift *State of Travel 2025* | 37% of global travellers used AI tools such as ChatGPT to plan in Q3 2024 | Older (2024 data) | [claimed] |
| Skift Research, *The Disappearing Destination* | 63% of surveyed travellers have used AI to plan a trip | | [claimed] |
| Deloitte Holiday Travel Survey (Sep–Oct 2025, n=3,896 US) | **24%** expected GenAI use for holiday planning (16% 2024, 8% 2023); Millennials 31%, Gen Z 30% | Tasks: activities 67%, destinations 56%, accommodation 54% | [verified] |
| Deloitte Summer Travel Survey 2025 | 15% using GenAI in trip planning (10% previous year) | A lower figure from a different survey | [verified] |
| Booking.com *Global AI Sentiment Report* (Apr–May 2025, n=37,325, 33 markets) | 91% excited about AI; 89% interested in using AI for future planning; 67% have used AI in some aspect of travel | Strong positive framing from a sponsor | [verified] |
| Booking.com (business travel study) | 44% of business travellers use AI to plan trips | | [claimed] |
| Accenture Consumer Pulse (Jan 2025, ~18,000 consumers, 14 countries) | GenAI is now the **#1 travel discovery channel for weekly AI users**, ahead of social media and OTAs | No age breakdowns reported | [claimed – secondary] |
| McKinsey (Germany press release, Sep 2025) | 70% of consumers want to use digital assistants for trip planning | | [claimed] |
| Expedia Group / YouGov *AI Trust Gap* (14 Apr 2026, n>5,700, US/UK/(India)) | Only **8%** rely on AI chatbots for planning, against 59% search engines and 49% OTAs | Sponsor has an incentive to downplay chatbots | [verified – press release] |

**Interpretation [inferred].** Measured adoption ranges from **8% to 67%**. The range is not noise. It reflects (a) "ever used for any part of travel" versus "rely on it for planning", (b) sponsor incentives: OTAs report low chatbot reliance, while AI-optimistic consultancies report high readiness, and (c) geography (APAC and India are higher). A defensible planning assumption for 2026 is that **~35–55% of active travellers in the US and Europe touch AI somewhere in planning, but under 10–15% treat it as their primary planning tool.**

### 2.2 Trust and willingness to delegate or book

| Source | Metric | Label |
|---|---|---|
| Booking.com Global AI Sentiment (2025) | Only **6% fully trust** AI (APAC 8%); travellers "draw a firm line at letting technology make decisions without human oversight" | [verified] |
| Booking.com Oceania (KarryOn, 2026) | 63% will likely use AI for 2026 travel, but **only 3% trust it enough to transact with their credit card** | [claimed – exec quote] |
| Booking.com 2026 Travel Trends | Categories travellers trust AI to book: **restaurants 38%, excursion tickets 38%, hotels 35%, flights 32%** | [claimed – secondary] |
| Booking Holdings Q2 2026 earnings call | LLM-referred traffic (paid + unpaid) "significantly below 1% of our room nights" | [claimed – secondary coverage] |
| Expedia / YouGov (Apr 2026) | **53%** comfortable letting AI *suggest options*; **40%** would use AI to *build itineraries*; **8%** comfortable *booking* via an AI platform; **68%** prefer to book with a trusted brand even when AI booking is available; two-thirds would not trust an AI assistant to buy or book on their behalf | [verified – press release] |
| Expedia (secondary summary) | 57% fear losing control or payment privacy | [claimed] |
| Phocuswright *Chat, Plan, Book* | Only ~1/3 fully trust GenAI answers; **~1/4 to 1/3 willing to let an assistant book**; younger travellers more open | [verified – preview] |
| Skift / McKinsey *Remapping Travel with Agentic AI* (Sep 2025) | "Traveler comfort collapses at the point of transaction"; most prefer to confirm flights and hotels themselves; only **14%** say *nothing* would convince them to allow automated booking | [claimed – secondary] |
| Skift *State of Travel 2025* | **2%** willing to give an AI tool full autonomy to make and change bookings. Note: McKinsey's page may describe this group as travel executives, not consumers | [claimed – base unclear] |
| Accenture Consumer Pulse 2025 | **57%** want AI assistants that work *across multiple brands and services* to handle trips | [claimed] |
| Accenture Holiday Survey (Aug–Sep 2025, US) | ~60% "ready" for fully AI-booked travel; 36% have used an airline's GenAI tool | [claimed – stated attitude only] |
| YouGov US (2025) | **30%** comfortable using AI for trip planning, **40%** not; **23% prefer not to use AI at all**; 18–24 comfort 47%→34%; 25–34 47%→38%; 55+ 16%→20%; men 39%→34%, women 26% flat; women 44% not comfortable vs 36% of men | [verified] |
| YouGov UK (2025) | Comfort rising, 15%→20% | [verified] |

**Key takeaways [inferred from the above]:**
- **The trust ladder is clear.** Suggest (53%) > build itinerary (40%) > book low-stakes items such as restaurants and tours (~38%) > book hotels (35%) > book flights (32%) > transact by card (3–8%) > full autonomy (2%). A product should **climb this ladder rather than skip to the top**.
- **Cross-brand neutrality is wanted.** 57% (Accenture) want an assistant that works *across* brands. That plays against single-OTA assistants such as Romie, Booking AI and Kayak, which can only show their own inventory.
- **The demographic surprise.** Gen Z and young Millennials are the heaviest users (Deloitte), yet their *comfort* is falling (YouGov). This suggests disillusionment after real use, consistent with accuracy complaints. It is a warning that trial does not equal retention.
- **Women are a structurally more sceptical segment**, likely tied to safety stakes [inferred]. That is an opportunity for safety-grounded features.

### 2.3 Behavioural signal: AI referral traffic (Adobe Analytics)

| Period | Metric | Label |
|---|---|---|
| Feb 2025 vs Jul 2024 | GenAI traffic to US travel, leisure and hospitality sites **+1,700%** | [verified – Adobe blog] |
| May 2025 vs Jul 2024 | AI referrals to travel **~33x** | [verified – Adobe blog] |
| Jul 2025 YoY | +119%; conversion gap vs non-AI traffic narrowed to ~1% (from 47% a year earlier) | [claimed – secondary] |
| Holiday 2025 | Travel AI traffic +539% YoY; AI referrals converted 31% more | [claimed – conflicting] |
| May 2026 YoY | AI traffic to US travel sites **+194%**; AI-referred visitors converted **28% less** than non-AI traffic, but engagement is higher | [verified – Search Engine Land on Adobe] |

**Interpretation [inferred].** Traffic is growing from a small base. Conversion results conflict across Adobe releases, and the most recent (May 2026) shows AI-referred visitors converting *worse*. Together with Booking's <1% of room nights, the behavioural data says **AI is a research layer that hands off to a booking site**. The handoff is where value, and frustration, sits.

---

## 3. What reviewers and users say, tool by tool

*Coverage is uneven. See §0.*

### 3.1 Layla (layla.ai)
- **Ratings:** Trustpilot TrustScore **4.0 from 76 reviews** (.com), **3.5 from 49** (Canada), **3.8 from 54–55** (Switzerland, Poland) **[verified – Trustpilot listing snippets]**. Google Play reportedly **2.7**, but only per a competitor's comparison page (Pilot) **[claimed, unverified]**.
- **Praise themes:** a personalised end-to-end itinerary, budget adjustment, and a **human travel expert** who helps with bookings.
  - "laid it all out end to end and helped tweak it to my budget" (Trustpilot, via search excerpt) — https://www.trustpilot.com/review/layla.ai?page=2
  - Reviewer valued "the human aspect of process at the end" (Trustpilot, via search excerpt).
- **Complaint themes:** **cancellation or subscription problems** ("cancellation traps" are referenced by reviewers), and doubts about it as a full-trip planner.
  - "Its not flawless but its genuinely one of the most usefull travel tools ive come across." (mixed review, Trustpilot)
  - One reviewer wrote they were not convinced Layla is "the best option for planning a full trip."
- **Booking:** reportedly **links out** to partner sites rather than booking in-app **[claimed – competitor page]**.
- **Brand confusion:** a review guide warns there are two unrelated products called "Layla AI" (https://www.endlesstravelplans.com/guides/planning-tools/layla-ai-review) **[claimed]**.

### 3.2 Wanderlog (the incumbent manual planner with AI add-ons)
- **Ratings:** Google Play **4.7 from ~34,805 ratings** (per a travel blog, July 2026) **[claimed]**. An aggregator analysed 30.9K reviews (marlvel.ai). Trustpilot is small and negative, around **2/5** **[verified – listing snippet]**.
- **Top complaints:** (1) **subscription and billing**, such as being charged after a "free" sign-up turned into a trial, and difficulty cancelling; (2) **technical bugs**, including "white screen" bugs after payment; (3) **auto-import of bookings is less reliable than TripIt**; (4) the **AI features are underwhelming** and gated behind Premium.
  - "the app stated you could use for free but when I signed up it stated one week free trial" (Trustpilot, via search excerpt) — https://www.trustpilot.com/review/wanderlog.com?page=2
  - One Trustpilot reviewer called the AI "nothing useful" (via search excerpt).
  - A guide site says experienced users treat AI output "as a starting draft" (https://www.endlesstravelplans.com/guides/planning-tools/wanderlog-review) **[claimed]**.
- **Insight [inferred]:** Wanderlog's very high Play rating comes from its **manual collaborative itinerary + map** core, not AI. Users love a structured, editable, shareable, map-anchored plan, and that is the bar any AI planner is judged against.

### 3.3 Mindtrip
- Product Hunt: one user called it "hands down the most beautiful and useful travel app" (via search excerpt, https://www.producthunt.com/products/mindtrip). Another Product Hunt reviewer left a negative review, but I did not see the details.
- App Store reviewer: had not tried it on a vacation yet, only locally. This is typical of aspirational usage, where people try the tool more than they rely on it [verified snippet / inferred pattern].
- PhocusWire Hot 25 for 2025. The mobile app positioned as an "on-trip companion" and is built on OpenAI technology **[verified]**.
- Free to use, **monetised via booking partnerships** **[claimed – directory]**. This means recommendations may be steered toward bookable inventory, a sponsored-bias risk users increasingly ask about [inferred].
- Travel Awaits hands-on test: a four-night, arts-focused, crowd-avoiding Barcelona itinerary (May 2025). The search tool did not surface the verdict.

### 3.4 ChatGPT and general LLMs used for travel
- **The Points Guy (2023, older):** "Each time I asked the AI to revert to the previous version, it drifted further from the original brief." This is **revision drift**: the plan state is not stable across edits. https://thepointsguy.com/news/chatgpt-ai-holiday-trip-planning-experience **[verified snippet; dated]**
- **Fox News tech (2025):** AI "invents answers" when it fills gaps; advises verifying "as you would with a travel agent." https://www.foxnews.com/tech/even-with-glitches-planning-your-next-trip-with-ai-is-making-me-rethink-travel
- **Fodor's forum, "Has anyone tried ChatGPT to plan a trip" (late 2025):** one poster said a follow-up answer "quoted my own words from Trip Advisor". Another still finds **Google Maps more useful for road trips**. https://www.fodors.com/community/travel-tips-and-trip-ideas/has-anyone-tried-chatgpt-to-plan-a-trip-1733260/page2
  - *Insight [inferred]:* the "hyperlocal knowledge" in LLMs is often regurgitated forum content. Power users notice, and it undermines perceived originality and authority. Attribution ("this tip comes from X, posted 2025") could become a trust feature.
- **Coleman Concierge roundup of Reddit discussions (secondary blog, anecdotal):** one Reddit traveller who planned trips across six countries estimated **AI gave wrong opening hours ~20% of the time**. Commenters cited travellers being sent to **closed or non-existent attractions**. **Over-ambitious Japan itineraries** rushed through Tokyo, Kyoto, Osaka and Hiroshima. Itineraries "look complete" but felt "strangely incomplete". https://www.colemanconcierge.com/ai-travel-planning-mistakes-real-travelers/ **[claimed – I could not load the underlying Reddit threads]**

### 3.5 Not covered this pass
Kayak AI mode, Expedia Romie, Booking.com AI Trip Planner, GuideGeek, iMean, Airial, Stippl, Holiwise, Wonderplan, Trip Planner AI, Gemini, and the major journalist hands-on tests (NYT, WSJ, Verge, Wired, CNET, CNT, Skift) were not researched because the search budget ran out. **Do not read the absence of complaints here as absence of problems.**

---

## 4. Do users confirm the four known problems?

| Known problem | User-side evidence | Verdict |
|---|---|---|
| **(1) Generic, cliché recommendations; no hyperlocal knowledge** | Itineraries "look complete but feel strangely incomplete" (Coleman/Reddit). Over-packed "greatest hits" Japan routes (Coleman). Fodor's poster saw their own TripAdvisor words regurgitated. Skift Research's *The Disappearing Destination* frames AI as a filter that narrows discovery to well-known places [claimed]. Wanderlog users treat AI as "a starting draft". | **Confirmed, but needs refining.** The complaint is less "it's generic" and more "**it's the same canon everyone gets, stitched together without judgement**": no sense of *why* a place matters to *me*, no seasonal or timing nuance, no trade-offs. |
| **(2) Poor booking interoperability** | Layla links out to partners [claimed]. Wanderlog auto-import less reliable than TripIt [claimed]. 57% want cross-brand assistants (Accenture). LLM traffic <1% of Booking room nights. Adobe shows AI-referred visitors convert worse (May 2026). | **Confirmed, but users frame it as a handoff problem.** They don't want the AI to book everything. They want the **plan-to-book transition** and **book-to-plan import** to be lossless (prices, dates and confirmations flowing both ways). |
| **(3) Stale data / hallucinations** | Wrong opening hours ~20% (anecdotal). Closed or non-existent attractions. "Invents answers" (Fox). Booking.com: 6% fully trust. YouGov speculates accuracy concerns drive falling youth comfort. | **Strongly confirmed.** This is the most cited quality failure, and it compounds: one bad fact makes users re-verify *everything*, which erases the time saved. |
| **(4) No accountability** | Users phrase it as "I fact-check", "I want human oversight" (Booking.com), "I'd book with a trusted brand" (Expedia: 68%), and they praise Layla's human expert. Only 3–8% would transact through AI. | **Confirmed, but implicit.** Users rarely say "accountability". They show it by refusing to pay through AI and by preferring brands with customer service and refund rails. |

### Problems the brief did not list (new)

| # | New problem | Evidence | Label |
|---|---|---|---|
| 5 | **Subscription and billing dark patterns** (trial traps, hard cancellation, paywalled AI) | Top complaint category in Layla and Wanderlog Trustpilot excerpts and in aggregator analysis | [verified snippets; small n] |
| 6 | **Revision drift and fragile plan state**: edits re-generate the whole plan, earlier versions are lost, chat history isn't a plan | TPG test (2023); chat-only tools have no persistent itinerary object | [verified, dated] + [inferred] |
| 7 | **Unrealistic pacing and geography**: too many cities, ignores transit time and jet lag | Japan examples; "over-ambitious" itineraries | [claimed] |
| 8 | **Organising bookings already made** (email or confirmation import) is unreliable | Wanderlog vs TripIt comparison | [claimed] |
| 9 | **Opaque monetisation and sponsored bias**: free planners funded by booking commissions | Mindtrip monetisation model; Expedia's "trusted brands" framing | [inferred] |
| 10 | **Derivative content without attribution** erodes authority | Fodor's "quoted my own words" | [verified snippet, n=1] |
| 11 | **Trust erosion after use** (novelty wears off) | YouGov 18–24 comfort −13 pts YoY while use rises (Deloitte) | [verified data; causal link inferred] |
| 12 | **Gendered trust gap and safety** | Women 44% not comfortable vs 36% of men (YouGov) | [verified data; safety link inferred] |

---

## 5. Jobs-to-be-done across the trip lifecycle

Ratings of AI helpfulness are mostly **[inferred]**. They synthesise the survey task data (Deloitte; Expedia's 53% suggest / 40% itinerary; Booking.com category trust) and the complaint themes above. Rows marked **(E)** have direct evidence.

| Stage | Job | Where AI helps today | Where it fails or users don't trust it | Opportunity |
|---|---|---|---|---|
| Inspiration | "Give me ideas that fit me" | **(E)** Top use. Deloitte: activities 67%, destinations 56%. Accenture: GenAI is the #1 discovery channel for heavy users | Same canon for everyone; homogenisation (Skift *Disappearing Destination*) | Taste profiles from real signals (saved TikToks, Maps lists, past trips); "why this fits you" explanations |
| Destination choice | Compare options against budget, season, weather, crowds, events | Quick comparisons | Stale prices; no live event or closure data; little seasonality nuance | Live-grounded comparisons with dated citations |
| Logistics and routing | Build a feasible day-by-day plan | **(E)** 40% would use AI to build itineraries (Expedia) | **(E)** Over-packed days, ignored transit times, wrong opening hours | Constraint solver: opening hours, travel times, pace, rest blocks, with every fact checked and timestamped |
| Booking | Buy flights, hotels, tours, restaurants | Discovery, then handoff | **(E)** 3–8% would transact via AI; <1% of Booking room nights; 2% want full autonomy | Approval-gated booking, starting with low-stakes items (restaurants, tours: 38%) |
| Pre-trip prep | Visas, entry rules, vaccines, eSIM, insurance, money, packing | Checklists | High-stakes facts where hallucination is dangerous (visa and entry rules) | Authoritative-source grounding and per-passport rules; reminders tied to dates |
| On-trip | Navigation, reservations, translation, changes, "what's open near me now" | Mindtrip positions itself as an "on-trip companion" **(E)** | Plans are static; no re-planning when it rains or a place is closed | Live re-planning with location, weather and closures; offline mode |
| Disruption | Cancelled flight, strike, illness | Little evidence of AI help | **(E)** Accountability gap: users want a brand or human behind it | Disruption copilot: rebooking options, rights (EU261 etc.), scripts, escalation to a human |
| Post-trip | Expenses, splitting, memories, sharing, reviews | Not evidenced | Not evidenced | Auto-generated trip journal, expense split, shareable itinerary as a "recipe" |

**Key structural insight [inferred]:** current AI planners are concentrated at the two stages where users trust AI most and where switching costs are lowest: inspiration and itinerary drafting. The **high-value, high-trust-required stages** (booking, disruption, on-trip changes) are where users say they still want a brand or a human. Owning those requires accountability mechanisms, not better prose.

---

## 6. Underserved segments

This section is mostly **[inferred]**. I could not run the segment-specific searches (accessibility, LGBTQ+, families, group travel). It should be re-validated with forum evidence.

| Segment | Why underserved | Evidence strength |
|---|---|---|
| **Women and solo female travellers** | Measurably lower comfort with AI (44% not comfortable, YouGov). Safety-critical decisions (neighbourhood safety at night, transport after dark) are where generic advice is least acceptable | Data [verified]; needs [inferred] |
| **Older travellers (55+)** | Fastest-*growing* comfort (16%→20%, YouGov) but from a low base. Likely value pacing, accessibility and human backup | [verified] trend; needs [inferred] |
| **Gen Z / young Millennials** | Heaviest users (Deloitte 30–31%) but comfort falling sharply (YouGov), i.e. churn risk. Budget-sensitive; social-native discovery (TikTok) | [verified] |
| **Group travel** | Planners are built around a single user's chat. Decisions, voting, cost splitting and divergent preferences are unmodelled; Wanderlog's collaborative editing is the benchmark | [inferred] |
| **Families with kids** | Nap and meal schedules, stroller and transport logistics, age-appropriate filtering; over-packed itineraries hit hardest here | [inferred] |
| **Accessibility / disabled travellers** | Need *verified* step-free access and room specifics. A hallucinated "accessible" is harmful | [inferred]; high severity |
| **Dietary restrictions / allergies** | Needs restaurant-level, current data; hallucination risk is a health risk | [inferred] |
| **Multi-country / overland / rail** | Routing feasibility, border rules, rail passes, transit times; AI produces over-ambitious multi-city plans (Japan examples) | [claimed] |
| **Business + leisure** | 44% of business travellers use AI to plan (Booking.com) but corporate policy, expensing and loyalty integration are absent | [claimed] |
| **Non-English / APAC markets** | APAC shows higher enthusiasm (Booking.com: 93% want AI in plans, 8% full trust; 64% use AI to plan) but most tools are English- and US-centric | [claimed] |
| **LGBTQ+ travellers** | Legal and safety context by country and neighbourhood | [inferred]; no data gathered |

---

## 7. Personalisation reality check

What the evidence shows:
- **Users expect a draft, not a plan.** Wanderlog's power users treat AI "as a starting draft". Booking.com respondents want AI to help, not decide. The current *perceived* ceiling of AI personalisation is "a decent first draft to edit" **[claimed/verified]**.
- **Constraints get ignored.** Pace is the clearest example: over-packed, multi-city sprints. Budget gets better marks; Layla praise specifically mentions tweaking to budget, which suggests budget is the one constraint tools handle reasonably **[claimed]**.
- **Editing is the failure point.** Revision drift (TPG) and chat-as-plan architectures mean users lose earlier versions and can't make surgical edits ("swap only Tuesday afternoon") **[verified, dated + inferred]**.
- **"It doesn't know me."** No evidence in this pass that any tool learns from past trips, saved places or social saves. Personalisation is limited to what users type in a prompt. That makes every itinerary converge on the canon **[inferred]**.
- **Ads and sponsored bias.** No direct user quote found this pass. The structural risk is clear (commission-funded free planners; OTA assistants showing only their own inventory), and Accenture's 57% wanting cross-brand assistants hints at demand for neutrality **[inferred]**.

---

## 8. Workarounds: what users do instead, and why it persists

Evidence here is mostly **[inferred]**, except where noted.

| Workaround | Why it persists | Implication |
|---|---|---|
| **Search engines + OTAs** (59% and 49% use for planning; Expedia/YouGov) **(E)** | Familiar, current, comparable prices, trusted refunds | AI must hand off cleanly or embed live inventory |
| **Wanderlog / TripIt** for organisation **(E)** | Structured, editable, collaborative, map-anchored; TripIt's email import is reliable | A persistent, structured itinerary object is table stakes |
| **Google Maps saved lists** (Fodor's: Maps "more useful" for road trips) **(E – n=1)** | Ground truth on location, hours and reviews; you can see the geography | Integrate with or import Maps lists; show the map first |
| **Forums and Reddit** ("asking locals") | Human judgement, recency, contrarian advice, accountability via reputation | Cite and timestamp human sources; offer a human-expert escalation path (Layla's human expert is praised) |
| **Google Docs / Sheets / Notion templates** | Full control, shareable, no subscription, never "drifts" | Export and two-way sync; never hold the plan hostage |
| **TikTok / Instagram saves** | Inspiration is social and visual | Ingest saved posts as preference signals |
| **Human travel agents and advisors** | Accountability, disruption handling, complex trips | Hybrid human + AI service for high-stakes trips |
| **Fact-checking AI output manually** (Booking.com: users fact-check; only 6% fully trust) **(E)** | Hallucinations | Show sources and verification timestamps by default |

**Why workarounds win [inferred]:** each is *trusted for one thing*: Maps for place truth, OTAs for prices and refunds, Reddit for judgement, Sheets for control. AI planners try to replace all of them at once but are trusted for none, so users fall back to stitching the old tools together.

---

## 9. What users explicitly do NOT want

| Don't want | Evidence |
|---|---|
| **AI booking or paying without explicit approval** | 2% want full autonomy (Skift); 3% would let AI transact by card (Booking.com Oceania); 8% comfortable booking via AI (Expedia); "firm line at letting technology make decisions without human oversight" (Booking.com) |
| **Losing control or payment privacy** | 57% fear losing control or payment privacy (Expedia, secondary) |
| **Being locked into one brand's inventory** | 57% want cross-brand assistants (Accenture) [claimed] |
| **Subscription traps / surprise charges** | Top Trustpilot complaint for Layla and Wanderlog |
| **Confident but unverified facts** | Fact-checking behaviour; 6% full trust |
| **Over-scheduled itineraries** | Japan "sprint" complaints [claimed] |
| **AI in the loop at all (a sizeable minority)** | **23%** of US travellers prefer not to use AI for planning (YouGov). The product needs a no-chat, manual-first mode |

## 10. Delight features users praise

| Delight | Evidence |
|---|---|
| End-to-end draft in minutes, adjusted to budget | Layla Trustpilot: "laid it all out end to end and helped tweak it to my budget" |
| A human expert behind the AI | Layla Trustpilot: "the human aspect of process at the end" |
| Beautiful, map-first, visual UI | Mindtrip Product Hunt: "hands down the most beautiful and useful travel app" |
| Collaborative, editable itineraries + map (manual core) | Wanderlog's 4.7 Play rating [claimed] |
| Reliable confirmation import | TripIt benchmark (vs Wanderlog) [claimed] |
| "GenAI improves trip planning" overall | 78% (Phocuswright) |

---

## 11. Ranked pain points (frequency × severity)

**Evidence count** is the number of independent sources in this report supporting the point (surveys + reviews + articles). It is small because of the constraints in §0, so treat it as directional.

| Rank | Pain point | Frequency | Severity | Evidence count | Maps to brief |
|---|---|---|---|---|---|
| 1 | **Hallucinated or stale facts** (hours, closures, non-existent places, entry rules), forcing users to re-verify everything | High | High (wasted trips, safety, money) | 6 (Coleman/Reddit, Fox, Booking 6% trust, Phocuswright 1/3 trust, YouGov accuracy note, Fodor's) | #3 |
| 2 | **Trust and accountability gap at the transaction**: won't pay through AI, wants a brand or human behind it | Very high (survey majority) | High (blocks monetisation) | 7 (Expedia, Booking ×2, Skift, McKinsey/Skift, Phocuswright, Booking Holdings <1%) | #4 |
| 3 | **Generic, same-y, canon-only itineraries** that lack judgement and local nuance | High | Medium | 5 (Coleman, Fodor's, Skift *Disappearing Destination*, Wanderlog "starting draft", Layla mixed review) | #1 |
| 4 | **Over-packed, geographically unrealistic plans** that ignore pace | Medium–High | Medium | 2 (Coleman Japan, "strangely incomplete") | new |
| 5 | **Subscription and billing dark patterns** in AI planner apps | Medium (dominant on Trustpilot) | Medium–High (brand-killing) | 3 (Layla TP, Wanderlog TP, aggregator analysis) | new |
| 6 | **Broken plan-to-book and book-to-plan handoff** (link-outs, unreliable import, re-entering data) | Medium | Medium | 4 (Layla link-out, Wanderlog vs TripIt, Accenture cross-brand, Adobe conversion gap) | #2 |
| 7 | **Fragile editing, revision drift, plan lives in chat** | Medium | Medium | 1 direct (TPG, 2023) + inferred | new |
| 8 | **Trust erosion after use** (young-user comfort decline) | Emerging | High (retention) | 1 strong dataset (YouGov) | new |
| 9 | **Sponsored or commission bias and single-brand inventory** | Unknown (no direct quotes) | Medium | 2 indirect (Mindtrip model, Accenture 57%) | new |
| 10 | **Segment blind spots**: groups, accessibility, diet, safety for women and LGBTQ+ | Unknown | High for affected users | 1 dataset (YouGov gender) + inferred | new |

---

## 12. Top gaps and opportunities (user perspective)

1. **"Verified itinerary" as the product.** Every place, hour, price and entry rule carries a source and a "checked on" timestamp, with automatic re-verification before departure and on the day. This is the most direct answer to pain #1, and users already do it manually.
2. **Climb the trust ladder with approval-gated, accountable booking.** Start with restaurants and tours, where 38% trust AI, before hotels and flights. Always require explicit approval. Book through brands users trust, or offer clear guarantees and a human escalation path. Don't sell autonomy, which only 2% want. Sell **"I'll handle the tedious parts, you approve, and we're on the hook if it breaks."**
3. **A persistent, structured, collaborative plan object, not a chat log.** Surgical edits, version history, group voting and cost splitting, two-way sync with Google Maps lists, Sheets and email confirmations, reliable TripIt-grade import. Beat Wanderlog on its own turf, then add AI.
4. **Judgement over listings.** Pace-aware, geography-realistic plans with explicit trade-offs ("skip Hiroshima or you'll spend 9 of 14 days on trains"), personal rationale ("because you saved X"), and attributed, recent human local knowledge rather than unattributed regurgitation.
5. **Honest business model and safety-first segments.** No trial traps, a disclosed neutral ranking, and cross-brand inventory, which 57% want. Lead with segments where generic AI is weakest and stakes are highest: solo women's safety, accessibility, dietary needs and multi-country overland. That also reaches the sceptical 44% of women and the 23% who avoid AI.

---

## 13. Follow-up research needed (not done in this pass)

- App Store and Google Play ratings and complaint mining for Mindtrip, Layla, Wonderplan, Trip Planner AI, GuideGeek, iMean, Airial, Stippl, Holiwise, Expedia (Romie), Booking.com, Kayak.
- Direct Reddit threads (r/travel, r/solotravel, r/JapanTravel, r/digitalnomad, r/ChatGPT, r/onebag) and Hacker News "Show HN" AI travel planner threads.
- Journalist hands-on tests: NYT, WSJ, The Verge, Wired, CNET, Condé Nast Traveler, Skift, The Points Guy (2025–26).
- Segment-specific forum evidence: accessibility, LGBTQ+, families, group travel, dietary needs.
- Willingness-to-pay data for AI planners (not found this pass).
- Primary-source verification of the Phocuswright, Booking Holdings Q2 2026 and Accenture figures.

---

## Sources

**Demand, adoption and trust data**
- https://www.phocuswright.com/Travel-Research/Consumer-Trends/Chat-Plan-Book-GenAI-Goes-Mainstream
- https://www.phocuswright.com/Travel-Research/Research-Updates/2025/From-hype-to-habit-78-percent-of-travelers-say-GenAI-improves-trip-planning
- https://www.phocuswright.com/Travel-Research/Research-Updates/2025/Phocuswright-Research-Roundup-2H25
- https://www.phocuswright.com/Travel-Research/Research-Updates/2025/search-slips-ai-surges
- https://www.phocuswright.com/Travel-Research/Research-Updates/2026/Travel-Forward-Data-Insights-and-Trends-for-2026
- https://www.breakingtravelnews.com/news/article/majority-of-u.s.-travelers-now-use-ai-for-trips-marking-fastest-behavioral/
- https://www.travelpulse.com/news/technology/ai-goes-mainstream-in-travel-planning-new-report-finds
- https://www.traveldailynews.com/statistics-trends/ai-adoption-reshapes-travel-planning-behavior-in-the-u-s-phocuswright-reports/
- https://www.hospitalitynet.org/news/4131919/expedia-group-reveals-the-ai-trust-gap-travelers-embrace-ai-for-planning-but-rely-on-trusted-brands-to-book
- https://partner.expediagroup.com/en-us/resources/blog/ai-trust-gap-why-travelers-continue-to-choose-trusted-brands
- https://emergingtravel.news/expedia-report-ai-travel-booking-trust/
- https://www.stocktitan.net/news/EXPE/expedia-group-reveals-the-ai-trust-gap-travelers-embrace-ai-for-qe4tlvya4599.html
- https://news.booking.com/bookingcom-releases-the-global-ai-sentiment-report/
- https://www.hospitalitynet.org/news/4128268.html
- https://www.webintravel.com/?p=71130
- https://globetrender.com/?p=85894
- https://karryon.com.au/industry-news/other-technology/ai-booking/
- https://www.traveldailynews.com/mice-industry/business-travel/nearly-half-of-business-travellers-use-ai-tools-for-trip-planning-booking-com-study-finds/
- https://www.travelerstoday.com/articles/60754/20260805/hotel-bookings-via-ai-chatbots-stay-below-1-booking-holdings-confirms.htm
- https://skift.com/2026/11/03/booking-com-bets-travelers-will-research-with-ai-but-book-with-it
- https://skift.com/2025/08/01/booking-trends-ai-tools-and-the-new-rules-of-travel-planning/
- https://research.skift.com/reports/the-disappearing-destination-ai-as-a-new-filter-in-discovery/
- https://www.mckinsey.com/industries/travel-transport-and-logistics/our-insights/remapping-travel-with-agentic-ai
- https://www.mckinsey.com/de/news/presse/2025-09-22-verbraucher-ki-reiseplanung
- https://www.chinatravelnews.com/article/188186
- https://www.hospitalitynet.org/news/4129865/2025-deloitte-holiday-travel-survey
- https://lodgingmagazine.com/deloitte-holiday-travel-intent-increases-amid-financial-concerns/
- https://cxm.world/cxm-news/summer-travel-gets-a-reality-check-in-2025/
- https://www.yougov.com/en-us/articles/52770-comfort-with-ai-in-travel-planning-dips-among-younger-americans
- https://www.travelmarketreport.com/top-story/articles/younger-americans-becoming-less-comfortable-with-ai-travel-planning/
- https://yougov.com/en-gb/articles/53267-brits-more-comfortable-using-ai-for-trip-planning-than-last-year2
- https://www.phocuswire.com/generative-ai-driving-travel-discovery-accenture-study
- https://www.travelpulse.com/news/features/new-consumer-report-says-ai-has-surpassed-social-media-otas-for-travel-discovery
- https://www.hotelinvestmenttoday.com/Forecasts/Are-Americans-ready-for-AI-booked-travel/61666/
- https://ftnnews.com/?p=60371

**AI referral traffic (Adobe)**
- https://business.adobe.com/blog/the-explosive-rise-of-generative-ai-referral-traffic
- https://business.adobe.com/blog/ai-driven-traffic-surges-ahead-in-q2
- https://searchengineland.com/ai-referrals-engagement-travel-sites-adobe-480445
- https://www.hotelnewsresource.com/article141764.html
- https://superpowerdaily.com/posts/ai-travel-referrals-are-surging-airlines-may-be-hardest-for-bots-to-read
- https://tech.yahoo.com/ai/deals/articles/ai-traffic-travel-sites-booming-112000665.html

**Product reviews and user complaints**
- https://www.trustpilot.com/review/layla.ai?page=2
- https://ca.trustpilot.com/review/layla.ai
- https://www.endlesstravelplans.com/guides/planning-tools/layla-ai-review
- https://www.pilotplans.com/compare/layla-ai-alternative-feature-comparison (competitor page; treat with caution)
- https://www.trustpilot.com/review/wanderlog.com?page=2
- https://www.endlesstravelplans.com/guides/planning-tools/wanderlog-review
- https://kimola.com/reports/unlock-insights-with-the-wanderlog-app-feedback-analysis-google-play-en-us-154237
- https://marlvel.ai/apps/wanderlog-travel-planner/reviews
- https://www.producthunt.com/products/mindtrip
- https://apps.apple.com/app/id6503107567
- https://www.travelawaits.com/3005771/inside-new-travel-ai-mindtrip/
- https://www.phocuswire.com/mindtrip-launches-mobile-app-ai-trip-planner
- https://tooldirectory.ai/tools/mindtrip
- https://thepointsguy.com/news/chatgpt-ai-holiday-trip-planning-experience
- https://www.foxnews.com/tech/even-with-glitches-planning-your-next-trip-with-ai-is-making-me-rethink-travel
- https://www.fodors.com/community/travel-tips-and-trip-ideas/has-anyone-tried-chatgpt-to-plan-a-trip-1733260/page2
- https://www.colemanconcierge.com/ai-travel-planning-mistakes-real-travelers/
