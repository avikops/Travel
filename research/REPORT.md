# AI Trip Planning: State of the Art and Where to Win

**Date:** 17 Nov 2026
**Scope:** Consumer AI trip planning, plus the booking, data, legal and research layers underneath it.
**Built from:** 7 parallel research streams (full reports in [`raw/`](raw/)) and a spot-check of the headline facts.

---

## 0. How to read this

**Sources.** Each section draws on one or more of the 7 detailed reports, and section headers point to the file:

| # | File | Covers |
|---|---|---|
| 01 | [raw/01-ai-native-startups.md](raw/01-ai-native-startups.md) | Mindtrip, Layla, Lola, Vayo, Odessia, Airial, Stardrift, Axel, GuideGeek, Wanderlog, social-to-itinerary apps, Fora/Tern |
| 02 | [raw/02-incumbents-llm-platforms.md](raw/02-incumbents-llm-platforms.md) | Google, ChatGPT, Perplexity, Copilot, Claude, Meta, Apple, Expedia, Booking Holdings, Airbnb, Kayak, Trip.com, Hopper, Navan/Perk/Spotnana, airlines |
| 03 | [raw/03-hyperlocal-data-freshness.md](raw/03-hyperlocal-data-freshness.md) | Hallucination evidence, POI and transit data sources, licensing, grounding techniques, recommended data stack |
| 04 | [raw/04-booking-interop-infra.md](raw/04-booking-interop-infra.md) | Flight, hotel, rail, activity and restaurant APIs; MCP and agentic payments; merchant-of-record models; integration phasing |
| 05 | [raw/05-accountability-support.md](raw/05-accountability-support.md) | Competitors' terms of service, *Moffatt*, EU package-travel rules, ATOL, seller-of-travel laws, guarantees, disruption tech |
| 06 | [raw/06-user-voice-reviews.md](raw/06-user-voice-reviews.md) | Adoption and trust surveys, reviews, pain points, underserved segments, workarounds |
| 07 | [raw/07-research-frontier-market.md](raw/07-research-frontier-market.md) | Benchmarks (TravelPlanner etc.), solver+LLM results, architecture, unit economics, funding, startups that died |

**Confidence.** Confidence is moderate overall, and high on the headline facts.
- **Thin coverage.** All research ran through web search; direct page fetches were blocked by this environment's network policy. A shared search budget ran out partway through, so some areas are thin. They're listed in §11.
- **Tags.** Every claim in the raw reports is tagged [verified], [claimed], [inferred] or [recall/background]. In this report, **✅** marks facts I re-checked independently in a second pass (§12). Anything marked *(unverified)* is from model recall and must be checked before you rely on it.
- **No hands-on testing.** No competitor product was tested hands-on. §11 has a test battery to run once that's possible.

**Scoring rubric** used across all reports:

| Dimension | Levels |
|---|---|
| **P**ersonalisation | P0 none · P1 form prefs · P2 in-session refinement · P3 persistent profile · P4 learns from behaviour, bookings, linked accounts |
| **G**ranularity | G1 city list · G2 day list · G3 time-slotted with hours · G4 + real transit, routing, buffers · G5 door-to-door incl. bookings and tickets |
| **B**ooking | B0 none · B1 affiliate links · B2 in-app, some verticals · B3 multi-vertical, one checkout · B4 + post-booking changes and refunds |
| **L**ive / on-trip | L0 none · L1 static · L2 companion chat · L3 real-time alerts · L4 automatic disruption re-plan and rebook |

---

## 1. Bottom line

**Nobody is the best AI trip planner today, because no product combines the four things that matter:**
1. plans that are actually feasible and verified;
2. local, non-generic taste;
3. booking and managing across suppliers;
4. standing behind the trip when it breaks.

Each leader is strong on one or two of these and absent on the rest:

| Leader | Strong on | Missing |
|---|---|---|
| Google | Data and personalisation | Accountability |
| Lola / Booking Holdings | Multi-vertical booking, human concierge | Neutrality, routing detail |
| Airial | Transit routing | Booking |
| Navan | Accountability | Corporate only |
| Fora | A human owns the trip | Not AI-native, not mass-market |

**The open position is the planner that stands behind its plan.** Every place, hour and connection is checked and timestamped. A solver guarantees the plan is feasible. Recommendations come with real local reasons and sources. The whole trip is monitored after booking, wherever it was booked. When something breaks there is repair, a human, and a guarantee.

Each part of that is technically proven somewhere:
- Solver-backed planning reaches 93.9% on the main benchmark versus 0.6% for an LLM alone.
- Closure detection by phone call exists.
- Corporate travel tools already do disruption rebooking.
- Insurers already price guarantees.

**No one has assembled the parts for leisure travellers.** That is the gap.

### Ten findings that shape the strategy

1. **The independent AI planners have been bought or out-built in 2026.**
   - Expedia bought Layla (Jul) ✅.
   - OpenAI bought Odessia and shut the service down about a month after launch, leaving users holding live bookings (Nov) ✅.
   - Booking Holdings launched Lola (Sep) ✅. Lola has since added flights and a planned $100M investment ✅. Booking Holdings is also testing Vayo.
   - Mindtrip is the strongest independent left. It books flights through Sabre and PayPal.
   *(01, 02)*
2. **"Plan in the AI, book with the brand" won 2026.**
   - OpenAI pulled ChatGPT's in-chat checkout (Mar).
   - Google AI Mode books hotels, but the partner stays merchant of record and handles service ✅.
   - LLM referrals are under 1% of Booking.com room nights.
   *(02, 04)*
3. **Hallucination is mostly an operational problem, not invented places.**
   - 55% of AI-using travellers hit a bad recommendation, and about 1 in 6 were sent somewhere that doesn't exist ✅ (Greetwell, n=485, commissioned).
   - One audit of 356 AI itineraries found a fault on 43% of planned days; 53% of the closed-day errors fell on Mondays.
   - The dominant failures are closed venues, wrong hours and last departures, and infeasible sequencing. All of them can be checked mechanically.
   *(03, 06)*
