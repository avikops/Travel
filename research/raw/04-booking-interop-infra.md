# 04 — Booking & Interoperability Infrastructure for an AI Trip Planner (state as of 2026-11-17)

**Owner:** Deep-research agent 4 of 7 (booking / integration layer); gap-fill pass by a second agent on the same date
**Date:** 2026-11-17

## Method and confidence notes (read first)

- **Pass 1 limits.** All research went through WebSearch. WebFetch was blocked by the container's network allow-list (duffel.com, phocuswire.com, skift.com and flightpowers.com all failed DNS), so I could not read any primary page in full. Partway through, the WebSearch budget shared by all parallel agents ran out. Areas this cut short: Skyscanner/Kayak affiliate status, Kiwi's MCP, Expedia's B2B MCP go-live, Booking.com's Claude connector, Travelfusion, Klook/Tiqets/Headout/Fever, SevenRooms/Tock/TheFork, FlixBus/Busbud, CarTrawler, Uber, and seller-of-travel law details. For those I used background knowledge (training data to about mid-2026), labelled **[background]**.
- **Pass 2 (gap-fill, same day).** A second agent ran 60 more WebSearch queries (no WebFetch), aimed at every [background] row, Duffel, agentic payments, post-booking and accreditation. Running notes with URLs are in `research/notes/04-gapfill-notes.md`. Results of this pass:
  - Most [background] items were re-tagged as [verified] or [claimed], or corrected.
  - **Corrections:** Duffel Stays inventory is about 1.6M properties, not 2M+. Duffel automatically accepts airline-initiated changes for only about 24 airlines. Mastercard's first live Asian agentic ride was in Korea (via hoppa), not a Hong Kong taxi. The Ryanair v. Booking.com CFAA jury verdict was set aside in January 2025. Perplexity's hotel booking launched in March 2025. CarTrawler is now owned by Expedia (deal closed 1 Sep 2026). Tock's API cannot create reservations.
  - **New since pass 1:** Duffel powers flights in Meta's Muse agent (Sep 2026). The Amadeus–Anthropic Claude Code toolkit is on a waitlist. Travelport TripServices offers a self-service sandbox. Visa TAP is live with eDreams ODIGEO. ChatGPT added restaurant booking (OpenTable, Resy, Yelp). Ferryhopper and Kiwi run their own MCP servers.
  - **Still [background]:** items no search reached, mostly EU/UK package law, US DOT rules, PCI and chargebacks.
- **Tags:**
  - **[verified]**: corroborated by two or more independent 2026 sources, or by an official vendor or developer page seen in search results.
  - **[claimed]**: a single source, a vendor's own marketing, or trade-press repeating a vendor.
  - **[inferred]**: my own analysis.
  - **[background]**: prior knowledge, not re-checked in either pass. Re-verify before any commercial decision.

---

## 0. Executive summary

1. **The open self-serve era of travel APIs is over.**
   - Amadeus Self-Service shut down on 17 July 2026 **[verified]**. Its replacement for developers, a Claude Code toolkit announced with Anthropic on 3 Sep 2026, is waitlist-only and has no published access or pricing terms **[verified]**.
   - Kiwi Tequila has been partner-only since May 2024 **[verified]**.
   - TripIt's public API no longer accepts new integrations (Feb 2026) **[verified]**.
   - Booking.com's Demand API needs Managed Affiliate status, and reportedly written approval to use AI **[claimed]**.
   - Expedia Rapid needs approval plus a compliance review **[verified]**.
2. **Duffel is the one credible self-serve "book-and-manage" rail for flights, stays and cars, alongside Nuitée LiteAPI for hotels.** Both let a startup transact without IATA accreditation:
   - Under Duffel's **Managed Content**, Duffel tickets, services and settles orders as the licensed agent of record, using its own or a partner's IATA accreditation. Going live requires KYC **[verified, Duffel services agreement and help centre]**.
   - Duffel is now the flights rail inside **Meta's Muse agent** (US, launched 8 Sep 2026). It says AI platforms are among its fastest-growing segments and it has passed a $1bn TTV run rate **[verified]**.
   - LiteAPI publishes an open-source MCP server that can search, book and manage **[verified]**.
   - Ground (Distribusion, Trainline Partner Solutions, Omio, Rail Europe, Busbud, Ferryhopper) and activities (Viator, GetYourGuide, Tiqets, Musement, Headout) are reachable through partner programmes. Approval is required, but these programmes are designed for distributors **[verified]**.
3. **Supplier-side agentic infrastructure became real in 2025–26, but incumbents control it:**
   - Sabre's MCP server has about 80 airline and agency clients piloting or in production (Sept 2026) **[claimed]**. It powers Mindtrip Flights (launched 6 May 2026, Sabre Mosaic and PayPal) **[verified]**.
   - Travelport launched **TripServices** (11 Jun 2026), a cloud-native API layer for AI booking with self-service sandbox credentials **[verified]**.
   - Distribusion launched a Retailer API MCP server (Feb 2026) **[verified]**.
   - Expedia announced a B2B MCP server "in the coming months" (May 2026). As of mid-Nov 2026 I still find no launch confirmation **[verified as announced; launch unconfirmed]**. Expedia also bought CarTrawler (closed 1 Sep 2026) **[verified]**.
   - Google AI Mode launched agentic hotel booking in the US (Aug 2026), with partners as merchant of record and UCP as the long-term protocol **[verified]**.
4. **Consumer-surface agentic checkout is real but tiny, and mostly hands off to the supplier:**
   - OpenAI scaled back ChatGPT Instant Checkout in March 2026 and moved to "discover in AI, buy on site" **[verified]**.
   - The OTAs' and Uber's ChatGPT apps hand off to their own checkout **[verified]**.
   - Volumes are small:
     - **Booking Holdings Q3 2026:** LLM referrals are "significantly less than 1%" of Booking.com room nights, though accelerating **[verified]**.
     - **OpenTable in ChatGPT:** seated about 190k diners in September, roughly 0.1% of monthly volume **[claimed]**.
     - **Uber Q3 2026:** reported only **four** rides arranged by third-party AI agents **[claimed]**.
5. **Airlines are pushing back on unsanctioned agents, while card networks build sanctioned rails:**
   - On 11 Nov 2026 United restricted unauthorized third-party AI agents from booking and from MileagePlus accounts, including via OTAs **[verified]**.
   - Two days later, Travelport, Booked AI, Basis Theory and Mastercard announced a live, sanctioned agentic NDC booking using Agent Pay tokens, with the airline as merchant **[verified]**.
   - Visa's Trusted Agent Protocol is live with 30+ European issuers, and with eDreams ODIGEO for travel (Jul 2026) **[verified]**.
   - In practice, **screen-scraping and computer-use booking now carry reputational and ToS risk; sanctioned API rails plus network agent tokens are the path forward** **[inferred]**.
6. **The interoperability ceiling sits at post-booking.**
   - Search and book are attainable for flights, hotels, rail and activities.
   - Servicing (changes, IROPs re-accommodation, refunds, loyalty) is only reliable for bookings made through your own rail. Even there, Duffel automatically accepts airline schedule changes for only about 24 airlines **[verified, Duffel help centre]**.
   - Bookings made elsewhere can only be observed (email parsing, AwardWallet), not managed. That is the accountability gap.

---

## 1. Flights

### 1.1 Access paths

