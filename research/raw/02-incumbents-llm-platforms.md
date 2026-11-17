# 02: Incumbents and General-Purpose AI Platforms in AI Trip Planning (state as of 17 Nov 2026)

**Scope:** general AI platforms (Google, OpenAI, Perplexity, Microsoft, Anthropic, Meta, Apple), OTAs and metasearch (Expedia, Booking Holdings, Airbnb, Kayak, Skyscanner, Tripadvisor, Trip.com, Hopper, Agoda, Priceline, Klook, Viator, GetYourGuide), corporate travel (Navan, Perk, Spotnana, Amex GBT/Egencia, SAP Concur, Ramp/Brex), and airline and hotel concierges.

**Method and limits.** Everything here comes from web search result snippets and summaries. WebFetch could not reach primary domains from this container (phocuswire.com, geekwire.com, blog.google and techcrunch.com all failed DNS), so I could not read full primary articles. The shared search budget also ran out before I could check Tripadvisor's 2026 strategy, Google AI Mode's restaurant-booking partners, or Airbnb Experiences in detail. Those gaps are marked **[prior knowledge, not re-verified]**.

**Gap-fill pass (17 Nov 2026).** A second pass ran 58 shared-budget web searches across files 01 and 02, again with no WebFetch. Raw notes are in `research/notes/01-02-gapfill-notes.md`.
- It **resolved all three [prior knowledge] items**: Google AI Mode restaurant partners, Airbnb Experiences, and the Tripadvisor 2026 strategy.
- It added 2026 facts on Google AI Mode flights and Chrome auto browse, Expedia's Fall 2026 release and Romie's retirement, Kayak Ask AI, Trip.com TripGenie, Meta Muse, Apple iOS 27, Airbnb's Q3 call, and consumer auto-rebooking by airlines.
- It corrected Vayo's booking status.
- Perplexity, Microsoft Copilot and Hopper's consumer app produced **no 2026 travel news**. That absence is noted rather than filled with older facts.

Evidence tags:
- **[verified]**: several independent outlets or a primary source agree.
- **[claimed]**: the vendor's statement, or a single outlet.
- **[inferred]**: my own analysis.

Most coverage is trade press (Skift, PhocusWire, earnings transcripts). Many blog sources had inconsistent dates and I treated them with caution.

---

## 1. Executive picture

1. **Plan in the AI, book with the brand.** In 2026 the market settled on this model [verified]:
   - **OpenAI** pulled back Instant Checkout in early March 2026 and moved transactions to partner apps inside ChatGPT.
   - **Google** launched agentic hotel booking in AI Mode on 27 Aug 2026, but Google is **not merchant of record**. The partner handles service, changes and refunds.
   - **Meta Muse + Expedia** (live Nov 2026) books, but does **not** handle cancellations or rebooking. Meta calls travel "a top use case" for Muse and wants a cut of transactions [verified, Skift 21 Oct 2026].
   - **Expedia's CEO:** agents are "strongest in discovery", and travelers still book with trusted brands.
   - **Booking Holdings:** LLM referrals are "significantly less than 1%" of Booking.com room nights.
2. **Nobody owns the trip end to end.** General AI platforms deliberately avoid liability (no merchant of record, no servicing). OTAs own servicing but only for their own inventory. Corporate tools (Navan, Perk, Spotnana, Egencia) are the only segment with real duty of care, policy logic, 24/7 human escalation and automated disruption rebooking. They are B2B-only.
3. **OTAs are consolidating AI planners.**
   - Expedia bought **Layla** (31 Jul 2026) and moved from the single Romie concierge, now reportedly retired, to specialised "point agents". Its Fall 2026 release shipped 30+ AI features, including an end-to-end Hotels.com AI agent.
   - Booking Holdings launched **Lola** (29 Sep 2026), a separate service run by Kayak co-founders Hafner and English.
     - It books hotels, restaurants, events and activities in chat, and **now flights (via Duffel)**.
     - Memberships are $5 and $25/month.
     - It is US-only and backed by a conditional **$100M commitment**.
   - Booking Holdings is also testing **Vayo** in private beta. Vayo has the same $100M commitment and books only restaurants so far.
   - Priceline rebuilt **Penny** on Claude (Jun 2026), with flight purchase inside the conversation.
   - Airbnb plans a standalone AI travel agent for **H1 2027** that is "not limited to Airbnb's platform".
4. **Suppliers are starting to resist agents.** United Airlines changed its contract of carriage on 11 Nov 2026 to ban unauthorised third-party AI agents from making, modifying or servicing tickets [verified: Bloomberg, WaPo, Forbes, TechCrunch]. Delta and American did not follow. Bank of America warned customers not to share credentials with AI assistants. Delta's own AI Concierge wrongly cancelled a passenger's ticket (Aug 2026). Agentic booking through scraped consumer sessions is becoming legally and technically fragile.
5. **Hallucination and staleness are still unsolved for general LLMs.** Documented 2025–26 incidents:
   - "Sacred Canyon of Humantay" in Peru, which does not exist.
   - Wrong last-cable-car time on Mount Misen, Japan; travelers were stranded.
   - Invented "Weldborough Hot Springs" in Tasmania.
   - Informal 2026 tests show Gemini, ChatGPT and Grok itineraries with closed venues, wrong drive times and missed seasonality.
   - A Greetwell survey of 1,000 US adults (Sep 2026) found **1 in 6** AI-using travellers had been recommended a place or tour that does not exist. 55% hit at least one bad recommendation, most often wrong prices or hours [verified, Stacker syndication].

   Google is the best-grounded general platform because of Maps' roughly 300M places and reviews from about 500M contributors. Even so, it gives no accountability when it is wrong.

---

## 2. General-purpose AI platforms

### 2.1 Google: Gemini app, AI Mode in Search, Maps (Ask Maps), Flights/Hotels

**What it does today**

- **AI Mode in Search: hotel booking** [verified: Skift 27 Aug 2026, SEJ, PhocusWire, Hotel-Online]
  - Launched 27 Aug 2026. US only, English, 18+, US billing address, select properties.
  - The "Continue on Google" flow uses Google Pay.
  - Ten partners: Booking.com, Expedia, Hotels.com, Priceline, Trip.com, Choice, Hilton, IHG, Marriott, Wyndham.
  - **Google is not the merchant of record.** The partner handles customer service, changes and refunds.
  - Google passes partners only the minimum booking data (name, payment, occupancy, property) and keeps the chat context and inspiration signals [claimed, Skift].
  - Google says ads do not currently influence AI Mode hotel rankings [claimed].
  - Independent hotels were not in the launch set [verified, Hotel-Online].
  - Re-checked mid-Nov 2026: **still US-only and English-only**. No country expansion was found [verified absence].
- **AI Mode: flights** (27 Aug 2026 update) [verified: TechCrunch, View from the Wing, PhocusWire]
  - Searches options across 300+ airlines and travel sites.
  - Price tracking is available in 180+ countries and territories, **excluding the EEA**.
  - Shows **loyalty-points prices** with launch partners Alaska, Hawaiian and American. Lufthansa Group, LATAM and Flying Blue (and Accor and Hyatt on the hotel side) are "coming".
  - Award bookings hand off to the airline to redeem.
  - **No in-chat flight purchase confirmed.** Google first flagged direct flight booking as a future plan in Nov 2025.
- **AI Mode: restaurants, event tickets, local appointments** [verified: Google blog Aug and Nov 2025, TechRadar, GSMArena, Engadget, SEJ]
  - Launch partners (Aug 2025): **OpenTable, Resy, Tock** for dining; **Ticketmaster, StubHub, SeatGeek** for events; **Booksy** for appointments. This confirms the earlier prior-knowledge list.
  - Launched for US AI Ultra subscribers in Labs, then expanded to more US users in Nov 2025. Restaurants are broadly available; events and beauty/wellness appointments still need Labs.
  - **Mechanism:** Google's own post says AI Mode checks real-time availability across reservation sites and **links to the partner's booking page so the user takes the last step**. It is a guided hand-off, not a Google-completed booking. Some secondary reports say "it makes the booking for you", but Google's wording is the more reliable source.
- **Chrome auto browse** (28 Jan 2026, Gemini 3) [verified: Google blog and support page, Bloomberg]
  - An agent in Chrome that can research hotel and flight prices across date options and **find and book accommodation** on third-party sites.
  - Asks for confirmation before sensitive actions. Labelled experimental ("can make mistakes").
  - Launched for US AI Pro and Ultra subscribers.
  - Secondary reports (Jul 2026) say the long-running "Gemini Spark" agent now uses auto browse [claimed].
  - This is Google's browser-agent route, separate from the partner-API route in AI Mode. It is exposed to the same supplier pushback as Comet (see United, §5).