4. **The research has already shown the fix and products haven't shipped it.**
   - An LLM that turns the request into a constraint problem solved by a formal solver (SMT) passes 93.9% of TravelPlanner tasks, versus 0.6% for a frontier LLM alone.
   - No consumer product publicly claims solver-verified feasibility.
   - The unsolved frontier is open-ended, preference-heavy, real-world requests (about 37% on ChinaTravel), plus group trips and pacing.
   *(07)*
5. **The good data is walled off and licensing shapes the architecture.**
   - Google Maps terms forbid caching (except place IDs) and AI training. Yelp forbids feeding its data to any generative model outside its own AI API. Tripadvisor allows AI use only by signed deal.
   - Reddit is licensed to Google and OpenAI. TikTok and Instagram are closed.
   - You can't build a proprietary knowledge base on Google. You *can* build on Overture and Foursquare open data and licensed local content, and use Google only for live checks.
   *(03)*
6. **The self-serve booking-API era is over.**
   - Amadeus Self-Service shut on 17 Jul 2026 ✅. Kiwi's flight API is invite-only. TripIt's API is closed to new integrations.
   - Still reachable without airline-industry accreditation: Duffel (flights, stays, cars), LiteAPI (hotels, with an MCP server), Viator and GetYourGuide (activities), Distribusion and Trainline (ground), Mozio (transfers).
   - Restaurants are the most closed vertical.
   *(04)*
7. **Suppliers are fighting unsanctioned agents.**
   - United banned unauthorised third-party AI agents on 11 Nov 2026 ✅, including agents working through travel agencies and even when the user approves. Delta reportedly blocks agents technically.
   - Two days later, an airline-approved booking by an agent went live on Travelport with Mastercard Agent Pay.
   - Booking agents that drive consumer websites are now a dead end. Use official APIs, tokenised payments and explicit user approval.
   *(02, 04)*
8. **Accountability is the emptiest field.**
   - Every consumer AI planner disclaims its advice ("as is"; "not a travel agent"). No planner has been found compensating a user. *Moffatt v Air Canada* shows such disclaimers are weak.
   - The revised EU Package Travel Directive (Directive (EU) 2026/1024) ✅ abolishes "linked travel arrangements". Linked online bookings with data passed between suppliers within 24 hours become a package, which makes an agentic multi-booker a likely **organiser** with full liability.
   *(05)*
9. **Users want AI to plan and humans or brands to answer for it.**
   - Only 6% fully trust AI (Booking.com, n=37k); 8% are comfortable booking through an AI platform; 2% want full autonomy.
   - The trust ladder: suggest 53% > build itinerary 40% > book restaurants or tours 38% > hotels 35% > flights 32%.
   - Comfort among 18–24s fell from 47% to 34% in a year, even as their usage rose, which signals disillusionment after use.
   - New complaints beyond your four: subscription traps, plans drifting with each revision, over-packed days, unreliable booking import.
   *(06)*
10. **Investors pay for AI plus accountable humans, not pure AI.**
    - Fora raised $60M at a $1B valuation (Jul 2026) ✅. Tern's AI drafts work that advisors approve.
    - Earlier chat-concierge startups (the first Lola, Mezi) died or were absorbed by card issuers.
    - Affiliate economics are thin (hotels about 3–6%, flights about zero), so cost per plan must be engineered below about $0.20.
    *(01, 07)*

---

## 2. The landscape on one page

Combined from 01 and 02. Scores are evidence-based but not from hands-on testing.

| Product | Owner / status (Nov 2026) | P | G | B | L | What it does best | Biggest hole |
|---|---|---|---|---|---|---|---|
| **Google** (AI Mode + Ask Maps + Gemini) | Google | **P4** (opt-in Gmail, Photos) | G3–4 | B2 (hotels via 10 partners, dining, events; no flights) | L2–3 | Best grounding (about 300M places), itineraries inside Maps navigation, calls businesses for you | No liability; popularity-ranked (cliché); US-first |
| **ChatGPT** + partner apps | OpenAI (+ Odessia team) | P3 | G2–3 | B1 (hands off to partners) | L1–2 | Distribution, the default first question | Pulled checkout; apps not in EU; no servicing |
| **Lola** | Booking Holdings | P3 (Gmail) | G2–3 | **B3** (hotels, dining, events, activities, now flights) | L2 | No ads or paid placement; $25/mo tier includes human concierge (Ten Group) | Booking-family bias; routing detail unknown; US-only at launch |
| **Vayo** | Booking Holdings (beta) | P4 (inbox) | G1–2 | B0→B2 | **L3** | Monitors bookings you already made for price drops, sold-out rooms reopening and schedule changes | Monitors only; no re-plan |
| **Expedia** (+Layla, Romie) | Expedia | P3 | G2–3 | **B4** | L2–3 | Full booking and servicing for its own inventory; partners with every AI surface | Its own inventory only; Layla still runs separately |
| **Mindtrip** | Independent (~$22.5M raised) | P3–4 | G3 | B2 (flights via Sabre) | L2–3 | Map-first UX, group chat, social-to-plan, tourism-board (DMO) distribution, cross-trip memory | Invented hotels, closed restaurants, wrong hours in tests; no accountability |
| **Airial** | Independent ($3M seed) | P2 | **G4** | B1 | L0–1 | Real multimodal logistics (which train, transfer times) | No ticketing, English only |
| **Wanderlog** | Independent | P1–2 | G3–4 | B1 | L1 | Best manual editor and collaboration; Gmail import | AI is a weak add-on; billing complaints |
| **Stardrift / Axel** | YC startups | P3–4 / P2–3 | G2–3 / G1 | B2 | L2 / **L3** | Calendar-aware booking; automatic refunds when prices drop | Narrow, logistics-only |
| **Trip.com TripGenie** | Trip.com | P3 | G3 | B3–4 | L3 | Most complete incumbent stack, incl. rail; alerts even for trips not booked with Trip.com | Weak on Western long-tail places; edits don't sync to bookings |
| **Hopper / HTS** | Hopper | P2 | G1 | B2–3 | **L3–4** | Disruption Guarantee: rebooks you on any airline | $35M FTC settlement over hidden fees; flights-centric |
| **Airbnb** AI agent | Airbnb (H1 2027) | — | — | — | — | Promised: cross-platform, rich UI, group planning | Not shipped |
| **Navan / Perk / Spotnana** | Corporate | P3 | G3 | B4 | **L3–4** | Duty of care, 24/7 humans, automated rebooking, import of external bookings | Corporate only |
| **Fora / Tern** (reference) | Human-advisor platforms | P4* | G5* | B4* | L4* | A licensed human owns the trip (*done by humans, not AI) | Doesn't scale to the mass market |
| **Social-to-itinerary apps** (Plotline, Triply, feedtrip, Strollio…) | Early startups | P1–2 | G2–3 | B0 | L0–1 | Extract places from TikTok and Reels | Commoditised; keep names, lose reasons; no accuracy data |

