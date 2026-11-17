# 06 — The Voice of the Traveller: Reviews, Complaints, Demand Data and What Users Want from AI Trip Planning

*Research agent 6 of 7. Compiled 2026-11-17. Scope: the user side. Reviews and complaints, demand and adoption data, jobs-to-be-done, personalisation, workarounds.*

---

## 0. Read this first: method, evidence quality and gaps

**Evidence labels.** **[verified]** means the figure or quote appeared in a search result attributed to the named primary source or its press release. **[claimed]** means it appeared only in secondary coverage, competitor marketing or an aggregator, or the sources conflict. **[inferred]** means it is my analysis or domain reasoning, not a sourced user statement.

**Hard limits on this run (please read before relying on it):**
- **WebFetch was blocked.** `phocuswright.com`, `trustpilot.com` and `colemanconcierge.com` all failed with DNS errors because they are outside this session's allowed network domains, so I could not read primary pages. Every quote below is text that the search tool pulled from the named URL. I did not load the page itself. To read primary sources, these domains (and reddit.com, apps.apple.com, play.google.com and producthunt.com) need to be allowed in the session's network settings.
- **First pass:** the shared web-search budget ran out after about 22 searches (limit 200 per turn across 7 parallel agents).
- **Gap-fill pass (same day, 58 searches, no page loads).** It added: App Store, Google Play and Trustpilot figures for 18 tools (§3.0 summary table, §3.5–§3.19); eight journalist or tester hands-on tests (§3.20); forum and Hacker News evidence (§3.21); segment evidence for accessibility, families, groups, women, LGBTQ+, older travellers, diet, India, Japan and Latin America (§6); a willingness-to-pay and pricing section (§2.4); and primary-source checks of the Booking Holdings, Accenture, Skift, Phocuswright and Expedia figures (§2.2).
- **Most store ratings come from third-party mirrors** (AppFollow, Similarweb, apptail) or from **competitor comparison pages** (Pilot publishes "Pilot vs X" pages for most rivals). Apple and Google pages could not be opened. Treat star ratings as **[claimed]** unless marked otherwise. Review counts differ across mirrors by date.
- **Reddit is poorly indexed by the search tool, and reddit.com is blocked.** No Reddit thread text was retrieved directly. Reddit evidence is second-hand (journalists or blogs describing threads), so it is labelled **[claimed – second-hand Reddit]**. Fodor's, Rick Steves, FlyerTalk, Australian Frequent Flyer and early-retirement.org forums stand in as proxies.
- **Coverage now:** strong on demand, trust and segment survey data; moderate on tool ratings and journalist tests; still weak on verbatim user reviews of newer tools (Airial, Stardrift, Lola, Trip Planner AI) because they have very few public reviews. What remains is in §13.

---

## 1. Executive summary

1. **Usage is mainstream but shallow.** In 2025–26 roughly a quarter to over half of travellers used AI for some part of trip planning, depending on wording. Use is concentrated at the **inspiration and research** end. Deloitte found the top AI travel tasks were researching activities (67%), destinations (56%) and accommodation (54%) **[verified]**.
2. **There is a huge gap between saying and doing on booking.** Sponsor-run "readiness" surveys report that up to ~60% of US travellers are "ready" for AI-booked travel (Accenture) **[claimed]**. In other surveys only **8%** are comfortable booking through an AI platform (Expedia/YouGov, 2026), **6%** fully trust AI (Booking.com, 37k respondents), and **3%** trust it enough to pay by card (Booking.com Oceania) **[verified/claimed]**. Actual behaviour: LLM traffic is **"significantly below 1%" of Booking.com room nights** (Booking Holdings Q2 2026 call) **[claimed, via secondary coverage]**.
3. **Trust is cooling among the youngest users.** YouGov found US 18–24s comfortable with AI trip planning fell from **47% to 34%** in one year, while comfort among those 55+ rose from 16% to 20% **[verified]**. Women remain more sceptical: 44% are not comfortable, against 36% of men **[verified]**.
4. **Complaint evidence matches the brief's four problems, with additions.** Hallucinated or stale facts (closed or non-existent places, wrong opening hours) and generic, over-packed itineraries show up repeatedly. "No accountability" shows up in surveys as "I always fact-check" and "I want human oversight", not as a named complaint. **New problems not on the list:** (a) **subscription and billing dark patterns** are the #1 complaint in Trustpilot data for both Layla and Wanderlog; (b) **revision drift** and poor editing; (c) **unrealistic pacing and geography**; (d) **unreliable import and organisation** of bookings already made; (e) **opaque monetisation** and possible sponsored bias.
5. **Where AI planners earn praise:** an end-to-end draft in minutes, budget tweaking, beautiful maps-first UI (Mindtrip), and a **human expert in the loop** (Layla). The pattern is "AI drafts, human verifies or decides".
6. **(Gap-fill) Store ratings reward organisers, not AI.** The highest-rated, most-reviewed apps are **manual organisers**: Wanderlog (App Store 4.9 from ~30–34K ratings; Play 4.7 from ~35K) and TripIt (Play 4.7 from ~93K). AI-native planners have **tiny review bases**: Mindtrip ~319 App Store ratings, Stippl 414, Layla's new iOS app 18 in Italy, Holiwise ~130 on Trustpilot, Airial and Stardrift almost none **[claimed – mirrors]**. On Trustpilot, which skews towards billing complaints, scores fall to 1.8 (Wanderlog), 2.9 (Stippl), 3.2 (iMean) and 3.5 (Pilot, Axel, Wonderplan). The only standout is **Holiwise at 4.9**, and reviewers there praise its human concierge ("you speak with a real person, not ChatGPT").
7. **(Gap-fill) Journalist tests agree: useful drafts, unreliable facts.** Afar called Mindtrip "the most sophisticated AI plan-and-book tool", but its chatbot told the writer the trip dates "were in the past". Skift's verdict was "Fewer Errors, Still Buggy" (Kayak, Despegar). WSJ found that asking the same question twice gives different answers (Gemini, ChatGPT). NYT called Gemini a "digital Swiss Army knife… with notable gaps". An agency test found errors in **90%** of ChatGPT itineraries (2024, GPT-3.5). A Greetwell 2026 survey found **1 in 6** AI-using travellers had been recommended a place that did not exist **[claimed]**.
8. **(Gap-fill) Willingness to pay is thin.** **50%** of US travellers say AI help should come free, and only **4%** expect it to justify a premium (Amadeus). Paid AI planners cluster at **$40–60 a year**. Proven travel monetisation is **protection and ancillaries**, not planning: about half of Hopper bookings attach a fintech product **[claimed, 2022]**.
9. **(Gap-fill) Identity-driven segments use AI the most and need it to be right.** 66% of LGBTQ+ travellers used AI to plan in the past year, and 76% of trans travellers, whose top reason was checking safety and legal rights (Booking.com Travel Proud 2026). Women *use* AI slightly more than men (24% vs 22%, Global Rescue) but are *less comfortable* with it (YouGov). Adults 50+ doubled their use from 8% to 16% (AARP 2026).

---

## 2. Demand and adoption data (2024–2026)

### 2.1 Adoption: who uses AI for travel planning

