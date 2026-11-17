# AI Trip Planning: State of the Art and Where to Win

**Date:** 17 Nov 2026
**Version:** v2. Rebuilt after a second, gap-filling research pass.
**Scope:** consumer AI trip planning, and the data, booking, legal, research and market layers under it.

---

## 0. How this was built, and how far to trust it

**Method**
- Seven research streams ran in two passes: about 140 searches in the first pass and about 350 in the second, which targeted every gap and every claim taken from memory.
- I re-checked the nine headline claims myself (§13).
- Full reports, about 70k words with several hundred source links, are in [`raw/`](raw/). Running notes with every URL are in [`notes/`](notes/).

| # | File | Covers |
|---|---|---|
| 01 | [AI-native startups](raw/01-ai-native-startups.md) | Mindtrip, Layla, Lola, Vayo, Odessia, Airial, Stardrift, Axel, Tryp.com, GuideGeek, Wanderlog, Holiwise, Stippl, Pilot, social-to-itinerary apps, Fora and Tern |
| 02 | [Incumbents and AI platforms](raw/02-incumbents-llm-platforms.md) | Google, ChatGPT, Perplexity, Copilot, Claude, Meta Muse, Apple, Expedia, Booking Holdings, Airbnb, Kayak, Tripadvisor, Trip.com, Hopper, Navan, Perk, Spotnana, Delta and American |
| 03 | [Hyperlocal data and freshness](raw/03-hyperlocal-data-freshness.md) | Hallucination incidents and rates, place data, editorial and taste data, events, entry rules, accessibility and safety data, transit, licensing, grounding, recommended data stack |
| 04 | [Booking infrastructure](raw/04-booking-interop-infra.md) | Flights, hotels, ground, activities and restaurant APIs; MCP servers; agent payments; post-booking; merchant-of-record models; accreditation paths; integration phasing |
| 05 | [Accountability and law](raw/05-accountability-support.md) | Competitor terms, *Moffatt*, UK CMA guidance, EU and UK package law, EU261 reform, US DOT, seller-of-travel laws, AI insurance, disruption technology, harm cases |
| 06 | [Traveller voice](raw/06-user-voice-reviews.md) | Adoption and trust surveys, ratings for 18 apps, 16 journalist tests, forum evidence, segments, willingness to pay, pain-point ranking |
| 07 | [Research frontier and market](raw/07-research-frontier-market.md) | Benchmarks, solver and reinforcement-learning results, architecture, FY2025 market sizes, funding, startups that died, commission rates, unit economics |

**Confidence: good on the headline facts and moderate on the long tail.**
- **Search snippets only.** Primary pages (vendor sites, arXiv, Reddit, Trustpilot, app stores) were blocked by this environment's network settings, so evidence comes from search-result snippets of official pages and trade press.
- **Tags.** Every claim in the raw reports is tagged [verified], [claimed], [inferred] or [recall/background]. In this report:
  - **✅** marks facts I re-checked independently.
  - *(claimed)* or *(estimate)* marks single-source or vendor figures.
- **No hands-on testing yet.** No product was tested hands-on; that's §12.

**Scoring rubric** used in every report:

| Dimension | Levels |
|---|---|
| **P**ersonalisation | P0 none · P1 form prefs · P2 in-session refinement · P3 persistent profile · P4 learns from behaviour, bookings, linked accounts |
| **G**ranularity | G1 city list · G2 day list · G3 time-slotted with hours · G4 + real transit, routing, buffers · G5 door-to-door incl. bookings and tickets |
| **B**ooking | B0 none · B1 affiliate links · B2 in-app, some verticals · B3 multi-vertical, one checkout · B4 + post-booking changes and refunds |
| **L**ive / on-trip | L0 none · L1 static · L2 companion chat · L3 real-time alerts · L4 automatic disruption re-plan and rebook |

---

## 1. Bottom line

**Nobody is the best AI trip planner today, because nobody combines all four things that matter:**
1. plans that are actually feasible and verified;
2. local, non-generic taste;
3. booking and managing across suppliers;
4. standing behind the trip when it breaks.

Each leader is strong on one or two of these and missing the rest:

| Leader | Strong on | Missing |
|---|---|---|
| Google | Data and personalisation (P4) | Accountability; popularity-ranked picks |
| Lola (Booking Holdings) | Multi-vertical booking (B3) and a paid human concierge | Neutrality across suppliers; routing detail |
| Mindtrip | Booking flights and hotels | Still invents places in tests; no guarantee |
| Airial | Transit routing (G4) | Booking |
| Navan, Delta, American | Automatic rebooking (L4) | Corporate travel or their own flights only |
| Fora | A human owns the trip | Not AI-native |

**The open position: the planner that stands behind its plan.**
- Every place, hour and connection is checked and timestamped.
- A solver guarantees the plan is feasible.
- Picks come with real, attributed local reasons.
- The whole trip is watched and repaired, wherever each part was booked.
- A human and an insured guarantee stand behind it.

**Every part already exists somewhere:**
- **Feasibility:** solver-backed planning passes 93.9% of a standard benchmark, against 0.6% for an AI model planning alone.
- **Freshness:** checking a place by phone costs about $0.10 a call.
- **Rebooking:** corporate travel tools and airlines already rebook automatically.
- **Guarantees:** insurers now write cover for AI errors.

No one has assembled these parts for leisure travellers. Pass 2 also confirmed the commercial key: **travellers won't pay for planning, but they do pay for certainty.**

### Twelve findings that shape the strategy

1. **The big companies bought or built the independent AI planners in 2026.**
   - Expedia bought Layla ✅.
   - OpenAI bought Odessia and shut it the same day, with users holding live bookings ✅.
   - Booking Holdings launched Lola ✅. Lola now books flights through Duffel ✅ and has a conditional $100M commitment. Booking's second agent, Vayo, books only restaurants so far.
   - Expedia retired its Romie assistant.
   - Mindtrip, the strongest independent, added flight booking (May, via Sabre) and hotel booking (Jul). It earned an estimated ~$3.6M in 2025 revenue *(estimate)*.
   *(01, 02, 07)*
2. **In 2026 the model became "plan in the AI, book with the brand".**
   - OpenAI pulled its in-chat checkout.
   - Google AI Mode books US hotels, but the partner stays the merchant of record ✅. Restaurant bookings hand off to the partner's page. Flights are tracking-only.
   - Usage is tiny:
     - LLM referrals are under 1% of Booking.com room nights.
     - OpenTable seated about 0.1% of its monthly diners through ChatGPT.
     - Uber reported 4 rides arranged by AI agents in Q3.
   *(02, 04)*