**Reading across the table:**
- **No AI-native consumer product reaches G4+, B3+ and L3+ at once.**
- G5 and L4 exist only where humans do the work (Fora) or for corporate customers (Navan).
- Combining high granularity, multi-vertical booking, live repair and a guarantee is the unclaimed position.

---

## 3. Problem by problem: state of the art, depth, ceiling, gap

### 3.1 Generic, cliché recommendations and no hyperlocal knowledge *(01, 03, 06, 07)*

**How bad it is**
- Simon-Kucher: 47% of dissatisfied AI users say answers are "too generic".
- Users describe itineraries that "look complete but feel strangely incomplete" and say power users notice recycled forum content.
- Skift Research frames AI as narrowing discovery toward well-known places.
- The real complaint is less "generic" than **the same canon for everyone, stitched together without judgement**: no "why this fits *me*", no timing or seasonal nuance, no trade-offs.

**How the leaders approach it**

| Mechanism | Who | How deep it goes |
|---|---|---|
| Tourism-board (DMO) first-party content | Mindtrip (Norway by Locals: 150+ municipalities), GuideGeek (NYC, Toronto, Colorado…) | Authoritative but **promotional**, favouring board members |
| Social-video ingestion | Mindtrip Start Anywhere, Airial, about 8 apps, Tripadvisor demo | Extracts **names, not reasons**. No published accuracy for matching to the right place. Drops the creator's context (dish, time of day, why) |
| Popularity and reviews | Google (500M contributors), Tripadvisor (1B reviews) | Ranks by review volume, which *is* the cliché problem |
| Licensed editorial | OpenAI (Eater, CNT, T+L publisher deals) *(unverified)*; Atlas Obscura revenue-share deal | Big labs only; startups must negotiate |
| Reddit-style candid local advice | Licensed to Google and OpenAI; free API reportedly ends by Mar 2027 | **Walled off from startups** |

**Ceiling today**
- Neighbourhood-level advice is partially served.
- Street- and dish-level insight is unserved, except by accident from model training data.
- Time-of-day and seasonal nuance is largely unserved.
- Safety exists only as country-level advisories.
- Accessibility is shallow yes/no fields.
- Nobody measures or reports how generic their recommendations are.

**Gap to exploit**
- A **licensed, attributed, dated local-knowledge graph**. For every place, store *why*, *when*, *for whom* and *what to order*, with the source and date. Sources: revenue-share deals with local newsletters and guides, a paid network of verified locals, and tourism-board open data.
- An **anti-cliché objective in the solver** that rewards novelty, penalises popularity, and is tunable from "first-timer classics" to "local-only".
- A **published cliché rate**, e.g. the share of picks inside the top-20 Tripadvisor attractions.
- **Explanations tied to the user's own signals**: "because you saved X", "this is the Tuesday market locals use".

### 3.2 Poor interoperability with booking and trip management *(04, 02, 01)*

**State of the art by vertical**

| Vertical | Best AI-planner reality | Best startup access path now | Achievable depth |
|---|---|---|---|
| Flights | Mindtrip on Sabre + PayPal; Lola (new); Odessia (dead) | **Duffel** (no accreditation; $3 per order + 1% on managed content) | Book + voluntary changes; flight disruptions only partly |
| Hotels | Lola, Google AI Mode (partner merchant), Expedia/Booking apps | **LiteAPI** (self-serve, MCP), Duffel Stays, then Expedia Rapid (compliance review) | Book + cancel + retrieve |
| Rail, bus, ferry | **Nobody in AI planners**; Trip.com within Asia | **Distribusion** (MCP, incl. Amtrak, SNCF, DB, Eurostar), Trainline Partner Solutions, 12Go (SE Asia) | Book + after-sales |
| Transfers | Nobody | **Mozio** | Book + cancel |
| Activities | Lola (GetYourGuide, FareHarbor), ChatGPT apps (handoff) | **Viator** (Full + Booking tier), **GetYourGuide** (BOOKING tier) | Book + cancel |
| Restaurants | Google AI Mode, Lola (OpenTable), Resy in ChatGPT | Mostly deep links; partner deals required (OpenTable, SevenRooms, TheFork) | Search and deep-link |
| Vacation rentals | Expedia (Vrbo) | Vrbo via Expedia Rapid; **Airbnb: no API** | Book via Rapid |
| Bookings made elsewhere | Vayo, Lola, Wanderlog (Gmail), TripIt (API closed) | Forward-to-address email parsing + AwardWallet | **Watch only, can't act** |

**Where the ceiling is**
- Search is mostly solved.
- Booking is solvable, one cart per supplier.
- **Managing bookings is the real ceiling.** You can change or rebook only what went through your own channel; bookings from elsewhere can only be watched.
- Loyalty credentials are now explicitly off-limits (United).
- Payments for agents are converging on tokenised cards (Mastercard Agent Pay, Visa) with the user confirming the final amount.