| Source (date, sample) | Headline metric | Notes | Label |
|---|---|---|---|
| Phocuswright, *Chat, Plan, Book: GenAI Goes Mainstream* (Jul 2025; US + Europe) | ~1 in 3 travellers use GenAI to plan or enhance trips | Full report paywalled (US$595) | [verified – preview] |
| Phocuswright, *Search Slips, AI Surges* (2025, US) | ~40% of US travellers use AI, **+11 pts YoY** | | [verified – summary] |
| Phocuswright Research Roundup 2H25 (US) | 58% of active US travellers use AI for something; **39% use it for travel** | | [verified – summary] |
| Phocuswright, *The AI Surge: Travel's Fastest Behavioral Shift in a Decade* (2026; n=1,570 US leisure travellers, fielded 8–17 Feb 2026); also in *Travel Forward 2026* | **56%** used AI for at least one trip in the past 12 months, up from **43% in late 2025**. GenAI platforms (ChatGPT, Gemini) were used by **33% for trip research**, close to search engines at **35%**. **64%** of AI users used standalone AI tools. **51%** used AI for real-time recommendations at the destination. Half of AI-search users still click through to source sites | Gap-fill check: the baseline is late 2025; sample and dates confirmed in Phocuswright and PhocusWire summaries | [verified – summary] |
| Global Rescue Fall 2025 Traveler Safety & Sentiment Survey | **22%** used AI tools to plan a trip: non-US 30%, US 20%, **women 24%, men 22%**. Women used it for itineraries (74%), research (68%) and restaurants (36%) | Earlier summer-2025 wave: under-35s more than twice as likely as over-55s | [verified – company blog] |
| AARP *2026 Travel Trends* (n=1,189 adults 50+, Nov–Dec 2025) | AI use for travel planning **doubled from 8% to 16%**. 76% not likely or unsure about using AI | Used to find deals, compare places and organise itineraries, "not to determine destinations" | [verified – press release] |
| Agoda *2026 Travel Outlook* (India, May 2026) | **33%** of Indian travellers already use AI for travel planning; **68%** likely to for the next trip; 88% trust or are neutral on AI recommendations | Allianz Partners 2026 reports a higher 82% "used or plan to", which mixes use and intent | [verified – press release] |
| JTB Research (Japan, 2025) | **77.8%** of weekly GenAI users have used it for travel (women in their 20s 89.3%). GenAI as a travel-info source rose from **9.7% to 28.8%** in a year (JTB smartphone survey, Nov 2025) | Adyen 2025: only 11% of Japanese consumers use AI for travel search or booking, against a 34% global average | [verified – Travel Voice] |
| Marriott Latin America study (frequent travellers, 7 markets incl. Brazil and Mexico) | **54%** use AI to organise trips, up from 43%; Gen Z 64% | Not representative of all LatAm travellers. Booking.com: ~7 in 10 in LATAM and APAC use AI for planning | [claimed – secondary] |
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
| Booking Holdings Q2 2026 earnings call (4 Aug 2026) | **CFO Ewout Steenbergen** (not CEO Glenn Fogel): LLM referral traffic, paid and unpaid, is "still significantly below 1% of our room nights" and has not materially changed. Asked about AI-driven bookings, Fogel said: "I don't know, they don't tell me." | [verified – consistent across PhocusWire, MarketBeat and PYMNTS; transcript PDF exists on the Booking IR site but was not loaded] |
| Expedia / YouGov *AI Trust Gap* (released 14 Apr 2026 via BusinessWire; fieldwork 10–25 Mar 2026; >5,700 adults in US, UK and India) | **53%** comfortable letting AI *suggest options*; **40%** would use AI to *build itineraries*; **8%** comfortable *booking* via an AI platform; **68%** prefer to book with a trusted brand even when AI booking is available; **66%** would not trust an AI assistant to book on their behalf. Gap-fill note: Expedia's own blog describes the 8% as the share who *rely on* AI platforms for *planning*, not booking. The two readings conflict. No India-only figures surfaced | [verified – press release; meaning of the 8% disputed] |
| Amadeus *Tailored Horizons* (US) | **50%** say travel companies should provide AI help at no extra cost; **4%** think AI help will become essential enough to justify a premium; **23%** would pay a small fee | [verified – press release] |
| Amadeus *Connected Journeys* (9,500 travellers, 7 countries) | Nearly **two-thirds** willing to pay for an AI assistant *during* trips; **17%** would spend up to 5% of total trip cost | [claimed – PhocusWire] |
| Expedia (secondary summary) | 57% fear losing control or payment privacy | [claimed] |
| Phocuswright *Chat, Plan, Book* | Only ~1/3 fully trust GenAI answers; **~1/4 to 1/3 willing to let an assistant book**; younger travellers more open | [verified – preview] |
| Skift / McKinsey *Remapping Travel with Agentic AI* (Sep 2025) | "Traveler comfort collapses at the point of transaction"; most prefer to confirm flights and hotels themselves; only **14%** say *nothing* would convince them to allow automated booking | [claimed – secondary] |
| Skift *State of Travel 2025* | **2%** willing to give an AI tool full autonomy to make and change bookings. **Gap-fill check: this is a traveller figure, not an executive one.** McKinsey writes: "Only 2 percent of respondents in Skift's State of Travel 2025 report say that they're currently willing to give an AI tool full autonomy". Skift's own wording is "2% of U.S. travelers surveyed by Skift Research". McKinsey's separate executive survey covered 86 executives; 80% plan agentic AI at scale within 3–5 years. A later (2026) joint report: **74%** prefer to finalise bookings themselves. One May 2026 Skift summary narrows the 2% to "young leisure travelers", which is inconsistent with the other wording | [verified – McKinsey page; exact sample of the 2% unconfirmed] |
| Accenture Consumer Pulse 2025 (18,000+ consumers, 14 countries) | **57%** want AI assistants that work *across multiple brands and services* to solve travel needs autonomously. Same study: 80% use GenAI tools; 93% would trust GenAI to support purchase decisions. Accenture *Talk to My AI Agent* (date unconfirmed): 87% open to working with an AI travel agent; 55% would tell their agent which brands to consider; **7%** would grant full autonomy over purchases | [verified – consistent across Travolution, Globetrender and TravelPulse; Accenture PDF not loaded] |
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

### 2.4 Willingness to pay and competitor pricing (gap-fill)

**Survey evidence on paying for AI planning**

| Source | Finding | Label |
|---|---|---|
| Amadeus *Tailored Horizons* (US) | **50%** say AI help should come at no extra cost; **23%** would pay a small fee; only **4%** expect AI to become essential enough to justify a premium | [verified – press release] |
| Amadeus *Connected Journeys* (9,500, 7 countries) | ~**2/3** would pay for an AI assistant *during* a trip; **17%** up to 5% of trip cost. This is in-trip help, not planning | [claimed – PhocusWire] |
| Accenture | 1/3 would hand over purchase decisions; **9%** would let AI purchase for them | [claimed – secondary] |
| Global Rescue (2025) | Under **20%** comfortable letting AI design an entire itinerary autonomously | [claimed] |
| Family Travel Association 2025 (n≈1,600 parents and grandparents) | **48%** worried about personal-data security when booking online | [claimed – secondary] |
| AARP 2025 | Among 50+ non-users of AI, **data privacy** was the main reservation (**40%**) | [verified – press release] |

**Competitor pricing (consumer), as found in Nov 2026**

| Product | Price | Model | Label |
|---|---|---|---|
| Layla | **$9.99/month, $49.99/year**; 7-day free trial | AI planner subscription + human-expert booking | [verified – App Store listing snippet] |
| Wanderlog Pro | **$39.99/year** (one user cites $50); monthly option in the app | Freemium organiser; AI limited to 5 messages per trip on free | [claimed – multiple] |
| TripIt Pro | ~**$48–49/year** | Freemium organiser with alerts | [claimed] |
| Flighty Pro | **$59.99/year**, $119 family, $299 lifetime (Tapsmart: $70/year or $9/month) | Paid flight tracker | [claimed – Recurdash, Jul 2026] |
| iMean | **$6.99/month** | AI agent subscription | [claimed – directory] |
| Lola (Booking Holdings-backed consumer AI agent) | Free core; **Plus $5/month, VIP $25/month** (12-month commitment; ~$300/year, pitched against premium credit cards). Launched Sep 2026 | Membership + booking | [claimed – secondary] |
| Axel | $35/year (company reply on Trustpilot) vs "no upfront fees, weekly billing" (FAQ); not reconciled | Price-drop monitoring, books after confirmation | [claimed – conflicting] |
| Mindtrip | **Free** for consumers; enterprise tier with undisclosed price; one unverified "$8/month Pro" claim | Booking and affiliate commission | [claimed] |
| Wonderplan, GuideGeek, Stardrift, Pilot, Trip Planner AI | **Free** (Pilot also sells bookings; GuideGeek is funded through destination-marketing deals) | Free / B2B | [claimed] |
| Stippl, Airial | AI planner is a paid **PRO**/premium feature (price not surfaced) | Freemium | [claimed] |

**Evidence of conversion**
- **Travel apps convert trials well but start few of them.** RevenueCat data, via secondary write-ups, shows Travel with the **highest median trial-to-paid conversion** of any category: **43.5%** (2026 edition) or 48.7% (2025). Install-to-trial, however, is among the **lowest at ~4.1%** **[claimed – secondary; RevenueCat report not loaded]**. In plain terms, few users ever start a trial, but those who do, convert.
- **Flighty:** third-party estimate of **~$400–500K/month revenue** and 100K+ monthly downloads (Adapty) **[claimed – estimate]**.
- **Layla:** modelled revenue of **~$2.2–2.8M (2025)** (Latka, Prospeo) and a claimed "5M users" **[claimed – estimates]**. If both are roughly right, paid conversion is well under 5% of users [inferred].
- **Hopper (benchmark for protection products):** just over half of bookings attach at least one fintech product, averaging ~1.5 products; fintech was ~**50% of revenue** (TechCrunch, 2022); Price Freeze averages **$30**; Cancel/Leave For Any Reason ~**$30 per hotel booking**. For white-label partners, Hopper's B2B arm cites only "high single-digit" attach **[claimed – 2021–22 sources]**.