| Path | Who can get access | Commercial model | Operations | Coverage | Pain points / status |
|---|---|---|---|---|---|
| **Duffel** | Self-serve sign-up with test mode. Going live needs **KYC verification**, after which Duffel activates you as a merchant in production **[verified, Duffel services agreement]**. **No IATA/ARC needed on Managed Content**: Duffel tickets, services and settles as agent of record under its or a partner's IATA accreditation. You can mix your own IATA number for some airlines with Managed Content for others **[verified, help.duffel.com]**. | $3.00 per confirmed order; 1% of order value on Managed Content (older help article said 0.5%); $2 per paid ancillary; excess-search fee above a 1,500:1 search-to-book ratio at $0.005 per search **[verified via multiple secondary snapshots of duffel.com/pricing, May 2026]**. Possible ~2% FX fee **[claimed]**. You set your own markup **[background]**. | Search, price, book, hold (where the airline supports it), seat maps, bags, loyalty numbers. Changes via Order Change requests/offers. Cancellations, including **refunds to airline credits** **[verified, Duffel docs and changelog]**. **Airline-initiated changes:** webhook `order.airline_initiated_change_detected` plus an AIC API (accept, change, cancel) **[verified]**. **Only about 24 airlines support automatic AIC acceptance.** For most others, post-AIC change or cancel is not available via API, and orders on your own IATA number must be resolved with the airline and PATCHed back **[verified, Duffel help/docs]**. | "300+" airlines in older material; Duffel's Sep 2026 Muse announcement says 500+ airlines **[claimed]**. Includes major NDC carriers and LCCs **[background]**. | Best developer experience in the market **[claimed]**. **No official Duffel MCP server.** Only community MCPs exist (e.g. FortripEngineering `duffel-mcp` v0.1.0, `@taskingagency/mcp-duffel-travels`) **[verified absence in search]**. Powers flights in **Meta Muse** (US, 8 Sep 2026) and Rippling Travel (Aug 2026) **[verified]**. Duffel Cars and Stays are live **[verified]**. IROPs re-accommodation is still largely manual **[inferred from AIC limits]**. |
| **Sabre (Dev Studio / Mosaic APIs and the Sabre MCP server)** | Transactional APIs need a **PCC, or an iPCC (API-only agency access)**. Without IATA/ARC you can obtain one under a **host agency or consolidator** via a downline agreement. Production requires PCC provisioning, certification, and an agreement amendment per new API or region **[verified for PCC/iPCC definitions, developer.sabre.com; claimed for process]**. Separately, Sabre's **Developer Hub MCP** (developer.mcp.sabre.com/mcp) is public, read-only documentation, with no auth, token or PCC **[verified]**. | GDS segment incentives flow to the agency. Contract-specific fees **[background]**. | Full lifecycle: shop, price, book, ticket, exchange, refund, seat maps, ancillaries, NDC **[background]**. Exposed via agentic APIs and MCP (launched Sept 2025; ~80 airline and agency customers piloting or live by Sept 2026) **[claimed, Sabre PR]**. | GDS plus activated NDC carriers through one connection **[claimed]** | Heavy onboarding. Mindtrip is the reference consumer AI deal **[verified]**. |
| **Travelport (Travelport+, JSON APIs, "TripServices")** | **TripServices** launched 11 Jun 2026 as a cloud-native API suite for AI-driven booking **[verified, Travelport PR and Skift]**. The developer portal advertises **self-service credentials, sandbox and guided onboarding** **[verified, developer.travelport.com FAQ]**. Production NDC still requires IATA or TIDS, being on Travelport+, and an NDC-live country. Some airlines (United, Emirates) whitelist, and Air Canada requires registration **[verified, Travelport support docs]**. Travelport announced a Cognizant + Anthropic collaboration in May 2026 **[claimed]**. | Contract; no published startup tier **[verified absence]** | Full lifecycle. Live end-to-end agentic NDC booking with Booked AI and Mastercard Agent Pay (13 Nov 2026) **[verified]**. | GDS plus NDC | The sandbox is now reachable without a contract. Production still needs accreditation plus per-airline NDC registration. |
| **Amadeus Enterprise** | Self-Service portal **decommissioned 17 July 2026**: keys disabled, SDK repos archived **[verified]**. Enterprise needs IATA/ARC and a formal agreement **[verified, secondary]**. **Amadeus × Anthropic (3 Sep 2026):** a Claude Code developer toolkit (connectivity, docs, auth, content) is **waitlist-only**. A Claude Cowork plugin for travel sellers was announced, but sources conflict on whether it has shipped. Access and pricing relative to the old portal are undisclosed **[verified]**. | Contract | Full lifecycle | Largest GDS. UCP vertical co-developer, with no UCP timeline committed **[claimed]**. | No self-serve path left today. Join the Claude Code toolkit waitlist **[inferred]**. |
| **Kiwi.com Tequila** | Partner-only since May 2024, refocused on airlines, airports and DMCs. Existing partners kept access **[verified]**. New partners reportedly need a live product or established distribution case **[claimed]**. One source claims the portal fully closed 17 July 2026 **[claimed, unconfirmed]**. | Free registration; revenue share on bookings **[claimed]** | Search plus "virtual interlining" booking, where Kiwi is merchant **[background]** | Strong LCC and self-transfer coverage | Effectively unavailable to new startups as an API. **Kiwi runs its own hosted MCP at mcp.kiwi.com**: search plus booking deeplinks, usable from Claude, ChatGPT and Cursor, built with Alpic. A ChatGPT app was previewed in Dec 2025. Kiwi claims MCP searches grew 10× since Jan 2026 **[verified]**. Self-transfer carries missed-connection risk **[background]**. |
| **Mystifly (SSP)** | B2B contract, quote-based on volume, markets and sources **[claimed]** | Quote-based | Search, book, post-booking servicing **[claimed]** | GDS + NDC + LCC + consolidator; "700+ airlines" **[claimed, reseller page]** | Strongest for consolidator fares in Asia/Middle East **[background]**. No MCP found. |
| **Travelfusion** | B2B; contact sales@travelfusion.com. No startup programme found **[verified absence]** | Contract; one local report says no extra booking fee **[claimed]** | tfFlight API: shopping, booking, merchandising, payment, servicing **[claimed, Travelfusion site]** | **400+ LCCs and 55+ NDC carriers** **[claimed, Travelfusion site]** | Enterprise-oriented; no MCP found |
| **Hopper HTS** | B2B for banks, airlines and loyalty programmes (Capital One, RBC, CommBank, Serko) **[verified]** | Revenue share; fintech add-ons **[background]** | Flights API (multi-provider, fare rules, seats, bags) and a new Hotels API (Aug 2026) **[claimed, HTS]**. **Cancel For Any Reason, Disruption Guarantee/Assistance** APIs (OAuth2 REST) **[claimed]**. | Frontier NDC live **[claimed]** | Targets large distribution partners, not startups. **The fintech protection APIs could be layered onto bookings to address "accountability"** **[inferred]**. |
| **Skyscanner / Kayak** | **Skyscanner:** Travel API applications are reviewed against official criteria: an established business with **>100k monthly traffic** and brand alignment **[verified, Skyscanner partner support]**. No self-serve sandbox. Lighter affiliate-link tier via the partner portal **[claimed]**. **Kayak:** affiliates.kayak.com offers flight, hotel and car APIs plus Inline/CompareTo Ads APIs. Access is by application, manual approval and an account manager; small developers are often declined **[verified for product; claimed for gate]**. | CPC/CPA. Kayak affiliate ~$0.08–1.90 per click or sale **[claimed]**. Skyscanner forbids caching prices **[claimed]**. | Search and deeplink only (metasearch; no booking) | Very broad | Affiliate-only, and gated by traffic. You don't own servicing, but you also carry no liability. |
| **Google Flights / ITA** | **No API.** QPX Express closed in 2018 **[background]**. ITA Matrix is web-only. | — | — | — | Scraping violates ToS. Google is building its own agentic flights in AI Mode; at the hotel launch, PhocusWire reported flights are "still waiting" **[verified]**. UCP has no live flights vertical **[verified]**. |
| **NDC direct** | Airline-by-airline. Generally requires IATA/TIDS plus a bilateral agreement **[background]** | Varies; some airlines pay NDC incentives or levy GDS surcharges | Full Offer/Order where the airline supports it | One airline per integration | Not worth it before scale. Use an aggregator (Duffel, Travelport, Sabre). |

### 1.2 How Mindtrip built flights (reference architecture)

- **Launch:** Mindtrip Flights launched on **6 May 2026** **[verified]**:
  - Sabre Mosaic Air APIs supply inventory, pricing, availability and ticketing.
  - Sabre also handles after-sales service **[claimed]**.
  - PayPal processes payment and verifies identity, and offers BNPL. A launch promo gave 5,000 PayPal points on BNPL bookings over $250 **[verified]**.
- **How autonomous it is:** Accounts conflict. Some call it "fully autonomous", others "not a fully autonomous purchasing agent" **[verified conflict]**. The user confirms in a chat checkout.
- **Lesson [inferred]:** Mindtrip avoided becoming an IATA ticketing agent and payment processor by renting both from Sabre and PayPal. It owns the conversation and the checkout UX. Uptake remains the open question: a Siften piece cites survey data that only about 2% of leisure travellers would let AI book for them **[claimed]**.
- **Contrast: Meta Muse (Sep 2026)** uses Duffel for flights, US only. Stays are not yet in the integration, and Meta has not said who is merchant of record **[verified/claimed]**. This shows the Duffel rail is accepted at big-platform scale **[inferred]**.

---

## 2. Hotels and stays

| Path | Access | Commercial model | Ops | Coverage | Notes |
|---|---|---|---|---|---|
| **Expedia Rapid API** | Apply, get approved, certify, then pass a **compliance review before launch**. Launch requirements differ for B2C vs B2B **[verified, developers.expediagroup.com]** | Negotiated revenue share. Expedia is usually merchant of record on "Expedia Collect" rates. Partner booking charges are allowed only if labelled as the partner's ("affiliate booking charge", never "fee") and kept separate from taxes and fees **[verified]**. Rates not public **[verified]**. | Search, price check, book, cancel, itinerary retrieval. Also Vrbo inventory, Rapid Car API, and per-rate MoR flags **[verified for car MoR flag; background for Vrbo]** | ~700k+ properties plus Vrbo **[background]** | The Expedia **B2B MCP server / Intelligent Experience Platform** was announced May 2026 at Explore 26, "in coming months". Pilot partners and terms undisclosed. **Still no launch confirmation by mid-Nov 2026** **[verified]**. A separate **Expedia Dev MCP** helps with docs and integration testing **[verified, Expedia partner blog]**. Expedia **acquired CarTrawler** (announced 20 May 2026, closed 1 Sep 2026) **[verified]**. |
| **Booking.com Demand API** | Managed Affiliate Partner status, a signed contract, and account-manager enablement. Ordinary affiliate status (e.g. via CJ) does **not** grant Demand API access **[claimed, multiple secondary]**. General Partner Terms v5 reportedly prohibit using an AI system to perform the agreement without **prior written approval**, and bar training AI on Booking materials **[claimed; single secondary source, primary text not found]**. Customer Terms (15 Sep 2025) reportedly bar unauthorized automated or AI browser assistants **[claimed]**. | Affiliate commission (CPA). Booking.com is merchant or the hotel collects **[background]**. | Demand API 3.2 covers accommodations, **cars, flights and attractions** endpoints plus orders **[verified, developers.booking.com]** | ~3M+ listings **[background]** | Hardest gate for an AI startup. **Booking.com's official Claude connector** (launched ~23 Apr 2026 in Anthropic's consumer-connector wave) is **search only**: no booking, account access or payments. Remote MCP over OAuth **[verified, developers.booking.com/mcp]**. Booking.com is also a Google AI Mode hotel launch partner, a UCP co-developer, and has a ChatGPT app **[verified]**. |
| **Nuitée LiteAPI** | **Self-serve** developer sign-up; Enterprise tier for scale **[verified/claimed]** | You set the commission or margin, including per query; Dynamic Markup **[verified, Nuitée updates]**. MCP tool calls and AI-completed bookings billed per use **[claimed]**. | Search, rates, prebook, book, cancel, retrieve. Built-in payment option, so LiteAPI can be merchant **[background]** | Aggregated wholesale (2M+ properties) **[background]** | **Open-source and hosted remote MCP** for Claude, GPT and Gemini: search, rate-check, book, manage **[verified]**. Lowest-friction path. |
| **Duffel Stays** | On top of a Duffel account. Separate live-access approval is likely but no public process was found **[background]** | The accommodation provider pays commission and Duffel shares it with you; your share grows with volume **[verified, Duffel pricing quote]** | Search, rates, quote, book, cancel; negotiated rates API; rate-source visibility; test hotel in test mode **[verified, docs/changelog]** | **~1.6M properties**, with claimed +10,000% growth over 12 months **[claimed, Duffel/Muse coverage]** (corrects the earlier "2M+") | Single contract with flights and cars. Used by Rippling Travel **[verified]**. A Duffel–Katanox partnership targets hotel booking breakdowns for AI agents **[claimed]**. Not yet part of Meta Muse. |
| **Hotelbeds (Apitude)** | Commercial agreement; tiered access by volume; **certification before go-live**; "four-step" onboarding portal **[claimed, integrator and competitor pages]** | Net rates; you mark up **[background]**. No public pricing **[claimed]**. | Full booking lifecycle | ~300k hotels, strong in leisure and Mediterranean **[background]** | No public minimums found. B2B net rates often carry **parity restrictions**: you can't display them publicly below retail without packaging **[background]**. |
| **WebBeds** | API connectivity to **approved partners** via WebBeds Marketplace. Structured onboarding, then property and room mapping. Request via sales form **[verified, webbeds.com]** | Net rates, contract | Full lifecycle | Large | Sales-gated |
| **RateHawk (Emerging Travel Group)** | Needs an active RateHawk B2B partner account. API key and token; sandbox, then **certification**, then production keys (ETG API v3) **[claimed, integrator pages]** | Net rates | Full lifecycle | Large | Relatively accessible to registered agencies **[background]** |
| **Agoda** | Official Demand API docs (developer.agoda.com/demand). After commercial terms you get a welcome package, then IP whitelisting, QA, a UAT booking, and go-live. Two models: **Fulfill Assisted** (Agoda does post-booking service) or **Partner Fulfillment** **[verified, Agoda developer docs]** | Affiliate CPA ~4–7% tiered **[claimed]** | Search 2.0 (Oct 2026), booking and post-booking APIs; Booking List pagination (Nov 2026) **[verified, Agoda changelog]** | APAC strength | Actively maintained booking API; partner-gated. Fulfill Assisted suits a startup with no service desk **[inferred]**. |
| **Airbnb** | **No public guest API.** Partner API is invite-only for software and host partners. No official MCP, ChatGPT app or Claude connector as of Nov 2026 **[claimed, consistent across sources]**. Airbnb's own agent is expected in 2027 **[claimed]**. | — | — | — | Third-party "Airbnb MCPs" read public pages or misuse private APIs, a ToS risk **[claimed]**. Vacation rentals are reachable via Vrbo (Expedia Rapid), Booking.com, or PMS-side MCPs (e.g. Hospitable) **[claimed]**. |
| **Selfbook / direct hotel booking engines** | Partnership | Hotel is merchant; Selfbook does payments and tokenization **[verified]** | Book direct at hotel rates | ~140k properties **[claimed]** | **Perplexity's in-chat hotel booking** launched **March 2025** with Selfbook plus Tripadvisor content **[verified]**. No 2026 update found. |
| **Google AI Mode (as a channel, not an API)** | US only, English, about 10 large chains and OTAs (Booking, Expedia, Marriott, Hilton, IHG, Trip.com, etc.) **[verified]** | Partner is merchant of record and handles post-booking **[verified]** | — | — | Independent hotels are booked through OTAs **[claimed]**. UCP hotel vertical announced at Google Marketing Live (20 May 2026). Co-developers: Amadeus, Booking.com, Hilton, Marriott and others **[verified]**. |