**Gap to exploit**
- **Door-to-door G5**: flight, train or ferry, transfer, hotel and activity on one timeline with real buffers. Nobody stitches ground transport in.
- **An AI-native trip hub** that imports everything (forwarded emails, loyalty data), then offers to *protect or migrate* bookings onto your rails. TripIt's closed API leaves this open.
- **An approved-agent posture as a moat**: official APIs, agent payment tokens, never asking for passwords, clear user approval.

### 3.3 Stale, poor data and hallucinations *(03, 07, 06)*

**How bad it is**
- 55% hit at least one bad recommendation; 16% were sent somewhere that doesn't exist (Greetwell ✅).
- 43% of AI-planned days contain a verifiable fault (vendor audit of 356 trips).
- Google Maps missed about 27% of confirmed closures in a 400-place vendor test.
- Even Mindtrip invented hotels ("Holiday Inn Express Tokyo"), recommended a Lisbon restaurant closed since 2024, and made up weather numbers in third-party tests.
- Documented incidents: the non-existent "Sacred Canyon of Humantay" (Peru), the last ropeway on Mount Misen (stranded couple), the missed ESTA for Puerto Rico (denied boarding), the fake "Kuak Skyride" cable car video (Malaysia).

**Failure classes, most to least common:**
1. Stale status (closed or moved).
2. Wrong operational times: hours, last entry, last ropeway or ferry, weekly closing days.
3. Infeasible sequencing: backtracking, overruns.
4. Invented places, often two real names merged.
5. Fake AI-generated content contaminating sources.

Classes 1–3 can be fixed with data plus constraint checking. Class 4 needs every place tied to a real database ID. Class 5 needs source tracking.

**How the leaders ground their answers**
- **Google:** live Maps status, phone calls to businesses (Duplex), "hours may have changed" flags.
- **Mindtrip:** an 11M-place database plus Google, Tripadvisor and OpenTable.
- **Layla:** live prices.
- **Data vendors** now sell "AI" products at $14–36 per 1,000 calls (Gemini Maps grounding, Yelp AI API, Foursquare Ask), and forbid feeding their raw data to other companies' models.
- **VOYGR** offers an existence and closure-check API with automated calls. It doesn't cover opening hours yet.

**Ceiling today**
- No product shows "last verified" timestamps or confidence to users.
- No consumer product documents a deterministic feasibility check.
- Nobody publishes an accuracy benchmark.

**Gap to exploit**
1. **A per-field freshness record.** Store value, source, observed time, method (API, crowd, call, editorial) and confidence, and show it: "Hours confirmed by phone 2 days ago."
2. **A deterministic feasibility checker plus repair loop.** It checks hours by weekday, last entry, travel time, buffers, holidays and daylight. Target a public "0 infeasible days" metric.
3. **A proprietary dataset of special services:** cable cars, funiculars, seasonal ferries, park shuttles, last-entry and timed-ticket sellouts. None of these are in transit feeds or place APIs. This is a moat.
4. **Reconfirmation** of booked or critical stops 24–48 hours ahead by automated call or API.
5. **Traveller "it was closed" reports** that update the shared record for everyone, Waze-style.

### 3.4 No accountability or support when things go wrong *(05, 02, 04)*

**What everyone promises: almost nothing.**
- **Mindtrip:** "AS IS"; doesn't sell anything directly.
- **GuideGeek:** "no claims or warranties as to the accuracy".
- **Layla:** the chatbot "cannot bind" anyone; liability capped.
- **Expedia AI terms:** answers are "based on publicly available information, the accuracy of which Expedia has not verified".
- **Google:** "the hotel or booking platform will handle the booking and any customer service".

This splits liability in two. **Transaction liability** is accepted by OTAs and suppliers. **Advice liability**, meaning whether the itinerary is right, is accepted by nobody. Most harm sits in advice.

**Accountability matrix** (0–5; from 05)

| Player | Advice | Transaction | Human support | Disruption execution | Financial guarantee | Overall |
|---|---|---|---|---|---|---|
| ChatGPT / Gemini | 1 | 1 | 0 | 0 | 0 | **0.5** |
| Mindtrip, Wanderlog, GuideGeek | 1 | 1 | 1 | 0 | 0 | **~1** |
| Booking.com / Expedia | 1 | 3 | 3 | 2 | 2 | **~2.5** |
| Airbnb (AirCover) | 1 | 3 | 3 | 2 | 3 | **~3** |
| Hopper | 1 | 3 | 2 | 4 | 4 | **~3** |
| Card travel desks (Amex, Chase) | 2 | 3 | 4 | 3 | 4 | **~3.5** |
| Navan / Perk | 2 | 3 | 5 | 4 | 3 | **~4** |
| EU package organiser | 3 | 5 | 3 | 3 | 5 | **~4** |
| **Unoccupied** | **≥3** | **≥3** | **≥3** | **≥4** | **≥3** | consumer, AI-native |

**Ceiling today**
- Where accountability works, it is pre-funded by fees, card annual fees, service fees or insurance premiums. It is never funded by an AI subscription.
- AI can book a flight but not rebook it.
- Airbnb, with the best AI support figures, still resolves only about 40–45% of issues without a human.

**Gap to exploit**
- **Itinerary Accuracy Guarantee.** Check the facts a trip depends on (entry documents, last departures, opening hours, transfer feasibility). If a *checked* fact was wrong and it cost the traveller money, pay out up to a cap, with an insurer behind it. Nobody offers this.
- **Watch and act.** Monitor the trip 24/7 and re-plan the knock-on effects: a late flight shifts the hotel check-in note, the dinner booking and the train. A human with airline-booking-system access (via a partner agency) handles what AI can't, with a published response time.
- **Claims on autopilot.** File EU261/UK261, US DOT refunds, Canada's APPR and insurance claims at 0% commission, versus about 30–35% at AirHelp-type services.
- **Continuity by design.** Odessia's shutdown left people holding bookings. Publish a continuity commitment so bookings survive if you don't.

### 3.5 Problems not on your list *(06)*