**Implication [inferred].** Users will not pay much for *planning* intelligence: the norm is free or $40–60 a year, and half of US travellers expect AI help to be free. They *do* pay for **certainty and protection** (Hopper-style attach on about half of bookings; Flighty's paid alerts; Axel's savings promise; Holiwise and Layla's human concierge). A paid tier is more likely to work if sold as "we guarantee and fix it" (re-verification, disruption handling, price-drop recovery) than as "better itineraries".

### 2.5 The AI referral funnel, restated with 2026 data

Phocuswright (Feb 2026): ChatGPT and Gemini are already at **33%** for trip research, against 35% for search engines. Booking Holdings (Aug 2026): LLM referrals are still **well under 1%** of room nights. Kayak's product chief (Apr 2026, on launching Ask AI): when plans are vague, people shape the trip in conversation, but "when it comes time to compare and commit, they return to the results pages and filters they already know" **[claimed – secondary]**. All three point the same way: **AI owns research, and booking stays on familiar transactional interfaces** [inferred].

---

## 3. What reviewers and users say, tool by tool

*Coverage is uneven. See §0. Ratings come from search snippets of store mirrors, Trustpilot listings and competitor pages. Apple and Google pages were not opened.*

### 3.0 Ratings at a glance (gap-fill)

| Tool | App Store | Google Play | Trustpilot | Other | Main praise | Main complaint |
|---|---|---|---|---|---|---|
| **Wanderlog** | **4.9** (29.9K–33.9K) | **4.7** (~34.8K) | **1.8** (~45–48 reviews) | | Map + collaborative manual planner | Billing and trials; Premium AI locked to the payer only; AI "nothing useful" |
| **TripIt** | 4.6–4.8 (varies by storefront) | **4.7** (93.2K) | low, small n | G2 4.6 (44) | Reliable import; disruption alerts ("alerted me to a canceled flight in the middle of the night") | Login and password bugs; import corrupting dates and flight numbers; Pro value |
| **Mindtrip** | **~4.8** (319, via Similarweb mirror) | not found | n/a | PH 4.3 (6) | Beautiful, visual, linked itinerary | Wrong dates ("in the past"); invented facts; weaker logistics |
| **Layla** | 4.6 (18, Italy, new 2026 app); 4.9 claimed by Pilot | **2.7** (Pilot claim) | **4.0** (76) / 3.5 (49, CA) | | End-to-end draft, budget tweaking, human expert | Subscription and cancellation; no manual editing or collaboration |
| **Stippl** | **4.6** (414, Feb 2026) | 4.7 (Pilot claim) | **2.9** (Pilot claim) | PH 2.7 (3); combined 3.7 (~2K) | Visual route planner | "More of a source of frustration than a helpful tool" (PH); AI is paid PRO |
| **Holiwise** | not found | not found | **4.9** (~129–130) | | Human concierge, premium hotel matching | none surfaced (company replies to reviews; possible curation) |
| **Pilot** | n/a | n/a | **3.5** (11) | self-claim 4.7 | Free collaborative planner | Wanted a mobile app (since launched) |
| **iMean** | no native app (at review time) | n/a | **3.2** (thin) | | Cheap ($6.99/month), multi-city | Booking flow fragments; redirects to partners |
| **Axel** | n/a | n/a | **3.5** (~25–27) | | "Low-effort money back" | "Saved nothing after two months"; refund dispute |
| **Wonderplan** | n/a | n/a | 3.5 (1) | PH 5.0 (1) | Free, fast first draft, PDF export | Accuracy (general) |
| **Airial** | web-only / beta | n/a | n/a | PH 5.0 (2); Indexator 4.0 (11) | "Thought through from travelers' perspective" | Premium features locked; no mobile app |
| **GuideGeek** | no app (WhatsApp, IG, Messenger) | n/a | n/a | G2: too few | No download; instant answers | Loops ("kept on sharing… flight deals"); misreads ("Crete Freeze" as "Crete, Greece") |
| **Trip Planner AI** | not found (name collisions) | not found | not found | G2: 0 | Free ("Trippy" chatbot) | n/a |
| **Stardrift** | iOS app exists | n/a | n/a | "No user reviews yet" | Calendar-aware; live flight, hotel and Amtrak prices | n/a |
| **Lola** (consumer) | not found | not found | (lola.com reviews are a different B2B company) | | Free core; perks membership | n/a (launched Sep 2026) |
| **Kayak AI Mode / Ask AI** | n/a (in Kayak app) | n/a | n/a | G2 page exists | Conversational search on Kayak data | Rigid dates; bugs (Skift, Vice) |
| **Expedia Romie** | n/a | n/a | n/a | | Proactive weather and change alerts (claimed) | **PhocusWire describes Romie as "now-defunct"** |
| **Booking.com AI Trip Planner** | inside Booking app | inside Booking app | n/a | | Convenience | Ties you to Booking's own listings; English markets only |

**Pattern [inferred].** (1) Store ratings are high wherever there is a **structured, manual core** (Wanderlog, TripIt, Stippl). (2) **Trustpilot is where billing anger concentrates**, and every subscription AI planner scores lower there than in stores. (3) The **two best Trustpilot scores in the set, Holiwise 4.9 and Layla 4.0, both sell a human in the loop**. (4) Most AI-native tools are **too new or too small to have a meaningful review base**, which is itself a signal of low retained usage relative to press attention.

### 3.1 Layla (layla.ai)
- **Ratings:** Trustpilot TrustScore **4.0 from 76 reviews** (.com), **3.5 from 49** (Canada), **3.8 from 54–55** (Switzerland, Poland) **[verified – Trustpilot listing snippets]**. Google Play reportedly **2.7**, but only per a competitor's comparison page (Pilot) **[claimed, unverified]**. Gap-fill: a new iOS listing (id6758730467) shows **4.6 from 18 ratings** in the Italian store. Pilot claims 4.9 on the App Store **[claimed]**.
- **Price (gap-fill):** **$9.99/month or $49.99/year**, with a 7-day free trial **[verified – App Store listing snippet]**. A reviewer "almost didn't wanna do the subscription, because of some of the reviews on here before trying it" (Trustpilot snippet). Another Trustpilot complaint concerned a charge the reviewer could not cancel; the company replied.
- **Tests (gap-fill):** NYT (Aug 2025) described Layla as similar in design to Mindtrip, but "sometimes takes Layla a few prompts to unfurl the visuals". TechRadar tested Layla against TripAdvisor and Vacay; Layla was the only paid tool (verdict not retrieved). A third-party guide says Layla has "no drag-and-drop or manual editing, and there's no multi-user collaboration". Modelled revenue is ~$2.2–2.8M (2025) **[claimed – estimates]**.
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
- **Gap-fill:** App Store **4.9 from 29.9K–33.9K ratings**; Trustpilot **1.8** per Pilot's page, from ~45–48 reviews; Pro **$39.99/year** (one Play reviewer cites "$50/year") **[claimed]**. Free AI is capped at **5 messages per trip** (an aggregator summarising Reddit). On Reddit, the AI feature is reportedly *not* a main reason people choose Wanderlog; "map and collaboration features get mentioned more often". The usual r/travel combination is reportedly **Wanderlog to build the plan + TripIt to manage bookings** **[claimed – second-hand Reddit]**. Group paywall complaint: "if we pay for premium, the features are only available for ourselves, so anyone in the groups is still locked out of the features" (Trustpilot snippet).
- **Insight [inferred]:** Wanderlog's very high Play rating comes from its **manual collaborative itinerary + map** core, not AI. Users love a structured, editable, shareable, map-anchored plan, and that is the bar any AI planner is judged against.

### 3.3 Mindtrip
- Product Hunt: one user called it "hands down the most beautiful and useful travel app" (via search excerpt, https://www.producthunt.com/products/mindtrip). Another Product Hunt reviewer left a negative review, but I did not see the details.
- App Store reviewer: had not tried it on a vacation yet, only locally. This is typical of aspirational usage, where people try the tool more than they rely on it [verified snippet / inferred pattern].
- PhocusWire Hot 25 for 2025. The mobile app positioned as an "on-trip companion" and is built on OpenAI technology **[verified]**.
- Free to use, **monetised via booking partnerships** **[claimed – directory]**. This means recommendations may be steered toward bookable inventory, a sponsored-bias risk users increasingly ask about [inferred].
- Travel Awaits hands-on test: a four-night, arts-focused, crowd-avoiding Barcelona itinerary (May 2025). The search tool did not surface the verdict.
- **Gap-fill ratings:** App Store **~4.78 from 319 ratings** (Similarweb and appfelstrudel mirrors of Apple data); ToolDirectory 4.84 from 108; Product Hunt **4.3 from 6** **[claimed – mirrors]**. No Google Play rating found. Watch for a name collision with "MindTrip: AI Mind Training CBT", an unrelated app.
- **Gap-fill tests:** **Afar** (2025) called Mindtrip "the most sophisticated AI plan-and-book tool", yet its chatbot "incorrectly told me the dates for my trip were in the past". An Aug 2026 roundup ranked it best overall but found it "invented a wind speed". A Layla-run comparison (biased) says it "falls short in practical travel logistics". Reported **in-chat flight booking via Sabre + PayPal from 6 May 2026** **[claimed]**. Consumer use is free; revenue comes from booking and affiliate commissions, including a creator commission programme **[claimed]**.

### 3.4 ChatGPT and general LLMs used for travel
- **The Points Guy (2023, older):** "Each time I asked the AI to revert to the previous version, it drifted further from the original brief." This is **revision drift**: the plan state is not stable across edits. https://thepointsguy.com/news/chatgpt-ai-holiday-trip-planning-experience **[verified snippet; dated]**
- **Fox News tech (2025):** AI "invents answers" when it fills gaps; advises verifying "as you would with a travel agent." https://www.foxnews.com/tech/even-with-glitches-planning-your-next-trip-with-ai-is-making-me-rethink-travel
- **Fodor's forum, "Has anyone tried ChatGPT to plan a trip" (late 2025):** one poster said a follow-up answer "quoted my own words from Trip Advisor". Another still finds **Google Maps more useful for road trips**. https://www.fodors.com/community/travel-tips-and-trip-ideas/has-anyone-tried-chatgpt-to-plan-a-trip-1733260/page2
  - *Insight [inferred]:* the "hyperlocal knowledge" in LLMs is often regurgitated forum content. Power users notice, and it undermines perceived originality and authority. Attribution ("this tip comes from X, posted 2025") could become a trust feature.
- **Coleman Concierge roundup of Reddit discussions (secondary blog, anecdotal):** one Reddit traveller who planned trips across six countries estimated **AI gave wrong opening hours ~20% of the time**. Commenters cited travellers being sent to **closed or non-existent attractions**. **Over-ambitious Japan itineraries** rushed through Tokyo, Kyoto, Osaka and Hiroshima. Itineraries "look complete" but felt "strangely incomplete". https://www.colemanconcierge.com/ai-travel-planning-mistakes-real-travelers/ **[claimed – I could not load the underlying Reddit threads]**

*§3.5–§3.21 were added in the gap-fill pass. **Few reviews does not mean few problems**: many of these tools have almost no public review base.*

### 3.5 TripIt (incumbent organiser, the import benchmark)
- **Ratings:** Google Play **4.7 from 93.2K** (tracker, Feb 2026); iOS 4.6–4.8 depending on storefront; G2 (TripIt Pro) **4.6 from 44** **[claimed – mirrors]**. Pro costs ~**$48–49/year**.
- **Praise:** syncs with Concur; "alerted me to a canceled flight in the middle of the night" (G2 snippet). FlyerTalk: "TripIt is still the undisputed king for travel itineraries / organization for me."
- **Complaints:** the app rejects passwords "without explaining why" (Trustpilot 2026 snippet). Email import "no longer works reliably, itineraries get corrupted with incorrect dates and flight numbers" (retailcoupons, secondary, 2.2/5 from 16). On Pro value, the point tracker is "worthless considering most airlines/hotels/car rentals all have their own apps". Free-version bugs: "I had to double book some hotels" (G2).
- **Insight [inferred]:** even the import benchmark suffers **import regressions**, so a reliable, verifiable book-to-plan import is still an open differentiator.

### 3.6 Stippl
- App Store **4.6 from 414** (Feb 2026); a third party shows **3.7 from ~2K** across iOS and Android; Product Hunt **2.7 from 3**, with one reviewer: "in its current state, it's more of a source of frustration than a helpful tool". Pilot cites Trustpilot 2.9 and Play 4.7 **[claimed]**. The AI planner is a paid **PRO** feature.

### 3.7 Holiwise
- Trustpilot **4.9 from ~129–130 reviews** (jp and at storefront snippets) **[verified – listing snippet]**. Praise: "you speak with a real person, not ChatGPT"; it "did surface a few options I hadn't seen elsewhere"; AI matching premium hotels to "your style and mood". A concierge is available to premium members, and it handles bookings. No app-store ratings found. The company replies to reviews, so the sample may be curated **[claimed]**.

### 3.8 Pilot (pilotplans.com)
- Trustpilot **3.5 from 11** (one reviewer wanted a mobile app; Pilot replied it is now on iOS and Android). Pilot self-reports "40,000+ travelers across 183 countries… 4.7 stars", which is unverified. **Note:** Pilot publishes "Pilot vs X" comparison pages for Layla, Wanderlog, Stippl and TripIt, which are the source of several third-party ratings in this report. Treat those as competitor claims.

### 3.9 GuideGeek (Matador Network)
- Free; **no download**; runs on WhatsApp, Instagram and Messenger. Matador reports **7.7M questions answered in 15 months** (self-reported). G2 has too few reviews to score.
- Testers: answers are fast and grouped "by mood and distance" (hands-on blog); MSPoweruser praises its flexibility and links. Complaints: the bot "got stuck with Flight and kept on sharing details again and again on flight deals" (Chasing Whereabouts, affiliate blog). Fox News saw it confuse "Crete Freeze" with "Crete, Greece". Monetised through **destination-marketing white-label deals** (e.g. Aruba) **[claimed – press]**.

### 3.10 Wonderplan
- Free with no paid plans; PDF export. Trustpilot **3.5 from 1 review**; Product Hunt **5.0 from 1**. A 2026 tester ranked it "best for a fast, free first draft" but said AI still gets details wrong. A Dec 2025 review recommends checking pacing, geography, routes and hours manually **[claimed]**.

### 3.11 Trip Planner AI (tripplanner.ai)
- **No store, Trustpilot or G2 ratings found** (G2: 0 reviews). Heavy name collisions: Orbt's "AI Trip Planner" has 4.5 from 36 App Store reviews, and Trip.com's "Trip.Planner" is separate. MSPoweruser: free, with an in-app chatbot called "Trippy" **[claimed]**.

### 3.12 Airial
- Product Hunt **5.0 from 2**; Indexator **4.0 from 11** ("Amazing tool, thought through from travelers' perspective"). Directory scores of 4.3–4.6. Described as web-only or public beta with a mobile app "planned"; Insidea notes "Premium features locked behind paid tiers" **[claimed – directories]**. Distinct from "AiRial Flights".

### 3.13 iMean
- **$6.99/month**; called the "most affordable competent AI travel agent in 2026" (AI Agent Square). Booking is ambiguous: the "Book Now" button redirects to the airline or hotel partner with details pre-filled. A tutorial flags "booking flow fragmentation" and, at review time, no native mobile app. Trustpilot ~**3.2** (thin). Claims to monitor booked flights and hotels for changes **[claimed – directories]**.

### 3.14 Stardrift
- Free; reads Google Calendar and Outlook; claims live hotel, flight and **Amtrak** prices; remembers preferences; has an iOS app. **No user reviews found** ("No user reviews yet"). One directory files it as corporate travel software, which conflicts with the consumer positioning **[claimed]**.

### 3.15 Lola (Booking Holdings-backed consumer AI agent)
- Engadget: "Lola is a new AI travel agent backed by the company behind Booking.com", built by Kayak's founders. A **membership model launched Sep 2026**: free core, **Plus $5/month, VIP $25/month** (12-month commitment, ≈$300/year), positioned against premium credit cards. Its terms warn AI output "can be inaccurate or incomplete". **No hands-on review or store rating found.** Name collision: Lola.com (Boston business travel, $1,188/year) and its Trustpilot reviews are a different company **[claimed – secondary]**.

### 3.16 Axel (helloaxel.com)
- Monitors booked flights and hotels and claims refunds when prices drop; **books only after the user confirms**. Trustpilot **3.5 from ~25–27**. Praise: "low-effort money back". Complaints: a refund dispute (Japanese review) and "saved nothing after two months". The company claims ~**$327/year saved per user** (GWU tip sheet). The FAQ admits that "complex group trips, visas, and special-assistance itineraries" may be limited **[claimed]**.

### 3.17 Kayak AI Mode / Ask AI
- **AI Mode** launched 15 Oct 2025: ChatGPT plus Kayak data on desktop and mobile web. **Ask AI** followed in Apr 2026, designed from AI Mode usage data. Kayak's CPO: people shape vague trips through conversation, then "return to the results pages and filters they already know" to compare and commit **[claimed – secondary]**.
- **Tests:** Vice found the beta "needs polish" and too rigid with dates: it only looked for stays starting exactly on 10 December. **Skift (7 Mar 2024), "We Tested New AI Trip Planners From Despegar and Kayak: Fewer Errors, Still Buggy":** clicking the hotel option opened *flight* results; Despegar's Sofia froze after too many questions, forcing a restart. Verdict: users "will likely return frustratedly to the Google search bar" **[verified – Skift snippet]**.

### 3.18 Expedia Romie
- Released in alpha via EG Labs, May 2024, pitched as "travel agent, concierge and personal assistant, all in one". **PhocusWire now calls Romie "now-defunct"** **[claimed – single source, verify]**. Skift tested the Hotels.com chatbot built on it (May 2025; only described as qualitative). A Yahoo/AOL writer used it after booking a hotel (verdict not retrieved). A critique noted Expedia did not say what happens to the user data Romie can access.
- **Insight [inferred]:** the flagship OTA "AI travel agent" did not survive as a consumer product, which fits the 8% booking-comfort figure.

### 3.19 Booking.com AI Trip Planner
- Launched Jun 2023 in the app only, in English-speaking markets (US, UK, AU, NZ). No user-level ratings found. Booking's CTO (Skift, Mar 2025): users "may not rely on AI to plan a trip from start to finish" but increasingly consult it at some point. A third-party reviewer said it "probably ties you to their own accommodation listings" **[claimed]**.

### 3.20 Journalist and tester hands-on tests (2024–2026)

| Outlet (date) | What was tested | Verdict / specific errors | Label |
|---|---|---|---|
| **NYT** (Aug 2025, syndicated in Khaleej Times and Oman Observer) | Several AI planners including **Layla, Mindtrip** | Tools are "sort of good"; "varying levels of accuracy"; Layla "takes a few prompts to unfurl the visuals". Per-tool verdict not retrieved | [verified – syndicated snippet] |
| **NYT** (30 Apr 2026) | **Gemini** for flights, activities and routes | "A useful digital Swiss Army knife, but with notable gaps", e.g. it left underwear off a packing list. Strength: direct access to Google Flights and Hotels | [claimed – via summaries] |
| **NYT** (2024, Ceylan Yeğinsu) | AI planners for Norway | (verdict not retrieved) | [claimed – FlowingData] |
| **WSJ** (Dawn Gilbertson, 13 Apr 2026) | AI bot as travel agent, which chose Saltburn-by-the-Sea, England | Resulting trip covered as video; details not retrieved | [claimed – listing] |
| **WSJ** (Gilbertson) | **Gemini**, two-night London escape | "Some hits and big misses" | [claimed – Newser] |
| **WSJ** | **Gemini vs ChatGPT**, Boston | Fast outline, but **asking the same question twice gave different answers**; a human still makes the booking | [claimed – reprint] |
| **WSJ** | Airline and OTA chatbots | AI "still makes mistakes and can't yet automate the whole process" | [claimed – reprint] |
| **Afar** (2025) | 4 apps ("3 that actually worked") incl. **Mindtrip**, Gemini | Mindtrip "most sophisticated AI plan-and-book tool", but said the trip dates "were in the past"; tools' information "often dated", "prone to hallucinating". A companion piece lists "4 common mistakes" and cites chatbots being error-free only ~10% of the time | [verified – Afar snippet] |
| **Skift** (Mar 2024) | **Kayak, Despegar** | "Fewer Errors, Still Buggy" (see §3.17) | [verified – snippet] |
| **TechRadar** ("AI planned it" series) | **TripAdvisor, Vacay, Layla** (AI chose destination and itinerary) | Verdict not retrieved | [claimed] |
| **Vice** | Kayak AI beta | "Needs polish", rigid dates | [claimed] |
| **InsureMyTrip** | ChatGPT, Gemini | "Looked polished, but a closer look revealed many small and large errors" | [claimed – insurer blog] |
| **Outside** | Free AI planners | "None completely nailed" the trip | [claimed] |
| **Kiplinger** | ChatGPT | Useful start, but it may draw on "a Reddit thread about a cave that may no longer exist" | [claimed] |
| **SEO Travel** (agency study, 2024; GPT-3.5; 2-day plans in 10 cities) | ChatGPT | **90%** had at least one error: an 08:00 breakfast at a Tokyo café that opens at 12:00; the Pergamon Museum, closed until 2026; ~**1 in 4** needed backtracking or detours; ~1 in 4 included a closed venue; some places did not exist | [verified – Travolution, TravelNews] |
| **Greetwell survey** (2026) | AI-using travellers | **1 in 6** had been recommended a place, tour or activity that did not exist | [claimed – secondary] |

**Not found:** hands-on tests from The Verge, Wired, CNET, Condé Nast Traveler, Fast Company, Forbes, Tom's Guide, Lifehacker or The Points Guy (2025–26). There are 16 rows above, from **11 distinct publishers or studies**. **Every test whose verdict was retrieved (13 of 16) reports factual errors, bugs or inconsistency. None found an AI planner reliable enough to use without checking.**

**Real-world hallucination incidents (2025–26)** **[claimed – secondary press]:**
- **Peru, Oct 2025:** two tourists paid ~US$160 (reports vary) to hike to a non-existent "Sacred Canyon of Humantay" from an AI screenshot. Local guide Miguel Angel Gongora Meza intercepted them. Coverage cites a 2024 survey: **37%** of AI trip planners said the tools did not give enough information, and **33%** said recommendations contained false information (original source not found).
- **Tasmania, Jan–Feb 2026:** an AI-generated travel website sent tourists to non-existent hot springs (Euronews; LADbible).
- **LIVE JAPAN reader survey** (LINE; fail stories from Taiwan respondents): route plans that ignore distances and transfer times ("zigzagging"); outdated transit information; wrong ticket prices; closed businesses; shops that no longer exist.

### 3.21 Forums, Reddit (second-hand) and Hacker News

| Source | Theme | Evidence | Label |
|---|---|---|---|
| Reddit (via News On Japan) | Over-ambitious Japan plans | A user posted a ChatGPT Japan itinerary "and the replies tore it apart" | [claimed – second-hand Reddit] |
| early-retirement.org "Japan Itinerary by AI" | Too many cities | Asks if it is "too ambitious ie too many cities?"; reply: see more in fewer cities | [verified snippet] |
| ivisitkorea (blog) | Over-packing | Seoul AI plan with "as many as 9 stops within a single day" | [claimed] |
| tabiji (blog) | Generic | "every AI travel planner I've tried gives me the same TripAdvisor top 10" | [claimed – vendor blog] |
| Rick Steves forum | Closures, routing | Asks if followers hit "things being closed or being sent zig-zagging across town" | [verified snippet] |
| Fodor's (late 2025) | Useful draft | Slovenia motorbike itinerary was "a perfect way to start planning", tweaked along the way; another poster prefers forums and Reddit for local knowledge | [verified snippet] |
| Australian Frequent Flyer forum | Mixed | Saves hours of research, but "good for finding tourist spots but doesn't do a great job planning the whole itinerary" | [verified snippet] |
| FlyerTalk "Better than TripIt?" | Organiser loyalty | TripIt "still the undisputed king" | [verified snippet] |
| r/travel (via aggregator) | Tool pairing | Wanderlog to plan + TripIt for bookings; AI not the reason to choose Wanderlog | [claimed – second-hand Reddit] |
| Business Insider (2 first-person pieces) | Time saved | ChatGPT "saved me hours of research", but the writer still checked local Reddit threads. A digital-nomad coach saved "two to five hours" on a 2-week Europe trip: "inspiration rather than a finished plan" | [verified snippet] |
| Coleman Concierge (first pass) | Wrong hours ~20%; closed or non-existent places | see §3.4 | [claimed – second-hand Reddit] |
| Hacker News | Builder interest, little user signal | Only one "Show HN" (Planitly, May 2025) and one "Ask HN" (a site to build an itinerary from destination cities) surfaced, with no comment text | [verified – listing] |

**Theme counts across §3.4, §3.20 and §3.21** (independent sources; directional only):
- Factual errors (wrong hours, closures, non-existent places, wrong dates): **~16**
- Over-packed or geographically unrealistic plans: **~7**
- "Good first draft, must verify": **~9**
- Generic or canonical picks: **~4**
- Bugs and loops (freezes, wrong tab, repeated answers): **~5**
- Inconsistent answers across runs: **1** (WSJ)
- Explicit praise for time saved: **~5**

---

## 4. Do users confirm the four known problems?

| Known problem | User-side evidence | Verdict |
|---|---|---|
| **(1) Generic, cliché recommendations; no hyperlocal knowledge** | Itineraries "look complete but feel strangely incomplete" (Coleman/Reddit). Over-packed "greatest hits" Japan routes (Coleman). Fodor's poster saw their own TripAdvisor words regurgitated. Skift Research's *The Disappearing Destination* frames AI as a filter that narrows discovery to well-known places [claimed]. Wanderlog users treat AI as "a starting draft". *Gap-fill:* "the same TripAdvisor top 10" (tabiji); "good for finding tourist spots but doesn't do a great job planning the whole itinerary" (AFF forum); AARP: older users don't let AI "determine destinations". | **Confirmed, but needs refining.** The complaint is less "it's generic" and more "**it's the same canon everyone gets, stitched together without judgement**": no sense of *why* a place matters to *me*, no seasonal or timing nuance, no trade-offs. |
| **(2) Poor booking interoperability** | Layla links out to partners [claimed]. Wanderlog auto-import less reliable than TripIt [claimed]. 57% want cross-brand assistants (Accenture). LLM traffic <1% of Booking room nights. Adobe shows AI-referred visitors convert worse (May 2026). *Gap-fill:* iMean's "Book Now" redirects to partners ("booking flow fragmentation"). Kayak's CPO says users go back to the results pages to commit. Skift found Ask Kayak's hotel button opening *flight* results. Romie is reportedly defunct. TripIt's import "corrupts dates and flight numbers" (secondary). The Booking.com planner is tied to its own listings. | **Confirmed, but users frame it as a handoff problem.** They don't want the AI to book everything. They want the **plan-to-book transition** and **book-to-plan import** to be lossless (prices, dates and confirmations flowing both ways). |
| **(3) Stale data / hallucinations** | Wrong opening hours ~20% (anecdotal). Closed or non-existent attractions. "Invents answers" (Fox). Booking.com: 6% fully trust. YouGov speculates accuracy concerns drive falling youth comfort. *Gap-fill:* SEO Travel: 90% of itineraries had at least one error. Afar: Mindtrip said the dates "were in the past"; chatbots error-free ~10% of the time. Greetwell: 1 in 6 were sent to a non-existent place. Peru "Sacred Canyon" and Tasmania hot-springs incidents. Surveys report 33% got false information. JTB (Japan) names accuracy as the main concern. WSJ: different answers to the same question. | **Strongly confirmed.** This is the most cited quality failure, and it compounds: one bad fact makes users re-verify *everything*, which erases the time saved. |
| **(4) No accountability** | Users phrase it as "I fact-check", "I want human oversight" (Booking.com), "I'd book with a trusted brand" (Expedia: 68%), and they praise Layla's human expert. Only 3–8% would transact through AI. *Gap-fill:* the top Trustpilot score in the set goes to Holiwise (4.9), praised for "a real person, not ChatGPT". 74% prefer to finalise bookings themselves (McKinsey/Skift 2026). Accenture: 7–9% would let AI purchase. Lola's terms disclaim accuracy. Axel books only after user confirmation. | **Confirmed, but implicit.** Users rarely say "accountability". They show it by refusing to pay through AI and by preferring brands with customer service and refund rails. |

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
| 13 | **Non-determinism**: the same question gives different answers, so the plan can't be trusted to be reproducible | WSJ Gemini/ChatGPT Boston test | [claimed – reprint; n=1] (gap-fill) |
| 14 | **Chatbot loops and freezes** that force a restart | Despegar Sofia froze (Skift); GuideGeek looped on flight deals | [verified snippet / claimed] (gap-fill) |
| 15 | **Group paywalls**: premium AI unlocks for the payer only, not co-planners | Wanderlog Trustpilot | [verified snippet; n=1] (gap-fill) |
| 16 | **Product abandonment risk**: big-brand AI assistants are launched, then dropped | Expedia Romie "now-defunct" (PhocusWire) | [claimed] (gap-fill) |

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

The first pass was mostly **[inferred]**. The gap-fill pass found survey evidence for most segments; the "needs" column remains partly inferred. Several key sources are **vendor-sponsored** (Booking.com, Matador/GuideGeek), so treat their adoption figures as upper bounds.

| Segment | Evidence (gap-fill additions in bold) | Why underserved | Evidence strength |
|---|---|---|---|
| **Women and solo female travellers** | YouGov: 44% of women not comfortable vs 36% of men. **Global Rescue Fall 2025: women *use* AI slightly more (24% vs 22% of men), mostly for itineraries (74%) and research (68%).** **JourneyWoman: 93% of women consider safety when planning; AI is "creating new concerns about safety among women".** **21% of solo female travellers feared for their safety on a trip in the past year; 59% (separate n=5,000) say safety is a barrier to solo travel** | Women **use AI but trust it less**, a quality gap rather than an adoption gap. No tool found that grounds night-time, neighbourhood or transport safety in verified sources | [verified] use & comfort data; [claimed] safety surveys; no AI-safety-feature evidence |
| **Older travellers (50+/55+)** | YouGov 55+ comfort 16%→20%. **AARP 2026 (n=1,189, 50+): AI planning use doubled 8%→16%; 76% not likely or unsure; uses are deals, comparisons and organising, "not to determine destinations". AARP 2025: privacy was the main barrier for 40% of non-users. Global Rescue: under-35s more than twice as likely as over-55s to use AI** | Fastest *relative* growth from a low base. They want **organising and deal help with privacy assurances**, not AI-chosen destinations | [verified] |
| **Gen Z / young Millennials** | Heaviest users (Deloitte 30–31%) but comfort falling sharply (YouGov), i.e. churn risk. **Marriott LatAm: Gen Z 64% use AI to organise trips. JTB Japan: women in their 20s 89.3% of weekly GenAI users have used it for travel** | Budget-sensitive; social-native discovery (TikTok) | [verified] |
| **Group travel** | **Experian (Jun 2025, n>700 US): unexpected costs and fair splitting are the top stresses; 48% of Millennials, 43% of Gen X and 39% of Boomers worry about splitting fairly; only ~1/4 of groups set a budget in advance; 40% overspent by 11–25%. 1 in 5 ended a friendship over a money dispute (GOBankingRates/Experian). 1 in 3 fought on a group vacation (vacation-rental survey, n=2,000). CIT Bank "Peace Tax": 82% willing to overpay to keep the peace (secondary). Klook (n=2,725, 10 markets): for designated planners, budgets are the #1 challenge (57.6%). Wanderlog Premium AI is locked to the payer, not the group (Trustpilot). Axel's FAQ: group trips "may be limited"** | Pain centres on **money and decisions**, not itinerary text. AI planners are single-user chats; none surfaced with voting, budget-setting or settlement | [verified – Experian]; others [claimed] |
| **Families with kids** | **GuideGeek/Matador: families with kids 69% more likely to have used AI for a trip (vendor). Family Travel Association 2025 (n≈1,600): 81% plan with Google or Bing; 48% worry about data security when booking online; top challenges are school-break timing (51%), vacation time (47%) and finding something everyone enjoys (40%)** | Families are early adopters, but their hardest problems (**calendar constraints, multi-age consensus, privacy**) aren't what AI planners optimise. Over-packed itineraries hit hardest here [inferred] | [claimed – vendor + FTA secondary] |
| **Accessibility / disabled travellers** | **Matador/GuideGeek (Jul 2024): 82.5% who used AI to plan for someone with a disability were satisfied; 89% would use it again (vendor survey). WheelchairTravel.org: AI is trained on outdated accessibility information, e.g. a city page listing wheelchair taxis that had not run for about a decade; it expects AI's impact to be "negative before positive". Fable: travel websites have the most accessibility problems of any industry it tested** | Satisfaction is high when it works, but the **underlying data is stale**, and a hallucinated "accessible" is harmful. Verified, dated accessibility attributes are a clear gap | [claimed – vendor] + [verified – advocacy]; high severity |
| **Dietary restrictions / allergies** | **No traveller-specific data found.** A Polish study of ChatGPT allergy meal plans: the expert warns of a "risk that LLMs give dangerous nutrition advice" and that the model can't account for severity. Allergen-safety writer: a chatbot "can be fluently wrong". The AllerGuide travel app tells users to verify with restaurant staff | Health risk. AI is best used to *prepare* (allergy cards, phrasing), not to *choose* restaurants | [claimed]; evidence gap |
| **Multi-country / overland / rail** | AI produces over-ambitious multi-city plans (Japan). **Forum: "too many cities?" (early-retirement.org). LIVE JAPAN: route plans ignore distances and transfer times. Stardrift is the only tool found claiming live Amtrak data** | Routing feasibility, border rules, rail passes, transit times | [claimed] |
| **Business + leisure** | 44% of business travellers use AI to plan (Booking.com). TripIt's Concur sync is praised | Corporate policy, expensing and loyalty integration are absent from AI planners | [claimed] |
| **India** | **Agoda 2026: 33% already use AI for travel planning, 68% likely next trip, 88% trust or are neutral. Amadeus: 17%→26% among tech-savvy travellers. Kaspersky: under 1/3 trust AI to plan, but 96% of those who do are satisfied. Expedia/YouGov sampled India but no India split surfaced** | High intent and trust; few India-specific tools surfaced in this research | [verified – press releases] |
| **Japan** | **JTB: 77.8% of weekly GenAI users have used it for travel; GenAI as a travel-info source 9.7%→28.8% in a year. Meiji Yasuda (Jun 2026): 61.2% with summer plans will use GenAI. Yomiuri Advertising: travel is the #1 AI-use category (35.3%). But Adyen: only 11% use AI for travel search or booking vs 34% globally. Accuracy is the main concern (JTB)** | Fast-growing usage, mainly in general chatbots. Low use in booking flows | [verified – Travel Voice] |
| **Latin America** | **Marriott: 54% of frequent travellers in 7 markets use AI to organise trips (up from 43%). Booking.com: LATAM 98% excited about AI, ~7 in 10 use it for planning** | Highest enthusiasm, yet tools are English- and US-centric; no LatAm tool reviews surfaced except Despegar's buggy Sofia (Skift 2024) | [claimed – sponsor surveys] |
| **APAC (general)** | Booking.com: 93% want AI in plans, 8% full trust, 64% use AI to plan | Most tools are English- and US-centric | [claimed] |
| **LGBTQ+ travellers** | **Booking.com *Travel Proud 2026* (n≈13,300, 19 countries): 66% used AI to plan a trip in the past year; 43% of those trust AI for objective, non-judgmental identity-related advice; trans travellers 76%, top reason (43%) to quickly check safety or legal rights; only 31% are out when travelling; 40% would hide their identity to visit a dream destination. APAC 73%, Thailand 89%, Canada 46% (secondary). Matador: 62.1% open to AI for summer travel** | **The heaviest-using segment found**, using AI for exactly the high-stakes job (legal and safety status) where a hallucination is dangerous. No tool found offering sourced, dated LGBTQ+ legal and safety information | [verified – Booking.com press release; sponsor] |

---

## 7. Personalisation reality check

What the evidence shows:
- **Users expect a draft, not a plan.** Wanderlog's power users treat AI "as a starting draft". Booking.com respondents want AI to help, not decide. The current *perceived* ceiling of AI personalisation is "a decent first draft to edit" **[claimed/verified]**.
- **Constraints get ignored.** Pace is the clearest example: over-packed, multi-city sprints. Budget gets better marks; Layla praise specifically mentions tweaking to budget, which suggests budget is the one constraint tools handle reasonably **[claimed]**.
- **Editing is the failure point.** Revision drift (TPG) and chat-as-plan architectures mean users lose earlier versions and can't make surgical edits ("swap only Tuesday afternoon") **[verified, dated + inferred]**.
- **"It doesn't know me."** No evidence in the first pass that any tool learns from past trips, saved places or social saves. Personalisation is limited to what users type in a prompt. That makes every itinerary converge on the canon **[inferred]**. *Gap-fill:* only marketing claims of memory surfaced. Stardrift says it "remembers these details and applies them to future searches" and reads your calendar; Romie was pitched as saving preferences before reportedly being discontinued. **No user review was found praising a tool for knowing them**, while "same TripAdvisor top 10" complaints persist **[claimed]**.
- **Reproducibility (gap-fill).** WSJ found the same question gives different answers. To a user, personalisation that changes on every run looks random, not personal **[claimed – n=1]**.
- **The human-concierge premium (gap-fill).** The two best Trustpilot scores in the set (Holiwise 4.9, Layla 4.0) both include a human: "you speak with a real person, not ChatGPT". Users experience *human-checked* output as the most personal **[verified snippet]**.
- **Segment-level personalisation is where usage is highest and stakes are biggest (gap-fill).** LGBTQ+ (66%; trans 76%) and accessibility users rely on AI for identity- or need-specific facts. The data behind those facts is stale, per WheelchairTravel.org **[verified/claimed]**.
- **Ads and sponsored bias.** No direct user quote found in either pass. Gap-fill: a reviewer said Booking.com's planner "probably ties you to their own accommodation listings"; Mindtrip runs a creator commission programme; several "reviews" in this space are written by competitors (Pilot, Layla, Stippl blogs) **[claimed]**. The structural risk is clear (commission-funded free planners; OTA assistants showing only their own inventory), and Accenture's 57% wanting cross-brand assistants hints at demand for neutrality **[inferred]**.

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
| **Paying extra for AI help** (gap-fill) | 50% say AI help should come at no extra cost; 4% expect it to justify a premium (Amadeus US) |
| **Handing over personal data** (gap-fill) | 40% of 50+ non-users cite privacy (AARP 2025); 48% of family travellers worry about data security when booking online (FTA 2025); critique of Romie's unclear data use |
| **AI choosing the destination** (gap-fill) | AARP: older travellers use AI to organise and find deals, "not to determine destinations" |

## 10. Delight features users praise

| Delight | Evidence |
|---|---|
| End-to-end draft in minutes, adjusted to budget | Layla Trustpilot: "laid it all out end to end and helped tweak it to my budget" |
| A human expert behind the AI | Layla Trustpilot: "the human aspect of process at the end" |
| Beautiful, map-first, visual UI | Mindtrip Product Hunt: "hands down the most beautiful and useful travel app" |
| Collaborative, editable itineraries + map (manual core) | Wanderlog's 4.7 Play rating [claimed] |
| Reliable confirmation import | TripIt benchmark (vs Wanderlog) [claimed] |
| "GenAI improves trip planning" overall | 78% (Phocuswright) |
| **Hours saved on research** (gap-fill) | Business Insider: ChatGPT "saved me hours of research"; a digital-nomad coach saved "two to five hours" on a 2-week Europe trip; AFF forum: "skip hours of research" |
| **A human in the loop** (gap-fill) | Holiwise Trustpilot 4.9 (~130): "you speak with a real person, not ChatGPT"; Layla's human expert |
| **No-download, chat-native access** (gap-fill) | GuideGeek on WhatsApp, Instagram and Messenger; 7.7M questions (self-reported) |
| **Proactive disruption alerts** (gap-fill) | TripIt: "alerted me to a canceled flight in the middle of the night" (G2) |
| **Money back without effort** (gap-fill) | Axel: "low-effort money back" (Trustpilot); Flighty's paid alerts sustain an estimated ~$400–500K/month |
| **Surfacing options not found elsewhere** (gap-fill) | Holiwise: "did surface a few options I hadn't seen elsewhere" |
| **Linked, bookable itinerary** (gap-fill) | Mindtrip "itineraries include links to all the sites, restaurants, and hotels"; Afar: "most sophisticated AI plan-and-book tool" |
| **Calendar and live-price awareness** (gap-fill, claimed only) | Stardrift reads your calendar and pulls live flight, hotel and Amtrak prices (vendor claim, no reviews) |

---

## 11. Ranked pain points (frequency × severity)

**Evidence count** is the number of independent sources in this report supporting the point (surveys + reviews + articles + tests). The gap-fill pass roughly tripled the counts. Counts are shown as *first pass → after gap-fill*. Still directional: many sources are secondary or vendor-run.

| Rank | Pain point | Frequency | Severity | Evidence count | Maps to brief |
|---|---|---|---|---|---|
| 1 | **Hallucinated or stale facts** (hours, closures, non-existent places, wrong dates, entry rules), forcing users to re-verify everything | High | High (wasted trips, safety, money) | 6 → **~18** (+ SEO Travel 90%, Afar ×2, Greetwell 1-in-6, Peru incident, Tasmania incident, 33% false-info survey, LIVE JAPAN, InsureMyTrip, Outside, Kiplinger, Mindtrip "wind speed", GuideGeek "Crete Freeze", JTB accuracy concern) | #3 |
| 2 | **Trust and accountability gap at the transaction**: won't pay through AI, wants a brand or human behind it | Very high (survey majority) | High (blocks monetisation) | 7 → **~12** (+ Booking Holdings CFO confirmed, McKinsey/Skift 74%, Accenture 7–9%, Kayak CPO "return to results pages", Holiwise human-concierge praise) | #4 |
| 3 | **Generic, same-y, canon-only itineraries** that lack judgement and local nuance | High | Medium | 5 → **~8** (+ tabiji "same TripAdvisor top 10", AFF forum, AARP "not to determine destinations") | #1 |
| 4 | **Over-packed, geographically unrealistic plans** that ignore pace | Medium–High | Medium | 2 → **~7** (+ SEO Travel 1-in-4 backtracking, early-retirement.org "too many cities", News On Japan Reddit "tore it apart", ivisitkorea 9 stops/day, LIVE JAPAN zigzagging, Rick Steves forum) | new |
| 5 | **Subscription and billing dark patterns** in AI planner apps | Medium (dominant on Trustpilot) | Medium–High (brand-killing) | 3 → **~7** (+ Layla subscription hesitancy and uncancellable charge, Wanderlog Trustpilot 1.8, Stippl/Airial AI behind PRO, Axel refund dispute) | new |
| 6 | **Broken plan-to-book and book-to-plan handoff** (link-outs, unreliable import, re-entering data) | Medium | Medium | 4 → **~9** (+ iMean redirect "fragmentation", Skift Kayak wrong-tab bug, TripIt import corruption, Booking.com own-inventory lock-in, Romie defunct) | #2 |
| 7 | **Fragile editing, revision drift, inconsistent answers, plan lives in chat** | Medium | Medium | 1 → **~5** (+ WSJ non-determinism, Despegar freeze/restart, GuideGeek loop, Layla "no manual editing or collaboration") | new |
| 8 | **Trust erosion after use** (young-user comfort decline) | Emerging | High (retention) | 1 → **~3** (+ tiny review bases for AI-native apps vs organisers; Kaspersky India: under 1/3 trust) | new |
| 9 | **Sponsored or commission bias and single-brand inventory** | Unknown (still no direct user quote) | Medium | 2 → **~4** (+ Booking.com planner "ties you to own listings", competitor-written reviews flooding search) | new |
| 10 | **Segment blind spots**: groups, accessibility, diet, safety for women and LGBTQ+ | Medium (now evidenced) | High for affected users | 1 → **~12** (+ Experian, Klook, CIT, FTA, Matador accessibility, WheelchairTravel.org, Fable, Booking Travel Proud, Global Rescue women, JourneyWoman, allergy study) | new |
| 11 | **Low willingness to pay for planning** (a business-model pain, not a user complaint) | High | High for startups | **new: ~5** (Amadeus 50% free / 4% premium, Accenture 9%, RevenueCat ~4% install-to-trial, Layla revenue estimates) | new |

---

## 12. Top gaps and opportunities (user perspective)

1. **"Verified itinerary" as the product.** Every place, hour, price and entry rule carries a source and a "checked on" timestamp, with automatic re-verification before departure and on the day. This is the most direct answer to pain #1, and users already do it manually.
2. **Climb the trust ladder with approval-gated, accountable booking.** Start with restaurants and tours, where 38% trust AI, before hotels and flights. Always require explicit approval. Book through brands users trust, or offer clear guarantees and a human escalation path. Don't sell autonomy, which only 2% want. Sell **"I'll handle the tedious parts, you approve, and we're on the hook if it breaks."**
3. **A persistent, structured, collaborative plan object, not a chat log.** Surgical edits, version history, group voting and cost splitting, two-way sync with Google Maps lists, Sheets and email confirmations, reliable TripIt-grade import. Beat Wanderlog on its own turf, then add AI.
4. **Judgement over listings.** Pace-aware, geography-realistic plans with explicit trade-offs ("skip Hiroshima or you'll spend 9 of 14 days on trains"), personal rationale ("because you saved X"), and attributed, recent human local knowledge rather than unattributed regurgitation.
5. **Honest business model and safety-first segments.** No trial traps, a disclosed neutral ranking, and cross-brand inventory, which 57% want. Lead with segments where generic AI is weakest and stakes are highest: solo women's safety, accessibility, dietary needs and multi-country overland. That also reaches the sceptical 44% of women and the 23% who avoid AI.
6. **(Gap-fill) Monetise certainty, not intelligence.** Planning is expected to be free (Amadeus: 50%), and paid planners cluster at $40–60 a year. Travellers pay for **protection and recovery**: Hopper-style attach on about half of bookings, Flighty's paid alerts, Axel's price-drop refunds, Holiwise and Layla's human concierge. A defensible paid tier bundles **re-verification + disruption handling + price-drop recovery + a human escalation path**.
7. **(Gap-fill) Win the group, not the individual.** Group pain is money and decisions: fair splitting worries 39–48% across generations, only ~1/4 of groups set a budget, and 1 in 5 ended a friendship over money. No AI planner surfaced with budget-setting, voting or settlement, and Wanderlog locks premium AI to the payer. A shared plan where every member gets the AI features is an open, viral wedge [inferred from §6 data].
8. **(Gap-fill) Sourced safety and legal facts for identity-driven segments.** 66% of LGBTQ+ travellers (76% of trans travellers) use AI, with checking legal and safety status the top reason. Accessibility data is stale. These are segments where a **cited, dated, human-reviewed** fact layer is both most needed and most defensible.

---

## 13. Follow-up research still needed (after the gap-fill pass)

The gap-fill pass used 58 of its 60-search budget. The items below are what remains. Most need **network access to reddit.com, apps.apple.com, play.google.com and trustpilot.com**, or paid reports.

- **Direct Reddit thread text** (r/travel, r/solotravel, r/JapanTravel, r/digitalnomad, r/ChatGPT, r/europe). The search tool doesn't index Reddit well and reddit.com is blocked, so all Reddit evidence here is second-hand. A proper theme count needs ~50–100 threads read directly.
- **Hacker News**: only one Show HN (Planitly) and one Ask HN surfaced, with no comment text. Try Algolia HN search (hn.algolia.com) if allowed.
- **Official store pages** to confirm mirror ratings (Wanderlog, TripIt, Mindtrip, Stippl, Layla), plus **Google Play ratings not found** for Mindtrip, Layla (only Pilot's 2.7 claim), Holiwise, Lola and iMean.
- **Store complaint mining at scale** (e.g. 1-star review text from AppFollow or Sensor Tower) to quantify themes per tool. This pass has ratings, but few review texts for AI-native apps.
- **Journalist tests not found:** The Verge, Wired, CNET, Condé Nast Traveler, Fast Company, Forbes, Tom's Guide, Lifehacker, The Points Guy (2025–26). **Per-tool verdicts not retrieved** for the NYT (Aug 2025), Afar, TechRadar and WSJ Saltburn pieces.
- **Confirm Expedia Romie's status** ("now-defunct" per a single PhocusWire mention) and **Lola's official pricing**; reconcile **Axel's pricing**.
- **Expedia/YouGov:** resolve whether the 8% means *booking comfort* or *planning reliance*, and get the India split from the full report.
- **Skift *State of Travel 2025*:** exact sample and wording behind the 2% autonomy figure (US travellers vs "young leisure travelers").
- **Phocuswright *The AI Surge* full report** (paywalled): booking-intent figures by segment.
- **Dietary and allergy traveller data**: no survey found; possible primary research opportunity.
- **Conversion data for AI planners specifically** (free to paid). Only estimates (Layla revenue, Flighty revenue) and category benchmarks (RevenueCat) were found.

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

**Gap-fill pass (2026-11-17): primary-source checks and new demand data**
- https://www.phocuswright.com/Travel-Research/Consumer-Trends/The-AI-Surge-Travels-Fastest-Behavioral-Shift-in-a-Decade
- https://www.phocuswright.com/Travel-Research/Research-Updates/2026/The-fastest-shift-in-travel-behavior-just-became-the-default
- https://www.phocuswire.com/ai-surge-us-behavioral-shift-travel-phocuswright-research-2026
- https://www.phocuswire.com/news/finance/booking-holdings-q2-2026-earnings
- https://www.marketbeat.com/instant-alerts/booking-q2-earnings-call-highlights-2026-08-04/
- https://www.pymnts.com/dashboard-post/earnings/2026/ai-can-plan-the-trip-but-booking-holdings-wants-the-transaction/
- https://s25.q4cdn.com/383369491/files/doc_financials/2026/q2/BKNG-Q2-2026-Earnings-Call-Transcript.pdf (not loaded)
- https://www.travolution.com/news/technology/accenture-research-finds-gen-ai-becoming-top-source-for-travel-discovery/
- https://globetrender.com/2025/06/09/gen-ai-overtakes-social-media-top-travel-discovery-channel/
- https://www.mckinsey.com/industries/travel/our-insights/remapping-travel-with-agentic-ai
- https://www.businesswire.com/news/home/20260414532485/en/Expedia-Group-Reveals-The-AI-Trust-Gap-Travelers-Embrace-AI-for-Planning-but-Rely-on-Trusted-Brands-to-Book
- https://deeparrival.com/news/travel-ai-trust-surveys-conflict-2026/
- https://amadeus.com/en/newsroom/press-releases/tailored-horizons-ai-travel-planning-trust
- https://www.travelagentcentral.com/your-business/new-amadeus-study-more-us-travelers-use-ai-travel-planning-bookings-trust-must-grow
- https://www.phocuswire.com/travelers-would-pay-ai-assistant-provide-in-trip-information
- https://www.globalrescue.com/common/blog/detail/international-travelers-and-women-lead-in-using-ai-for-trip-planning/
- https://lodgingmagazine.com/global-rescue-survey-international-travelers-lead-in-using-ai-for-trip-planning/
- https://www.aarp.org/press/releases/2026-03-10-aarp-travel-trends-2026.html
- https://www.aarp.org/press/releases/2025-3-6-older-americans-are-traveling-more-than-ever-says-2025-aarp-study.html

**Gap-fill: tool ratings and reviews (mostly mirrors, directories or competitor pages)**
- https://www.similarweb.com/app/apple/6503107567 ; https://appfelstrudel.com/id/6503107567/mindtrip-ai-travel-companion.html ; https://www.producthunt.com/products/mindtrip/reviews
- https://monkeytravel.app/blog/mindtrip-review-2026 ; https://www.datastudios.org/post/mindtrip-ai-travel-planning-in-chat-booking-and-pricing
- https://apps.apple.com/app/id6758730467 ; https://apps.apple.com/it/app/id6758730467 ; https://www.trustpilot.com/review/layla.ai?page=3
- https://getlatka.com/companies/layla.ai ; https://prospeo.io/c/layla-ai-trip-planner-revenue
- https://apps.appfollow.io/ios/wanderlog-travel-planner/1476732439?country=us ; https://www.pilotplans.com/compare/wanderlog-alternative-feature-comparison ; https://trustpilot.com/review/wanderlog.com ; https://www.aitooldiscovery.com/guides/wanderlog-reddit
- https://apppricinglab.com/app/google_play/com.tripit ; https://www.g2.com/products/tripit/reviews ; https://uk.trustpilot.com/review/www.tripit.com ; https://www.flyertalk.com/forum/travel-tools/2079146-better-than-tripit-printerfriendly.html
- https://apps.appfollow.io/ios/stippl-travel-planner/6443617088?country=us ; https://www.producthunt.com/products/stippl/reviews ; https://www.pilotplans.com/compare/stippl-alternative-feature-comparison
- https://jp.trustpilot.com/review/holiwise.com?page=6 ; https://at.trustpilot.com/review/holiwise.com
- https://ca.trustpilot.com/review/pilotplans.com ; https://www.pilotplans.com/pilot-reviews
- https://chasingwhereabouts.com/blog/guidegeek-review ; https://mspoweruser.com/guide-geek-ai-review ; https://www.g2.com/products/guidegeek/reviews ; https://prnewswire.com/news-releases/guidegeek-an-openai-powered-travel-assistant-from-matador-network-is-revolutionizing-vacation-planning-301799861.html
- https://ca.trustpilot.com/review/wonderplan.ai ; https://www.producthunt.com/products/wonderplan/reviews ; https://iweaver.ai/blog/wonderplan-ai-review-best-ai-travel-planner-alternative
- https://www.g2.com/products/trip-planner-ai/reviews ; https://mspoweruser.com/trip-planner-ai-review
- https://www.producthunt.com/products/airial-travel-2/reviews ; https://dev.indexator.ai/companies/airial-travel ; https://insidea.com/spotlight/listing/airial-travel/
- https://aiagentsquare.com/agents/imean-ai ; https://uk.trustpilot.com/review/imean.ai ; https://aiindigo.com/tutorials/getting-started-with-imean-ai-automate-complex-itineraries
- https://www.producthunt.com/products/stardrift ; https://www.g2.com/products/stardrift/reviews
- https://engadget.com/2271730/lola-is-bookingcoms-new-ai-travel-agent ; https://www.renascence.io/news/81186/lola-ai-travel-assistant-launches-membership-model ; https://briefglance.com/articles/unbundling-the-platinum-card-how-lolas-ai-is-rewiring-travel
- https://trustpilot.com/review/helloaxel.com ; https://no.trustpilot.com/review/helloaxel.com ; https://mediarelations.gwu.edu/node/16206 ; https://helloaxel.com/en/faq/is-axel-a-travel-agent
- https://skift.com/2025/10/15/kayak-ai-mode-natural-language-search/ ; https://vice.com/en/article/kayak-ai-beta-test/ ; https://www.travelpulse.com/news/technology/kayak-launches-ai-trip-planner-that-works-like-a-conversation
- https://www.phocuswire.com/expedia-group-ai-lessons-experimentation-chatbot ; https://bgr.com/tech/expedias-romie-wants-to-be-your-ai-travel-agent ; https://ca.news.yahoo.com/ai-trip-planning-tool-best-134756743.html
- https://skift.com/2025/03/25/booking-com-and-ai-now-vs-2023-tech-chief-explains-whats-changed-whats-next/ ; https://ttrweekly.com/site/2023/06/booking-com-tests-ai-trip-planner ; https://www.stork.ai/en/booking-com-ai-trip-planner

**Gap-fill: journalist tests, studies and incidents**
- https://www.khaleejtimes.com/travel/ai-travel-tools-everywhere-are-they-any-good (NYT syndication) ; https://www.omanobserver.om/ampArticle/1182812
- https://www.thestar.com.my/tech/tech-news/2026/05/07/opinion-a-tech-writer-puts-googles-ai-to-the-test-as-a-trip-planner
- https://flowingdata.com/2024/08/27/ai-based-travel-agent
- https://www.tovima.com/wsj/how-well-can-ai-plan-your-next-trip-we-tested-gemini-and-chatgpt (WSJ reprint)
- https://static2-cdn.newser.com/story/386094/ai-planned-her-vacation-with-some-hits-and-big-misses.html
- https://www.hospitality.today/article/dont-trust-an-ai-chatbot-with-all-your-travel-plans-just-yet
- https://www.afar.com/magazine/we-tested-ai-travel-planning-apps-here-are-the-3-that-actually-worked
- https://www.afar.com/magazine/the-most-common-mistakes-ai-makes-when-planning-travel
- https://skift.com/2024/03/07/we-tested-new-ai-trip-planners-from-despegar-and-kayak-fewer-errors-still-buggy
- https://www.techradar.com/computing/artificial-intelligence/can-an-ai-travel-agent-remove-the-stress-of-vacation-booking-i-tried-three-to-find-out
- https://www.insuremytrip.com/travel-advice/travel-planning/ai-travel-planning-reliability/
- https://www.outsideonline.com/adventure-travel/advice/ai-trip-planning
- https://www.kiplinger.com/personal-finance/travel/planning-vacation-with-ai-results
- https://travolution.com/news/marketing/survey-finds-chatgpt-itineraries-to-be-riddled-with-inaccuracies
- https://www.travelnews.co.za/article/ai-generated-itineraries-lead-travellers-astray
- https://fooddrinkdestinations.com/?p=10314 (Greetwell survey summary)
- https://www.eldiario.ec/mundo/turistas-llegan-a-destino-inexistente-en-peru-tras-seguir-recomendacion-erronea-de-inteligencia-artificial-09102025/
- https://www.t13.cl/noticia/tendencias/turistas-pagaron-160-dolares-para-viajar-al-canon-sagrado-humantay-creado-ia-09-10-2025
- https://www.euronews.com/2026/01/30/how-an-ai-generated-travel-website-sent-tourists-to-a-non-existent-hot-spring-attraction
- https://livejapan.com/en/article-a0005944/ ; https://livejapan.com/en/article-a0005946/

**Gap-fill: forums, second-hand Reddit and Hacker News**
- https://newsonjapan.com/article/146415.php
- https://www.early-retirement.org/threads/japan-itinerary-by-ai.123626/
- https://www.ivisitkorea.com/how-ai-travel-planners-can-ruin-your-trip/
- https://tabiji.pages.dev/resources/why-ai-travel-planners-give-generic-recommendations
- https://community.ricksteves.com/travel-forum/tech-tips/seeking-tips-for-using-chatgpt-as-a-part-of-travel-planning
- https://www.australianfrequentflyer.com.au/community/threads/are-you-using-ai-chatgpt-for-travel-planning-and-while-travelling.121141/post-2923908
- https://www.businessinsider.nl/im-an-avid-traveler-and-finally-found-a-useful-way-to-use-chatgpt-to-plan-my-trips-that-saves-me-hours
- https://hnews-reader.vercel.app/top/43982670 (Show HN: Planitly) ; https://hn.svelte.dev/item/41084757 (Ask HN)

**Gap-fill: segments and markets**
- https://hospitalitynet.org/news/4132732/closet-cationers-latest-bookingcom-research-reveals-majority-of-lgbtq-travelers-conceal-their-identity-when-traveling
- https://travelmole.com/news/booking-com-travel-proud-research-report-2026
- https://www.travolution.com/news/travel-sectors/matador-network-research-reveals-lgbtq-travellers-lead-way-in-adopting-ai-for-trip-planning
- https://journeywoman.com/safety/how-does-ai-in-travel-impact-womens-safety/
- https://www.solofemaletravelers.club/?p=29215
- https://www.travolution.com/news/travel-sectors/high-ai-satisfaction-for-disabled-travellers-who-use-it-to-plan-trips-says-matador-network
- https://wheelchairtravel.org/artificial-intelligence-impact-accessible-travel-will-be-negative-before-positive/
- https://makeitfable.com/insights/insights-accessibility-challenges-in-travel
- https://www.experian.com/blogs/ask-experian/survey-financial-stress-of-traveling-with-friends/
- https://www.timeout.com/usa/news/spring-break-travel-trends-group-travel-is-up-and-so-is-vacation-fighting-030926
- https://plus.inquirer.net/news/why-3-in-4-travel-plans-go-pfft/ (Klook)
- https://briefglance.com/articles/the-hidden-cost-of-friendship-are-you-paying-a-peace-tax-on-trips (CIT Bank, secondary)
- https://brands.guidegeek.com/press/half-of-summer-travelers-may-use-an-ai-assistant-this-year-especially-families
- https://www.travelmarketreport.com/canada/retail-strategies/articles/family-travel-association-2025-trends-survey-results
- https://aitopics.org/doc/news:5C833732 ; https://sagnikbhattacharya.com/blog/ai-chatbot-allergen-questions-restaurant ; https://apps.apple.com/us/app/id6759512120
- https://en.prnasia.com/releases/apac/68-of-indian-travelers-likely-to-use-ai-for-their-next-trip-agoda-532275.shtml ; https://www.ttrweekly.com/site/2026/05/agoda-indian-travellers-turn-to-ai-for-trip-planning/
- https://www.businesstoday.in/amp/technology/news/story/indian-travellers-embrace-ai-and-biometrics-for-smarter-seamless-journeys-amadeus-report-499469-2025-10-24 ; https://www.traveltrendstoday.in/kaspersky-survey-unveils-how-indian-travelers-are-using-ai-in-travel
- https://www.travelvoice.jp/20250822-158242 ; https://www.travelvoice.jp/english/trends-in-gathering-travel-information-are-structurally-changing-in-japan-with-three-times-more-ai-users ; https://english.adnkronos.com/2026/07/13/61-pct-in-japan-to-use-ai-for-summer-travel-planning-survey/ ; https://www.travelvoice.jp/20260804-160165
- https://www.latintimes.com/latin-american-travelers-are-prioritizing-mental-health-ai-stress-free-vacations-marriott-study-599515 ; https://www.contentgrip.com/global-ai-sentiment-report/

**Gap-fill: pricing, willingness to pay and conversion**
- https://recurdash.com/subscription-pricing/flighty ; https://www.tapsmart.com/?p=25189 ; https://adapty.io/paywall-library/flighty/
- https://thesocialoutline.com/blog/trial-to-paid-conversion-rate-benchmarks ; https://revenuecat.com/blog/growth/app-trial-conversion-rate-insights/
- https://newsroom.ca.paypal-corp.com/hopper ; https://www.mckinsey.com/industries/travel/our-insights/travel-disruptors-bringing-fintech-to-travel-booking ; https://techcrunch.com/2022/06/07/hopper-launches-offerings-more-flexibility-before-during-trips/ ; https://hts.hopper.com/products/cancel-for-any-reason-for-hotels

*Gap-fill working notes (raw snippets, search log, remaining gaps): /home/user/travel/research/notes/06-gapfill-notes.md*