- **AI Mode Canvas.** Trip-plan workspace for US Labs users (Nov 2025) [verified].
- **Personal Intelligence**
  - Opt-in linking of Gmail, Photos, Search history and YouTube to Gemini. Beta launched 14 Jan 2026 for US paid users. Added to AI Mode on 22 Jan 2026. Expanded to all US users in Mar 2026 and to Japan in Apr 2026 [verified: 9to5Google, TechCrunch, Google blog].
  - Google's own example: AI Mode reads your hotel booking in Gmail and travel memories in Photos to build an itinerary.
  - Google says Gemini does not train directly on your Gmail or Photos.
  - **This is the strongest P4 personalisation capability on the market.**
- **Ask Maps (Gemini in Google Maps)**
  - Launched 12 Mar 2026 in the US and India. Went global with an EEA/UK rollout in Aug 2026 [verified: CNBC, TechCrunch, 9to5Google].
  - The Aug update added Personal Intelligence, real-time transit, agentic food ordering and hotel discovery [claimed, 9to5Google].
  - **16 Nov 2026 update** [verified: Neowin, AndroidHeadlines and others]:
    - multi-day itineraries with numbered map pins;
    - itinerary available inside navigation ("pull up my itinerary as I head out");
    - real-time travel tips;
    - live availability checks on saved lists (e.g. "table for 5 within 30 min");
    - export to Google Docs and shareable lists;
    - **Google calling businesses on the user's behalf** to find appointments.
  - Grounding: more than 300M places, reviews from about 500M contributors, and more than 2B monthly Maps users [claimed via GSMArena and MacRumors, citing Google].
- **Gemini app**
  - Plans trips using Maps, Flights and Gmail.
  - "Agent Mode" in Gemini 3.1 (Mar 2026) and a long-running agent reportedly called "Gemini Spark" can drive browsers and fill booking forms [claimed; demo-grade coverage]. Chrome auto browse (above) is the shipped version of this capability [verified].
  - A 2026 guide says Gemini's own help page lists that it **cannot book, cancel, check in or set alerts**. Booking happens in AI Mode instead [claimed].
  - Gemini Gems can act as persistent trip-planner personas.
- **Google Flights "Flight Deals"**
  - Natural-language deal search ("a week somewhere warm in March under $500").
  - US/CA/IN first, then global from Nov 2025 [verified, TechCrunch 17 Nov 2025; older].

**Rubric**

| Dimension | Score | Evidence |
|---|---|---|
| Personalisation | **P4** (opt-in) | Personal Intelligence uses Gmail bookings, Photos history, Maps saves |
| Granularity | **G3–G4** | Maps itineraries with pins and live availability; Maps has real transit data, but tests show drive-time and seasonality errors in Gemini output |
| Booking | **B2** | Hotels completed in-flow via Google Pay (10 partners, US only); restaurants, events and appointments are guided hand-offs to partner pages; flights are search, points and tracking only; Chrome auto browse can book on third-party sites (experimental); no unified checkout across verticals |
| Live/on-trip | **L2–L3** | Itinerary inside navigation, real-time tips, Flights price tracking; no disruption re-planning |
| Data grounding | Best of the general platforms | Maps POI graph (hours, popular times, reviews), Flights/Hotels feeds via ITA/partners, Gmail confirmations |
| Collaboration | Medium | Shared lists, Docs export, Canvas; no real-time multi-user trip editing [inferred] |
| Accountability | **None** | Not merchant of record; partner owns service |

**Moats.** Maps POI data, Flights and Hotels price feeds, Gmail booking confirmations, Android and Search distribution, Google Pay.

**Won't or can't do**
- Take liability or service bookings.
- Share chat context with suppliers.
- Rank independent hotels (not at launch).
- Book flights (not yet).
- Fully commit to an editorial "opinion". Results lean toward popular, high-review-count POIs, so the cliché problem persists **[inferred]**.

**Failures.** Informal tests (2026) found Gemini Tokyo itineraries with 4 hallucinations (about 71% accuracy in one test), a stop that had closed on 31 Aug 2026, and a non-existent single-ticket routing in Southeast Asia [claimed: travelanywhere.blog, trripah, talkory; low-rigour sources]. An SEO-agency study instead ranked Gemini as the most accurate model. **Evidence is mixed.**

### 2.2 OpenAI: ChatGPT apps, agent, Instant Checkout

**What it does today**
- **Apps in ChatGPT.** Launched 6 Oct 2025 on the Apps SDK, which is built on MCP. Booking.com and Expedia were launch partners [verified]. Later additions:
  - **Tripadvisor**: hotel deals, US only [verified via tripadvisor.com/ChatGPT].
  - **Skyscanner**: flights only, US and UK, 27 Feb 2026 [verified].
  - **Klook, GetYourGuide, Viator** apps [claimed].
  - **Booking.com car rentals**: 20 May 2026 [claimed].
- Apps show live prices and availability in chat, then redirect to the partner to pay. **Not available in the EU** [claimed by several guides].
- **Instant Checkout / Agentic Commerce Protocol.** OpenAI pulled back on about 4–6 Mar 2026 [verified: Forbes 10 Mar 2026, PhocusWire, Skift via secondary]:
  - It "prioritises search and product discovery".
  - Checkout moves into partner apps.
  - Only about a dozen Shopify merchants ever went live.
  - Trade press framed travel as "too complex" (live pricing, cancellation policies, post-booking support).
  - Skift's headline: "ChatGPT bails on transactions, good news for Expedia and Booking."
- **ChatGPT agent / Operator / Atlas**
  - Atlas browser deprecated 9 Jul 2026 and shut down 9 Aug 2026 [verified across several sources].
  - ChatGPT agent mode reportedly removed in early Aug 2026; the help centre points to "ChatGPT Work" and a cloud browser [claimed; no official release note found].
  - Earlier tests: Operator failed 2 of 3 airline booking runs (session timeouts, CAPTCHAs, price changes between search and checkout) [claimed, travelanywhere.blog].
- **Ads.** Expedia went live with ChatGPT ads in Feb 2026 [claimed, GeekWire].
- **Apps in practice** (Skift hands-on, 6 Jul 2026) [verified]:
  - Connecting an app is not enough; the chatbot has to choose to use it.
  - In Skift's test, the Booking.com, Expedia and Viator apps and connectors were **initially skipped** (Claude connectors were tested too).
  - Sources conflict on whether checkout now runs inside the chat window or finishes on the partner site.
- New 2026 travel apps include Lighthouse (hotels, Mar 2026) and Almosafer (Apr 2026) [claimed, vendor blog].
- **Odessia acquisition** (10 Nov 2026): OpenAI bought an IATA-accredited AI travel agency and hired its founder, Francis Davidson, to work on travel. **No ChatGPT travel-booking product has been announced.** Any plan to sell travel directly is inference [verified; see file 01, §2.5].

**Rubric.**
- Personalisation P3: Memory persists across chats; no booking-history ingestion beyond what the user pastes or connects [inferred].
- Granularity G2–G3: day-by-day and time-slotted text; no native routing engine.
- Booking B1: deep links via apps.
- Live/on-trip L1–L2: chat companion, no alerts.
- Grounding: web search plus partner apps.
- Accountability: none.

**Moats.** Distribution (hundreds of millions of weekly users) and the default "first question" position.

**Won't or can't do:** transact travel, service bookings, take liability, operate in the EU for apps.

### 2.3 Perplexity: Selfbook + Tripadvisor hotels, Comet

- **Hotel booking** [verified for the Mar 2025 launch; **older**]
  - Launched with Selfbook (booking and payments) and Tripadvisor (reviews), about 140k hotels.
  - Testers in 2025–26 found the booking option often did not appear: "a discovery layer, not a booking platform" [claimed].
  - I found no 2026 documentation confirming it is still active [claimed, helloaxel]. Re-checked Nov 2026: still no 2026 hotel-booking announcement [verified absence].
  - Tripadvisor management called Perplexity-referred customers "incremental" and "high intent" (2025 call) [verified, Skift].
- **Comet browser**
  - Agentic browser with Expedia and Booking.com as pilot partners [claimed, WiT]. Expedia launched with Comet in Oct 2025 and gives users Silver One Key status for using it [verified, PhocusWire].
  - Can complete bookings on supplier sites but pauses for user confirmation before payment. The sites own the sale and support [claimed].
  - **2026 legal risk:** a US federal court temporarily barred Comet agents from accessing password-protected parts of Amazon to buy on users' behalf. The order was later suspended to allow an appeal [verified via secondary]. It is not travel-specific, but it is a precedent for agent access to logged-in consumer accounts.