| Problem | Evidence | Implication |
|---|---|---|
| **Subscription and billing traps** | Top Trustpilot complaint for both Layla and Wanderlog | Honest pricing is a differentiator; never trap a trial |
| **Plans drift on revision; the plan lives in a chat log** | Each revert drifts further from the brief (TPG); research shows models drop earlier constraints (Flex-TravelPlanner, TravelEval) | A persistent, structured plan with version history, targeted edits ("swap only Tuesday afternoon") and locked items |
| **Over-packed, geographically unrealistic days** | Japan "sprint" itineraries; Trip+ benchmark finds models ignore fatigue | Pacing as a hard constraint; explicit trade-offs ("drop Hiroshima or spend 9 of 14 days on trains") |
| **Unreliable import of existing bookings** | Wanderlog vs TripIt | TripIt-grade parsing is table stakes |
| **Commission bias** | Free planners funded by commissions; OTA assistants show only their own stock; 57% want cross-brand assistants (Accenture) | Neutral, disclosed ranking |
| **Trust erodes after real use** | 18–24 comfort down 13 points in a year while usage rose | Retention depends on being right, not on novelty |
| **Gender trust gap** | 44% of women vs 36% of men not comfortable (YouGov) | Safety-grounded features win a sceptical segment |
| **Some people want no AI at all** | 23% of US travellers prefer to avoid AI | A manual-first mode; never force chat |

---

## 4. How deep the competition goes: the ceiling on each dimension

| Dimension | Best in market today | Who | What nobody does yet |
|---|---|---|---|
| **Personalisation** | P4: Google reads Gmail bookings and Photos (opt-in); Vayo and Lola read inboxes; Mindtrip has cross-trip memory | Google, Booking Holdings, Mindtrip | Learning *taste* (not just logistics) from past trips, saves and ratings, and turning it into solver weights. A portable profile the user owns. Constraints that survive long conversations and are enforced (diet, mobility, pace). Fair handling of a group's preferences. |
| **Granularity** | G4: Airial (which train, transfer times); Wanderlog (route optimisation); Google Maps (itinerary inside navigation) | Airial, Wanderlog, Google | **G5**: door-to-door with tickets and buffers that re-flows on change. Last-departure warnings. Accounting for terrain, steps and heat. Special services (ropeways, seasonal ferries). |
| **Customisation and control** | Wanderlog drag-and-drop; Mindtrip group chat, likes and comments | Wanderlog, Mindtrip | Locking items; hard vs soft constraints; "explain why not" when a request can't be met (with suggested relaxations); version history; two-way sync with Maps lists and Sheets. |
| **Booking** | B3–4: Lola (multi-vertical in one chat), Expedia and Trip.com (own inventory), Navan | Booking Holdings, Expedia, Trip.com | **Neutral** multi-supplier booking incl. ground transport; managing bookings made elsewhere. |
| **Live / on-trip** | L3: Vayo, Axel, Mindtrip agents (monitoring); L4 only at Hopper (flights), Navan (corporate) and Delta (own flights) | Hopper, Navan, Delta | **Consumer L4 across the whole itinerary**: re-plan hotel, dinner, train and tour when a flight slips. |
| **Data grounding** | Google Maps (300M places, calls businesses) | Google | Visible freshness timestamps and confidence; a published accuracy rate; an attributed local corpus. |
| **Accountability** | Lola VIP human concierge; Hopper guarantees; AirCover | Booking Holdings, Hopper, Airbnb | An accuracy guarantee on advice; one accountable party across suppliers; free automated claims. |

---

## 5. Market constraints

These constraints hold regardless of what we build, and they decide the design.

1. **Licensing beats technology for data.**
   - Google: no caching except place IDs, coordinates for 30 days, no AI training. Yelp: no use in generative models without its AI API. Tripadvisor: AI only by signed deal. Reddit: big labs only. Overture and Foursquare open data are usable but noisy.
   - **Implication:** own a backbone built on open data, use Google and others live only to verify and display, and *license* the local layer *(03)*.
2. **The booking channels are gated.** See §3.2. Duffel, LiteAPI, Viator, GetYourGuide, Distribusion, Trainline and Mozio cover most verticals without airline-industry accreditation. Full servicing beyond that needs IATA accreditation or a host agency for Sabre or Travelport *(04)*.
3. **Suppliers ban unapproved agents.** United's contract covers agents booking through travel agencies, even with the user's approval ✅. Browser-driving and computer-use booking is off the table. Use official APIs and agent tokens *(02, 04)*.
4. **Bundling triggers package law.**
   - Under the revised EU Package Travel Directive (2026/1024 ✅), linked online bookings with data passed between suppliers within 24 hours count as a package. Member states have about 28 months to transpose it, with application around 2029.
   - UK flight-inclusive bundles need an ATOL licence.
   - US: seller-of-travel registration in CA, FL, WA and HI.
   - Decide deliberately: per-component checkout, or become the organiser and hold insolvency cover. **Lawyer needed** *(05)*.
5. **Disclaimers don't protect you.** *Moffatt* found that linking to the correct policy page didn't cure a chatbot's misstatement. EU/UK unfair-terms law limits blanket exclusions. The UK competition regulator (CMA) reportedly says firms answer for their agents as for employees. From Dec 2026 the EU Product Liability Directive covers AI software for injury, though not pure financial loss *(05)*.
6. **The economics are thin.**
   - Hotels pay affiliates about 3–6%, activities about 8%, flights about zero.
   - An agentic itinerary costs about $0.10–2.00 in model plus maps fees.
   - Travel is infrequent (1–3 leisure trips a year) and paid acquisition is dominated by Google and the OTAs.
   - Cost per plan must be under about $0.20, revenue must come from high-commission verticals, B2B and subscriptions, and distribution must be organic or through partners *(07; numbers mostly unverified recall)*.
7. **General assistants are everyone's default front door.** Be callable *from* ChatGPT, Claude and Gemini via MCP and apps, not only standalone *(02, 07)*.

---

## 6. Threats over the next 12–24 months *(02)*