---

## 3. Ground transport

### 3.1 Rail

| Path | Access / model | Ops | Coverage | Notes |
|---|---|---|---|---|
| **Trainline Partner Solutions (Global API)** | B2B contract; no public sandbox; average integration ~12 weeks **[claimed, Trainline/API catalogue]**. Also an agent tool and white-label **[verified]** | Search, book, ticket, (refund/exchange per operator rules) **[background]** | 270+ rail and coach operators, 40 countries (Platform One) **[claimed]** | B2B net ticket sales +14% to £1.1bn; Global API in Europe +58% (May 2026). Partners include Amadeus Cytric, Spotnana, Navan **[verified]**. Primarily TMC-oriented. |
| **Distribusion** | B2B Retailer API; contact a partnership manager **[verified]** | Search, book, post-sales. **Retailer API MCP server (Feb 2026)**; Post-Sales AI Bot (May 2025) **[verified, Distribusion docs]** | Bus, rail, ferry, transfers. SNCF, DB, Trenitalia, Iryo, **Amtrak**, Eurostar, KAI Indonesia; Interrail reservations (Apr 2026) **[claimed]** | **Best single multimodal ground API for an AI planner** **[inferred]**. 1,500–2,000+ clients **[claimed]**. |
| **Omio** | Affiliate Search API plus deeplinks (~6% per Travelpayouts; Omio says the rate varies by market) **[claimed]**. B2B offers a **plug-and-play API or white label**. The **Booking API is for partners who become merchant of record** **[verified, Omio B2B]**. Meta Search API also available. | Search (affiliate); book (MoR partner) | 3,000+ operators: trains, buses, flights, ferries **[claimed, Omio]**. Partners include Uber, Kayak, Google, Iryo, LNER; TUI white-label (May 2026); easyTrain (Mar 2026) **[verified]** | Good fallback. The Uber deal is a commission share **[claimed]**. |
| **Rail Europe** | Centralized **API platform for global distributors launched Feb 2026**, with commission structures, group booking and commercial support **[claimed]**. Distributed via Juniper; Headout uses the Rail Europe API (Apr 2025) **[verified]** | Book, ticket | European rail | Commercial agreement first; onboarding "within days" via Juniper **[claimed]** |
| **G2Rail, SilverRail** | G2Rail: B2B API (Europe, Asia) **[background; nothing found in pass 2]**. SilverRail: rail connectivity and transaction layer behind Rail Europe (since 2017) and historically Expedia rail; TMC/operator-oriented **[verified, older trade press]** | — | — | Not startup-facing |
| **Amtrak** | No public booking API. Accessible via Distribusion **[claimed]** and GDS rail **[background]** | — | — | — |
| **Japan (JR)** | No public API. Shinkansen tickets resold via Klook and 12Go-type platforms; JR Pass via resellers **[background/inferred]** | — | — | Gap |
| **12Go (Travelier)** | Affiliate via agent.12go.com: deeplinks, search form, white label and **an API**, with a 30-day attribution window **[verified, 12Go]**. Affiliate 50% revenue share, about $3 average commission **[claimed, Travelpayouts]**. B2B reseller programme for agencies and hotels: 50% of 12Go's commission plus up to 20% price top-up **[claimed]**. 2,000+ partners **[claimed]** | Deeplink/affiliate; API | SE Asia (and wider Asia) buses, trains, ferries | Best Asia ground fallback **[inferred]** |

### 3.2 Buses and ferries

- **FlixBus:** static affiliate programme (TradeTracker) plus a "dynamic" API tier, which you apply for with company details and traffic figures **[verified, FlixBus partners page]**. Public `global.api.flixbus.com` endpoints are unofficial **[claimed]**.
- **Busbud:** API partnership programme and white-label for bus and rail inventory, plus an affiliate programme (~5%) **[verified for programme; claimed for rate]**.
- **Ferryhopper:** partner hub with affiliate, API, tour-operator and **AI-agent** tracks, plus its **own MCP server** for real-time ferry data **[verified, partners.ferryhopper.com]**.
- **Direct Ferries, Bookaway:** affiliate programmes **[background; not found in pass 2]**.
- **Distribusion** covers much of this through one contract **[verified]**.

### 3.3 Car rental

- **Duffel Cars** launched in 2026: 40 providers, 40,000+ locations, 200 countries **[verified]**.
- **Expedia Rapid Car API** has documented launch requirements and per-rate merchant-of-record flags **[verified]**.
- **CarTrawler is now part of Expedia Group B2B.** The deal was announced 20 May 2026 (reported ~$350M) and closed 1 Sep 2026. CarTrawler serves 300+ travel brands, including 70+ airlines **[verified]**. Expect CarTrawler content to converge with Rapid over time **[inferred]**.
- **Rentalcars Connect** (Booking Holdings): B2B white label for airlines and OTAs. Affiliate ~6% **[claimed]**. Programmatic car booking via the Priceline Partner Network API with Rentalcars content, which reportedly expects ≥5 bookings per day **[claimed]**.
- **Booking.com Demand API** also exposes cars **[verified]**.

### 3.4 Transfers and rides

- **Mozio:** API, widget or white-label. 3,000+ providers in 180 countries; feeds Rome2Rio (2025) **[claimed]**. No AI-specific integration found.
- **hoppa:** affiliate and B2B **[background]**. It was the merchant in Mastercard's first live agentic transaction in Korea (Mar 2026) **[verified]**.
- **Uber:**
  - The **ChatGPT app** (from the Oct 2025 app cohort) is US-only and on-demand only. You set up the trip in ChatGPT; the request and payment complete in the Uber app **[verified]**.
  - Programmatic ride requests for third parties remain restricted **[background]**.
  - Uber reported only **4 rides arranged by third-party AI agents in Q3 2026** and expects its own app to stay central **[claimed]**.
- **Bolt and Yango:** have ChatGPT ride-booking flows; Bolt's covers the EU and UK **[claimed]**.
- **Lyft:** no public AI-agent partner programme found. Ride requests are exposed via Curb Flow's open API (live in NYC, Jul 2026) **[verified]**. Lyft's Anthropic deal covers customer support, not booking **[verified]**.
- **Rome2Rio:** a planning and meta layer. Search API docs (v1.2/1.4) exist; the API returns no live prices **[verified, docs]**. New-user access terms are unclear **[background: long closed to new users; unconfirmed]**.

---

## 4. Activities and dining

### 4.1 Activities