- **Rubric:** P2, G2, B1–B2 (inconsistent), L0–L1. Grounding: web retrieval with citations, which is good for freshness on popular topics but carries no structured POI hours. Accountability: none.
- **Note:** United's agent ban targets exactly the Comet-style "drive the consumer site with my credentials" model [inferred].

### 2.4 Microsoft Copilot: Actions

- Copilot Actions (launched Apr–May 2025, Copilot Pro US first) lists partners: Booking.com, Expedia, Hotels.com, Kayak, OpenTable, Priceline, Tripadvisor, Skyscanner, Viator, Vrbo [verified on a Microsoft marketing page; **2025 info**].
- Always asks for confirmation before acting.
- Expedia announced integration with Copilot Actions (May 2025).
- **I found no 2026 evidence of meaningful travel traction**, and no 2026 consumer travel launch (re-checked Nov 2026) [verified absence].
- Flights in Copilot run on Skyscanner's Flights API, which also powers Bing Flights [verified, 2025].
- Corporate hotel provider CDS has opened hotel booking to Copilot and ChatGPT via MCP, with flights and cars planned for early 2027 [claimed, single outlet].
- Context: an Expedia survey (Apr 2026) found **only 8%** of travellers comfortable handing booking to AI [verified, Skift].
- Rubric: P2, G2, B1–B2, L0–L1. Accountability: none.
- Relevance is mostly enterprise: SAP Concur Joule integrates with M365 Copilot, and Egencia's assistant runs in Teams (see §4).

### 2.5 Anthropic Claude

- **Connector Directory** (MCP), all free plans [claimed: Tineo, Spiritt, felloai]:
  - Expedia connector (live pricing and availability, flights and hotels), launched 6 May 2026 [claimed].
  - Booking.com stays connector.
  - Viator connector.
  - Most guides say the connectors search and compare, and booking completes on the partner site.
- **Enterprise:** Amex GBT's **Egencia connector in Claude** (announced 27 Jul 2026; policy-compliant booking via agent-to-agent/MCP; customers in Q3 2026) [verified, Amex GBT press release]. **Perk** MCP connector (Jul 2026; booking, expense submission and event creation via Claude/ChatGPT from 19 Aug 2026; out-of-policy bookings routed to existing approval flows) [verified, BusinessWire].
- **Priceline Penny** is rebuilt on Claude (see §3.2). Hilton has a Claude connector "in development".
- **Security incident:** a June 2026 report linked exposure of 2.1M hotel booking records to MCP misuse [claimed; single outlet, details unverified].
- Rubric for consumer Claude: P3 (memory/projects), G2–G3, B1, L1. Accountability: none.

### 2.6 Meta: Muse (Meta AI)

- **Expedia hotels in Muse**: announced 24 Sep 2026, live in the US around 9 Nov 2026 [verified: Skift, PhocusWire]. Details:
  - natural-language search and **in-agent booking**;
  - **pay-now rates only**;
  - payment via **Stripe Link**;
  - **no cancellations or rebooking**: changes go to Expedia support as merchant of record.
- **Agoda** integrated with Muse for Singapore and Japan (discover, book, manage itineraries) [claimed, Booking Holdings Q3 call].
- **Flights:** some flight booking in Muse is enabled by **Duffel's API**, the same rail Lola uses [claimed, single outlet].
- **Surfaces:** the Muse app (iOS/Android), muse.ai on the web, and WhatsApp. US [verified].
- **Strategy:** Meta calls travel "a top use case" for Muse, and Zuckerberg wants a transaction cut [verified, Skift 21 Oct 2026].
  - Truist called Muse a bigger OTA threat than earlier LLMs. Expedia shares fell about 7% on the partnership news [claimed].
  - Airbnb's Chesky says Muse and similar general agents currently drive "little traffic and even fewer bookings" [verified, Q3 call].
- **Mechanism is disputed.** Expedia describes an API integration; Conduit describes browser-driving of consumer sites.
- **Distribution:** WhatsApp, Instagram and Facebook. Expedia had earlier put trip planning into Instagram DMs ("Trip Matching", 2025) [claimed].
- Rubric: P2–P3 (potential social-graph P4, not evidenced), G2, B2 (hotels), L0. Accountability: delegated to the OTA.

### 2.7 Apple

- **WWDC 2026:**
  - rebuilt Siri with personal context, screen awareness and deeper App Intents;
  - multi-step reasoning reportedly runs on a Gemini-based model under the Jan 2026 Apple–Google deal;
  - Maps added AI Flyover and "Local Lists" [claimed: Skift 8 Jun 2026, Geeky Gadgets].
- **Shipped:** iOS 27 with "Siri AI" was released on **14 Sep 2026** for Apple Intelligence iPhones (15 Pro and later). Its personal context draws on calendar and email with permission. Japanese followed in Oct [verified: Engadget, MacRumors].
  - Early reviews call it "practical but plain" (Engadget).
  - More Siri AI capability is staged into iOS 27.x (Macworld) [claimed].
- Skift: Siri **cannot book a trip**. Its value is in-trip retrieval (confirmation codes, passport details, hotel address), with action delegated to apps via App Intents. Examples: find a booking, flight status, open check-in, loyalty details.
- I found no Apple list of travel-specific Siri AI features post-launch [verified absence].
- Rubric: P4 potential (on-device personal context), G1–G2, B0 (delegates to apps), L2. Accountability: none.
- **Threat:** if iOS 27 Siri can see your Wallet passes, Mail confirmations and Maps, it becomes a very strong on-trip layer that no startup can match on iOS [inferred].

---

## 3. OTAs, metasearch and incumbents

### 3.1 Expedia Group (Expedia, Hotels.com, Vrbo; Romie; Layla)

- **Romie** (EG Labs alpha, 2024) [verified; **older**]:
  - joins SMS group chats;
  - pulls trip details from email;
  - suggests nearby restaurants;
  - monitors weather and disruption and suggests alternatives.
  - **Now reportedly retired.** A Jun 2026 report quotes CPO Shilpa Ranganathan on why Expedia's first booking chatbots, Romie among them, stalled:
    - users left when answers weren't tied to real inventory, rates and reservations;
    - the fix took about a year and was "almost none of it model work", mostly evaluation framework and data plumbing [claimed, single outlet: hospitality.today].
    - No official retirement notice was found.
- **2026 strategy shift to "multi-agentic"** [verified: Skift 31 Jul 2026, TravelMole, HospitalityNet]:
  - acquired **Layla** (Berlin conversational planner covering flights, stays, activities, dining, transport);
  - says one do-everything concierge "isn't practical yet";
  - building specialised agents: a Hotels.com AI agent, an activities agent, natural-language search on Vrbo [claimed].
  - Layla continues to run standalone; no integration date given (re-checked Nov 2026).
- **Fall 2026 product release** [verified: Expedia PR via HospitalityNet, PhocusWire]:
  - **30+ AI features** across Expedia, Hotels.com and Vrbo, including natural-language search, AI comparison tools and a **voice agent**;
  - the **Hotels.com AI Agent** puts conversational discovery, shopping and **servicing** behind one homepage entry point;
  - Hotels.com **AI Compare** for shortlisted properties;
  - **Property Expert** answers questions grounded in property data and guest reviews.
  - Expedia now describes these as "point agents" for specific journey stages [claimed, hospitality.today].
- **B2B agent access:** three Partner Central agents were shown at Explore (May 2026). Expedia is preparing a **B2B MCP server** so partners' AI agents can reach its inventory [verified, Skift 21 May 2026]. No announcement yet lets external agents book and pay autonomously over MCP.
- **Trust data:** an Expedia survey (Apr 2026) found only **8%** of travellers comfortable letting AI book [verified, Skift].
- **Distribution everywhere:**
  - ChatGPT app (Oct 2025) and ChatGPT ads (Feb 2026);
  - Claude connector (May 2026);
  - Google AI Mode hotel partner (Aug 2026);
  - Meta Muse (Nov 2026);
  - Perplexity Comet pilot;
  - Copilot Actions (2025) [verified across GeekWire, Skift, PhocusWire].
- **B2B is the growth engine.** Q3 2026 8-K: gross bookings +11%, B2B +19%, B2C +7%; revenue +12%; B2B revenue +23% [verified, SEC 8-K 4 Nov 2026].
- **Expedia's own data:** AI-powered customer support at scale. CEO Ariane Gorin: agents are "strongest in discovery", agent traffic is "small but high intent", and AI wins come "inside its own apps" [verified, Skift 9 Nov 2026, PYMNTS].
- **Rubric:**
  - P3: account history, loyalty (One Key). Romie's email ingestion has reportedly been retired.
  - G2–G3.
  - **B4**: full multi-vertical checkout plus post-booking changes, refunds and AI customer service (the Hotels.com AI Agent now includes servicing).
  - L2: trip alerts and an AI servicing agent. Romie's disruption monitoring was an alpha and is reportedly retired, so the earlier L3 is downgraded.