3. **Hallucination is mostly operational, not invented places.**
   - 55% of AI-using travellers hit a bad recommendation, and 1 in 6 were sent somewhere that doesn't exist ✅.
   - 43% of AI-planned days had a fault. 53% of the "closed that day" errors fell on a Monday.
   - **13 of 16 journalist and tester trials that reached a verdict found errors, and none judged a planner safe to use unchecked.**
   - The leading failures are closed venues, wrong hours and last departures, and impossible sequencing. Software can check all of these.
   *(03, 06)*
4. **Research has shown the fix, but no product ships it.**
   - Turning the request into a formal constraint problem and solving it reaches 93.9% on TravelPlanner, against 0.6% for an AI model planning alone.
   - A small model trained with reinforcement learning (Planner-R1) reaches 56.9%, against 21.2% for GPT-5.
   - The open frontier is real-world, preference-heavy requests (about 37%).
   - Group trips: under 12% valid plans even for the best agents.
   - Models "favor technically feasible but exhausting itineraries" (Trip+).
   - No consumer product claims solver-verified plans.
   *(07)*
5. **The good data is walled off, and licensing shapes the architecture.**
   - **Google:** no caching except place IDs, and no AI training on its data.
   - **Yelp** licensed its reviews to OpenAI (Jul 2026). **Tripadvisor** supplies Perplexity. **Reddit** is licensed to Google and OpenAI.
   - **Mapbox, HERE and TomTom don't give you a storable place database either** (a correction from pass 1).
   - **TikTok, Instagram and YouTube** have no commercial ingestion path.
   - **Lonely Planet, Time Out, The Infatuation and Michelin have no AI licensing deals yet**, so they are open to license.
   - **Implication:** build a base you own on open data (Overture, Foursquare's open set, OSM, tourism-board data), use Google live only to verify, and license the local layer.
   *(03)*
6. **The self-serve booking-API era is over, but a startup can still book everything except restaurants.**
   - **Duffel needs only identity checks:** Duffel itself is the licensed agent of record. It powers Lola's and Meta Muse's flights. It auto-handles airline schedule changes for only about 24 airlines.
   - **Other routes:** LiteAPI (hotels), Viator, GetYourGuide and Tiqets (activities), Distribusion and Trainline (rail, bus, ferry), Mozio (transfers).
   - **New routes:** Travelport's TripServices sandbox, and the Amadeus–Anthropic toolkit (waitlist only).
   - **Restaurants are the most closed vertical.**
   *(04)*
7. **Airlines are fighting unsanctioned agents while card networks build approved paths.**
   - United banned unauthorised AI agents (11 Nov), even when the user approves ✅. Delta reportedly blocks them technically.
   - Approved paths went live: Mastercard Agent Pay (Travelport) and Visa's Trusted Agent Protocol (eDreams).
   - Amex launched Agent Purchase Protection for wrong purchases by registered AI agents.
   - **Booking by driving consumer websites is a dead end.**
   *(02, 04, 05)*
8. **Accountability is still the emptiest space, and the law is moving toward it.**
   - Every consumer planner disclaims its advice.
   - The UK competition regulator (CMA) says a business answers for its AI agent "even if someone else designed" it ✅.
   - The revised EU Package Travel Directive turns linked multi-supplier online bookings into a "package" ✅, with the bundler legally responsible as organiser. Member states transpose it by about Sep 2028 and it applies from about 2029. The UK went the opposite way.
   - EU261 reform was adopted (claims window 9 months, airline reply within 30 days, from about late 2027).
   - Maryland now requires sellers of travel to carry $1M of errors-and-omissions insurance.
   - **AI-error insurance now exists** (Armilla/Lloyd's, Munich Re aiSure, Testudo), but **no travel company offers an accuracy guarantee.**
   - The first voluntary AI-error compensation found: United gave a $200 certificate.
   *(05)*
9. **Users want AI to plan and a human or a brand to answer for it.**
   - Only 6% fully trust AI. Two-thirds wouldn't let an AI book for them. 2% want full autonomy.
   - The trust ladder: suggest 53% > build itinerary 40% > restaurants and tours 38% > hotels 35% > flights 32%.
   - Comfort among 18–24s fell from 47% to 34%. 23% of US travellers avoid AI entirely.
   *(06)*
10. **Organisers are rated far above AI planners, and human-backed AI is rated highest.**
    - Wanderlog: 4.9 on the App Store from about 30K ratings. TripIt: 4.7 on Google Play from 93K.
    - AI-native apps have tiny review bases.
    - The best Trustpilot scores, Holiwise 4.9 and Layla 4.0, both sell a human in the loop.
    - Trustpilot complaints centre on billing traps.
    *(06)*
11. **Travellers won't pay for planning; they pay for certainty.**
    - 50% of US travellers say AI help should be free, and only 4% would pay a premium.
    - Paid planners cluster at $40–60 a year.
    - Meanwhile about half of Hopper bookings attach a paid protection product, and Flighty earns an estimated $400–500K a month from paid flight alerts.
    *(06)*
12. **The capital is going to AI plus accountable humans, and the climate is tightening.**
    - Fora is valued at $1B ✅. It is the only new travel unicorn of 2026.
    - Travel venture funding fell for two straight quarters, and AI rounds halved in Q3 2026.
    - Successful exits are acqui-hires (Odessia to OpenAI), OTA purchases (Layla to Expedia), or B2B and card-issuer deals (the original Lola, Mezi).
    - Travel apps keep about 2.8% of users at day 30.
    *(07)*

---

## 2. The landscape on one page

Rubric scores are from evidence, not hands-on testing. They were updated after pass 2.

| Product | Owner / status (Nov 2026) | P | G | B | L | What it does best | Biggest hole |
|---|---|---|---|---|---|---|---|
| **Google** (AI Mode, Ask Maps, Gemini) | Google | **P4** | G3–4 | B2 (US hotels via 10 partners; restaurants and events hand off; flights tracking only) | L2–3 | Best grounding (~300M places); itinerary inside Maps navigation; calls businesses for you | No liability; popularity-ranked; US-first |
| **ChatGPT** + partner apps | OpenAI (+ Odessia team) | P3 | G2–3 | B1 (partner apps; restaurants via OpenTable, Resy, Yelp) | L1–2 | Distribution; first place people ask | Pulled checkout; apps not in the EU; no servicing |
| **Lola** | Booking Holdings; US only | P3 | G2–3 | **B3** (hotels, dining, events, activities, flights via Duffel) | L2 | No ads or paid placement; $25/mo tier with human concierge (Ten Group) | Booking-family stock only; no hands-on reviews yet |
| **Vayo** | Booking Holdings (beta) | P4 (reads inbox) | G1–2 | B1–2 (restaurants only) | **L3** | Monitors bookings you already made | Monitors only; no re-plan |
| **Expedia** (+ Layla; Romie retired) | Expedia | P3 | G2–3 | **B4** | L2 | Hotels.com AI agent can service bookings; partners with every AI surface | Own inventory only; Layla still runs separately |
| **Mindtrip** | Independent (~$20M raised) | P3–4 | G3 | B2–3 (flights via Sabre; hotels via Expedia, Booking, Priceline, Agoda, Nuitee) | L2–3 | Map-first UX, group chat, social-to-plan, tourism-board distribution, memory | Invented hotels, wrong dates and hours in tests; no guarantee |
| **Airial** | Independent ($3M) | P2 | **G4** | B1 | L0–1 | Real multimodal logistics | No ticketing; web only |
| **Tryp.com** | Independent ($5.9M, Oct 2026) | — | G3–4? | B2–3 (multi-modal, claimed) | L2–3 ("Sandra" 24/7 AI) | Claims multi-modal booking plus companion | Thin evidence |
| **Wanderlog** | Independent | P1–2 | G3–4 | B1 | L1 | Best manual editor; 4.9 App Store from ~30K ratings | AI weak; billing complaints; AI only for the payer, not co-planners |
| **Stardrift / Axel** | YC | P3–4 / P2–3 | G2–3 / G1 | B1–2 / B2 | L2 / **L3** | Calendar-aware, live Amtrak prices / automatic price-drop refunds | Narrow |
| **Holiwise** | Pre-seed (UK) | P2–3 | G2–3 | B2–3 (packages) | L2 | Human concierge; Trustpilot 4.9; shows an ATOL number (unverified) | Small |
| **Trip.com TripGenie** | Trip.com | P3 | G3 | B3–4 (incl. rail, eSIM, attraction tickets) | L3 | Most complete incumbent stack | Weak on Western long tail; edits don't update bookings |
| **Hopper / HTS** | Hopper | P2 | G1 | B2–3 | **L3–4** | Rebooks you on any airline (Disruption Guarantee) | $35M FTC settlement over hidden fees |
| **Airbnb** AI agent | Airbnb (H1 2027) | — | — | — | — | Cross-platform, rich UI, group planning (promised) | Not shipped |
| **Apple Siri** (iOS 27, shipped Sep 2026) | Apple | P4 (on-device) | G1–2 | B0 | L2 | On-trip retrieval from Mail, Wallet, Maps | Can't book |
| **Navan / Perk / Spotnana** | Corporate | P3 | G3 | B4 | **L3–4** | Duty of care; 24/7 humans; Navan's Ava handles ~60% of interactions | Corporate only |
| **Delta / American** | Airlines | P2–3 | — | B4 (own flights) | **L4** | Automatic rebooking (American does it without asking) | Own flights only; documented errors |
| **Fora / Tern** (reference) | Human advisors | P4* | G5* | B4* | L4* | A licensed human owns the trip (*done by humans) | Doesn't scale to mass market |
| **Social-to-itinerary apps** (Plotline, Triply, feedtrip, Strollio…) | Early | P1–2 | G2–3 | B0 | L0–1 | Pull places out of TikTok and Reels | Commoditised; keep names, lose the reasons |

**Re-checked in Nov 2026: no AI-native consumer product reaches G4+, B3+ and L3+ at once.** G5 and L4 exist only where humans do the work, or for corporate travellers and an airline's own flights.

---

## 3. Problem by problem: state of the art, depth, ceiling, gap

### 3.1 Generic, cliché recommendations and no local knowledge *(01, 03, 06, 07)*

**How bad it is**
- 47% of dissatisfied AI users call the answers "too generic" (Simon-Kucher).
- Users report "the same TripAdvisor top 10" and that it's "good for finding tourist spots but doesn't do a great job planning".
- Older travellers use AI to organise trips, "not to determine destinations" (AARP).
- No user review was found praising a tool for knowing them.
- The real complaint is **the same canon for everyone, stitched together without judgement.**

**How the leaders approach it, and how deep it goes**

| Mechanism | Who | Depth / limit |
|---|---|---|
| Tourism-board first-party content | Mindtrip (Norway, Kentucky, Boston…), GuideGeek (NYC, Toronto, Colorado…) | Authoritative but promotional |
| Social-video ingestion | Mindtrip, Airial, ~8 apps, Tripadvisor demo | Extracts names, not reasons; no accuracy data; **no commercial ingestion path from TikTok, Instagram or YouTube** |
| Reviews at scale | Google (~500M contributors), Yelp→OpenAI, Tripadvisor→Perplexity | Popularity-ranked, which *is* the cliché problem; locked to the big AI labs |
| Licensed editorial | OpenAI has Eater, Food & Wine, Condé Nast | Big labs only; **Lonely Planet, Time Out, Infatuation and Michelin are unclaimed** |
| Taste graphs | Beli (120M+ ratings), Corner, Mapstr | Walled; no outbound APIs |
| Candid local advice | Reddit, licensed to Google and OpenAI | Walled off from startups |

**Ceiling today**
- Neighbourhood-level picks: partly served.
- Street and dish level: unserved.
- Time-of-day and seasonal nuance: unserved.
- Safety: neighbourhood scores exist only for businesses (GeoSure, used by TripIt).
- Nobody measures how generic their picks are.

**Gap to exploit**
- **Build a licensed, attributed, dated local-knowledge graph.** For each place, record why, when, for whom and what to order, sourced from:
  - revenue-share deals with the unclaimed guidebooks and with local newsletters;
  - a paid network of verified local experts;
  - tourism-board open data, such as France's DATAtourisme.
- **Make anti-cliché part of what the solver optimises**, with a published cliché rate.
- **Explain every pick from the user's own signals:** "because you saved X".

### 3.2 Poor booking interoperability *(04, 01, 02)*

| Vertical | Best AI-planner reality | Best startup access path now | Achievable depth |
|---|---|---|---|
| Flights | Mindtrip (Sabre), Lola and Meta Muse (Duffel) | **Duffel**: identity checks only, Duffel is agent of record; Travelport TripServices sandbox | Book + voluntary changes; auto-handles airline changes for ~24 airlines only; disruptions mostly manual |
| Hotels | Lola, Mindtrip Stays, Google AI Mode (partner merchant) | **LiteAPI** (self-serve, MCP), Duffel Stays (~1.6M), then Agoda, Expedia Rapid | Book + cancel + retrieve |
| Rail, bus, ferry | **Nobody among AI planners** (Trip.com in Asia; Tryp.com claims) | **Distribusion** (MCP), Trainline, Ferryhopper (MCP), Rail Europe, Busbud, 12Go | Book + after-sales |
| Transfers | Nobody | **Mozio** | Book + cancel |
| Activities | Lola, ChatGPT apps (hand-off) | **Viator**, **GetYourGuide**, **Tiqets** (free distributor API) | Book + cancel |
| Restaurants | Google AI Mode, ChatGPT (OpenTable, Resy, Yelp), Lola | Deep links; negotiate **TheFork** (EU) or **SevenRooms** (US); Tock's API can't create bookings | Mostly search and link-out |
| Vacation rentals | Expedia (Vrbo) | Vrbo via Expedia Rapid; **Airbnb has no API** | Book via Rapid |
| Bookings made elsewhere | Vayo, Lola, Wanderlog (read Gmail); TripIt API closed | Forward-to-address email parsing + AwardWallet; Gmail access needs an annual security assessment (about $550–15k) | **Can watch, can't change** |
| Flight status | — | **OAG** (self-serve) or FlightAware | Status + alerts |

**Where the ceiling is**
- Search is solved. Booking works one supplier at a time.
- **Managing bookings is the ceiling.** You can only change bookings made through your own channel, and even Duffel resolves airline schedule changes automatically for about 24 airlines only.
- Loyalty credentials are off-limits.
- **Gap:** door-to-door booking, including ground transport, on one timeline. An AI-native trip hub, since TripIt's API is closed. An approved-agent posture: official APIs, agent tokens, user approval for each purchase.

### 3.3 Stale data and hallucinations *(03, 06, 07)*

**How bad it is**
- **Greetwell survey:** 55% bad recommendation, 16% sent to a non-existent place ✅.
- **Vendor audit:** 43% of days had a fault.
- **Agency study:** errors in 90% of ChatGPT itineraries, including a breakfast booked at 08:00 at a café that opens at 12:00, and a museum closed until 2026.
- **Google Maps** missed about 27% of confirmed closures in a vendor test.
- **Mindtrip in tests:** invented hotels, trip dates "in the past" (Afar), invented weather numbers.
- **WSJ:** the same question gave different answers.
- **Incidents:**
  - Humantay "canyon" (Peru) and Weldborough "hot springs" (Tasmania; an operator's AI-written blog, ✅ verified in pass 2).
  - Mount Misen last ropeway (Japan).
  - "Unnecessary Mountain" hikers rescued (Canada).
  - A missed ESTA, leading to denied boarding.
  - Notion AI scheduled a "day trip" to a place several hundred km from the traveller's base.

**Failure classes:**
1. Stale status.
2. Wrong operating times.
3. Impossible sequencing.
4. Invented places.
5. AI-written content contaminating sources.

Classes 1–3 are fixed by data plus constraint checks, class 4 by tying every place to a real database ID, and class 5 by tracking sources.

**State of the art**
- **Google:** live status, phone calls to businesses, "may have changed" flags.
- **VOYGR:** closure and existence checks, now including hours, with phone calls at about $0.10 each. US-first.
- **Entry rules can be grounded today:** Sherpa°'s API covers visas, transit and vaccination, and VisaHQ has one too. A planner that gets visa rules wrong is choosing not to check.
- **Accessibility data exists:** accessibility.cloud/Wheelmap (open, about 1.3M places) and Google's four accessibility fields. WheelchairTravel.org documents AI giving accessibility advice that is a decade out of date.
- **Cable cars and funiculars:** the standard transit-feed format supports them, but operators rarely publish feeds. That is the Mount Misen gap.
- **Japan:** Google's transit API returns nothing there, so NAVITIME is the fallback.

**Ceiling.** Nobody shows users when a fact was last verified. Nobody publishes an accuracy benchmark. No consumer product documents a deterministic feasibility check.

**Gap to exploit**
1. **A freshness record for every fact** (value, source, when observed, how, confidence), shown to the user.
2. **A deterministic plan checker plus repair:** hours by weekday, last entry, travel time, buffers, holidays, daylight and pacing. Publish "0 infeasible days".
3. **A dataset of special services we own:** ropeways, funiculars, seasonal ferries, last departures, timed tickets, published as standard transit feeds.
4. **Reconfirmation** of critical stops 24–48 hours ahead by automated call. Outside the US this is uncovered.
5. **Traveller "it was closed" reports** that update the shared record for everyone.

### 3.4 No accountability or support *(05, 02, 04)*

**What competitors promise: almost nothing.**
- **Mindtrip:** "AS IS".
- **Layla:** the chatbot "cannot bind" anyone.
- **Kayak (1 Jul 2026 terms):** no accuracy guarantee for AI output.
- **Expedia AI terms:** information "the accuracy of which Expedia has not verified".
- **Google:** "the hotel or booking platform will handle the booking and any customer service" and has "no intention" of becoming a merchant of record.

**Advice liability, meaning whether the itinerary is right, is accepted by nobody.** Since 2026, AI *actions* are causing harm too:
- Delta's AI Concierge cancelled a member's whole award trip.
- American's system rebooks people onto wrong flights.
- United's text assistant confirmed a cancellation the customer had declined.

**Accountability matrix** (0–5; see 05 §8)

| Player | Advice | Transaction | Human | Disruption execution | Guarantee | Overall |
|---|---|---|---|---|---|---|
| ChatGPT / Gemini | 1 | 1 | 0 | 0 | 0 | **0.5** |
| Mindtrip, Wanderlog, GuideGeek | 1 | 1 | 1 | 0 | 0 | **~1** |
| Lola (VIP) | 1 | 3 | 3 | 1 | 1 | **~2** |
| Booking.com / Expedia | 1 | 3 | 3 | 2 | 2 | **~2.5** |
| Airbnb / Hopper | 1 | 3 | 2–3 | 2–4 | 3–4 | **~3** |
| Card travel desks | 2 | 3 | 4 | 3 | 4 | **~3.5** |
| Navan / Perk | 2 | 3 | 5 | 4 | 3 | **~4** |
| **Unoccupied** | **≥3** | **≥3** | **≥3** | **≥4** | **≥3** | consumer, AI-native |

**Gap to exploit**
- **An Itinerary Accuracy Guarantee.** Pay out up to a cap when a *checked* fact was wrong and cost the traveller money. It would be insurer-backed: Armilla, Munich Re aiSure and Testudo show the cover exists.
- **Watch and act.** Re-plan the whole downstream trip when something slips, with a human holding airline-system access for the cases automation can't handle.
- **Claims on autopilot** at 0%. The reformed EU261 makes in-app claims easier from late 2027 and squeezes the 30–35% claim agencies.
- **A continuity commitment**, after Odessia's shutdown.
- **Lesson from the FTC's Hopper case:** a support promise you miss is itself deceptive, so publish only response times you can keep.

### 3.5 Problems not on your list *(06)*

| Problem | Evidence | Implication |
|---|---|---|
| Subscription and billing traps | Trustpilot: Wanderlog 1.8, Stippl 2.9, Axel refund dispute | Honest pricing as a differentiator |
| Plan lives in a chat log, drifts, can't be reproduced | Revision drift; WSJ got different answers to the same question; freezes and loops | A structured, versioned plan; targeted edits; locked items |
| Over-packed, unrealistic days | ~7 sources ("replies tore it apart"; 9 stops a day); Trip+: "exhausting itineraries" | Pacing as a hard constraint; explicit trade-offs |
| Unreliable import of existing bookings | Wanderlog vs TripIt; TripIt import corrupting data | TripIt-grade parsing as table stakes |
| Group features locked to the payer | Wanderlog Premium AI covers the payer only | Every member gets the AI features |
| Products disappear | Romie retired; Odessia shut | A continuity promise |
| Commission bias | Booking's planner "ties you to own listings"; 57% want cross-brand assistants | Neutral, disclosed ranking |
| Trust erodes after use | 18–24 comfort down 13 points in a year | Retention depends on being right |
| Privacy worries | 40% of over-50 non-users and 48% of families cite privacy | Minimal data, clear consent |
| Some people want no AI | 23% of US travellers | A manual-first mode |

---

## 4. How deep the competition goes on each dimension

| Dimension | Best in market today | Who | What nobody does yet |
|---|---|---|---|
| **Personalisation** | P4: Google reads Gmail and Photos (opt-in); Vayo and Lola read inboxes; Apple uses on-device context; Mindtrip memory | Google, Booking Holdings, Apple, Mindtrip | Learning *taste* from past trips, saves and ratings as solver weights. Constraints that survive long conversations and are enforced (diet, mobility, pace). A portable profile the user owns. Fair handling of group preferences (best agents <12% valid group plans). |
| **Granularity** | G4: Airial, Wanderlog, Google Maps itineraries in navigation | Airial, Wanderlog, Google | **G5** door-to-door with tickets and buffers that re-flows on change; last-departure warnings; terrain, steps and heat; special services |
| **Control** | Wanderlog drag-and-drop; Mindtrip group chat | Wanderlog, Mindtrip | Locked items; hard vs soft constraints; "here's why not" with suggested relaxations; version history; two-way sync with Maps lists and Sheets; reproducible output |
| **Booking** | B3–4: Lola, Mindtrip (flights and hotels), Expedia, Trip.com, Navan | Booking Holdings, Expedia, Trip.com | **Neutral** multi-supplier booking including ground transport; managing bookings made elsewhere |
| **Live / on-trip** | L3 monitoring (Vayo, Axel, Mindtrip); L4 at Hopper, Navan, Delta and American | Hopper, Navan, airlines | **Consumer L4 across the whole itinerary**, with consent |
| **Grounding** | Google Maps (300M places, calls businesses) | Google | Visible freshness and confidence; a published accuracy rate; an attributed local corpus; grounded entry rules |
| **Accountability** | Lola VIP human concierge; Hopper guarantees; AirCover; Amex agent protection | Booking Holdings, Hopper, Airbnb, Amex | An accuracy guarantee on advice; one accountable party; free automated claims |

---

## 5. Market constraints that decide the design

1. **Data licensing.**
   - Own a base built on open data: Overture, Foursquare's open set, OSM, Wikidata, tourism-board data.
   - Use Google, Foursquare Premium and VOYGR live only, to verify and display.
   - License local and editorial content. Don't build on social video or aggregated reviews, both of which are locked to the big AI labs.
   - *(03)*
2. **Booking channels.**
   - Most of the trip can be booked without airline accreditation: Duffel, LiteAPI, Viator, GetYourGuide, Tiqets, Distribusion, Trainline, Mozio.
   - **Accreditation paths differ by market.** IATA's lighter TIDS registration isn't available in the US; ARC's Verified Travel Consultant credential is the US equivalent. Full airline ticketing needs ARC or IATA accreditation, or a host consolidator.
   - *(04)*
3. **Approved agents only.** No browser-driven booking. Use agent payment tokens (Mastercard, Visa), with explicit approval for each purchase. *(02, 04)*
4. **Package law decides checkout design.** *(05; lawyer needed)*
   - **EU:** linked online multi-supplier bookings become a package, from about 2029. The bundler becomes the organiser, with full liability and insolvency cover.
   - **UK, from Apr 2027:** one checkout makes you the organiser; a hand-off to another trader carries no package duty. ATOL is needed for flights; the levy is £2.50 per passenger, with reform pending.
   - **US seller-of-travel registration:**
     - California: $100 a year. It exempts sellers that forward all customer payments to a registered seller or ARC.
     - Florida: bond.
     - Washington and Hawaii: trust accounts.
     - Maryland: $1M errors-and-omissions insurance (from Oct 2026).
5. **Disclaimers don't protect you.**
   - *Moffatt* held the airline liable for its chatbot.
   - The CMA says the business answers for its agents.
   - The EU AI Act's chatbot-disclosure duty has applied since Aug 2026.
   - The EU Product Liability Directive covers AI software for injury from Dec 2026.
   - The FTC settled with Hopper for $35M over hidden fees and a support promise it didn't keep.
   - *(05)*
6. **The economics are thin.** *(07, 06)*

   | Line | Rate |
   |---|---|
   | Hotel affiliate | ~3–6% |
   | Activities | ~8% |
   | Flights | ~0% |
   | eSIM and insurance | ~10% |
   | Agentic plan cost | ~$0.10–2.00 per plan |
   | Retention | ~2.8% at day 30 |
   | Willingness to pay for planning | very low |

   Keep cost per plan under $0.20, monetise certainty and protection, and grow through partners and groups, not paid ads.
7. **General assistants are everyone's front door.** Be callable from ChatGPT, Claude, Gemini and Meta via MCP. *(02, 07)*

---

## 6. Threats over 12–24 months *(02)*

| Threat | Likelihood | Timing | What it closes | What stays open |
|---|---|---|---|---|
| Google adds flight booking and broader Personal Intelligence | High | 6–18 mo | Booking breadth, personalisation | Accountability, anti-cliché, neutrality |
| Airbnb AI agent (cross-platform, groups) | High | H1 2027 | Taste, experiences, group UX | Ground transport, accountability beyond Airbnb |
| Lola scales: flights live, $25 human concierge, $100M | Med–High | 6–18 mo | AI plus human at consumer scale | Neutrality, routing, Europe |
| Expedia: Hotels.com servicing agent plus Layla | Med–High | 12–24 mo | Own-inventory servicing | Neutrality; Romie gone, so no group or disruption layer |
| Meta Muse takes a cut at WhatsApp scale (Expedia hotels, Duffel flights) | Medium | 6–18 mo | Distribution | Servicing, accountability |
| OpenAI travel product (Odessia team) | Medium | 12–24 mo | Distribution plus agency know-how | Data rights, local layer, servicing |
| Apple Siri on-trip | Medium | now–12 mo | On-trip retrieval on iPhone | Planning, booking, accountability |
| More airlines block agents | Medium | Ongoing | Unapproved booking paths | Official-API routes |

**Our position has to hold even if Google and Airbnb win distribution.** Neither will take liability for advice, publish a cliché rate, rank neutrally, build a licensed local corpus, or repair trips booked elsewhere.

---

## 7. Where to win: the strategy

### 7.1 Positioning

> **"The trip planner that stands behind its plan."**
> Verified. Local. Repaired when it breaks. Guaranteed.

| Pillar | Answers | Mechanism | Why incumbents won't copy it quickly |
|---|---|---|---|
| **1. Verified plans** | Hallucination, staleness, over-packing | The solver guarantees feasibility (hours, transit, buffers, budget, pacing); a timestamp on every fact; entry rules grounded via Sherpa°; "here's why not, and what to relax"; 24–48h reconfirmation | Google ranks by popularity and won't certify; OTAs optimise conversion |
| **2. Real local taste** | Cliché | Licensed corpus from the unclaimed guidebooks and local networks; anti-cliché solver objective; published cliché rate; "why this, for you" | Labour, licensing and editorial stance; the labs' data deals are review-heavy, not local-expert |
| **3. Whole-trip watch and repair** | Interop, accountability | Import every booking; monitor; minimal-change re-plan of the knock-on effects; approved-API booking incl. ground (Distribusion, Trainline, Mozio) | OTAs only repair their own bookings; Google and OpenAI won't do servicing |
| **4. Someone accountable** | Accountability | Insurer-backed accuracy guarantee; human escalation with only response times we can keep; 0% compensation claims; continuity promise | They avoid liability; regulators watch "guarantee" claims; it needs real operations |

### 7.2 Product principles

1. **Planning is free; certainty is what we sell.** 50% expect AI help free; half of Hopper bookings buy protection *(06)*.
2. **Climb the trust ladder.** Users approve every purchase. Start booking with restaurants and tours, then hotels, then flights *(06)*.
3. **The plan is a structured object, not a chat log.** Version history, locked items, targeted edits, the same input giving the same plan, sync with Maps lists and Sheets, export anytime *(06)*.
4. **The language model narrates; the solver decides.** Constraints live in a typed store and are re-checked every turn *(07)*.
5. **Show uncertainty.** "Verified 2 days ago by phone" or "unverified, check before going". Cite and date local sources *(03, 05)*.
6. **Repair, don't regenerate.** Bookings are fixed; disruption triggers a minimal-change re-solve *(07)*.
7. **Groups are first-class.** Every member gets the AI. Budgets are set up front. Voting, fair splitting and settlement are built in *(06)*.
8. **Neutral and honest.** No paid placement in the ranking. No trial traps *(06)*.
9. **Approved channels only.** Never ask for loyalty passwords *(04)*.
10. **Privacy-minimal, with a manual-first mode** for the 23% who avoid AI *(06)*.

### 7.3 Segments to win first

The evidence points to where generic AI fails worst and the stakes are highest:
- **Complex multi-city and overland trips by rail (Europe, Japan).** These have the highest failure rates, and ground transport is the most under-served booking vertical.
- **Groups.** The pain is money and decisions: 39–48% worry about fair splitting, and only about a quarter set a budget in advance. No AI planner handles this, so it's a viral wedge.
- **Identity- and safety-driven travellers.**
  - 66% of LGBTQ+ travellers use AI, 76% of trans travellers, and the top reason is checking safety and legal rights.
  - Women use AI but trust it less.
  - Accessibility data is stale.
  - A sourced, dated, human-reviewed fact layer wins here (Sherpa°, GeoSure, accessibility.cloud).

**Recommended beachhead (my judgement): US travellers planning multi-city Europe trips with rail.**
- **Booking coverage:** Duffel, LiteAPI, Distribusion, Trainline, Viator and GetYourGuide cover the whole trip without airline accreditation.
- **Regulation:**
  - US seller-of-travel rules are manageable: California's forward-all-funds exemption, Maryland's insurance requirement.
  - Selling to US residents may limit EU package-law exposure, and the EU rules don't apply until about 2029 anyway. **Lawyer needed.**
- **Visible advantage:** transfer and feasibility checking show clearly against every competitor, and Lola, Google AI Mode hotel booking and ChatGPT apps are weak in Europe.
- **Group-first features** spread the product through each trip's co-travellers.
- **Next: Japan.** Interest is high and failures are notorious. Plan around NAVITIME for transit and resellers for rail.

### 7.4 Distribution

- **Standalone app/web**, where the structured plan, the group and trip-watching live.
- **Our own MCP endpoint,** so ChatGPT, Claude, Gemini and Meta can call the verified planner and trip protection.
- **B2B channels:**
  - Tourism boards: they want visitors dispersed, which matches anti-cliché.
  - Card issuers: Amex already sells agent-purchase protection, and Citi wants agents to carry liability.
  - Human advisors: Fora and Tern show AI multiplies them.

---

## 8. Reference architecture *(03 + 07)*

```
CONVERSATION (frontier LLM): elicit · narrate · explain from solver state · cite sources
        │ typed TripSpec                                     ▲ plan + trace + provenance
CONSTRAINT & PREFERENCE STORE (hard/soft, priority, owner/member, source turn; persisted; re-checked each turn)
        │
CANDIDATES: retrieval over Place Graph + licensed local corpus; LLM scores fit; popularity-debias
        │
SOLVER: CP-SAT/MILP (orienteering w/ time windows) + SMT for UNSAT cores → minimal relaxations;
        repair mode = freeze bookings, minimal-change re-solve; group fairness (least-misery + rotation);
        pacing/fatigue soft constraints; deterministic seeds → reproducible plans
        │
VERIFIER (independent): hours × weekday × last-entry × travel time × buffers × holidays × daylight × pacing;
        entity existence; freshness TTL re-fetch before display/booking; entry rules per passport
        │
DATA LAYER
  L0 Place Graph (owned): Overture GERS IDs + Foursquare OS Places + Wikidata + DATAtourisme/ATDW/Tokyo open data
     (+ OSM in a separate ODbL layer); store only external IDs for Google/Yelp/Apple. NOT Mapbox/HERE/TomTom POIs.
  L1 Live (display-only): Google Places status/hours/accessibility · Foursquare Premium · VOYGR (US) · BestTime · Fever
  L2 Freshness ledger: {field, value, source, observed_at, method, confidence} + closure detectors
     + voice-agent reconfirmation of booked/critical stops (~$0.10/call)
  L3 Licensed local corpus: Lonely Planet / Time Out / Infatuation / Michelin-type deals, newsletters, Atlas
     Obscura-style rev-share, own local-expert network; dated, attributed, place-linked, AI-content filtered
  L4 Ops: GTFS/GTFS-RT (Mobility Database) → OTP/MOTIS; Google Routes fallback; NAVITIME (Japan);
     Distribusion/Trainline/Ferryhopper/12Go inventories; SPECIAL SERVICES table as GTFS route_type 6/7;
     events (PredictHQ free tier, Ticketmaster user-driven, Fever, DATAtourisme); weather/daylight
  L4b Trip rules: Sherpa° (entry/visa), State Dept + GeoSure (safety), accessibility.cloud + Google + OSM
        │
ACTION LAYER: approval gates · Duffel / LiteAPI / Viator / GYG / Tiqets / Distribusion / Mozio · agent-token payments
        · forward-to-email importer · OAG status + Duffel change webhooks → repair triggers → human desk
TRUST LAYER: immutable log of what we said/showed · insurer-backed accuracy guarantee · claims autopilot
EVAL HARNESS: TravelPlanner/ChinaTravel/TripCraft/GroupTravelBench/τ-bench regression · real-city sandbox ·
        user simulator (multi-turn, group, unsolvable) · pass^k · infeasible-day rate · cliché/novelty ·
        human-calibrated judge · prod: edit rate, on-trip deviation, complaint/refund rate
```

**Cost control**
- Small reinforcement-trained models (Planner-R1 style) handle tool orchestration. Frontier models only elicit and narrate.
- Cache heavily, and let the solver do the combinatorics.
- Target under $0.20 per plan, including maps calls.

---

## 9. Business model *(05, 06, 07)*

| Revenue line | Role | Evidence |
|---|---|---|
| **Free planning** | Acquisition | 50% expect AI help free; paid planners stall at $40–60/yr |
| **Trip Protection** (per trip ~$29–79, or ~$10–20/mo for frequent travellers): watch and repair, human escalation, accuracy guarantee, claims autopilot, price-drop recovery | **Core revenue; funds accountability** | Hopper: about half of bookings attach protection; Flighty ~$400–500K/mo from alerts *(estimate)*; Lola VIP $25/mo; travel trial-to-paid ~43% (RevenueCat, secondary). *Prices are my hypotheses; test them.* |
| Activities and hotel commissions | Base | Activities ~8%, hotels ~3–6% |
| Embedded insurance, eSIM, parametric delay cover | High margin | ~10% affiliate; distributor shares are higher with licensing |
| B2B: tourism boards, card issuers, advisors | Durable | Mindtrip and GuideGeek prove tourism boards pay; Amex and Citi signal liability-shifting demand |
| Merchant-of-record packaging (later) | Highest margin | Brings package law, ATOL and chargeback exposure; one market at a time |
| Ads / sponsored placement | **Avoid** | Destroys the trust position |

**Failure modes to design around:** infrequent travel, ~2.8% day-30 retention, thin affiliate fees, model cost above revenue, paid acquisition.

**Retention levers:** on-trip and disruption value, group virality, everyday "hometown" use between trips (Lola's thesis), and continuity of the user's trip data.

---

## 10. Phased plan

| Phase | Weeks | Build | Prove |
|---|---|---|---|
| **0. Evidence** | 0–3 | Hands-on teardown (§12); eval harness; an "infeasible-day" and cliché benchmark across ChatGPT, Gemini, Mindtrip, Lola, Airial, Wanderlog | A public accuracy benchmark is itself marketing |
| **1. Verified planner** | 3–12 | Place Graph on open data, freshness ledger, solver + verifier, structured group plan editor, Maps-list import, Sherpa° entry rules; one corridor (e.g. Paris–Amsterdam–Berlin rail) | Zero infeasible days; cliché rate well below competitors; group usage |
| **2. Book and watch** | 12–24 | Duffel, LiteAPI, Viator, GetYourGuide, Tiqets, Distribusion/Trainline; Travelport sandbox; email importer; OAG + change webhooks; approval-gated checkout; seller-of-travel registrations incl. Maryland E&O | First paid bookings; first repaired disruptions |
| **3. Stand behind it** | 24–40 | Insurer-backed accuracy guarantee (Armilla/Munich Re-type); human desk via partner agency; claims autopilot; our own MCP endpoint | Guarantee loss ratio; containment rate; NPS during disruption; protection attach rate |
| **4. Expand** | 40+ | Japan; licensed local corpus at scale; tourism-board B2B; organiser status or ATOL in one market before EU application (~2029) | Unit economics per trip |

---

## 11. What's still unknown after two passes

Most of what remains needs primary pages or hands-on access, not more searching.
- **Reddit thread text and official app-store pages:** reddit.com and the stores are blocked here.
- **Hands-on tests not found:** The Verge, Wired, CNET, Condé Nast Traveler and The Points Guy.
- **Unresolved competitor details:**
  - Holiwise's ATOL number (check the CAA register).
  - Axel's real price.
  - Who is merchant of record for Mindtrip Stays.
  - Whether Vayo books flights and hotels yet.
  - Lola Plus status (one report says it ended 5 Nov).
- **Booking access:** Duffel Stays approval steps; the primary text of Booking.com's AI-approval clause; whether Nexion, KHM or Travel Leaders host agencies allow API booking; the Klook reseller API.
- **Legal primary texts:** Official Journal texts for the package-law, EU261 and AI Act dates; Visa/Mastercard agent-liability rule text; full Amex Agent Purchase Protection terms; Washington's fee; Nevada and Iowa.
- **Market numbers:** official affiliate rate cards (behind logins); a published cost per itinerary (none exists); funding for Axel, Stardrift and Pilot.
- **Data access:** pricing for GeoSure, Safeture and Timatic for startups; the TravelEval "collapse" wording.
- **"Boardwalk"** probably doesn't exist; it wasn't found in two passes.

---

## 12. Hands-on teardown (for when you have your laptop)

**To unblock:**
- **Allow sites:** under the cloud environment's **Network access** settings, allow mindtrip.ai, layla.ai, lola.com, airial.travel, tryp.com, stardrift.ai, wanderlog.com, wonderplan.ai, apps.apple.com, play.google.com, reddit.com, trustpilot.com and arxiv.org.
- **Then I drive them:** I can run their logged-out flows in a headless browser and record what they request and return.
- **Or use accounts:** you create accounts and run the test set below while I score the results.

**Test battery** (the same prompts for every product):
1. **Monday trap:** 3 days in Paris starting Monday, museums. Does it put the Louvre (closed Tue) or Orsay (closed Mon) on a closed day?
2. **Last departure:** sunset on Mount Misen, then dinner in Hiroshima. Does it know the last ropeway and ferry?
3. **Closed venue:** a restaurant known to have closed in 2025–26.
4. **Impossible request:** Tokyo, Kyoto, Osaka, Hiroshima and Hakone in 4 relaxed days. Does it say no and offer trade-offs?
5. **Constraints across turns:** vegetarian + wheelchair + $150/night in turn 1, then add 8 more preferences. Do the first ones survive?
6. **Group of 4 with conflicting preferences:** fairness, budget, cost splitting, and whether co-planners get the AI.
7. **Entry rules:** Spanish passport flying to Puerto Rico. Does it mention ESTA?
8. **Rail stitch:** Amsterdam → Paris → Barcelona by train with tickets. Real trains, buffers, can it book?
9. **Disruption:** "My Lisbon flight is 5h late." Does it re-plan the hotel, dinner and tour, and cite EU261?
10. **Cliché:** "Been to Rome twice; show me what locals do." Count the picks from the top 20.
11. **Reproducibility:** run test 1 twice. Does it give the same plan?
12. **Identity safety:** a same-sex couple to Dubai, then Bali. Are legal and safety facts sourced and dated?

---

## 13. Facts I re-checked independently

| Claim | Result | Source |
|---|---|---|
| Expedia acquired Layla (Jul 2026) | ✅ Layla keeps operating standalone | [Expedia IR](https://ir.expediagroup.com/news-and-events/news/news-details/2026/Expedia-Group-acquires-Layla-accelerating-its-AI-powered-trip-planning-and-booking-strategy/default.aspx), [PhocusWire](https://www.phocuswire.com/news/technology/expedia-group-acquires-ai-travel-planning-app-layla) |
| OpenAI acquired Odessia (10 Nov 2026); service closed | ✅ Davidson leads OpenAI travel; $6M Sequoia-led | [Skift](https://skift.com/2026/11/10/a-year-after-sonders-collapse-francis-davidson-sells-his-ai-travel-startup-to-openai/), [PhocusWire](https://www.phocuswire.com/news/startups/openai-acquires-ai-travel-agent-odessia) |
| United bans unauthorised AI agents (11 Nov 2026) | ✅ Covers agents booking through travel agencies, even with the user's approval; AI may still *show* fares; Delta reportedly blocks them technically | [Skift](https://skift.com/2026/11/11/united-airlines-moves-to-block-personal-ai-agents-from-booking-flights/), [PhocusWire](https://www.phocuswire.com/news/technology/united-blocks-third-party-ai-agents-from-app-website) |
| Lola (Booking Holdings) | ✅ No ads; Plus $5, VIP $25; US-only; later added flights and a $100M commitment | [PhocusWire launch](https://www.phocuswire.com/news/technology/steve-hafner-paul-english-launch-ai-assistant-lola), [PhocusWire flights](https://www.phocuswire.com/news/startups/bookings-lola-gets-flight-booking-capabilities-100-million-dollar-planned-investment) |
| Revised EU Package Travel Directive | ✅ Directive (EU) 2026/1024 in the Official Journal; linked travel arrangements deleted; ~28-month transposition | [EUR-Lex](https://eur-lex.europa.eu/eli/dir/2026/1024/oj), [CMS](https://cms.law/en/aut/legal-updates/the-eu-package-travel-directive-is-no-longer-really-about-package-holidays.-it-is-increasingly-about-who-controls-the-customer-journey) |
| Amadeus Self-Service shut (17 Jul 2026) | ✅ Enterprise unaffected; Anthropic developer partnership followed | [PhocusWire](https://www.phocuswire.com/amadeus-shut-down-self-service-apis-portal-developers), [Skift](https://skift.com/2026/09/03/amadeus-brings-travel-tech-into-claude/) |
| Google AI Mode hotel booking (27 Aug 2026) | ✅ US/English; 10 partners; partner is merchant of record | [PhocusWire](https://www.phocuswire.com/news/technology/google-ai-mode-hotel-booking-agentic-flights-loyalty), [Hotel Dive](https://www.hoteldive.com/news/google-introduces-ai-mode-hotel-booking/829265/) |
| Fora $60M Series D at $1B (16 Jul 2026) | ✅ 15k+ advisors, $3B+ booked | [Skift](https://skift.com/2026/07/16/fora-travel-the-unicorn-it-raised-60-million-at-a-1-billion-valuation/) |
| Greetwell: 55% bad rec, 1 in 6 sent somewhere nonexistent | ✅ Commissioned survey, 485 AI users | [Stacker](https://stacker.com/stories/travel/survey-ai-hallucinated-travel-destinations-1-6-users), [Tripprof](https://tripprof.com/en/blog/ai-travel-hallucination-survey/) |

**Corrections pass 2 made to pass 1 (all fixed in the raw reports):**
- **Funding and deals:** Perk was valued at $2.7B, not $1.4B. Amex GBT bought CWT for about $540M. Layla bought Roam Around in Feb 2024.
- **Research:** DeepTravel comes from HKUST(GZ) and DiDi, not Alibaba's Amap. TTG's 91% is translation accuracy, not plan accuracy.
- **Hopper:** the penalty was a US FTC settlement of $35M; no Canadian penalty was found.
- **Regulation:** EU261 reform is adopted.
- **Competitors:** Vayo books only restaurants. There is no GuideGeek spin-out.
- **Booking infrastructure:** Duffel auto-handles airline changes for about 24 airlines only. CarTrawler is now Expedia's.
- **Data layer:** Mapbox, HERE and TomTom don't offer a storable place base. VOYGR now covers opening hours.
- **Booking.com quote:** the "<1% of room nights" line came from the CFO.