| Threat | Likelihood | Timing | What it closes | What stays open |
|---|---|---|---|---|
| Google extends AI Mode booking to flights and spreads Personal Intelligence globally | High | 6–18 mo | Booking breadth, personalisation | Accountability, anti-cliché, neutrality (ads model) |
| Airbnb AI travel agent (cross-platform, group planning) | High | H1 2027 | Taste plus experiences plus group UX | Ground transport, accountability beyond Airbnb |
| Lola scales (flights added ✅, $25 human concierge) | Med–High | 6–18 mo | AI plus human at consumer scale | Neutrality, routing depth, Europe |
| Expedia integrates Layla into a multi-agent planner | Med–High | 12–24 mo | Own-inventory booking and servicing | Neutrality |
| Apple Siri (iOS 27) with personal context across Mail, Wallet and Maps | Medium | 6–12 mo | On-trip retrieval on iPhone | Planning, booking, accountability |
| OpenAI builds a travel product (Odessia team) | Medium | 12–24 mo | Distribution plus agency licence know-how | Data rights, local layer, servicing |
| More airlines block agents | Medium | Ongoing | Unapproved booking paths | Official-API approaches |

**Our position must hold up against Google and Airbnb.** Neither will take liability for advice, publish a cliché rate, or rank neutrally across suppliers. Neither will build a licensed local corpus or repair the whole trip regardless of where it was booked.

---

## 7. Where to win: the strategy

### 7.1 Positioning

> **"The trip planner that stands behind its plan."**
> Verified. Local. Repaired when it breaks. Backed by a guarantee.

This maps your four problems to four pillars, each answering a documented gap:

| Pillar | Answers | Product mechanism | Why incumbents won't copy it quickly |
|---|---|---|---|
| **1. Verified plans** | Hallucination and stale data | Solver-checked feasibility (hours, transit, buffers, budget, pacing); a freshness timestamp on every fact; explanations and relaxations when a request can't be met; 24–48h reconfirmation | Google ranks by popularity and won't certify; OTAs optimise conversion |
| **2. Real local taste** | Cliché and no local knowledge | Licensed, attributed local corpus; anti-cliché solver objective; published cliché rate; "why this, for you" | Needs labour, licensing deals and an editorial stance, which commodity models can't supply |
| **3. Whole-trip watch and repair** | Interop and accountability | Import every booking; monitor; minimal-change re-plan of knock-on effects; book through official channels; ground transport via Distribusion, Trainline and Mozio | OTAs only repair their own bookings; Google and OpenAI won't service |
| **4. Someone accountable** | Accountability | Insurer-backed accuracy guarantee; human escalation with a published response time; 0% compensation claims; continuity commitment | Liability shy; regulators watch "guarantee" language; this needs real operations |

### 7.2 Product principles

Each principle follows from the evidence:
1. **Climb the trust ladder; don't sell autonomy.** Users approve every purchase. Start booking with restaurants and tours (38% trust), then hotels and flights. Only 2% want full autonomy *(06)*.
2. **The plan is a structured object, not a chat log.** Version history, locked items, targeted edits, two-way sync with Google Maps lists and Sheets, export anytime. Never hold the plan hostage *(06)*.
3. **The language model narrates; the solver decides.** Constraints live in a stored record, not in the context window *(07)*.
4. **Show uncertainty.** Display "verified 2 days ago via phone" or "unverified, check before going". Cite and date local sources *(03, 05)*.
5. **Repair, don't regenerate.** Booked items stay fixed; disruptions trigger a minimal-change re-solve *(07)*.
6. **Neutral and honest.** No paid placement in the ranking (or clearly labelled and kept out of the solver). Clear pricing, no trial traps *(06)*.
7. **Official channels only.** Official APIs, MCP endpoints, agent payment tokens. Never ask for loyalty passwords *(04)*.
8. **Manual-first mode for the 23% who avoid AI** *(06)*.

### 7.3 Segments to target first

The evidence points to segments where generic AI fails worst and the stakes are highest:
- **Complex multi-city and overland trips, rail-heavy:** Europe rail and Japan. These carry the highest failure rates (pacing, transfers, last departures), and ground booking is the most under-served vertical.
- **Groups:** voting, budgets and fairness are unmodelled outside Mindtrip and Wanderlog.
- **Safety-sensitive travellers:** solo women (44% sceptical), accessibility needs, dietary restrictions.

**Recommended beachhead (my judgement):** US-based travellers planning **multi-city Europe trips with rail**.
- **Booking access:** Duffel, LiteAPI, Distribusion, Trainline, Viator and GetYourGuide cover the whole trip without airline-industry accreditation.
- **Regulation:** US seller-of-travel rules are manageable. Selling to US residents *may* reduce exposure to EU package-travel rules (**lawyer needed**).
- **Clear value:** feasibility and transfer checking show clearly against the competition.
- **Japan next:** huge interest and notorious AI failures. Rail booking is harder there (no JR API; resellers like Klook and 12Go).

### 7.4 Distribution
- **Standalone app/web**, where the structured plan and trip-watching live.
- **Our own MCP endpoint** so ChatGPT, Claude and Gemini can call our verified planner and trip protection. Axel and Pilot already position this way.
- **B2B:** tourism boards (which want visitors spread beyond hotspots, matching anti-cliché), card issuers (which want liability for AI agents placed on the agent; Citi says so), and human advisors (Fora and Tern show AI multiplies them).

---

## 8. Reference architecture *(03 + 07 combined)*