- **Moat.** About 3M+ properties, flights, cars, activities, packages, and first-party traveler data. The Rapid API supplies other AI agents [inferred from B2B growth].
- **Won't:** recommend non-Expedia inventory, or plan neutrally across suppliers (Ribbit and others argue Layla will tilt toward Expedia inventory [claimed/opinion]).

### 3.2 Booking Holdings (Booking.com, Priceline, Agoda, Kayak, OpenTable; Lola, Vayo)

- **Booking.com**
  - **AI Trip Planner**: US beta from Jun 2023, expanded to UK/AU/NZ/SG in Oct 2024. Gives destination ideas and itineraries with live availability, and books through normal checkout [verified; **older**].
  - **Smart Filters**: natural-language property filtering in five markets [claimed].
  - Features Booking.com calls "agentic" (Smart Messenger and Auto-Reply, Oct 2025) are guest–property messaging, **not booking agents** [claimed].
  - AI Voice Support for trip management [claimed].
  - Daily AI trip-search visitors up **10x from Q2 to Q3 2026** [verified, CNBC 5 Nov 2026].
  - **2026 status of the trip planner:** no new standalone planner launch was found.
    - Reports say the planner is being folded into an embedded AI companion available at key points in the booking journey.
    - On the Q1 2026 call (28 Apr), Booking.com cited enhanced natural-language search and **agentic post-booking flows that reduced support contacts**.
    - The CFO described "pre-trip, in-trip, post-trip" experiences, including proactive itinerary adjustments [claimed, secondary call summaries].
- **Priceline Penny**
  - Rebuilt and launched 3 Jun 2026 on **Anthropic Claude**, with Google Cloud and OpenAI for search and voice.
  - Multiple coordinated agents, a single-page booking experience, **flight purchase without leaving the conversation**.
  - Users save about 10 min per trip vs calling support.
  - CTO roadmap: "graduated delegation" (the user sets how much autonomy the AI has) and voice [verified: Forbes 29 Jul 2026, CX Dive].
- **Agoda AI Assistant**: live in 21 markets. Penny and Agoda assistant users convert about **2x** non-users; Agoda AI users show about **20% higher booking value** [verified, Q3 2026 call via CNBC/PYMNTS]. Usage share was not disclosed.
- **Lola** (29 Sep 2026) [verified: Skift exclusive, Engadget, Travel Weekly, Boston Globe]:
  - Booking Holdings-owned, run by Kayak co-founders Steve Hafner and Paul English.
  - Searches live availability and prices for **hotels, restaurants, events, activities** and **books in the same chat**.
  - Partners: Booking.com, OpenTable, Kayak, Priceline, Agoda, FareHarbor, plus ResX, BLADE, Aero, SeatGeek, GetYourGuide, Nuitee, Ten Group (concierge).
  - Memberships: free, Plus $5/mo, VIP $25/mo (preferred rates, priority dining, human concierge access).
  - Focus includes **hometown** dining and events, not just trips.
  - **Flights added post-launch, powered by Duffel**. Cars are still to come.
  - Booking Holdings has made a **$100M investment commitment**, "subject to continued advancement of the product and market commitments". Lola has about 20 staff [verified, PhocusWire].
  - **US-only.** One report says Lola Plus was discontinued on 5 Nov 2026, with members moved to VIP [claimed, single outlet].
  - Terms warn that AI output may be inaccurate. **No independent hands-on reviews found** (re-checked Nov 2026).
  - **This is the closest incumbent analogue to a startup "AI concierge with human backup".**
- **Vayo**: second Booking Holdings assistant, Seattle, CEO Mike Fridgen; private beta from 14 Oct 2026; $100M planned [verified, PhocusWire, GeekWire].
  - **Correction:** Vayo does **not** yet book flights. In beta it books **restaurants via OpenTable**.
  - Flights and hotels are searched and then handed off to the supplier. Transactional flight and hotel booking was promised "in the coming weeks", and no report confirms it has shipped as of mid-Nov 2026 [verified].
  - It monitors bookings made anywhere, including rival OTAs and direct.