| Path | Access tiers | Commission | Bookable programmatically? |
|---|---|---|---|
| **Viator Partner API** | Basic (instant, no prequalification), Full, Full + Booking (authorization required), plus a separate Merchant partner type. Basic and Full redirect to viator.com; Full + Booking keeps the transaction on your site via Viator payments **[verified, partnerresources.viator.com]** | "Standard commission". Third parties cite ~8% and a 30-day cookie **[claimed]**. No fees for API access **[verified]**. | **Yes** (Full + Booking or Merchant). A hosted Viator "experiences" MCP connector (2 read-only tools, no booking) appears in directories **[claimed]**. |
| **GetYourGuide Partner API** | BASIC/LIMITED_READ (catalogue), READ (live availability and pricing), BOOKING (end-to-end including payment) **[verified, partner-api-spec mirror]**. Free to join **[claimed]** | Affiliate rates not published. Supply-side commission is 20–30%, so affiliate share is lower **[claimed]** | **Yes**, at BOOKING tier. Only third-party MCPs exist **[verified absence of official]** |
| **Tiqets Distributor API** | Free, after an **eligibility review**. Connect your own checkout for order create and cancel, plus sales data. A separate **Booking API** is offered based on your performance **[verified, tiqets.com]** | Varies | **Yes** |
| **Musement (TUI) Partner API** | **Affiliate** (Musement's Stripe payment flow) or **Merchant** (you are MoR; "no-payment" flow needs special authorization). Sandbox plus production; OpenAPI v3.5.0 **[verified, partner-api.musement.com]** | Varies | **Yes**: search, availability, cart, order, cancellations, webhooks |
| **Headout Partner API** | **API partners** (full booking flow) vs **affiliates** (deeplinks). API-key auth **[verified, partner.headout.com]** | Varies | **Yes**: availability, booking, tickets, cancellations, reschedules |
| **Klook** | Affiliate programme; public Open API is **supply-side** (merchants and channel managers). A reseller Partner API is described only by third parties **[verified for supply-side; claimed for reseller API]** | Varies | Unclear for resellers |
| **Fever** | Affiliate programme for traffic partners. Feeds or custom API for selected larger partners **[verified, business.feverup.com]**. A Fever MCP server and partner Reporting API are reported **[claimed]** | Varies | Selected partners only |

### 4.2 Restaurants

| Platform | Programmatic booking for a third party? |
|---|---|
| **OpenTable** | Partner-gated: affiliate directory API, restaurant partner APIs, an "In House Booking (Voice AI) API" for approved voice-AI vendors. Signed agreement and QA review; 3–4 weeks onboarding; OAuth2 **[claimed, consistent]**. No public MCP **[claimed]**. **ChatGPT reservations (10 Aug 2026)**, global; card-required bookings hand off to OpenTable. About 190k diners seated in September **[verified/claimed]**. |
| **Resy (Amex)** | No public API. Partner API only for approved POS, CRM, loyalty and discovery partners. The consumer API is undocumented, and using lifted session tokens violates ToS **[verified]**. **Resy reservations in ChatGPT launched 10 Aug 2026** (US) **[verified, Resy newsroom]**. |
| **Yelp** | Reservations and waitlists in ChatGPT (US/Canada, Aug 2026) **[verified]** |
| **SevenRooms** | Versioned REST API (OAuth2); developer docs gated to approved venue operators and integration partners **[claimed]**. Listed as a Google AI Mode UK booking partner **[verified]**. |
| **Tock (Amex)** | Tock's own API FAQ reportedly says **reservations cannot be created or cancelled via the API** **[claimed, quoted in 2026 audit]**. Third-party writes are effectively closed. |
| **TheFork (Tripadvisor)** | **B2B/Partners API with write access** (POST reservation), credentials issued by the integrations team **[claimed, 2026 audit citing docs.thefork.io]**. Google AI Mode UK partner **[verified]**. |
| **Google Reserve / AI Mode** | Supply-side programme; not consumable by third parties. AI Mode's agentic restaurant booking launched in Aug 2025 (Labs) with OpenTable, Resy and Tock, then rolled out US-wide. The UK followed (Apr 2026) with TheFork, SevenRooms, ResDiary, OpenTable and others **[verified, Google blog]**. Sources conflict on whether it books in-line or deeplinks. |

**Takeaway [inferred]:** Dining is the most closed vertical, and ChatGPT and Google now hold first-party reservation deals with OpenTable, Resy and Yelp. A startup realistically gets deeplinks, plus one negotiated write API. **TheFork** (Europe) is the most documented partner write API. **SevenRooms** is the most likely US partner. **Tock is out** for third-party writes.

---

## 5. Aggregated layers and agentic commerce

### 5.1 Travel MCP servers (supplier-side)

| MCP | Status | Can book? |
|---|---|---|
| **Sabre MCP** | Live since Sept 2025; ~80 clients by Sept 2026; powers apps in ChatGPT and Claude **[claimed]**. Separate public Developer Hub docs MCP (no auth) **[verified]** | Yes, for PCC/iPCC holders |
| **Nuitée / LiteAPI MCP** | Live, open source, hosted remote endpoint **[verified]** | Yes |
| **Distribusion Retailer API MCP** | Live Feb 2026 **[verified]** | Yes (partners) |
| **Kiwi.com MCP** (mcp.kiwi.com) | Live, hosted, official; usable from Claude, ChatGPT and Cursor **[verified]** | Search plus booking deeplink only |
| **Booking.com connector** | Official Claude connector, launched ~Apr 2026; search only **[verified]**. B2B MCP restricted to approved strategic partners **[claimed]** | No (consumer); restricted (B2B) |
| **Ferryhopper MCP** | Live; real-time ferry data for LLM agents **[verified, Ferryhopper partner hub]** | Not confirmed |
| **Amadeus Claude Code toolkit** | Waitlist (Sep 2026) **[verified]** | Unknown |
| **Expedia B2B MCP** | Announced May 2026; launch unconfirmed as of Nov 2026 **[verified]**. Dev MCP (docs/testing) exists **[verified]** | Planned (lodging, flights, cars, activities) |
| **Viator, Fever** | Viator: hosted read-only "experiences" connector **[claimed]**. Fever: MCP reported **[claimed]** | No / unknown |
| **Duffel, GetYourGuide, Tripadvisor, Airbnb** | **No official MCP.** Community MCPs only **[verified absence]** | Community Duffel MCPs can book with your own token; others are mostly read-only or ToS-risky |

### 5.2 Consumer agentic surfaces (competitors and channels)

- **ChatGPT apps:**
  - Built on the Apps SDK on MCP. Expedia and Booking.com launched 6 Oct 2025 and hand off to the partner's checkout **[verified]**.
  - Uber (US, on-demand) completes in the Uber app **[verified]**.
  - **Restaurant reservations** with OpenTable, Resy and Yelp launched 10 Aug 2026 on all plans **[verified]**.
- **OpenAI Instant Checkout** (ACP, with Stripe) was scaled back in March 2026. OpenAI refocused on discovery and extended ACP to merchant catalogue feeds. ACP remains an open spec maintained by OpenAI and Stripe (agenticcommerce.dev) **[verified]**. Merchant uptake was tiny (about 12–30 merchants by various estimates) **[claimed]**.
- **Google AI Mode** books hotels in the US (Aug 2026) and restaurants in the US and UK. Partners are merchant of record. UCP has hotel and food verticals; flights are pending **[verified]**.
- **Meta Muse** (8 Sep 2026, US) books flights via Duffel **[verified]**.
- **Booking Holdings Q3 2026:** LLM referrals are <1% of room nights. Priceline and Agoda's own AI assistants convert about 2× better than non-users **[verified]**. The implication is that OTAs will keep transactions on their own surfaces **[inferred]**.

### 5.3 Payments for agents

| Rail | Status (Nov 2026) |
|---|---|
| **Mastercard Agent Pay** | Live agentic flight purchase on 13 Nov 2026 (Travelport NDC, Booked AI agent, Basis Theory tokenization). The airline stayed merchant and the user approved the exact amount **[verified]**. Earlier live transactions were ground rides: Korea via **hoppa** (Mar 2026) and Thailand with Krungthai Card via Elife (Apr 2026) **[verified, Mastercard releases]** (corrects the earlier "Hong Kong taxi"). Rollout to AU, NZ, SG, MY and IN in 2026 **[claimed]**. On 30 Sep 2026 Mastercard added trust and intelligence services, including an agent-initiated-transaction probability score (US testing) **[verified]**. Enrollment goes through issuers **[claimed]**. |
| **Visa Intelligent Commerce / Trusted Agent Protocol** | TAP introduced Oct 2025; Agentic Directory introduced 10 Jun 2026. **30+ European banks** enabled agent purchases at merchants including lastminute.com. **eDreams ODIGEO** (Jul 2026) lets TAP-verified agents complete purchases on eDreams, Opodo, GO Voyages and Travellink **[verified]**. Ramp corporate travel; Alchemy AgentCard **[claimed]**. Volume data not disclosed. |
| **Google AP2** | Launched Sept 2025 with 60+ partners **[verified]**. **Donated to the FIDO Alliance on 28 Apr 2026**, alongside Mastercard's Verifiable Intent. Payments working group chaired by Mastercard and Visa **[verified]**. Still at early pilots, with no verified third-party production deployment **[claimed, tracker]**. |
| **Google UCP** | Launched Jan 2026. Hotel and food-delivery verticals since May 2026; Stripe joined the UCP Tech Council (24 Apr 2026). No flights vertical live **[verified]**. |
| **Stripe** | ACP co-author. **Agentic Commerce Suite** (Sessions, 29 Apr 2026) gives one integration to sell across OpenAI, Microsoft, Meta and Google surfaces. **Shared Payment Tokens** are scoped by seller, time and amount. Link for agents requires per-spend user approval **[verified, Stripe newsroom]**. |
| **PayPal** | **Agent Ready** (accept agent-initiated payments) and **Store Sync** (catalogue to AI surfaces), announced Oct 2025 **[claimed]**. Mindtrip Flights payments plus identity and BNPL **[verified]**. PayPal × PhocusWire travel agentic-commerce whitepaper (Apr 2026) **[claimed]**. AP2 member via FIDO working group **[claimed]**. |

**Implication [inferred]:** For a startup, the realistic 2026–27 pattern is the following:
- Use a tokenized card (Stripe SPT, Agent Pay or VIC/TAP where available, otherwise a standard PSP vault) and an explicit human confirmation of the final price.
- Charge on the supplier's rail (airline or hotel as merchant via Duffel, Sabre or Expedia), or on your own rail (you as merchant).
- Fully autonomous, unattended purchases are not yet accepted by airlines (see United).

### 5.4 Computer-use and browser agents

- **United's November 2026 restriction** covers its own channels and OTA-intermediated bookings made by unauthorized agents. It cites credential sharing, surprise purchases, miles misuse, and DOT/FAA human check-in requirements **[verified]**.
- **Ryanair v. Booking.com:** a Delaware jury found a CFAA violation in July 2024 and awarded the $5,000 statutory minimum. **On 31 Jan 2025 the judge amended the verdict**, finding Ryanair had not proved the required $5,000 loss. Appeal status is unconfirmed **[verified, ch-aviation, RCFP, Holland & Knight]**. The legal risk of scraping is mainly contractual and reputational, plus airline blocking; a CFAA damages claim is harder to win **[inferred]**.
- **Booking.com Customer Terms** (Sep 2025) reportedly bar unauthorized AI browser assistants **[claimed]**.
- **Reliability:** browser agents fail on CAPTCHAs, 3-D Secure, dynamic seat maps and price-change interstitials **[inferred]**.
- **Verdict:** browser automation is acceptable only as a fallback for read-only tasks (checking a booking the user owns, with consent). Use it to book only where the supplier permits it. Never use it with shared loyalty credentials.

### 5.5 Standards

- **IATA ONE Order / Offers & Orders** **[verified, Lufthansa, Amadeus and trade press]**:
  - Live natively on Amadeus Nevio at Finnair (May 2025) and Saudia (July 2025), plus Riyadh Air.
  - Lufthansa Group signed in Jan 2026 to move to Nevio Order IDs gradually. This covers Lufthansa, SWISS, Austrian, Brussels, ITA, Eurowings, Edelweiss, Discover, Air Dolomiti and the City carriers.
  - AF-KLM runs its MOON programme.
  - TPConnects and Lufthansa Systems (27 Jul 2026) bring ONE Order into airline finance.
  - Outlook: IATA (June 2026) calls it an "inflection point" **[verified]**. Roland Berger sees 2026–28 as the phase of first production orders and interline, and mainstream adoption is projected beyond 2027 **[claimed]**.
  - No ONE Order commitment from American Airlines was found.
- **For startups:** Order-based servicing (single Order ID covering air plus ancillaries) improves post-booking APIs, but only through NDC aggregators **[inferred]**.
- **OpenTravel:** no notable 2025–26 agentic standard found.
- **FIDO Alliance** now hosts agent-authentication and agent-payments working groups (AP2 and Verifiable Intent) **[verified]**.
- **The emerging "standards" in practice:** MCP (transport), UCP (Google, commerce semantics), ACP (OpenAI/Stripe), AP2/FIDO (mandates), Visa TAP and Mastercard Agent Pay (agent identity and tokens) **[inferred]**.

---

## 6. Post-booking and trip-management interop

| Need | Option | Status |
|---|---|---|
| Import bookings made elsewhere | **Email parsing**: your own parser plus LLM extraction, or **AwardWallet Email Parsing API**: 600+ loyalty programmes; pricing and test credentials **on request only** **[verified, awardwallet.com/api]**. Or **Traxo**: 4,000+ formats, 20+ languages, air/car/hotel/activity/rail/cruise, manual fallback, inbox scanning; enterprise/TMC focus; sources mostly older **[claimed]**. | **Gmail restricted scopes** (gmail.readonly, .modify, .compose, .metadata, full) require Google verification plus an **annual CASA security assessment** **[verified, multiple integrator docs]**. Reported cost ranges from ~$550 (Tier 2 via low-cost assessors) to $5k–15k+ **[claimed]**. gmail.send is only "sensitive". A forward-to-address flow (like TripIt's plans@) avoids it **[inferred]**. |
| TripIt sync | Public API **closed to new integrations**; existing connections keep working **[verified]** | Dead end for a newcomer |
| Loyalty balances and status | **AwardWallet Account Access API** (end user authorizes sharing; basic free; Business plan for timeline export) and **Web Parsing API**; pricing on request **[verified]** | Airlines have no public loyalty APIs **[background]**. United now warns against sharing MileagePlus credentials with agents **[verified]**: web-parsing loyalty is a growing risk. |
| PNR retrieval and servicing | Only through the rail that created the booking (Duffel order, Sabre/Travelport PCC). Retrieving another agency's PNR is not generally possible **[background]**. | Core accountability constraint |
| Flight status, IROPs | **OAG Flight Info API**: self-serve developer portal; fixed fee per usage tier plus per-hit overage **[verified, OAG]**. **FlightAware AeroAPI**: Personal tier with $5/month credit; Premium from $1,000/month; billed per 15-record result set **[claimed]**. **Cirium (Sky)**: custom quotes, free trial via Developer Studio **[claimed]**. Monetised protection: HTS Disruption Assistance/Guarantee and CFAR **[claimed]**. Duffel airline-initiated change webhooks **[verified]**, auto-accept only for ~24 airlines **[verified]**. | Re-accommodation still needs an airline or GDS servicing path |
| Calendar | Google Calendar API, Microsoft Graph, ICS feeds | Easy |
| Wallet passes | Apple PassKit / Google Wallet generic passes for itineraries | Boarding passes are only issued by airlines **[background]** |

---

## 7. Merchant of record vs. agency vs. affiliate

### 7.1 Models

| Model | You do | You carry | Margin | Examples |
|---|---|---|---|---|
| **Affiliate / metasearch** | Discover and deeplink. The supplier or OTA checks out. | Little; no servicing | CPC or CPA (Viator ~8% claimed; Omio ~6% claimed; 12Go 50% rev share claimed; Agoda ~4–7% claimed) | Most AI planners in 2024–25; ChatGPT OTA apps; Kiwi MCP; Layla-style planners **[background]** |
| **Agency (supplier or consolidator is MoR)** | Book via API; supplier or aggregator charges the card | Customer-service expectations; some disclosure duties; seller-of-travel registration may apply **[background]** | Commission share, markup on top | Expedia Rapid (Expedia Collect), Duffel Managed Content (Duffel is agent of record) **[verified]**, Duffel Stays, Agoda Fulfill Assisted, Google AI Mode (partner MoR), Mindtrip-Sabre (ticketing by Sabre/agency) |
| **Merchant of record** | You charge the card, pay suppliers net | **Chargebacks, PCI scope, supplier insolvency, refunds, 24/7 servicing, packaging law** | Highest: markup on net rates, ancillaries, fintech add-ons | Omio Booking API partners, Musement Merchant partners, LiteAPI with your own payments, Hotelbeds net-rate sellers |

### 7.2 Legal and operational implications [mixed; re-verify with counsel]

- **US seller-of-travel laws** (California, Florida, Washington, Hawaii; others partial) require registration **[background]**.
- **California specifics** **[verified, CA Attorney General FAQ]**:
  - Sellers must keep a trust account or post a bond and participate in the Travel Consumer Restitution Fund.
  - **Exemption:** a seller with no California location may be exempt if it forwards **100% of passenger funds** to a registered TCRF-participating seller, to ARC, or to another registered seller's trust account. If the supplier rail (e.g. an agency-of-record aggregator) collects all funds, check with counsel whether this exemption applies **[inferred]**.
  - SB 95, which would have changed the trust-account rules, failed in the 2025–26 session **[claimed]**.
- **US DOT ticket-agent rules:** full-fare advertising and the 2024 automatic-refund rule extend obligations to ticket agents **[background]**.
- **EU Package Travel Directive (2015/2302)** and **UK Package Travel Regulations / ATOL** **[background]**:
  - Combining flight plus hotel (or other services) in one checkout, or via "linked" click-through within 24h, can make you an **organiser of a package** or a facilitator of a **linked travel arrangement**. That brings insolvency protection and liability for performance of all components.
  - Flight-inclusive packages sold to UK consumers require an **ATOL**.
  - **This is the main legal trap for an AI planner that "books the whole trip" in one cart [inferred].**
- **PCI DSS:** using supplier or PSP hosted fields or tokens (Duffel Payments, Stripe, Basis Theory) keeps you in SAQ A scope. Touching PAN data means SAQ D and annual assessment **[background]**.
- **Chargebacks:** travel has long delivery windows. As merchant you eat disputes when airlines fail or cancel, so PSPs often impose reserves on new travel merchants **[background]**.
- **Customer-service burden:** IROPs, schedule changes and refunds are the main cost. Agency and affiliate models offload most of it **[inferred]**.

### 7.3 Which model the AI planners use

| Company | Model |
|---|---|
| **Mindtrip** | Agency-style flights via Sabre (ticketing and after-sales by Sabre) and PayPal payments **[verified/claimed]** |
| **Meta Muse** | Flights via Duffel (Duffel is agent of record under Managed Content, if used); MoR setup not disclosed **[verified/claimed]** |
| **ChatGPT / Expedia / Booking / Uber / OpenTable / Resy apps** | Pure handoff; the supplier or OTA is MoR **[verified]** |
| **Google AI Mode** | Partner is MoR and services the booking **[verified]** |
| **Booked AI** | Agent on Travelport, airline as merchant, Mastercard tokens **[verified]** |
| **eDreams ODIGEO (agent-facing)** | OTA as merchant; external agents verified via Visa TAP **[verified]** |
| **Perplexity hotels** | Selfbook/Tripadvisor (since Mar 2025); hotel is MoR **[verified]** |
| **Most other planners** (Layla, Wanderboat, Trip Planner AI, etc.) | Affiliate deeplinks **[background]** |

**No major consumer AI planner is a full merchant of record across bundles** **[inferred]**, which also means none takes end-to-end accountability.

### 7.4 Accreditation and host-agency paths (new in pass 2)

| Path | What it gives | Requirements / cost | Fit for an AI-planner startup |
|---|---|---|---|
| **None (Duffel Managed Content)** | Ticketed flights, with Duffel as agent of record | KYC only **[verified]** | Default for Phase 0 |
| **IATA TIDS** | Identity code for non-accredited sellers (not ticketing). **Not available in the US**, where IATAN's non-ticketing programme is used instead **[verified, IATA TIDS FAQ]** | Business and tax registration, ownership docs, bank letter **[verified]**. Fee conflicting (free per Qatar Airways portal; historically ~CAD 165) **[claimed]** | Often needed for Travelport NDC registration outside the US **[verified, Travelport docs]** |
| **IATA accreditation (NewGen ISS)** | Ticketing via BSP. **GoLite**: no cash facility, pays via IATA EasyPay, generally no bank guarantee. **GoStandard/GoGlobal**: cash facility, financial security (bank guarantee or Global Default Insurance) **[verified, IATA]** | Fees vary by country (e.g. CHF 250 GoLite / CHF 1,500 GoStandard). Guarantees $25k–100k+ **[claimed]** | Phase 2+, needed for own Sabre/Travelport ticketing |
| **ARC Verified Travel Consultant (US)** | ARC number, ARC Pay Hub / card processing (separate approval), ARC Check listing; **no ticketing** **[verified, ARC]** | US-based; annual fee (historically ~$150) **[claimed]** | Low-cost US credential |
| **ARC full accreditation (US)** | Airline ticketing | Up to ~90 days; financial security **[claimed]** | Phase 2+ |
| **Host agency / consolidator** | Book under the host's accreditation; Sabre iPCC via a downline agreement **[verified for mechanism]** | Contract. Leisure host agencies (e.g. **Fora**: 15k advisors, $1B valuation, its own Via AI assistant) are built for human advisors. No public developer API found **[verified for Fora]**. Nexion, KHM and Travel Leaders were not checked. | Use a consolidator or GDS-friendly host, not an advisor host **[inferred]** |

---

## (a) Best access path per vertical, now

| Vertical | Best startup path (Nov 2026) | Accreditation needed | Achievable depth | Upgrade path |
|---|---|---|---|---|
| Flights | **Duffel** (Managed Content) | None: Duffel is agent of record; KYC only **[verified]** | **Book + manage**: voluntary changes, cancels incl. airline-credit refunds, ancillaries, seats, schedule-change webhooks. Airline-change auto-accept only for ~24 airlines; IROPs largely manual. | Travelport TripServices sandbox now, then production with TIDS/IATA. Sabre via host agency (iPCC) or IATA for GDS breadth and Sabre MCP. Amadeus Claude Code toolkit (waitlist). HTS CFAR/Disruption for protection. |
| Flights (discovery breadth) | Kiwi MCP (search + deeplink, check commercial terms) **[inferred]**; Kayak/Skyscanner affiliate if you meet traffic bars | None | Search + deeplink | — |
| Hotels | **LiteAPI** (self-serve, MCP) + **Duffel Stays** | None | **Book + cancel + retrieve** | Agoda Demand API (Fulfill Assisted). Expedia Rapid (compliance review). Hotelbeds/WebBeds/RateHawk net rates (certification). Booking.com Demand (hard, AI approval). |
| Vacation rentals | Vrbo via Expedia Rapid; Booking.com homes | Partner approval | Book (via Rapid) | Airbnb: none (2027 own agent) |
| Rail/bus/ferry | **Distribusion** (MCP) + **Trainline Partner Solutions** | B2B contract | **Book + post-sales** | Omio Booking API (become MoR). Rail Europe distributor API. Busbud API. Ferryhopper API/MCP. 12Go for Asia. FlixBus dynamic API. |
| Car rental | Duffel Cars / Expedia Rapid Car | Same as above | Book + cancel | CarTrawler (now Expedia B2B); Booking.com Demand cars; Priceline Partner Network |
| Transfers | **Mozio** API | Contract | Book + cancel | Uber/Lyft deeplinks (Uber agent rides negligible); hoppa |
| Activities | **Viator** (Full + Booking) + **GetYourGuide** (BOOKING tier) | Authorization | **Book + cancel** | Tiqets Distributor API (free, eligibility review); Musement and Headout partner APIs; Fever (large partners) |
| Restaurants | Deeplinks; OpenTable affiliate; negotiate **TheFork** (EU) or **SevenRooms** (US) partner API | Partnership | **Mostly search/deeplink** | OpenTable partner APIs; Tock not writable |
| Post-booking import | Forwarding-address email parsing + LLM extraction; AwardWallet APIs (quote) | None (avoid Gmail restricted scope initially) | **Observe only** for external bookings | Gmail CASA-verified integration (~$550–15k/yr); ONE Order via NDC aggregators |
| Flight status | **OAG Flight Info API** (self-serve tiers) or FlightAware AeroAPI | None | Status + alerts | Cirium (enterprise) |
| Payments | Stripe Agentic Commerce Suite / SPTs or Duffel Payments tokens; PayPal; Mastercard Agent Pay when issuers enable | PSP onboarding | Human-confirmed agentic checkout | Visa TAP / VIC (live in Europe), AP2/FIDO mandates |

## (b) The interoperability ceiling today (where it breaks)

1. **Search: mostly solved, with legal limits.**
   - Breadth is available via affiliates, metasearch, and now supplier MCPs (Kiwi, Booking.com connector, Ferryhopper).
   - The gaps are Google Flights (no API), Airbnb (no API), Japan rail, and restaurants (closed; first-party deals go to ChatGPT and Google).
   - Skyscanner and Kayak gate API access by traffic.
2. **Book: solvable for one cart per supplier rail, without accreditation, via Duffel, LiteAPI, Viator, GetYourGuide, Tiqets and Distribusion.** It breaks when:
   - you need GDS-only or corporate fares;
   - you need Booking.com inventory (AI approval gate);
   - you combine components into one payment, which triggers package law and ATOL;
   - an airline forbids agent bookings (United).
3. **Manage: the real ceiling.**
   - Voluntary changes and cancels work only for bookings on your own rails.
   - Even on Duffel, airline schedule changes auto-resolve for only ~24 airlines **[verified]**.
   - IROPs re-accommodation, refunds-to-original-form after airline cancellation, and loyalty accrual fixes still frequently need human contact with the airline.
   - For bookings made elsewhere you can only **observe** (email parse, AwardWallet), never **act**: no PNR retrieval or cross-agency servicing.
   - Loyalty credential sharing is now explicitly discouraged by airlines.
4. **Accountability: absent in the market.** Every AI surface pushes liability to the supplier or OTA as merchant of record. No AI planner guarantees the whole trip. Hopper HTS-style fintech (CFAR, disruption guarantee) is the only off-the-shelf "insurance" for this, and it is sold to banks and airlines, not to startups.
5. **Agent identity and authorization: converging, not settled.**
   - Mastercard Agent Pay and Visa TAP both have live travel transactions: Travelport/Booked AI (Mastercard) and eDreams (Visa).
   - AP2 and Verifiable Intent moved into FIDO working groups; UCP is Google's commerce layer.
   - Airlines demand "standardized, secure integrations" before allowing agents (United) **[verified]**.
   - Whoever ships a verifiable, consented agent identity on top of sanctioned rails is on the right side of this.

## (c) Top gaps and a phased integration strategy

### Top gaps / opportunities

1. **Whole-trip accountability layer** **[inferred, high value]**. Combine:
   - booking on owned rails (Duffel, LiteAPI, Distribusion, Viator);
   - continuous monitoring (schedule-change webhooks, flight status);
   - pre-packaged remedies (HTS-style CFAR or disruption cover, or self-insured);
   - an agent that executes re-bookings via API, plus a human desk for the airlines Duffel can't auto-resolve.

   Nobody does this end-to-end. Structure it to avoid organiser-of-package liability: separate contracts per component and LTA disclosures, or deliberately become an organiser with insolvency cover in one market.
2. **External-booking import plus "managed-through-us" migration.** TripIt's API is closed, which leaves an opening for an AI-native itinerary hub. It would parse forwarded emails and loyalty data, then offer to re-book or protect via your rails. Avoiding Gmail restricted scopes at first keeps compliance light.
3. **Sanctioned-agent posture as a moat.** United's ban plus the Mastercard/Travelport and Visa/eDreams launches show suppliers want identifiable, tokenized, human-confirmed agents. Be early on Agent Pay and TAP and transparent agent identity. Never ask for loyalty passwords.
4. **Multimodal ground in one MCP** (Distribusion plus Trainline plus Mozio, with Ferryhopper and 12Go at the edges). Rail, bus, ferry and transfer stitching is weak in every AI planner. Supplier MCPs now exist (Distribusion, Ferryhopper).
5. **Restaurants and Japan rail are closed verticals.** Win through partnerships with the writable mid-tier platforms (TheFork, SevenRooms) and Asia resellers (Klook, 12Go), rather than waiting on OpenTable or Resy. Those two now prioritise ChatGPT and Google.

### Phased integration plan

**Phase 0 (weeks 0–6): zero-accreditation coverage.**
- Duffel (flights, stays, cars; KYC only) and LiteAPI (hotels via MCP).
- Viator (Basic → Full + Booking), GetYourGuide (READ → BOOKING), and Tiqets Distributor API (eligibility review).
- Affiliate deeplinks: Omio, 12Go, Busbud, Booking.com affiliate, Kayak/Skyscanner where you meet the bar, OpenTable/Resy links, Uber/Lyft deeplinks.
- Stripe (Agentic Commerce Suite / SPTs) or Duffel Payments in tokenized mode.
- Email-forwarding importer; request AwardWallet API quote.
- **Start Travelport TripServices sandbox** and **join the Amadeus Claude Code toolkit waitlist** (both free to start).
- Legal: choose agency/disclosed-agent posture; register as seller of travel in CA, FL, WA and HI before selling there (check the CA "forward 100% of funds" exemption with counsel); per-component checkout to avoid package formation.

**Phase 1 (months 2–6): depth and ground.**
- Distribusion (MCP), Mozio, Ferryhopper.
- Expedia Rapid application (compliance review; Vrbo, cars; B2B MCP when live). Agoda Demand API (Fulfill Assisted).
- Trainline Partner Solutions (~12-week integration) or Rail Europe distributor API.
- OAG flight status plus Duffel change webhooks driving proactive rebooking; human desk for non-auto-AIC airlines.
- Pilot HTS CFAR/Disruption or an equivalent insurer partnership.
- One restaurant write API (TheFork in EU or SevenRooms in US).

**Phase 2 (months 6–12): accreditation and networks.**
- Accreditation route depends on market:
  - US: ARC VTC, then ARC accreditation.
  - Outside the US: IATA TIDS, then IATA GoLite or GoStandard.
  - Either way, a consolidator host can supply a Sabre iPCC instead.
- With accreditation, add Sabre (Sabre MCP; Mindtrip pattern) or Travelport production (TripServices; Booked AI pattern).
- Mastercard Agent Pay / Visa TAP token checkout.
- Hotelbeds/WebBeds/RateHawk net rates for margin.
- Booking.com Demand API application with explicit AI approval.

**Phase 3 (12+ months): become the accountable organiser in one market.**
- In one market (e.g. UK with ATOL or one EU state with insolvency cover), offer guaranteed whole-trip packages.
- Adopt ONE Order servicing through NDC aggregators as airlines go live (Lufthansa Group rolling out).
- Expose your own MCP/UCP endpoint so other agents (ChatGPT, Gemini, Claude, Meta Muse) can book your protected trips.

---

## Sources

- Amadeus Self-Service shutdown: https://www.phocuswire.com/amadeus-shut-down-self-service-apis-portal-developers ; https://airlabs.co/amadeus-self-service-api-shutdown ; https://www.tripgic.com/playbook/amadeus-api-shutdown-migration/ ; https://www.tripgic.com/playbook/amadeus-api/ ; https://oneclicktraveltech.com/blogs/amadeus-self-service-api-shutdown ; https://flightpowers.com/guides/amadeus-self-service-alternatives ; https://dev.to/ishemah/amadeus-self-service-shut-down-on-july-17-heres-a-drop-in-replacement-for-flight-prices-1npn
- Duffel pricing/stays/cars: https://duffel.com/pricing ; https://flightpowers.com/compare/duffel ; https://www.xpay.sh/saas-pricing/duffel/ ; https://duffel.com/blog/introducing-duffel-stays-the-fastest-way-to-sell-accommodation ; https://changelog.duffel.com/announcements/you-can-now-see-the-source-of-an-accommodation-rate-via-duffel-stays ; https://www.traveldailynews.com/people/new-appointments/duffel-launches-duffel-cars-expanding-its-travel-api-suite/
- Mindtrip/Sabre/PayPal: https://skift.com/2026/05/06/sabre-mindtrip-paypal-launch-agentic-ai-travel-booking/ ; https://www.travolution.com/en/article/mindtrip-switches-on-flight-booking-in-its-agentic-ai ; https://stellagent.ai/insights/mindtrip-sabre-paypal-agentic-flight-booking ; https://siften.com/read/travel/mindtrip-launches-ai-powered-flight-booking-with-sabre-and-paypal-but-only-2-of-leisure-travellers-w ; https://www.traveldailynews.com/technology/mindtrip-launches-ai-powered-flight-booking-platform/
- Kiwi Tequila: https://media.kiwi.com/articles-and-interviews/better-for-business-kiwi-com-takes-a-new-approach-to-partnerships/ ; https://flightpowers.com/compare/kiwi-tequila ; https://faun.dev/toolbox/amadeus-self-service-apis-vs-kiwicom-tequila/
- Sabre agentic/MCP: https://www.sabre.com/mosaic/ ; https://www.sabre.com/developers/ ; https://www.fairsonline.org/sabres-mcp-server-hits-scale-nearly-80-airline-agency-clients ; https://www.travelweekly.com/Travel-News/Travel-Technology/Sabre-launches-agentic-AI-solutions ; https://investors.sabre.com/news-releases/news-release-details/sabre-and-biztrip-ai-announce-strategic-partnership-deliver
- Travelport: https://support.travelport.com/webhelp/ndcPlugin/Content/AirlineRegistration.htm ; https://www.pulse.bot/hotels/video/ai-can-plan-the-trip-but-can-it-book-it-travelports-booking-layer-play-2d8dac10-c92e-4680-867e-fc3de2832a7a/
- Mystifly: https://mystifly.com/ssp-paas/ ; https://cxotoday.com/press-release/costco-travel-deploys-mystifly-ssp-to-sell-and-service-hawaiian-airlines-exclusive-ndc-content/
- Hopper HTS: https://hts.hopper.com/news/summer-2026-platform-update ; https://hts.hopper.com/news/a-new-milestone-in-our-partnership-with-capital-one ; https://www.hospitalitynet.org/news/4135133/hts-hopper-technology-solutions-and-serkoai-bring-novel-fintech-and-lodging-api-to-corporate-travel ; https://media.hopper.com/news/hopper-and-frontier-airlines-announce-ndc-partnership-enhancing-content
- Expedia Rapid / MCP: https://developers.expediagroup.com/rapid/setup/launch-requirements/b2c-standalone ; https://developers.expediagroup.com/rapid/setup/launch-requirements/b2b-standalone ; https://developers.expediagroup.com/rapid/setup/launch-requirements/car-launch-reqs ; https://track360.io/blog/expedia-affiliate-program-ean-taap-operator-teardown-2026 ; https://skift.com/2026/05/21/expedia-to-launch-agentic-ai-tools-for-b2b-partners/ ; https://newsletters.skift.com/p/expedia-b2b-goes-ai ; https://hospitality-on.com/en/distribution/expedia-group-opens-its-inventory-agentic-ai-partners-avoid-being-left-behind
- Booking.com Demand API: https://demand.developers.booking.com/ ; https://vorplabs.com/agent-tools/booking-demand-api ; https://github.com/wanderes-dev/wanderes/pull/1 ; https://www.anchorterminal.com/compare/booking-demand-api-vs-liteapi ; https://www.monocrawl.com/compare/booking-data-apis ; https://stayapi.com/blog/booking-com-api
- Nuitée/LiteAPI: https://docs.liteapi.travel/docs/mcp ; https://nuitee.com/connect/liteapi-agentic ; https://nuitee.com/insights/liteapi-product-updates-q1-2026 ; https://skift.com/2025/09/09/nuitee-travel-api-connectivity/
- ChatGPT apps / Instant Checkout: https://www.phocuswire.com/openai-chatgpt-apps-expedia-booking-tripadvisor ; https://upgradedpoints.com/news/expedia-booking-apps-live-inside-chatgpt/ ; https://www.conduit.ai/blog/how-ai-agents-book-hotels ; https://stellagent.ai/insights/openai-scales-back-instant-checkout ; https://ucphub.ai/chatgpt-shopping-checkout-why-openai-scaled-back-and-what-it-means-for-merchants-in-2026/ ; https://www.digitalapplied.com/blog/ai-agentic-commerce-discover-in-ai-buy-on-site-2026
- Google AI Mode / UCP / AP2: https://skift.com/2026/08/07/google-confirms-hotel-agentic-booking-is-now-in-testing/ ; https://www.phocuswire.com/news/technology/google-ai-mode-hotel-booking-agentic-flights-loyalty ; https://ppc.land/google-ai-mode-completes-hotel-bookings-with-10-partners-in-us-rollout/ ; https://stellagent.ai/insights/google-marketing-live-2026-ucp-hotels-ask-advisor ; https://techcrunch.com/2025/09/16/google-launches-new-protocol-for-agent-driven-purchases ; https://www.spark.money/research/google-ap2-agent-payment-protocol
- Visa/Mastercard: https://www.mastercard.com/global/en/news-and-trends/press/2026/november/end-to-end-AI-powered-travel-booking.html ; https://thepaypers.com/payments/news/travelport-and-mastercard-complete-live-agentic-flight-booking ; https://www.traveldailynews.com/technology/agentic-travel-booking-live-flight-purchase/ ; https://shatale.com/blog/mastercard-agent-pay-visa-intelligent-commerce ; https://www.pymnts.com/transportation/travel-payments/2026/mastercard-touts-successful-agentic-travel-transaction/
- United AI-agent restriction: https://techcrunch.com/2026/11/12/united-airlines-blocks-ai-agents-from-booking-flights-citing-cybersecurity-risks/ ; https://www.engadget.com/2314121/united-is-restricting-ai-agents-from-booking-flights/ ; https://www.paxnews.com/news/airline/no-bots-allowed-united-restricts-unauthorized-ai-booking-agents ; https://casrai.org/news/united-airlines-bars-unauthorized-ai-agents-2026
- Airbnb: https://vorplabs.com/agent-tools/airbnb-cli ; https://dev.to/_bassel_/there-is-no-official-airbnb-mcp-server-here-is-how-hosts-connect-chatgpt-and-claude-anyway-2584 ; https://www.nowistay.com/airbnb-mcp-chatgpt-claude-hosts
- Hotelbeds: https://phptravels.com/hotelbeds-api-xml-integration ; https://phptravels.com/blog/travel-api-suppliers
- Viator: https://partnerresources.viator.com/travel-commerce/affiliate/ ; https://docs.viator.com/partner-api/ ; https://partnerresources.viator.com/travel-commerce/technical-guide/
- GetYourGuide: https://context7.com/getyourguide/partner-api-spec ; https://support.ventrata.com/en/article/getyourguide-reseller-connection-1ab9gaj/ ; https://supergood.ai/api-report-card/getyourguide
- OpenTable/Resy: https://vorplabs.com/agent-tools/opentable-cli ; https://ainora.lt/blog/restaurant-booking-api-for-ai-agents-2026 ; https://github.com/api-evangelist/resy ; https://www.usecarly.com/blog/claude-resy-integration/ ; https://www.expedite.news/p/q-and-a-opentable-hypes-agentic-ai
- Rail/ground: https://tps.thetrainline.com/blog-and-media/trainline-partner-solutions-in-2025/ ; https://www.marketbeat.com/instant-alerts/trainline-h2-earnings-call-highlights-2026-05-06/ ; https://www.businesstravelnewseurope.com/Ground-Transport/Spotnana-expands-European-rail-content-with-new-Trainline-integration ; https://docs.distribusion.com/dt/api/what-s-new ; https://www.interrail.com/en/about-us/press-room/interrail-news/interrail-distribusion-partnership ; https://distribusion.com/news/distribusion-partners-with-kai-to-enable-global-sales-of-indonesia-rail-tickets ; https://www.omio.co.uk/corporate/omio-b2b/ ; https://www.omio.co.uk/affiliate ; https://www.travelpayouts.com/blog/train-affiliate-programs/ ; https://www.travelpayouts.com/blog/bus-and-train-affiliate-programs/amp/
- Mozio: https://transfers.th.edreams.com/online-travel-marketplaces ; https://en.10minhotel.com/2025/06/27/mozio-and-gonexus-group-form-strategic
- TripIt/AwardWallet/Traxo: https://help.tripit.com/en/support/solutions/articles/103000391296-tripit-public-api ; https://awardwallet.com/api ; https://awardwallet.com/api/account ; https://www.traxo.com/solutions/folio-parsing ; https://www.businesstravelnewseurope.com/Technology/Traxo-forges-partnership-with-Booking-com
- ONE Order: https://www.iata.org/en/iata-repository/pressroom/fact-sheets/fact-sheet-one-order ; https://juspay.io/blog/the-end-of-the-ticket-how-iata-s-offers-and-orders-is-rewriting-airline-commerce ; https://www.sutherlandglobal.com/insights/whitepaper/cleared-for-takeoff-one-order-moment

### Sources added in pass 2 (gap-fill)

- Duffel go-live, Managed Content, servicing: https://duffel.com/services-agreement ; https://help.duffel.com/hc/en-gb/articles/360019644700-Do-I-need-to-be-an-ARC-IATA-travel-agent ; https://help.duffel.com/hc/en-gb/articles/9066583986706-What-is-Managed-Content ; https://duffel.com/blog/benefits-of-using-duffel-content-services-duffels-accredited-agency-network ; https://duffel.com/docs/api/airline-initiated-changes ; https://duffel.com/docs/api/order-changes ; https://changelog.duffel.com/announcements/refunds-to-airline-credits ; https://changelog.duffel.com/announcements/new-functionality-for-airline-initiated-changes ; https://hookdeck.com/webhooks/platforms/guide-to-duffel-webhooks-features-and-best-practices ; https://duffel.com/docs/guides/getting-started-with-stays ; https://apis.io/plans/duffel/duffel-plans-pricing/ ; https://pricingsaas.com/companies/duffel
- Duffel 2026 (Muse, Stays, Cars, Rippling, community MCPs): https://duffel.com/blog/millions-of-users-can-now-use-duffel-to-search-book-and-manage-holidays-on-muse-the-new-personal-ai-agent-from-meta ; https://www.phocuswire.com/news/technology/meta-launches-ai-agent-travel-booking ; https://www.travelerstoday.com/articles/60971/20260911/meta-muse-books-flights-through-500-airlines-hotels-are-different-story.htm ; https://thebusinesstravelmag.com/duffel-partners-with-rippling-to-power-rippling-travel/ ; https://businesscloud.co.uk/news/duffel-hits-900m-run-rate-and-launches-cars-vertical/ ; https://glama.ai/mcp/servers/@FortripEngineering/duffel-mcp
- Kiwi MCP / ChatGPT: https://media.kiwi.com/company-news/kiwi-com-releases-mcp-server-prototype/ ; https://media.kiwi.com/company-news/technology-update-kiwi-com-introduces-early-preview-of-the-kiwi-com-chatgpt-app/ ; https://alpic.ai/case-studies/kiwi ; https://www.kiwi.com/ag/pages/mcp/ ; https://www.vervotech.com/hub/integrations/tequila-api/
- Skyscanner / Kayak: https://skyscannerpartnersupport.zendesk.com/hc/en-us/articles/10881149122717-What-is-the-acceptance-criteria-for-the-Travel-API ; https://ignav.com/docs/skyscanner-api-access ; https://affiliates.kayak.com/apis ; https://supergood.ai/api-report-card/kayak ; https://affilimate.com/programs/kayak-affiliate-program/
- Expedia (MCP status, Dev MCP, CarTrawler): https://partner.expediagroup.com/en-us/resources/blog/ai-at-explore-2026-what-partners-need-to-know ; https://www.jdsupra.com/legalnews/ai-takes-center-stage-at-expedia-4947978/ ; https://secure.businesswire.com/news/home/20260519556732/en/Expedia-Group-announces-agreement-to-acquire-CarTrawler-advancing-strategy-to-build-the-most-complete-B2B-travel-platform ; https://skift.com/2026/05/20/expedia-to-acquire-cartrawler-in-second-b2b-deal-of-2026/ ; https://partner.expediagroup.com/en-us/resources/blog/expedia-group-completes-cartrawler-acquisition ; https://www.irishtimes.com/business/2026/05/20/cartrawler-acquired-by-us-travel-group-expedia/
- Booking.com connector / Demand API: https://developers.booking.com/mcp/booking-connector/about ; https://www.pulse.bot/hotels/news/anthropics-claude-ai-gains-bookingcom-integration-boosting-hotel-booking-automation-fdaece82-56eb-44cd-aaf5-a702282fc4db/ ; https://mcpservers.org/remote-mcp-servers/booking ; https://developers.booking.com/demand/docs/open-api/3.2/demand-api
- Travelfusion / hotels wholesale / Agoda: https://corporate.travelfusion.com/products-services/tf-flight-api ; https://dmcquote.com/compare/hotelbeds-alternative ; https://www.traveldailynews.com/hotels-lodging/hotelbeds-launches-apitude-its-new-hotel-distribution-api/ ; https://tripcreator.com/integrations/ratehawk ; https://www.webbeds.com/buyers/solutions/ ; https://www.webbeds.com/buyers/support/ ; https://developer.agoda.com/demand/docs ; https://developer.agoda.com/demand/changelog/guides ; https://developer.pps.agoda.com/docs/faq ; https://track360.io/blog/agoda-affiliate-program-operator-teardown-2026
- Perplexity / Selfbook: https://www.phocuswire.com/perplexity-selfbook-agentic-ai-travel-booking-tripadvisor ; https://jdsupra.com/legalnews/travel-tech-trends-perplexity-s-booking-1053225
- Activities: https://tiqets.com/partner-program/distributor-api ; https://www.tiqets.com/partner-program/api-program ; https://partner-api.musement.com/api/getting-started/ ; https://partner.headout.com/docs ; https://apis.io/providers/klook/ ; https://business.feverup.com/en/partner-programs/affiliate-program/ ; https://providers.apievangelist.com/providers/fever/ ; https://mcpservers.org/remote-mcp-servers/viator
- Restaurants: https://ainora.lt/blog/restaurant-booking-api-for-ai-agents-2026 ; https://sevenrooms.com/en/platform/integrations-apis/ ; https://supergood.ai/api-report-card/sevenrooms ; https://blog.resy.com/newsroom/resy-launches-reservations-in-chatgpt/ ; https://androidauthority.com/chatgpt-restaurant-reservations-and-waitlists-3696712 ; https://cryptobriefing.com/opentable-chatgpt-integration-190000-diners/ ; https://blog.google/products/search/ai-mode-agentic-personalized/ ; https://blog.google/company-news/inside-google/around-the-globe/google-europe/united-kingdom/ai-mode-restaurants-uk/
- Ground: https://www.flixbus.com/company/partners/affiliate-partners ; https://www.busbud.com/partner/busbud-api/ ; https://partners.ferryhopper.com ; https://www.altexsoft.com/blog/car-rental-apis-integrations-with-gdss-otas-and-tech-providers ; https://www.autorentalnews.com/news/rentalcars-connect-partners-with-online-travel-agency ; https://railwaynews.net/?p=256375 ; https://www.globalrailwayreview.com/news/234588/rail-europe-expands-reach-through-juniper-travel-technology-integration/ ; https://www.headout.com/news/headout-and-rail-europe-join-forces-to-elevate-train-travel-in-europe ; https://www.businesstravelnewseurope.com/Technology/Silverrail-partners-with-Rail-Europe ; https://tps.thetrainline.com/our-products/global-api/ ; https://www.omio.co.uk/corporate/newsroom/press-releases/omio-expands-white-label-network-with-new-tui-partnership/ ; https://www.omio.co.uk/corporate/newsroom/press-releases/easytrain-joins-omios-white-label-network/ ; https://12go.com/about ; https://reseller.12go.com ; https://www.travolution.com/news/in-depth/sponsored-post-how-the-12go-affiliate-programme-empowers-travel-brands/ ; https://cms.rome2rio.com/documentation/1-4/search
- Rides: https://techcrunch.com/2026/04/06/how-to-use-chatgpt-apps-doordash-spotify-uber ; https://letsdatascience.com/news/uber-reports-only-four-ai-agent-rides-in-third-quarter-0d70ddf1 ; https://www.uctoday.com/productivity-automation/bolt-brings-ride-hailing-to-chatgpt/ ; https://www.businesswire.com/news/home/20260716711586/en/ ; https://techcrunch.com/2025/02/06/lyfts-new-ai-customer-assistant-is-powered-by-anthropics-claude
- Amadeus × Anthropic: https://skift.com/2026/09/03/amadeus-brings-travel-tech-into-claude/ ; https://www.phocuswire.com/news/technology/amadeus-anthropic-claude-developers-travel-sellers ; https://www.businesstravelnews.com/Technology/Amadeus-Partners-with-Anthropic-for-Tool-Integration-Developer-Access ; https://traveldistributionnews.com/amadeus-just-opened-claude-after-closing-its-developer-door/
- Sabre / Travelport access: https://mcp.so/servers/sabre-developer-hub ; https://www.phocuswire.com/sabre-api-agentic-ai-mcp ; https://developer.sabre.com/guides/travel-agency/intros/glossary ; https://www.travelport.com/press-releases/travelport-launches-tripservices ; https://skift.com/2026/06/11/travelport-tripservices-cloud-apis-ai-travel/ ; https://developer.travelport.com/resources/faq
- Agentic payments: https://www.mastercard.com/news/ap/en/newsroom/press-releases/en/2026/mastercard-completes-korea-s-first-live-agentic-transactions-unlocking-trusted-ai-powered-commerce/ ; https://www.mastercard.com/news/ap/en/newsroom/press-releases/en/2026/mastercard-and-krungthai-card-complete-first-live-agentic-transaction-in-thailand/ ; https://www.mastercard.com/global/en/news-and-trends/press/2026/september/new-trust-and-intelligence-services.html ; https://www.mynewsdesk.com/uk/visa/pressreleases/visa-and-banks-across-europe-reach-the-next-phase-of-agentic-commerce-unlocking-secure-access-to-merchants-3457328 ; https://thepaypers.com/payments/news/visa-expands-agentic-commerce-access-for-merchants-across-europe ; https://techintelpro.com/news/ai/agentic-ai/edreams-odigeo-and-visa-power-agentic-commerce-in-travel-with-secure-ai-agent-protocols ; https://fidoalliance.org/fido-alliance-to-develop-standards-for-trusted-ai-agent-interactions/ ; https://www.businesswire.com/news/home/20260427506015/en/FIDO-Alliance-to-Develop-Standards-for-Trusted-AI-Agent-Interactions ; https://www.paymentsjournal.com/google-donates-its-agentic-payments-protocol-to-the-fido-alliance/ ; https://stripe.com/gb/newsroom/news/agentic-commerce-suite ; https://www.digitaltransactions.net/stripe-launches-agentic-commerce-suite-with-brands-in-tow ; https://techinformed.com/openai-refocuses-chatgpt-shopping-on-discovery/ ; https://www.digitalcommerce360.com/2026/03/24/openai-agentic-commerce-updates-chatgpt-walmart/ ; https://agenticcommerce.dev/ ; https://getcoai.com/news/paypal-launches-ai-agent-payment-tools-as-shopping-automation-hits-40 ; https://stellagent.ai/insights/paypal-agentic-commerce-travel ; https://www.phocuswire.com/google-ucp-not-game-changer-travel ; https://www.altexsoft.com/travel-industry-news/googles-ucp-lets-ai-book-without-sending-users-away/
- Booking Holdings Q3 2026: https://www.phocuswire.com/news/finance/booking-holdings-q3-2026-earnings ; https://www.pymnts.com/?p=4040578
- Ryanair v Booking.com: https://www.ch-aviation.com/news/156303-lobby-groups-back-bookingcom-in-ryanair-legal-row ; https://hklaw.com/en/insights/publications/2024/08/district-court-ruling-offers-insight-into-computer-fraud ; https://news.bloomberglaw.com/litigation/ryanair-wins-jury-verdict-in-scraping-case-against-booking-com
- Post-booking data: https://awardwallet.com/api ; https://nango.dev/docs/api-integrations/google-shared/google-security-review ; https://www.unipile.com/gmail-api-scopes-guide/ ; https://learn.emailengine.app/docs/accounts/gmail/gmail-api-scopes ; https://flightaware.com/commercial/aeroapi/ ; https://supergood.ai/api-report-card/flightaware ; https://www.oag.com/knowledge/how-am-i-charged-for-using-flight-info-api ; https://developers.oag.com/ ; https://geekflare.com/guides/flight-data-api/ ; https://www.traxo.com/solutions/folio-parsing
- ONE Order 2026: https://www.travelweekly.com/Travel-News/Airline-News/Lufthansa-aims-simplify-bookings-Amadeus-technology ; https://www.businesstravelnewseurope.com/Technology/Lufthansa-Group-and-Amadeus-partner-on-Order-ID-initiative ; https://amadeus.com/en/blog/articles/building-future-airline-retailing-transformation-air-france-klm ; https://www.rolandberger.com/en/Insights/Publications/Airline-order-and-offer-management.html ; https://www.traveldailynews.com/aviation/tpconnects-and-lufthansa-systems-integrate-airline-retailing-finance/
- Accreditation / seller of travel / host agencies: https://www.iata.org/en/services/accreditation/tids/faq/ ; https://www.iata.org/en/services/travel-agency-program/tids/application/ ; https://www.iata.org/contentassets/aa1af9700ee94258b18a9b773c01b0e2/ngiss-overview.pdf ; https://www.iata.org/accreditation-travel ; https://www.acta.ca/Media/Default/actavision/2020/0130/IATA%20TIDS%20GoLite%20Comparison%20-%20Canada.pdf ; https://www2.arccorp.com/support-training/arc-vtc-mark ; https://www2.arccorp.com/support-training/vtc-faqs ; https://www.altexsoft.com/blog/arc-accreditation/ ; https://www.oag.ca.gov/travel/reg-faqs ; https://california.public.law/codes/ca_bus_and_prof_code_section_17550.15 ; https://skift.com/2026/07/16/fora-travel-the-unicorn-it-raised-60-million-at-a-1-billion-valuation/ ; https://www.travelagentcentral.com/your-business/fora-buys-ai-startup-legends-travel-industry-leans-back-end-tech