```
CONVERSATION (frontier LLM): elicit · narrate · explain from solver state · cite sources
        │ typed TripSpec                                     ▲ plan + trace + provenance
CONSTRAINT & PREFERENCE STORE (hard/soft, priority, owner, source turn; persisted; re-checked each turn)
        │
CANDIDATES: retrieval over Place Graph + licensed local corpus; LLM scores fit/utility; popularity-debias
        │
SOLVER: CP-SAT/MILP (orienteering w/ time windows) + SMT for UNSAT cores → minimal relaxations;
        repair mode = freeze bookings, minimal-change re-solve; group fairness (least-misery + day rotation)
        │
VERIFIER (independent): hours × weekday × last-entry × travel time × buffers × holidays × daylight × pacing;
        entity-existence; freshness TTL re-fetch before display/booking
        │
DATA LAYER
  L0 Place Graph (owned): Overture GERS IDs + Foursquare OS Places + Wikidata + tourism-board open data
     (+ OSM in a separate ODbL layer for trails/steps/accessibility); store only external IDs for Google/Yelp/Apple
  L1 Live enrichment (display-only): Google Places status/hours · Foursquare Premium · BestTime busyness · partner availability
  L2 Freshness ledger: {field, value, source, observed_at, method: api|crowd|call|editorial, confidence}
     + closure detectors + voice-agent reconfirmation for booked/critical stops
  L3 Licensed local corpus: revenue-share editorial/newsletters/guides + own local-expert network; dated, attributed,
     place-linked, AI-content filtered
  L4 Ops data: GTFS/GTFS-RT (Mobility Database) → self-hosted OTP/MOTIS; Google Routes fallback;
     Distribusion/Trainline/12Go inventories; hand-curated SPECIAL SERVICES table (ropeways, funiculars,
     seasonal ferries, last departures, timed tickets); events (PredictHQ, tourism boards); weather/daylight
        │
ACTION LAYER: approval gates · Duffel / LiteAPI / Viator / GYG / Distribusion / Mozio · agent-token payments
        · email-forward importer · flight status + change webhooks → repair triggers → human escalation (partner agency w/ GDS)
        │
TRUST LAYER: immutable log of what we said/showed and when · accuracy guarantee (insurer) · claims autopilot
EVAL HARNESS: TravelPlanner/ChinaTravel/TripCraft regression · real-city sandbox · user simulator (multi-turn,
        group, unsolvable) · pass^k · infeasible-day rate · cliché/novelty/serendipity · human-calibrated judge ·
        prod: edit rate, on-trip deviation, complaint/refund rate
```

**Cost discipline:**
- Small fine-tuned models handle tool orchestration (the Planner-R1 / DeepTravel pattern); frontier models only for elicitation and narration.
- Aggressive caching, and the solver does the combinatorics.
- Target under $0.20 per plan, including maps calls.

---

## 9. Business model *(05, 07)*

| Revenue line | Role | Notes |
|---|---|---|
| Activities and hotel commissions | Base | About 8% activities, 3–6% hotels (affiliate); more as merchant of record |
| **Trip Protection subscription** (per trip, about $29–79, or about $10–20/month for frequent travellers) | **Funds accountability** | Watch and repair, human escalation, claims autopilot, accuracy guarantee; the Lola VIP and card-issuer analogue *(prices are inferred, test them)* |
| Embedded insurance and parametric delay cover | High margin | Distributor commission often 20–40% of premium *(unverified)*; needs insurance distribution licences or a partner |
| B2B: tourism boards, card issuers, advisors | Durable | Long sales cycles, aligned incentives |
| Merchant-of-record packaging (later) | Highest margin | Brings package-travel, ATOL and chargeback exposure; one market at a time |
| Ads / sponsored | **Avoid** | Destroys the trust position |

**Failure modes to design around** (07): low trip frequency, high acquisition cost, thin affiliate fees, and LLM cost above revenue per session.