- Booking Holdings is running about five AI experiments in parallel [claimed, Skift 14 Sep 2026].
- **CEO Glenn Fogel:**
  - AI discovery is popular but converts to few bookings today;
  - envisions **agent-to-agent** (the Booking agent talks to the traveler's personal agent);
  - warns that the DMA, EU AI Act and DSA could slow horizontal agents in Europe [verified, Q3 call].
- **Accountability context:** Q3 2026 revenue included a **$900M reduction tied to an FTC investigation** involving Priceline and a B2B affiliate [verified via call summaries].
- **Rubric (Booking.com/Priceline):** P3 (Genius loyalty, history), G2, **B4** (B3 at Priceline/Lola across verticals), L2–L3.
- **Moat:** largest lodging inventory, Genius loyalty, OpenTable restaurants, Kayak meta data, FareHarbor activities supply.

### 3.3 Airbnb

- AI customer service agent:
  - about one third of US/Canada support handled by AI (Feb 2026);
  - 15% fewer users needing a human;
  - support cost per booking down more than 17% YoY (Q3 2026) [verified: TechCrunch, CX Dive].
- **AI travel agent planned for H1 2027.** Not a chatbot: a custom AI-native UI built from "hundreds of travel-specific interface components" (maps, comparisons, calendars, itineraries). It is explicitly **"not limited to Airbnb's platform"**, includes group planning, and voice is coming [verified, TechCrunch 5 Nov 2026].
  - On the Q3 2026 call, Chesky likened the UI to "generative UI".
  - He said sponsored listings and ads will come only **after** the agent launches and is refined [verified, PhocusWire Q3].
- Chesky argues general-purpose agents are a poor fit for trip planning because discovery is part of the experience. He also says Meta's Muse and similar agents generate "little traffic and even fewer bookings" for Airbnb [verified, Q3 call].
- AI support: in Q2 2026 the assistant resolved **about 45%** of issues that start with it without a human, up from Q1 [verified, Airbnb Q2 release].
- **Experiences:** Airbnb's Q1 2026 results say Experiences continued to scale and early results show it "becoming a demand flywheel" [verified, Airbnb Q1 release]. This replaces the earlier prior-knowledge note.
  - The May 2025 relaunch of Experiences plus Services is consistent with this, but I found no 2026 metrics specific to Services [verified absence].
- **Rubric today:** P3, G1, B2 (stays and experiences), L2 (support). **Threat level: high in 2027.** Airbnb has social and identity features, host supply and design capability.

### 3.4 Kayak

- AI Mode (Oct 2025, built on ChatGPT and Kayak data) evolved into **"Ask AI"**, launched by press release on 23 Apr 2026 (GlobeNewswire 29 Apr) and timed to the World Cup [verified, primary].
  - Natural-language chat, with live flight, hotel and car results updating **alongside** the conversation.
  - It is a conversational search layer, not an autonomous booking agent.
  - No later 2026 update was found.
  - Kayak embeds the experience in its own site rather than shipping a ChatGPT app [claimed, analysis].
- Kayak.ai test lab. **PriceCheck**: upload a booking screenshot and Kayak tells you if you overpaid.
- Booking: "we don't handle the actual booking or payment" [verified, Kayak help]. That makes it **B1**.
- **Kayak for Business** completes policy-compliant bookings with human confirmation and has an agent-to-agent connector (Amex GBT tie-up) [verified, Skift 2 Aug 2026].
- Rubric: P2, G1–G2, B1, L1 (price alerts).

### 3.5 Skyscanner

- ChatGPT app for flights only, US and UK, 27 Feb 2026, redirect to book [verified].
- Own natural-language search, plus a "Football Flight finder" for the World Cup.
- Stated stance: expand agentic scenarios "only where trust and economics work" [claimed].
- Rubric: P1–P2, G1, B1, L1.

### 3.6 Tripadvisor

- **Trips / AI trip builder**: GPT-4 plus about 1B reviews. An Aug 2024 rebuild used Tripadvisor's own recommender over reviews and **doubled save rates** [verified, Tripadvisor engineering blog; **older**]. Builds day-by-day plans from saved lists.
- **ChatGPT app**: hotel deals, US only [verified]. Perplexity partnership: reviews power Perplexity hotel results (2025).
- **Monetisation:** commissions via Viator (attractions) and TheFork (restaurants).
- **2026 AI activity** (resolved in the gap-fill pass) is mostly partnerships and demos. I found no single flagship agent launch:
  - **Best Western × Tripadvisor "Go for the Goal"** (29 Jan 2026): an AI multi-city trip planner for World Cup fans covering 200+ hotels within 25 miles of host stadiums [verified, multiple outlets].
  - **Tripadvisor and Viator in Claude and Alexa+** (newsroom, 23 Apr 2026): planning "wherever travelers choose to plan" [verified, primary].
  - **Video-to-trip demo** at Nvidia GTC 2026: drop in an influencer video and get a bookable plan, inside Tripadvisor's "native AI experience" (experimental) [verified, PhocusWire/AltexSoft].
  - Summer update (10 Jun 2026): AI trip planning and smarter discovery for Experiences [verified, primary].
  - A claim that the AI trip planner became the default for all logged-in users on 12 May 2026 rests on a single unofficial page [claimed, unverified].
- **Q3 2026: weak results** [claimed, secondary earnings summaries; verify against the 10-Q]:
  - revenue of about $436M missed consensus;
  - group revenue fell about 11%;
  - growth at Viator/Experiences stalled;
  - **CEO and CFO are both departing**;
  - strategy is shifting to a single B2C "experiences flywheel", with Hotels & Other run at smaller scale;
  - activist Starboard has called the pace of change "unacceptable".
- **AI channel economics:** AI-referred traffic is **under 1%** of the total but converts at about **5x** the site average on Viator and about 2x on Tripadvisor. Tripadvisor cites integrations with Anthropic, OpenAI, Gemini and Meta [claimed, Q3 call summary].
- Rubric: P2–P3, G2, B1–B2 (Viator and TheFork in-house), L1. Unchanged; the 2026 activity is distribution, not new booking depth.
- **Moat:** review corpus, which is increasingly licensed to LLMs. That turns Tripadvisor into a data supplier rather than a destination [inferred].

### 3.7 Trip.com: TripGenie / Trip.Planner

- TripGenie assistant covers:
  - itinerary generation;
  - booking interface;
  - **travel alerts whether or not booked through Trip.com**;
  - collaborative editing [claimed, Trip.com newsroom].
- About **60% of TripGenie interactions relate to booking decisions** [claimed, ITB Berlin 2026]. Trip.Planner was named ITB Innovator 2026.
- Mastercard demo planned for commercial rollout from early 2027.
- **2026 additions** [claimed: Trip.com releases, Google Cloud case study]:
  - Trip.Planner, Menu Assistant, Live Translation and Image Recognition;
  - **in-chat agentic booking for eSIMs and attraction tickets** (2026);
  - a "Live Guide" voice/multimodal mode on the Gemini Live API;
  - retrieval via Gemini Agent Search, with **grounding checks against verifiable data**.
  - Trip.com reports AI-assisted bookings up **400% YoY** and adoption of real-time AI features (translation, menus) up **300%** (Mar 2026).
  - Its stated aim is to turn TripGenie into a "travel butler".
- **Caveat:** itinerary edits do not automatically sync with supplier bookings [claimed, Sequenced analysis].
- Rubric: P3, G3, **B3–B4** (flights, trains, hotels, attractions in one app; strong on rail in China and Asia), L3.
- Probably the most complete incumbent "planner + booking + alerts" stack, but weak on Western long-tail local supply [inferred].

### 3.8 Hopper / HTS

- **HTS Assist** (B2B gen-AI servicing agent for banks and airlines) [verified, PhocusWire; **about 2025**]:
  - claims to handle all changes, cancellations, disruptions and refunds;
  - 65% servicing-cost reduction (Lotte Card, SMBC);
  - 200 markets, 30+ languages.
- **Disruption Assistance** (white-labelled for Frontier, Spirit, Viva, Wizz) [verified via HTS legal terms]:
  - rebooks on a new flight, or gives a partial refund;
  - explicitly a **"guarantee, not insurance"**;
  - missed-connection guarantee up to US$2,000 per passenger (Flair).
- **HTS summer 2026 platform update** (11 Aug 2026): voice infrastructure for real-time AI voice servicing, and a model that judges whether a traveller's issue was **actually resolved** [claimed, HTS newsroom]. Avelo has also launched Disruption Assistance on HTS.
- **Consumer Hopper app:** no new consumer AI feature found in 2026 [verified absence]. The 2026 AI work is B2B (HTS).
- **FTC settlement: $35M** (2 Jul 2026) over hidden pre-selected Tip and VIP Support fees and a misrepresented Price Freeze, with no admission [verified, ftc.gov].
- **Lesson:** fintech-style "protection" add-ons work as a business, but regulators are watching dark patterns in them.
- Rubric: P2, G1, B2–B3, L3–L4 (disruption rebooking product).

### 3.9 Klook, Viator, GetYourGuide

- **GetYourGuide**: ChatGPT app; AI review summaries from verified bookings; smart search; AI replies for operators [claimed].
- **Klook**: ChatGPT app covers activities plus hotels, cars and transfers, with activity-based itineraries. Strongest in Asia; few results per query [claimed]. Publishes an "llms"-style file for AI engines.
- **Viator**: ChatGPT app and Claude connector with live listings, ratings, prices and durations [verified, Tom's Guide]. Its public AI-crawl file restricts reviews, pricing and availability [claimed].
- **Pattern:** activities supply is exposed to LLMs as **apps and connectors** rather than open data. A startup can integrate the same APIs [inferred].
- Rubric: P1–P2, G1, B2, L1.

---

## 4. Corporate travel management: where accountability lives

| Player | AI agent (status) | Disruption handling | Duty of care / accountability | Interop |
|---|---|---|---|---|
| **Navan** | **Ava** handled about 60% of customer interactions in FQ2 2027 (Sep 2026), up from about 30%; about 50% of model calls on Navan-owned models; 81% CSAT claimed in 10-K [verified, Navan IR] | Ava does rebookings, hotel changes and refunds; **Waiver Agent** watches airline waivers and proactively prompts rebooking [claimed] | Hybrid: humans "orchestrated with" AI; 24/7 escalation; traveler location tracking; policy enforcement [claimed] | Own booking stack (NDC, GDS); listed on NASDAQ (Oct 2025) |
| **Perk** (ex-TravelPerk) | MCP connector (Jul 2026) to Claude, ChatGPT and others; booking, expense and event creation via assistants (19 Aug 2026); Slack agent coming [verified] | Markets automatic rebook/reroute ("traveler gets a notification it's handled") [claimed]; independent sources say this is not confirmed as a live autonomous agent | 24/7 humans with a 15-sec response target, but Trustpilot complains of multi-hour waits during disruptions [claimed] | MCP-first; approval flows preserved |
| **Spotnana** | Multi-agent architecture (Jul 2026): orchestrator plus servicing agent, external-booking import agent, agent co-pilot; actions via mapped APIs; judgment calls go to humans [verified, BTN] | Servicing agent for TMC agents first; traveler-facing tools "later 2026" | Infrastructure for TMCs (e.g. Direct Travel Avenir); the TMC holds liability | Open APIs, NDC |
| **Amex GBT / Egencia / CWT** | "Next-gen" Egencia (Apr 2026), conversational assistant in **Teams**; **Claude connector** (Jul 2026); Google Chat by end-2026; agent-to-agent infrastructure [verified, Amex GBT PR] | Large human-agent network and TMC servicing | Contractual duty of care, risk management, traveler tracking | Concur Expense integration; Kayak for Business tie-up |
| **SAP Concur** | Joule Booking Agent; Meeting Location Planner agent in development; Early Adopter Care with GA "later 2026"; Joule in M365 Copilot [verified] | Via TMC partners (Amex GBT "Complete") | Via TMC | SAP ecosystem |
| **Ramp / Brex** | Travel booking (flights, hotels, cars) inside spend platforms; **no travel-booking AI agent found**; Brex about $25/trip; Brex acquired by Capital One (2026, timing unconfirmed) [claimed] | Basic | Light | Card and expense-native |

**What consumer planners can learn from corporate travel**
- **Delegated authority with policy.** Pre-approved bounds for spend, cabin and hotel tier, plus approval flows for exceptions.
- **Waiver monitoring and proactive rebooking** before the traveler is stranded.
- **Agent-assist plus human escalation, measured by containment rate** (Navan about 60%).
- **Traveler tracking and duty of care.** Navan argues that bookings made outside the system can't be tracked, which is the same reason a consumer planner wants every booking imported.
- **External-booking import agents** (Spotnana). This is a key primitive for a consumer product that doesn't own all bookings.

---

## 5. Airlines and hotel chains

- **Delta Concierge**
  - AI assistant rolled out to all SkyMiles members (Aug 2026).
  - Handles disruption rebooking, eligible cancellations, bag tracking, eCredits.
  - Delta credits it, with simpler rebooking, for a **25+ point NPS gain during irregular operations** [verified: FTE, CX Dive].
  - **Failure:** it told a Platinum member her return flight was safe, then cancelled the ticket and quoted double to rebook. Delta fixed the logic; the assistant is still labelled BETA [verified: View from the Wing, Aviation A2Z, Aug 2026].
- **American Airlines AURA / Connect Assist.** The most automatic consumer rebooking found in 2026.
  - Expanded in 2026 to hubs including Chicago, Miami and Phoenix.
  - It **moves delayed passengers onto later flights without asking first**.
  - Passengers report wrong itineraries and missed connections, mainly on tight connections [claimed/press: TravelPulse, InsideFlyer].
  - An earlier 2025 version let passengers self-rebook instantly.
  - Lesson: autonomy without consent creates its own trust failures.
- **Disruption and rebooking: who actually rebooks automatically (consumer side, Nov 2026)** [inferred from the evidence in this file and file 01]:
  - **Carriers do, for their own flights.** American rebooks proactively without consent. Delta Concierge offers alternatives for the traveller to approve. HTS-powered Disruption Assistance (Frontier, Spirit, Avelo and others) is a paid guarantee.
  - **OTAs service their own bookings** with AI support agents (Expedia, Booking.com, Airbnb, Priceline). None was found to rebook proactively across a whole trip.
  - **General AI platforms do not rebook at all.** Google, OpenAI, Meta and Apple are not merchant of record.
  - **AI-native startups monitor but don't rebook** (Vayo, Axel, Mindtrip agents). TripAgent.ai's claim is unverified.
  - Only corporate TMCs (Navan, Perk) market autonomous cross-booking disruption handling, and even there it is partly unconfirmed.
  - Ada's 2026 research: only **24%** of consumers say AI fully resolved their issue without a human [claimed, vendor research].
- **United** bans third-party AI agents (11 Nov 2026) but stays bookable via Google Flights, Kayak and Hopper [verified].
- **Hilton AI Planner** (web, Mar 2026, beta), expanding to Google AI Mode, ChatGPT and a Claude connector. Hilton's CIO says AI agents put OTAs "under real threat", meaning a route back to direct bookings [verified, Skift 29 Sep 2026].
- **Marriott, IHG, Wyndham:** conversational search tools; Marriott's enterprise AI is in "Phase 3" [claimed]. No Marriott rebooking concierge found.

---

## 6. Comparison table (rubric)

| Product | Pers. | Gran. | Booking | Live | Grounding | Collab | Accountability |
|---|---|---|---|---|---|---|---|
| Google AI Mode + Maps + Gemini (+ Chrome auto browse) | **P4** (opt-in Gmail/Photos) | G3–G4 | B2 (US hotels via 10 partners; dining/events/appointments as guided hand-off; flights tracking and points only) | L2–L3 | Maps 300M POIs, Flights/Hotels feeds | Lists, Docs export, Canvas | None (not MoR) |
| ChatGPT (+ apps) | P3 | G2–G3 | B1 | L1–L2 | Web + partner apps | Group chats/shared [inferred] | None |
| Perplexity / Comet | P2 | G2 | B1–B2 (inconsistent) | L0–L1 | Cited web + Tripadvisor | Low | None |
| Copilot Actions | P2 | G2 | B1–B2 | L1 | Partners (2025) | Low | None |
| Claude (+ connectors) | P3 | G2–G3 | B1 | L1 | Web + Expedia/Booking/Viator MCP | Projects | None |
| Meta Muse | P2–P3 | G2 | B2 (Expedia pay-now hotels; some flights via Duffel) | L0 | Expedia API, Duffel | Social (potential) | Delegated to Expedia |
| Apple Siri AI (iOS 27, shipped Sep 2026)/Maps | P4 (personal context, opt-in) | G1–G2 | B0 | L2 | On-device context, Apple Maps | iMessage | None |
| Expedia (+Layla; Romie retired) | P3 | G2–G3 | **B4** | L2 | Own inventory; Hotels.com AI Agent with servicing | Low (Romie group chat retired) | MoR, support |
| Booking.com / Priceline Penny | P3 | G2 | **B4** | L2–L3 | Own inventory, Genius | Low | MoR, support |
| Lola (Booking Holdings; US-only) | P3 | G2 | B3 (hotels+dining+events+flights via Duffel) | L2 | BH brands + partners + Duffel | Itinerary sharing | MoR + VIP human concierge |
| Vayo (Booking Holdings; beta) | P4 | G1–G2 | B1–B2 (restaurants only so far) | L3 | Inbox confirmations from any supplier | Planned | Unknown |
| Airbnb (today / 2027 plan) | P3 | G1→G3? | B2 | L2 | Listings, reviews | Group planning (planned) | Host-guest policies, AirCover |
| Kayak Ask AI | P2 | G1–G2 | B1 | L1 | Meta price data | Low | None |
| Skyscanner | P1–P2 | G1 | B1 | L1 | Meta flights | Low | None |
| Tripadvisor (leadership transition) | P2–P3 | G2 | B1–B2 | L1 | ~1B reviews; licensed to Claude, Alexa+, ChatGPT, Perplexity | Trips sharing | Viator policies |
| Trip.com TripGenie | P3 | G3 | **B3–B4** (incl. in-chat eSIM and attraction tickets) | L3 | Own inventory incl. rail; Gemini grounding | Collaborative edit | MoR, 24/7 |
| Hopper/HTS | P2 | G1 | B2–B3 | **L3–L4** | Price prediction | Low | Guarantees (FTC history) |
| Navan (Ava) | P3 | G3 | B4 | **L3–L4** | GDS/NDC | Admin | **Duty of care, 24/7 humans** |
| Perk | P3 | G3 | B4 | L3 (L4 claimed) | GDS/NDC | Admin/Slack | Duty of care |
| Delta Concierge | P3 | n/a | B4 (own flights) | **L4** | Own ops data | n/a | Carrier obligations |
| American AURA/Connect Assist | P2 | n/a | B4 (own flights) | **L4** (proactive, without consent; error complaints) | Own ops data | n/a | Carrier obligations |

---

## 7. Structural constraints: what incumbents can't or won't do

1. **General AI platforms won't be merchant of record or service bookings** (Google, OpenAI, Meta). OpenAI's retreat from checkout shows the servicing burden is the blocker. They can't do neutral "fix my trip" support across suppliers [verified].
2. **OTAs won't recommend outside their inventory.** Expedia/Layla and Booking/Lola plan with their own supply, so independents, small guesthouses, non-bookable local gems, and most cross-OTA comparison are excluded. Lola is a partial exception through partners [inferred].
3. **Hyperlocal and anti-cliché curation is nobody's priority.** Google ranks by popularity and review volume. OTAs rank by conversion and commission. Tripadvisor ranks by review counts. No incumbent shows a mechanism for "locals' picks", seasonality, or under-reviewed but excellent venues [inferred; I found no incumbent feature claims in this direction].
4. **Interoperability is per-brand, not per-trip.** Each OTA app in ChatGPT is a silo. Google hands off to ten partners. Nobody stitches flights, trains, local transport and activities across suppliers into one door-to-door timeline. Trip.com comes closest, and only within its own inventory [inferred].
5. **Agent access is closing on the supply side.** United's ban plus bank credential warnings mean browser-agent booking on consumer accounts is risky. Durable booking needs API, MCP or agent-to-agent agreements [verified + inferred].
6. **Europe lags.** ChatGPT apps are reportedly unavailable in the EU. Google AI Mode hotel booking is still US-only (Nov 2026), and AI Mode flight tracking excludes the EEA. Lola is US-only. Fogel flags DMA, AI Act and DSA friction [claimed/verified].
7. **Accountability exists only in B2B and with carriers.** Consumer AI planners offer no guarantees. Lola's VIP concierge and Hopper/HTS guarantees are the only consumer-side signals.

---

## 8. Strategic gaps an independent startup could exploit (ranked)

1. **Cross-supplier trip ownership and accountability ("the trip's merchant of care").** No consumer AI service takes responsibility for the whole trip regardless of where it was booked.
   - Corporate tools prove the playbook: waiver monitoring, proactive rebooking, a 60% AI containment rate with human escalation, and an external-booking import agent.
   - A consumer version would: import all confirmations from Gmail or forwarding; monitor flights, trains, weather and venue closures; proactively re-plan; and offer human escalation plus a paid guarantee in the HTS style but transparent (FTC lesson).
   - Google, OpenAI and Meta structurally refuse this role. OTAs only do it for their own bookings.
2. **Hyperlocal, opinionated, verified curation.** Incumbents optimise for popularity or commission.
   - Build a curated, freshness-verified POI layer: local creator and guide sourcing; closure detection by checking hours, menus and recent reviews; phone or agent verification. Google's call-the-business feature shows feasibility, but Google uses it for appointments, not for verification.
   - Pair it with taste profiles that explicitly *avoid* the top-N tourist list.
   - This attacks problems (1) and (3) directly, and it is defensible because it is labour-plus-data, not model-only.
3. **Door-to-door multimodal timelines with real transit and buffers (G4–G5) across suppliers.** Nobody does G5 across verticals and suppliers.
   - Combine routing (GTFS/real-time transit, rail APIs such as Trainline/Omio, ride-hail), opening hours, ticket times and booking holds into one executable timeline that re-flows on disruption.
   - Google has the pieces but won't book trains or hold liability. Trip.com does it only for its own inventory.
4. **Neutral, API-based booking orchestration via MCP and agent-to-agent.** Supply is now exposed through MCP and apps (Expedia, Booking, Viator, Klook, GYG, Perk, Egencia), and Fogel openly envisions agent-to-agent.
   - A neutral orchestrator can: compare across OTAs and direct hotel channels (Hilton and others want direct); use sanctioned APIs, not scraping (avoiding United-style bans); and give one itinerary-level checkout or ledger even if transactions are per supplier.
   - Add "graduated delegation" policies like Priceline's: user-set spend and cancellation bounds.
5. **Group and collaborative planning plus Europe-first availability.**
   - Group planning is mostly a promise: Romie SMS (alpha, reportedly retired), Airbnb (2027), Vayo (promised), Trip.com collaborative edit.
   - US platforms are blocked or slow in the EU (ChatGPT apps, AI Mode booking). A GDPR-compliant, EU-native planner with real collaboration (voting, budgets, split payments) has a 12–18-month window.

Honourable mentions:
- Transparent pricing and an anti-dark-pattern stance, a trust brand against the Hopper and Booking FTC history.
- "Hometown plus travel" continuity (Lola's thesis), to raise usage frequency.
- Accuracy SLAs: publish measured hallucination and closure rates.

---

## 9. Threats: where incumbents will likely close gaps in 12–24 months

| Threat | Likelihood | Timing | Notes |
|---|---|---|---|
| **Google** extends AI Mode booking to flights, adds Maps itinerary-in-navigation re-planning, expands Personal Intelligence globally | High | 6–18 mo | Strongest data and distribution; still no liability. Hyperlocal and accountability gaps survive. |
| **Airbnb AI agent** (H1 2027), cross-platform, rich UI, group planning | High | 6–9 mo | Directly targets "planner with taste" plus experiences. Biggest consumer-brand threat. |
| **Booking Holdings Lola/Vayo** scaling with paid concierge memberships | Medium-high | 6–18 mo | Copies the "AI + human concierge" model with inventory and margin advantages. |
| **Expedia + Layla** integrated multi-agent planner; Hotels.com AI Agent (discovery + shopping + servicing) extended across brands | Medium-high | 12–24 mo | Owns B4 servicing. Romie retired, so disruption features would have to be rebuilt. Neutrality gap remains. |
| **Meta Muse** taking a transaction cut on travel (Expedia hotels, Duffel flights) at WhatsApp scale | Medium | 6–18 mo | Distribution threat. Still no servicing, and Chesky says traffic is small today. |
| **Apple Siri (iOS 27)** with personal context across Mail, Wallet and Maps | Medium | 6–12 mo | Could own on-trip retrieval on iPhone. Booking via App Intents means startups must be Siri-integrated. |
| **Corporate TMCs going consumer or bleisure** (Navan, Perk MCP in Claude/ChatGPT) | Low-medium | 18–24 mo | Have the accountability stack; consumer economics unattractive to them. |
| **ChatGPT** re-entering transactions or adding travel memory and alerts | Medium | 12–24 mo | Retreated once; would likely partner rather than own servicing. |
| **Supply-side lock-out** (more airlines following United; hotels favouring direct channels) | Medium | ongoing | Risk to any agent that scrapes. Mitigate with sanctioned APIs, MCP and agency accreditation. |

---

## Sources

General AI platforms
- https://skift.com/2026/08/27/googles-agentic-hotel-booking-tool-comes-to-ai-mode/
- https://www.searchenginejournal.com/google-starts-rolling-out-hotel-booking-in-ai-mode/587288/
- https://www.phocuswire.com/news/technology/google-ai-mode-hotel-booking-agentic-flights-loyalty
- https://www.hotel-online.com/news/google-just-started-booking-hotels-inside-ai-independent-hotels-were-not-on-the-list
- https://ppc.land/google-steers-holiday-hotel-dinner-and-ticket-bookings-into-ai-mode/
- https://www.travelerstoday.com/articles/60289/20260622/google-ai-mode-travel-booking-how-booking-flights-hotels-about-change-this-year.htm
- https://skift.com/2025/11/17/google-is-building-agentic-travel-booking-plus-other-travel-ai-updates/
- https://techcrunch.com/2025/11/17/google-rolls-out-its-ai-flight-deals-tool-globally-adds-new-travel-features-in-search/
- https://www.bgr.com/2028290/google-flight-deals-ai-mode-canvas-travel/
- https://9to5google.com/2026/01/14/gemini-personal-intelligence/
- https://blog.google/products-and-platforms/products/search/personal-intelligence-ai-mode-search/
- https://techcrunch.com/2026/03/17/googles-personal-intelligence-feature-is-expanding-to-all-us-users
- https://blog.google/products-and-platforms/products/gemini/how-gemini-plans-trips/
- https://www.cnbc.com/2026/03/12/google-brings-more-gemini-ai-to-navigation-with-ask-maps-feature.html
- https://techcrunch.com/2026/03/12/google-maps-is-getting-an-ai-ask-maps-feature-and-upgraded-immersive-navigation/
- https://www.macrumors.com/2026/03/12/google-maps-gemini-integration/
- https://9to5google.com/2026/08/06/google-ask-maps-global/
- https://www.neowin.net/news/google-maps-can-now-plan-entire-road-trips-and-even-call-businesses-to-find-appointments/
- https://www.androidheadlines.com/2026/11/google-maps-can-now-build-itineraries-book-appointments-and-check-your-saved-lists.html
- https://blog.google/products-and-platforms/products/maps/ask-maps-immersive-navigation/
- https://www.tomsguide.com/ai/google-just-unlocked-agent-mode-for-gemini-3-1-here-are-7-things-it-can-now-do-for-you
- https://ai-watch-blog.vercel.app/en/posts/2026-08-07-gemini-how-gemini-plans-trips/
- https://www.phocuswire.com/openai-chatgpt-apps-expedia-booking-tripadvisor
- https://www.forbes.com/sites/jasongoldberg/2026/03/10/why-openais-checkout-retreat-spells-trouble-for-its-commerce-strategy/
- https://www.phocuswire.com/news/technology/openai-chatgpt-instant-checkout-travel-intermediaries
- https://www.chatsi.ai/post/openais-pivot-away-from-instant-checkout/
- https://www.tourismtribe.com/chatgpt-instant-checkout-travel-operators/
- https://www.travelanywhere.blog/blog/ai-trip-planners-that-book-flights-tested
- https://prosopo.io/blog/chatgpt-atlas-discontinued/
- https://geminy.ai/2026/08/27/chatgpt-agent-mode-what-it-actually-does-2026/
- https://www.tripadvisor.com/ChatGPT
- https://www.uktech.news/ai/skyscanner-turns-to-chatgpt-with-ai-flight-app-20260227
- https://www.phocuswire.com/news/technology/skyscanner-chatgpt-app-flights
- https://www.travelindustry.news/selfbook-and-tripadvisor-offer-hotel-booking-through-perplexity/
- https://helloaxel.com/en/compare/axel-vs-perplexity
- https://www.webintravel.com/expedia-partners-with-openai-for-access-connectors-perplexity-for-comet-launch/
- https://www.microsoft.com/en-us/microsoft-copilot/for-individuals/do-more-with-ai/general-ai/take-back-your-time-with-copilot-actions
- https://www.microsoft.com/en-us/microsoft-copilot/for-individuals/do-more-with-ai/general-ai/how-to-plan-a-vacation-with-copilot
- https://tineo.ai/blog/best-claude-connectors-for-travel/
- https://spiritt.ai/resources/guides/ai-that-plans-and-books-a-trip
- https://www.travelerstoday.com/articles/60308/20260626/claude-ai-travel-tools-expand-mcp-security-flaw-exposes-21m-booking-records.htm
- https://skift.com/2026/11/09/expedia-goes-live-on-muse-but-its-ai-wins-are-inside-its-own-apps/
- https://www.phocuswire.com/news/online/expedia-hotel-booking-meta-muse
- https://www.conduit.ai/blog/how-ai-agents-book-hotels
- https://skift.com/2026/06/08/apples-rebuilt-siri-opens-new-doors-for-travel-apps/
- https://www.altexsoft.com/travel-industry-news/apples-siri-ai-pushes-travel-apps-toward-smarter-in-trip-help/

OTAs and incumbents
- https://www.sec.gov/Archives/edgar/data/0001324424/000132442426000059/earningsrelease-q32026.htm
- https://www.geekwire.com/2026/were-experimenting-aggressively-how-expedia-sees-ai-reshaping-travel-and-its-own-business/
- https://www.geekwire.com/2026/expedia-group-sees-reward-and-risk-in-the-rise-of-ai-powered-travel/
- https://www.pymnts.com/earnings/2026/expedia-says-travelers-plan-with-ai-agents-but-book-direct/
- https://skift.com/2026/07/31/expedia-acquired-ai-trip-planner-layla-exclusive/
- https://www.hospitalitynet.org/news/4133792/expedia-group-acquires-layla-accelerating-its-ai-powered-trip-planning-and-booking-strategy
- https://www.hoteldive.com/news/expedia-ai-assistant-romie/716315/
- https://www.expedia.com/newsroom/spring-product-release-2024
- https://news.booking.com/bookingcom-enhances-travel-planning-with-new-ai-powered-features--for-easier-smarter-decisions/
- https://news.booking.com/bookingcom-debuts-agentic-ai-innovations-adding-to-its-robust-suite-of-genai-tools-for-customers/
- https://tripian.com/what-is-booking-coms-ai-trip-planner-strategy/
- https://www.cnbc.com/2026/11/05/booking-holdings-q3-earnings-ai-opportunity.html
- https://www.fool.com/earnings/call-transcripts/2026/11/04/booking-holdings-bkng-q3-2026-earnings-call-transcript/
- https://www.phocuswire.com/news/finance/booking-holdings-q3-2026-earnings
- https://www.pymnts.com/earnings/2026/booking-holdings-ai-assistants-slash-costs-and-boost-bookings/
- https://skift.com/2026/09/29/kayak-co-founders-launch-lola-booking-holdings-new-ai-assistant-exclusive/
- https://www.engadget.com/2271730/lola-is-bookingcoms-new-ai-travel-agent/
- https://www.travelweekly.com/Travel-News/Travel-Technology/Booking-Holdings-AI-tool-restaurants-and-activities
- https://www.travelweekly.com/On-The-Record/Steve-Hafner-Lola
- https://www.bostonglobe.com/2026/10/02/business/lola-ai-travel-agent-paul-english/
- https://newstalk870.am/booking-vayo-ai-travel-assistant/
- https://skift.com/2026/09/14/bookings-5-ai-experiments-and-why-agodas-is-next/
- https://www.forbes.com/sites/peterhigh/2026/07/29/how-pricelines-cto-is-rebuilding-travel-with-ai/
- https://www.customerexperiencedive.com/news/priceline-travel-booking-agentic-ai-penny/822142/
- https://www.hospitality.today/article/claude-was-the-threat-booking-made-it-the-product
- https://techcrunch.com/2026/11/05/airbnb-says-its-launching-an-ai-travel-agent-in-the-first-half-of-2027/
- https://techcrunch.com/2026/02/13/airbnb-says-a-third-of-its-customer-support-is-now-handled-by-ai-in-the-u-s-and-canada/
- https://www.customerexperiencedive.com/news/airbnb-reduces-customer-support-cost-per-booking-17/874307/
- https://www.fastcompany.com/91425623/brian-chesky-on-airbnb-ai-and-social-reinvention
- https://www.kayak.com/news/introducing-kayak-ai/
- https://seekingalpha.com/pr/20267224-kayak-introduces-ai-mode-conversational-travel-search-just-in-time-for-holiday-planning
- https://www.ai-tools-hq.com/tools/kayak-ai/
- https://skift.com/2026/08/02/amex-gbt-kayak-ai-agentic-booking-business-travel/
- https://medium.com/tripadvisor/cracking-the-code-to-the-ai-travel-planner-27d8d0f222c8
- https://getaibriefs.com/tools/tripadvisor-ai/
- https://www.trip.com/newsroom/tripgenie-new-features-2/
- https://www.travelandtourworld.com/news/article/trip-com-group-unleashes-ai-power-at-itb-berlin-2026-as-tripgenie-transforms-global-travel-booking/
- https://sequenced.ai/articles/trip-com-group-blueprint
- https://www.phocuswire.com/hts-assist-ai-agent-hopper
- https://hts.hopper.com/legal/Frontier-Airlines-Disruption
- https://hts.hopper.com/legal/hts-connect-missed-connection-guarantee-flair-customers
- https://ftc.gov/news-events/news/press-releases/2026/07/travel-app-hopper-pay-35-million-settle-ftc-allegations-it-charged-fees-without-consent-deceived
- https://finance.yahoo.com/sectors/technology/articles/getyourguide-launches-ai-powered-features-130000622.html
- https://www.tomsguide.com/ai/i-asked-chatgpt-and-claude-to-plan-my-next-dream-trip-to-japan-with-viator-one-delivered-much-better-destinations
- https://uncompromised.travel/travel-intelligence/getyourguide-vs-viator-vs-klook

Corporate travel
- https://investors.navan.com/news-releases/news-release-details/navan-announces-strong-second-quarter-fiscal-year-2027-results
- https://finance.yahoo.com/markets/stocks/articles/navan-q2-earnings-call-highlights-230340815.html
- https://navan.com/blog/business-travel-booking-tools-last-minute-changes
- https://navan.com/blog/duty-of-care-travel-management
- https://www.catchagent.ai/blog/reviews/navan-review
- https://www.morningstar.com/news/business-wire/20260819835051/perk-leads-the-race-in-travel-and-spend-mcp-as-the-first-platform-to-launch-travel-booking-expense-submission-and-event-creation-capabilities-via-ai-assistant
- https://www.perk.com/
- https://accomy.com/blog/agentic-ai-in-corporate-travel-the-shift-to-autonomous-booking/
- https://www.businesstravelnews.com/Technology/Spotnana-Introduces-AI-Tools-for-Agents-as-Part-of-New-AI-Architecture
- https://www.amexglobalbusinesstravel.com/press-releases/amex-gbt-launches-business-travel-agent-to-agent-infrastructure-debuts-egencia-ai-connector-in-claude/
- https://www.amexglobalbusinesstravel.com/press-releases/amex-gbt-reloads-egencia-with-conversational-ai-assistant-and-concur-expense-integration/
- https://www.concur.com/blog/article/agentic-ai-travel-expense-management
- https://erp.today/sap-concur-fusion-2026-sap-embeds-joule-ai-across-travel-expense-and-payments-workflows/
- https://resources.rework.com/tools/spend-expense/ramp-vs-brex

Airlines, hotels, supply-side
- https://www.bloomberg.com/news/articles/2026-11-11/united-blocks-ai-agents-from-booking-flights-ahead-of-holidays
- https://www.washingtonpost.com/travel/2026/11/12/united-airlines-blocks-ai-agents-booking-flights/
- https://www.forbes.com/sites/suzannerowankelleher/2026/11/12/united-airlines-blocks-ai-agents-booking-flights/
- https://techcrunch.com/2026/11/12/united-airlines-blocks-ai-agents-from-booking-flights-citing-cybersecurity-risks/
- https://www.futuretravelexperience.com/2026/08/delta-rolls-out-ai-powered-concierge-to-all-skymiles-members-for-personalised-travel-support/
- https://www.customerexperiencedive.com/news/delta-simplified-rebooking-ai-assistant-nps-boost/824980/
- https://viewfromthewing.com/deltas-ai-told-a-passenger-her-flight-home-was-safe-then-canceled-it-and-demanded-double-to-rebook/
- https://aviationa2z.com/index.php/2026/08/06/delta-ai-told-passenger-return-flight-was-booked-then-canceled-ticket/
- https://skift.com/2026/09/29/hilton-tech-exec-says-ai-agents-put-otas-under-real-threat/
- https://www.hoteldive.com/news/artificial-intelligence-powered-hotel-search-tool-launches-2026/828419/

Failures and accuracy
- https://futurism.com/artificial-intelligence/ai-hallucination-landmarks-tourists
- https://euronews.com/travel/2026/01/30/how-an-ai-generated-travel-website-sent-tourists-to-a-non-existent-hot-spring-attraction
- https://kioncentralcoast.com/news/2026/10/03/bad-travel-advice-from-ai-from-bogus-bars-to-visa-fails/
- https://www.travelanywhere.blog/blog/chatgpt-vs-gemini-vs-claude-trip-planning-2026-tested-comparison
- https://www.trripah.com/blog/ai-trip-planning-honest-review-2026
- https://firstpagesage.com/seo-blog/which-ai-is-best-for-travel-planning/