**Retention answers:**
- On-trip and disruption value.
- Group virality: each trip brings in co-travellers.
- "Hometown" use between trips (Lola's thesis).

---

## 10. Phased plan

| Phase | Weeks | Build | Prove |
|---|---|---|---|
| **0. Evidence** | 0–3 | Hands-on teardown of competitors (§11 battery); build the eval harness and an "infeasible-day" and cliché benchmark across ChatGPT, Gemini, Mindtrip, Lola, Airial and Wanderlog | A public accuracy benchmark is itself marketing |
| **1. Verified planner** | 3–12 | Place Graph on open data, freshness record, solver + verifier, structured plan editor, Maps list import, one city cluster (e.g. Paris–Amsterdam–Berlin rail corridor) | 0 infeasible days on the benchmark; cliché rate well below competitors; user-tested trust |
| **2. Book and watch** | 12–24 | Duffel, LiteAPI, Viator, GetYourGuide, Distribusion/Trainline; email importer; flight status + webhooks; approval-gated checkout; seller-of-travel registrations | First paid bookings; first repaired disruptions |
| **3. Stand behind it** | 24–40 | Insurer-backed accuracy guarantee; human escalation via partner agency; claims autopilot; MCP endpoint for other assistants | Guarantee loss ratio; containment rate; NPS during disruption |
| **4. Expand** | 40+ | Japan; licensed local corpus at scale; tourism-board B2B; organiser status or ATOL in one market | Unit economics per trip |

---

## 11. What we still don't know (next research pass)

**Search-budget gaps.** These were not covered or were covered thinly because the shared search budget ran out:
- App Store and Google Play ratings for most competitors.
- Direct Reddit and Hacker News threads.
- NYT, WSJ, Verge, Wired and CNET hands-on tests.
- Smaller players: Tripnotes, iMean, Stippl 2026, Holiwise, Wonderplan, Kayak, Romie.
- Beli, Corner, Mapstr, Fever, local-guide marketplaces.
- The TikTok, Instagram and YouTube APIs; Citymapper and Moovit.
- Restaurant APIs beyond OpenTable and Resy; Kiwi MCP; whether Expedia's MCP server has launched.
- Funding and market numbers (07 Part B is unverified recall).
- EU261 reform status, US DOT rules, AI Act Article 50 timing, state seller-of-travel statute details.
- Insurers' and advisors' published response times.
- Willingness-to-pay data.

**Hands-on testing (the competitor teardown you asked for).**
- This environment's network policy blocked direct access to mindtrip.ai, layla.ai, wonderplan.ai, reddit.com and trustpilot.com.
- **To unblock:** allow those domains (plus airial.travel, lola.com, stardrift.ai, wanderlog.com, apps.apple.com, play.google.com, producthunt.com, arxiv.org) under the cloud environment's **Network access** settings. Then I can drive their logged-out flows in a headless browser and record what they request and return.
- **Or:** you create accounts and run this battery while I score the outputs.

**Test battery** (same prompts for every product):
1. **Monday trap:** "3 days in Paris starting Monday, museums focus." Do they schedule the Louvre (closed Tue) or Orsay (closed Mon) on a closed day?
2. **Last departure:** "Sunset on Mount Misen, Miyajima, then dinner in Hiroshima." Do they know the last ropeway time and ferry connection?
3. **Closed venue:** ask for a specific restaurant known to have closed in 2025–26. Do they recommend it?
4. **Impossible request:** "Tokyo, Kyoto, Osaka, Hiroshima and Hakone in 4 days, relaxed pace." Do they say it's infeasible and offer trade-offs?
5. **Hard constraints over many turns:** state vegetarian + wheelchair + $150/night in turn 1, then add 8 more preferences. Do the turn-1 constraints survive?
6. **Group:** four travellers with conflicting preferences. Is there fairness and attribution?
7. **Entry rules:** "Spanish passport, flying to Puerto Rico." Do they mention ESTA?
8. **Rail stitch:** "Amsterdam → Paris → Barcelona by train, with tickets." Do they show real trains and buffers, and can they book?
9. **Disruption:** "My flight to Lisbon is 5 hours late." Do they re-plan the hotel, dinner and next-day tour? Do they mention EU261?
10. **Cliché test:** "I've been to Rome twice; show me what locals do." Count picks in the Tripadvisor top 20.

---

## 12. Facts re-checked independently (second pass, 17 Nov 2026)

| Claim | Result | Source |
|---|---|---|
| Expedia acquired Layla (Jul 2026; terms undisclosed) | ✅ Confirmed. Layla keeps operating standalone | [Expedia IR](https://ir.expediagroup.com/news-and-events/news/news-details/2026/Expedia-Group-acquires-Layla-accelerating-its-AI-powered-trip-planning-and-booking-strategy/default.aspx), [PhocusWire](https://www.phocuswire.com/news/technology/expedia-group-acquires-ai-travel-planning-app-layla) |
| OpenAI acquired Odessia (10 Nov 2026); service closed | ✅ Confirmed. Davidson leads OpenAI travel; $6M Sequoia-led round; claimed $60M/yr planned travel | [Skift](https://skift.com/2026/11/10/a-year-after-sonders-collapse-francis-davidson-sells-his-ai-travel-startup-to-openai/), [PhocusWire](https://www.phocuswire.com/news/startups/openai-acquires-ai-travel-agent-odessia) |
| United bans unauthorised AI agents (11 Nov 2026) | ✅ Confirmed. Covers agents booking through travel agencies, even with user approval; AI may still *show* fares; Delta reportedly blocks agents technically | [Skift](https://skift.com/2026/11/11/united-airlines-moves-to-block-personal-ai-agents-from-booking-flights/), [PhocusWire](https://www.phocuswire.com/news/technology/united-blocks-third-party-ai-agents-from-app-website), [View from the Wing](https://viewfromthewing.com/united-airlines-ceo-scott-kirby-bans-ai-agents-from-booking-tickets-doesnt-want-another-middleman/) |
| Lola (Booking Holdings; Hafner and English) | ✅ Confirmed. No ads; Plus $5, VIP $25; US-only at launch; **later added flight booking and a planned $100M investment** | [PhocusWire launch](https://www.phocuswire.com/news/technology/steve-hafner-paul-english-launch-ai-assistant-lola), [PhocusWire flights](https://www.phocuswire.com/news/startups/bookings-lola-gets-flight-booking-capabilities-100-million-dollar-planned-investment) |
| EU Package Travel Directive revision | ✅ Directive (EU) 2026/1024 (29 Apr 2026), in the Official Journal; linked travel arrangements deleted; 24-hour linked online bookings with data transfer = package; ~28-month transposition | [EUR-Lex](https://eur-lex.europa.eu/eli/dir/2026/1024/oj), [HFW](https://www.hfw.com/insights/revision-of-the-package-holidays-directive-whats-changing/), [CMS](https://cms.law/en/aut/legal-updates/the-eu-package-travel-directive-is-no-longer-really-about-package-holidays.-it-is-increasingly-about-who-controls-the-customer-journey) |
| Amadeus Self-Service shut down (17 Jul 2026) | ✅ Confirmed. Enterprise unaffected; Amadeus later partnered with Anthropic for developers | [PhocusWire](https://www.phocuswire.com/amadeus-shut-down-self-service-apis-portal-developers), [Amadeus statement](https://amadeus.com/en/industry-messaging/statement-regarding-amadeus-for-developers-portal), [Skift](https://skift.com/2026/09/03/amadeus-brings-travel-tech-into-claude/) |
| Google AI Mode hotel booking (27 Aug 2026) | ✅ Confirmed. US/English; 10 partners; partner is merchant of record and handles service | [PhocusWire](https://www.phocuswire.com/news/technology/google-ai-mode-hotel-booking-agentic-flights-loyalty), [Hotel Dive](https://www.hoteldive.com/news/google-introduces-ai-mode-hotel-booking/829265/) |
| Fora $60M Series D at $1B (16 Jul 2026) | ✅ Confirmed. 15k+ advisors, $3B+ booked since 2021 | [Skift](https://skift.com/2026/07/16/fora-travel-the-unicorn-it-raised-60-million-at-a-1-billion-valuation/) |
| Greetwell survey: 55% hit a bad rec; 1 in 6 sent somewhere nonexistent | ✅ Confirmed. Caveat: commissioned, n=485 AI users, by a concierge company | [Stacker](https://stacker.com/stories/travel/survey-ai-hallucinated-travel-destinations-1-6-users), [Tripprof analysis](https://tripprof.com/en/blog/ai-travel-hallucination-survey/) |

Full source lists (several hundred URLs) are at the end of each raw report.
