# 04 — Booking & Interoperability Infrastructure for an AI Trip Planner (state as of 2026-11-17)

**Owner:** Deep-research agent 4 of 7 (booking / integration layer)
**Date:** 2026-11-17

## Method and confidence notes (read first)

- **Research limits in this session.** All research went through WebSearch. WebFetch was blocked by the container's network allow-list (duffel.com, phocuswire.com, skift.com and flightpowers.com all failed DNS), so I could not read any primary page in full. Partway through, the WebSearch budget shared by all parallel agents ran out. Areas this cut short: Skyscanner/Kayak affiliate status, Kiwi's MCP, Expedia's B2B MCP go-live, Booking.com's Claude connector, Travelfusion, Klook/Tiqets/Headout/Fever, SevenRooms/Tock/TheFork, FlixBus/Busbud, CarTrawler, Uber, and seller-of-travel law details. For those I used background knowledge (training data to about mid-2026), labelled **[background]**. Re-verify these before any commercial decision.
- **Tags:**
  - **[verified]**: corroborated by two or more independent 2026 sources, or by an official vendor or developer page seen in search results.
  - **[claimed]**: a single source, a vendor's own marketing, or trade-press repeating a vendor.
  - **[inferred]**: my own analysis.
  - **[background]**: my prior knowledge, not re-checked in this session.

---

## 0. Executive summary

1. **The open self-serve era of travel APIs is over.** Amadeus Self-Service shut down on 17 July 2026 **[verified]**. Kiwi Tequila has been invite-only since May 2024 **[verified]**. TripIt's public API no longer accepts new integrations (Feb 2026) **[verified]**. Booking.com's Demand API needs Managed Affiliate status, and reportedly written approval to use AI **[claimed]**. Expedia Rapid needs approval plus a compliance review **[verified]**.
2. **The two credible self-serve "book-and-manage" rails left for a startup are Duffel (flights, stays, cars) and Nuitée LiteAPI (hotels).** Both let you transact without IATA accreditation:
   - Duffel acts as ticketing agent under its "Managed Content" model **[background]**.
   - LiteAPI publishes an open-source MCP server that can search, book and manage **[verified]**.
   - Ground (Distribusion, Trainline Partner Solutions, Omio) and activities (Viator, GetYourGuide) are reachable through partner programmes. Approval is required, but these programmes are designed for distributors.
3. **Supplier-side agentic infrastructure became real in 2025–26, but it is controlled by incumbents:**
   - Sabre's MCP server has about 80 airline and agency clients piloting or in production (Sept 2026) **[claimed]**. It powers Mindtrip Flights (launched 6 May 2026, Sabre Mosaic and PayPal) **[verified]**.
   - Distribusion launched a Retailer API MCP server (Feb 2026) **[verified]**.
   - Expedia announced a B2B MCP server "in the coming months" (May 2026). I found no confirmation that it has launched **[verified as announced; launch unconfirmed]**.
   - Google AI Mode launched agentic hotel booking in the US (Aug 2026), with partners as merchant of record and UCP as the long-term protocol **[verified]**.
4. **Consumer-surface agentic checkout has stalled.** OpenAI scaled back ChatGPT Instant Checkout in March 2026 and moved to "discover in AI, buy on site" **[verified]**. The OTAs' ChatGPT apps hand off to their own checkout **[verified]**. Booking Holdings said LLM traffic is "significantly below 1% of room nights" (Aug 2026) **[claimed]**.
5. **Airlines are pushing back on unsanctioned agents.** On 11 Nov 2026 United restricted unauthorized third-party AI agents from booking and from MileagePlus accounts, including via OTAs **[verified]**. Two days later, Travelport, Booked AI, Basis Theory and Mastercard announced a live, sanctioned agentic NDC booking using Agent Pay tokens, with the airline as merchant **[verified]**. In practice, **screen-scraping and computer-use booking now carry reputational and ToS risk; sanctioned API rails plus network agent tokens are the path forward** **[inferred]**.
6. **The interoperability ceiling sits at post-booking.** Search and book are attainable for flights, hotels, rail and activities. Servicing (changes, IROPs re-accommodation, refunds, loyalty) is only reliable for bookings made through your own rail. Bookings made elsewhere can only be observed (email parsing, AwardWallet), not managed. That is the accountability gap.

---

## 1. Flights

### 1.1 Access paths

| Path | Who can get access | Commercial model | Operations | Coverage | Pain points / status |
|---|---|---|---|---|---|
| **Duffel** | Self-serve sign-up with test mode. Going live needs KYC and a contract **[background]**. No IATA needed on Managed Content, where Duffel is the ticketing agent **[background]**. | $3.00 per confirmed order; 1% of order value on Managed Content; $2 per paid ancillary; 1,500 free searches per order, then $0.005 per search **[verified via multiple secondary quotes of duffel.com/pricing]**. Possible ~2% FX fee **[claimed]**. You set your own markup **[background]**. | Search, price, book, hold (where the airline supports it), seat maps, bags, changes and cancellations via order change requests, loyalty numbers, airline credits, webhooks for schedule changes **[background]** | 300+ airlines, including major NDC carriers (AA, BA, LH Group, AF-KLM, UA and others) and LCCs **[background]** | Best developer experience in the market **[claimed]**. Thin GDS-only content in some markets. Servicing beyond voluntary changes (IROPs) still often needs airline contact **[inferred]**. Duffel added Cars and keeps expanding Stays **[verified]**. |
| **Sabre (Dev Studio / Mosaic APIs and the Sabre MCP server)** | Requires a Pseudo City Code (PCC) **[background]**. This normally means IATA/ARC accreditation or a host agency, plus a commercial contract. Not self-serve. | GDS segment incentives flow to the agency. Contract-specific fees **[background]**. | Full lifecycle: shop, price, book, ticket, exchange, refund, seat maps, ancillaries, NDC **[background]**. Exposed via agentic APIs and MCP (launched Sept 2025; ~80 airline and agency customers piloting or live by Sept 2026) **[claimed, Sabre PR]**. | GDS plus activated NDC carriers through one connection **[claimed]** | Heavy onboarding. Mindtrip is the reference consumer AI deal **[verified]**. |
| **Travelport (Travelport+, JSON APIs, "Trip Services API")** | Approval-based, sandbox, then UAT, then production. Requires IATA or TIDS, being on Travelport+, and an NDC-live country. Some airlines (United, Emirates) whitelist, and Air Canada requires registration **[verified, Travelport support docs]**. | Contract **[background]** | Full lifecycle. A cloud-native Trip Services API aimed at startups was reported in June 2026 **[claimed]**. Live end-to-end agentic NDC booking with Booked AI and Mastercard Agent Pay (13 Nov 2026) **[verified]**. | GDS plus NDC | Accreditation plus per-airline NDC registration |
| **Amadeus Enterprise** | Self-Service portal **decommissioned 17 July 2026**: keys disabled, SDK repos archived **[verified]**. Enterprise needs IATA/ARC and a formal agreement **[verified, secondary]**. | Contract | Full lifecycle | Largest GDS. Listed as a UCP lodging partner **[claimed]**. | No self-serve path left. Any tutorial built on Amadeus Self-Service is dead. |
| **Kiwi.com Tequila** | Invite-only since May 2024. Existing partners kept access **[verified]**. One source claims the portal fully closed 17 July 2026 **[claimed, unconfirmed]**. | Free API; commission on bookings **[claimed]** | Search plus "virtual interlining" booking, where Kiwi is merchant **[background]** | Strong LCC and self-transfer coverage | Effectively unavailable to new startups. Self-transfer itineraries carry missed-connection risk; Kiwi's own guarantee covers this **[background]**. |
| **Mystifly (SSP)** | B2B contract, quote-based on volume, markets and sources **[claimed]** | Quote-based | Search, book, post-booking servicing **[claimed]** | GDS + NDC + LCC + consolidator; "700+ airlines" **[claimed, reseller page]** | Strongest for consolidator fares in Asia/Middle East **[background]**. No MCP found. |
| **Travelfusion** | B2B contract **[background]** | Per-transaction plus contract **[background]** | LCC and NDC direct-connect booking and ancillaries **[background]** | LCC-heavy (Europe) | Not re-verified in this session |
| **Hopper HTS** | B2B for banks, airlines and loyalty programmes (Capital One, RBC, CommBank, Serko) **[verified]** | Revenue share; fintech add-ons **[background]** | Flights API (multi-provider, fare rules, seats, bags) and a new Hotels API (Aug 2026) **[claimed, HTS]**. **Cancel For Any Reason, Disruption Guarantee/Assistance** APIs (OAuth2 REST) **[claimed]**. | Frontier NDC live **[claimed]** | Targets large distribution partners, not startups. **The fintech protection APIs could be layered onto bookings to address "accountability"** **[inferred]**. |
| **Skyscanner / Kayak** | Skyscanner's B2B Travel API has been restricted to approved high-traffic partners since about 2023. Kayak runs an affiliate network programme **[background]**. | CPC / CPA | Search and deeplink only (metasearch; no booking) | Very broad | Affiliate-only. You don't own servicing, but you also carry no liability. |
| **Google Flights / ITA** | **No API.** QPX Express closed in 2018 **[background]**. ITA Matrix is web-only. | — | — | — | Scraping violates ToS. Google is building its own agentic flights in AI Mode; at the hotel launch, PhocusWire reported flights are "still waiting" **[verified]**. |
| **NDC direct** | Airline-by-airline. Generally requires IATA/TIDS plus a bilateral agreement **[background]** | Varies; some airlines pay NDC incentives or levy GDS surcharges | Full Offer/Order where the airline supports it | One airline per integration | Not worth it before scale. Use an aggregator (Duffel, Travelport, Sabre). |

### 1.2 How Mindtrip built flights (reference architecture)

- **Launch:** Mindtrip Flights launched on **6 May 2026** **[verified]**:
  - Sabre Mosaic Air APIs supply inventory, pricing, availability and ticketing.
  - Sabre also handles after-sales service **[claimed]**.
  - PayPal processes payment and verifies identity, and offers BNPL. A launch promo gave 5,000 PayPal points on BNPL bookings over $250 **[verified]**.
- **How autonomous it is:** Accounts conflict. Some call it "fully autonomous", others "not a fully autonomous purchasing agent" **[verified conflict]**. The user confirms in a chat checkout.
- **Lesson [inferred]:** Mindtrip avoided becoming an IATA ticketing agent and payment processor by renting both from Sabre and PayPal. It owns the conversation and the checkout UX. Uptake remains the open question: a Siften piece cites survey data that only about 2% of leisure travellers would let AI book for them **[claimed]**.

---

## 2. Hotels and stays

| Path | Access | Commercial model | Ops | Coverage | Notes |
|---|---|---|---|---|---|
| **Expedia Rapid API** | Apply, get approved, certify, then pass a **compliance review before launch**. Launch requirements differ for B2C vs B2B **[verified, developers.expediagroup.com]** | Negotiated revenue share. Expedia is usually merchant of record on "Expedia Collect" rates. Partner booking charges are allowed only if labelled as the partner's ("affiliate booking charge", never "fee") and kept separate from taxes and fees **[verified]**. Rates not public **[verified]**. | Search, price check, book, cancel, itinerary retrieval. Also Vrbo inventory, Rapid Car API, and per-rate MoR flags **[verified for car MoR flag; background for Vrbo]** | ~700k+ properties plus Vrbo **[background]** | The Expedia **B2B MCP server / Intelligent Experience Platform** was announced May 2026, "in coming months". Pilot partners and terms undisclosed **[verified]**. No launch confirmation found. |
| **Booking.com Demand API** | Managed Affiliate Partner status, a signed contract, and account-manager enablement. Ordinary affiliate status (e.g. via CJ) does **not** grant Demand API access **[claimed, multiple secondary]**. General Partner Terms v5 reportedly require **prior written approval to use AI** **[claimed, unverified]**. Booking's MCP server is limited to approved strategic partners **[claimed]**. | Affiliate commission (CPA). Booking.com is merchant or the hotel collects **[background]**. | Search, availability, booking for enabled partners, orders **[claimed]** | ~3M+ listings **[background]** | Hardest gate for an AI startup. Booking.com is a launch partner in Google AI Mode hotel booking and has a ChatGPT app **[verified]**. |
| **Nuitée LiteAPI** | **Self-serve** developer sign-up; Enterprise tier for scale **[verified/claimed]** | You set the commission or margin, including per query; Dynamic Markup **[verified, Nuitée updates]**. MCP tool calls and AI-completed bookings billed per use **[claimed]**. | Search, rates, prebook, book, cancel, retrieve. Built-in payment option, so LiteAPI can be merchant **[background]** | Aggregated wholesale (2M+ properties) **[background]** | **Open-source and hosted remote MCP** for Claude, GPT and Gemini: search, rate-check, book, manage **[verified]**. Lowest-friction path. |
| **Duffel Stays** | Approval on top of a Duffel account **[background]** | The accommodation provider pays commission and Duffel shares it with you; your share grows with volume **[verified, Duffel pricing quote]** | Search, quote, book, cancel; negotiated chain rates; rate-source visibility **[verified, changelog]** | 2M+ properties **[claimed]** | Single contract with flights and cars |
| **Hotelbeds (Apitude)** | Contract, credit and prepayment terms. Access depends on volume, markets and supplier relationships **[claimed]** | Net rates; you mark up **[background]** | Full booking lifecycle | ~300k hotels, strong in leisure and Mediterranean **[background]** | No public minimums found. B2B net rates often carry **parity restrictions**: you can't display them publicly below retail without packaging **[background]**. |
| **WebBeds, RateHawk (Emerging Travel Group)** | B2B contracts; RateHawk is relatively accessible to registered agencies **[background]** | Net rates | Full lifecycle | Large | Not re-verified (search budget) |
| **Agoda** | Affiliate programme with content, search and deeplink APIs. Booking API only for selected partners **[background]** | CPA | Mostly search plus deeplink | APAC strength | Not re-verified |
| **Airbnb** | **No public guest API.** Partner API is invite-only for software and host partners. No official MCP, ChatGPT app or Claude connector as of Nov 2026 **[claimed, consistent across sources]**. Airbnb's own agent is expected in 2027 **[claimed]**. | — | — | — | Third-party "Airbnb MCPs" read public pages or misuse private APIs, a ToS risk **[claimed]**. Vacation rentals are reachable via Vrbo (Expedia Rapid), Booking.com, or PMS-side MCPs (e.g. Hospitable) **[claimed]**. |
| **Selfbook / direct hotel booking engines** | Partnership | Hotel is merchant; Selfbook does payments and tokenization **[background]** | Book direct at hotel rates | Chains and independents | Background: Perplexity's in-chat hotel booking used Selfbook plus Tripadvisor (2025) **[background, re-verify]**. |
| **Google AI Mode (as a channel, not an API)** | US only, English, about 10 large chains and OTAs (Booking, Expedia, Marriott, Hilton, IHG, Trip.com, etc.) **[verified]** | Partner is merchant of record and handles post-booking **[verified]** | — | — | Independent hotels are booked through OTAs **[claimed]**. UCP hotel vertical spec announced at Google Marketing Live (May 2026) **[verified]**. |

---

## 3. Ground transport

### 3.1 Rail

| Path | Access / model | Ops | Coverage | Notes |
|---|---|---|---|---|
| **Trainline Partner Solutions (Global API)** | B2B contract; also an agent tool and white-label **[verified]** | Search, book, ticket, (refund/exchange per operator rules) **[background]** | 270+ rail and coach operators, 40 countries (Platform One) **[claimed]** | B2B net ticket sales +14% to £1.1bn; Global API in Europe +58% (May 2026). Partners include Amadeus Cytric, Spotnana, Navan **[verified]**. Primarily TMC-oriented. |
| **Distribusion** | B2B Retailer API; contact a partnership manager **[verified]** | Search, book, post-sales. **Retailer API MCP server (Feb 2026)**; Post-Sales AI Bot (May 2025) **[verified, Distribusion docs]** | Bus, rail, ferry, transfers. SNCF, DB, Trenitalia, Iryo, **Amtrak**, Eurostar, KAI Indonesia; Interrail reservations (Apr 2026) **[claimed]** | **Best single multimodal ground API for an AI planner** **[inferred]**. 1,500–2,000+ clients **[claimed]**. |
| **Omio** | Affiliate Search API plus deeplinks (~6% per Travelpayouts; Omio says the rate varies by market) **[claimed]**. **Booking API requires the partner to be merchant of record** **[verified, Omio B2B]**. Meta Search API also available. | Search (affiliate); book (MoR partner) | Trains, buses, flights, ferries across Europe and beyond; 800+ partners **[claimed]** | Good fallback |
| **Rail Europe** | B2B distribution API for agencies **[background]** | Book, ticket | European rail | Not re-verified |
| **G2Rail, SilverRail** | G2Rail: B2B API (Europe, Asia) **[background]**. SilverRail: rail booking tech, mostly TMC/operator **[background]** | — | — | Not found in this session's searches |
| **Amtrak** | No public booking API. Accessible via Distribusion **[claimed]** and GDS rail **[background]** | — | — | — |
| **Japan (JR)** | No public API. Shinkansen tickets resold via Klook and 12Go-type platforms; JR Pass via resellers **[background/inferred]** | — | — | Gap |
| **12Go Asia** | Affiliate: 50% revenue share, about $3 average commission per booking **[claimed, Travelpayouts]**. B2B API on request **[background]** | Deeplink/affiliate | SE Asia buses, trains, ferries | — |

### 3.2 Buses and ferries

- **FlixBus, Busbud, Bookaway:** affiliate programmes, with partner APIs by negotiation **[background; not re-verified]**.
- **Distribusion** covers most of this through one contract **[verified]**.

### 3.3 Car rental

- **Duffel Cars** launched in 2026 **[verified]**.
- **Expedia Rapid Car API** has documented launch requirements and per-rate merchant-of-record flags **[verified]**.
- **CarTrawler** is B2B and airline-focused. **Rentalcars Connect** (Booking Holdings) runs an affiliate programme **[background]**.

### 3.4 Transfers and rides

- **Mozio:** API, widget or white-label. 3,000+ providers in 180 countries; feeds Rome2Rio (2025) **[claimed]**. No AI-specific integration found.
- **Hoppa:** affiliate **[background]**.
- **Uber/Lyft:** deeplinks universally available. Programmatic ride requests are restricted to approved partners. Uber was an early ChatGPT-apps partner **[background]**.
- **Rome2Rio:** a planning and meta layer. Its public API has been closed to new users for years **[background]**.

---

## 4. Activities and dining

### 4.1 Activities

| Path | Access tiers | Commission | Bookable programmatically? |
|---|---|---|---|
| **Viator Partner API** | Basic (instant, no prequalification), Full, Full + Booking (authorization required), plus a separate Merchant partner type. Basic and Full redirect to viator.com; Full + Booking keeps the transaction on your site via Viator payments **[verified, partnerresources.viator.com]** | "Standard commission". Third parties cite ~8% and a 30-day cookie **[claimed]**. No fees for API access **[verified]**. | **Yes** (Full + Booking or Merchant) |
| **GetYourGuide Partner API** | BASIC/LIMITED_READ (catalogue), READ (live availability and pricing), BOOKING (end-to-end including payment) **[verified, partner-api-spec mirror]**. Free to join **[claimed]** | Affiliate rates not published. Supply-side commission is 20–30%, so affiliate share is lower **[claimed]** | **Yes**, at BOOKING tier. Only community, read-only MCPs exist **[claimed]** |
| **Klook, Tiqets, Musement (TUI), Headout, Fever** | Affiliate plus B2B/distributor APIs by agreement **[background]** | Varies | Tiqets and Musement have booking-capable distributor APIs **[background]**. Not re-verified. |

### 4.2 Restaurants

| Platform | Programmatic booking for a third party? |
|---|---|
| **OpenTable** | Partner-gated: affiliate directory API, restaurant partner APIs, an "In House Booking (Voice AI) API" for approved voice-AI vendors. Signed agreement and QA review; 3–4 weeks onboarding; OAuth2 **[claimed, consistent]**. No public MCP **[claimed]**. |
| **Resy (Amex)** | No public API. Partner API only for approved POS, CRM, loyalty and discovery partners. The consumer API is undocumented, and using lifted session tokens violates ToS **[verified]**. Resy reservations in ChatGPT reportedly launched 10 Aug 2026 **[claimed]**. |
| **SevenRooms, Tock (Amex), TheFork (Tripadvisor)** | Partner APIs by agreement **[background]** |
| **Google Reserve / AI Mode** | Supply-side programme; not consumable by third parties. Google's own agentic restaurant booking in AI Mode works through OpenTable, Resy, Tock, SevenRooms and others **[background]**. |

**Takeaway [inferred]:** Dining is the most closed vertical. A startup realistically gets deeplinks, plus one negotiated partner (OpenTable affiliate or SevenRooms). Distribution deals go first to the big AI surfaces (ChatGPT, Google).

---

## 5. Aggregated layers and agentic commerce

### 5.1 Travel MCP servers (supplier-side)

| MCP | Status | Can book? |
|---|---|---|
| **Sabre MCP** | Live since Sept 2025; ~80 clients by Sept 2026; powers apps in ChatGPT and Claude **[claimed]** | Yes, for PCC holders |
| **Nuitée / LiteAPI MCP** | Live, open source, hosted remote endpoint **[verified]** | Yes |
| **Distribusion Retailer API MCP** | Live Feb 2026 **[verified]** | Yes (partners) |
| **Expedia B2B MCP** | Announced May 2026; launch unconfirmed **[verified]** | Planned (lodging, flights, cars, activities) |
| **Booking.com MCP** | Restricted to approved strategic partners and enabled affiliates. A consumer Claude connector exists for searching stays **[claimed]** | Restricted |
| **Duffel, Kiwi, Tripadvisor, Amadeus MCPs** | Not verified this session (search budget). Kiwi had a consumer-facing MCP/ChatGPT presence and Duffel has community MCPs **[background]** | — |
| **Community MCPs** (GetYourGuide, Airbnb, etc.) | Read-only or ToS-risky **[claimed]** | Mostly no |

### 5.2 Consumer agentic surfaces (competitors and channels)

- **ChatGPT apps** (Apps SDK on MCP; Expedia and Booking.com launched 6 Oct 2025) hand off to the partner's checkout **[verified]**.
- **OpenAI Instant Checkout** (ACP, with Stripe) was scaled back in March 2026. OpenAI said it is "moving to apps"; ACP continues as an Apache-2.0 standard **[verified]**. Merchant uptake was tiny (about 12–30 merchants by various estimates) **[claimed]**.
- **Google AI Mode** books hotels in the US (Aug 2026). Partners are merchant of record. UCP has a hotel vertical spec; flights are pending **[verified]**.

### 5.3 Payments for agents

| Rail | Status (Nov 2026) |
|---|---|
| **Mastercard Agent Pay** | Live agentic flight purchase on 13 Nov 2026 (Travelport NDC, Booked AI agent, Basis Theory tokenization). The airline stayed merchant and the user approved the exact amount **[verified]**. Enrollment goes through issuers **[claimed]**. Earlier: Hong Kong taxi (Mar 2026) **[claimed]**. |
| **Visa Intelligent Commerce / Trusted Agent Protocol** | Closed-beta pilots. Ramp corporate-travel partnership; Alchemy AgentCard (June 2026) **[claimed]**. No live airline or hotel booking found. |
| **Google AP2** | Launched Sept 2025 with 60+ partners; travel is the flagship example **[verified]**. Reportedly donated to the FIDO Alliance in April 2026; about 3 production deployments by mid-2026 **[claimed, single source]**. |
| **Stripe** | ACP co-author; agent toolkit and Shared Payment Tokens **[background]** |
| **PayPal** | Agent toolkit and MCP; Mindtrip Flights payments plus identity and BNPL **[verified for Mindtrip]**; AP2 wallet integration **[claimed]** |

**Implication [inferred]:** For a startup, the realistic 2026–27 pattern is the following:
- Use a tokenized card (Agent Pay or VIC where available, otherwise a standard PSP vault) and an explicit human confirmation of the final price.
- Charge on the supplier's rail (airline or hotel as merchant via Duffel, Sabre or Expedia), or on your own rail (you as merchant).
- Fully autonomous, unattended purchases are not yet accepted by airlines (see United).

### 5.4 Computer-use and browser agents

- **United's November 2026 restriction** covers its own channels and OTA-intermediated bookings made by unauthorized agents. It cites credential sharing, surprise purchases, miles misuse, and DOT/FAA human check-in requirements **[verified]**.
- **Ryanair's scraper litigation:** Ryanair has a long litigation history against screen scrapers, including a 2024 US jury CFAA finding against Booking.com **[background]**.
- **Reliability:** browser agents fail on CAPTCHAs, 3-D Secure, dynamic seat maps and price-change interstitials **[inferred]**.
- **Verdict:** browser automation is acceptable only as a fallback for read-only tasks (checking a booking the user owns, with consent). Use it to book only where the supplier permits it. Never use it with shared loyalty credentials.

### 5.5 Standards

- **IATA ONE Order / Offers & Orders:** live natively at Finnair (May 2025, Nevio), Saudia (July 2025) and Riyadh Air. Lufthansa Group signed in Jan 2026 to move to Nevio Order IDs; AF-KLM is in the pipeline **[claimed, vendor blog]**. IATA (June 2026) calls it an "inflection point"; mainstream adoption is projected beyond 2027 **[verified]**.
- **For startups:** Order-based servicing (single Order ID covering air plus ancillaries) improves post-booking APIs, but only through NDC aggregators **[inferred]**.
- **OpenTravel:** no notable 2025–26 agentic standard found (search budget).
- **The emerging "standards" in practice:** MCP (transport), UCP (Google, commerce semantics), ACP (OpenAI/Stripe), AP2 (mandates) and network agent tokens **[inferred]**.

---

## 6. Post-booking and trip-management interop

| Need | Option | Status |
|---|---|---|
| Import bookings made elsewhere | **Email parsing**. Your own parser plus LLM extraction, or **AwardWallet Email Parsing API** (pricing on request) **[verified]**, or **Traxo** (4,000+ formats, 20+ languages, manual fallback; enterprise/TMC focus) **[claimed]**. | Reading Gmail via API requires Google's **restricted-scope verification plus annual third-party security assessment (CASA)** **[background]**. Forward-to-address (like TripIt's plans@) avoids it **[inferred]**. |
| TripIt sync | Public API **closed to new integrations**; existing connections keep working **[verified]** | Dead end for a newcomer |
| Loyalty balances and status | **AwardWallet Account Access API** (basic free; Business plan for timeline export; admins need Plus) and **Web Parsing API** (no AwardWallet account needed; pricing on request) **[verified]** | Airlines have no public loyalty APIs **[background]**. United now warns against sharing MileagePlus credentials with agents **[verified]**: web-parsing loyalty is a growing risk. |
| PNR retrieval and servicing | Only through the rail that created the booking (Duffel order, Sabre/Travelport PCC). Retrieving another agency's PNR is not generally possible **[background]**. | Core accountability constraint |
| Flight status, IROPs | Data APIs (FlightAware AeroAPI, Cirium, OAG) for status **[background]**. HTS Disruption Assistance/Guarantee and CFAR for monetised protection **[claimed]**. Duffel airline-initiated change webhooks **[background]**. | Re-accommodation still needs an airline or GDS servicing path |
| Calendar | Google Calendar API, Microsoft Graph, ICS feeds | Easy |
| Wallet passes | Apple PassKit / Google Wallet generic passes for itineraries | Boarding passes are only issued by airlines **[background]** |

---

## 7. Merchant of record vs. agency vs. affiliate

### 7.1 Models

| Model | You do | You carry | Margin | Examples |
|---|---|---|---|---|
| **Affiliate / metasearch** | Discover and deeplink. The supplier or OTA checks out. | Little; no servicing | CPC or CPA (Viator ~8% claimed; Omio ~6% claimed; 12Go 50% rev share claimed) | Most AI planners in 2024–25; ChatGPT OTA apps; Layla-style planners **[background]** |
| **Agency (supplier or consolidator is MoR)** | Book via API; supplier or aggregator charges the card | Customer-service expectations; some disclosure duties; seller-of-travel registration may apply **[background]** | Commission share, markup on top | Expedia Rapid (Expedia Collect), Duffel Stays, Google AI Mode (partner MoR), Mindtrip-Sabre (ticketing by Sabre/agency) |
| **Merchant of record** | You charge the card, pay suppliers net | **Chargebacks, PCI scope, supplier insolvency, refunds, 24/7 servicing, packaging law** | Highest: markup on net rates, ancillaries, fintech add-ons | Omio Booking API partners, LiteAPI with your own payments, Hotelbeds net-rate sellers |

### 7.2 Legal and operational implications [mostly background; re-verify with counsel]

- **US seller-of-travel laws** (California, Florida, Washington, Hawaii; others partial) require registration. California also requires a trust account or bond and Travel Consumer Restitution Fund participation. They apply to anyone selling to residents, including online sellers **[background]**.
- **US DOT ticket-agent rules:** full-fare advertising and the 2024 automatic-refund rule extend obligations to ticket agents **[background]**.
- **EU Package Travel Directive (2015/2302)** and **UK Package Travel Regulations / ATOL:**
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
| **ChatGPT / Expedia / Booking apps** | Pure handoff; the OTA is MoR **[verified]** |
| **Google AI Mode** | Partner is MoR and services the booking **[verified]** |
| **Booked AI** | Agent on Travelport, airline as merchant, Mastercard tokens **[verified]** |
| **Perplexity hotels** | Selfbook/Tripadvisor; hotel is MoR **[background]** |
| **Most other planners** (Layla, Wanderboat, Trip Planner AI, etc.) | Affiliate deeplinks **[background]** |

**No major consumer AI planner is a full merchant of record across bundles** **[inferred]**, which also means none takes end-to-end accountability.

---

## (a) Best access path per vertical, now

| Vertical | Best startup path (Nov 2026) | Accreditation needed | Achievable depth | Upgrade path |
|---|---|---|---|---|
| Flights | **Duffel** (Managed Content) | None (Duffel tickets) **[background]** | **Book + manage** (voluntary changes, cancels, ancillaries, seats; schedule-change webhooks). IROPs only partial. | Sabre/Travelport via host agency or IATA (TIDS → IATA) for GDS breadth and Sabre MCP; HTS CFAR/Disruption for protection |
| Flights (discovery breadth) | Kayak/Skyscanner affiliate where approved | None | Search + deeplink | — |
| Hotels | **LiteAPI** (self-serve, MCP) + **Duffel Stays** | None | **Book + cancel + retrieve** | Expedia Rapid (compliance review), then Hotelbeds/RateHawk net rates, then Booking.com Demand (hard, AI approval) |
| Vacation rentals | Vrbo via Expedia Rapid; Booking.com homes | Partner approval | Book (via Rapid) | Airbnb: none (2027 own agent) |
| Rail/bus/ferry | **Distribusion** (MCP) + **Trainline Partner Solutions** | B2B contract | **Book + post-sales** | Omio Booking API (become MoR); 12Go for SE Asia |
| Car rental | Duffel Cars / Expedia Rapid Car | Same as above | Book + cancel | CarTrawler (enterprise) |
| Transfers | **Mozio** API | Contract | Book + cancel | Uber/Lyft deeplinks |
| Activities | **Viator** (Full + Booking) + **GetYourGuide** (BOOKING tier) | Authorization | **Book + cancel** | Tiqets/Musement/Klook distributor APIs |
| Restaurants | Deeplinks; OpenTable affiliate; negotiate one partner API | Partnership | **Mostly search/deeplink** | OpenTable/SevenRooms partner APIs |
| Post-booking import | Forwarding-address email parsing + LLM extraction; AwardWallet APIs | None (avoid Gmail restricted scope initially) | **Observe only** for external bookings | Gmail CASA-verified integration; ONE Order via NDC aggregators |
| Payments | Stripe/Duffel Payments tokens; PayPal; Mastercard Agent Pay when issuers enable | PSP onboarding | Human-confirmed agentic checkout | Visa VIC/TAP, AP2 mandates |

## (b) The interoperability ceiling today (where it breaks)

1. **Search: mostly solved, with legal limits.** Breadth is available via affiliates and metasearch. The gaps are Google Flights (no API), Airbnb (no API), Japan rail, and restaurants (closed).
2. **Book: solvable for one cart per supplier rail, without accreditation, via Duffel, LiteAPI, Viator, GetYourGuide and Distribusion.** It breaks when:
   - you need GDS-only or corporate fares;
   - you need Booking.com inventory (AI approval gate);
   - you combine components into one payment, which triggers package law and ATOL;
   - an airline forbids agent bookings (United).
3. **Manage: the real ceiling.**
   - Voluntary changes and cancels work only for bookings on your own rails.
   - IROPs re-accommodation, refunds-to-original-form after airline cancellation, and loyalty accrual fixes still frequently need human contact with the airline.
   - For bookings made elsewhere you can only **observe** (email parse, AwardWallet), never **act**: no PNR retrieval or cross-agency servicing.
   - Loyalty credential sharing is now explicitly discouraged by airlines.
4. **Accountability: absent in the market.** Every AI surface pushes liability to the supplier or OTA as merchant of record. No AI planner guarantees the whole trip. Hopper HTS-style fintech (CFAR, disruption guarantee) is the only off-the-shelf "insurance" for this, and it is sold to banks and airlines, not to startups.
5. **Agent identity and authorization: unstandardised.** Mastercard Agent Pay, Visa TAP, AP2 mandates and UCP are competing. Airlines demand "standardized, secure integrations" before allowing agents (United) **[verified]**. Whoever ships a verifiable, consented agent identity on top of sanctioned rails is on the right side of this.

## (c) Top gaps and a phased integration strategy

### Top gaps / opportunities

1. **Whole-trip accountability layer** **[inferred, high value]**. Combine:
   - booking on owned rails (Duffel, LiteAPI, Distribusion, Viator);
   - continuous monitoring (schedule-change webhooks, flight status);
   - pre-packaged remedies (HTS-style CFAR or disruption cover, or self-insured);
   - an agent that executes re-bookings via API.

   Nobody does this end-to-end. Structure it to avoid organiser-of-package liability: separate contracts per component and LTA disclosures, or deliberately become an organiser with insolvency cover in one market.
2. **External-booking import plus "managed-through-us" migration.** TripIt's API is closed, which leaves an opening for an AI-native itinerary hub. It would parse forwarded emails and loyalty data, then offer to re-book or protect via your rails. Avoiding Gmail restricted scopes at first keeps compliance light.
3. **Sanctioned-agent posture as a moat.** United's ban plus the Mastercard/Travelport demo show airlines want identifiable, tokenized, human-confirmed agents. Be early on Agent Pay / VIC tokens and transparent agent identity. Never ask for loyalty passwords.
4. **Multimodal ground in one MCP** (Distribusion plus Trainline plus Mozio). Rail, bus, ferry and transfer stitching is weak in every AI planner. Supplier MCPs now exist (Distribusion).
5. **Restaurants and Japan rail are closed verticals.** Win through partnerships with mid-tier platforms (SevenRooms, TheFork, Tock) and Asia resellers (Klook, 12Go) rather than waiting on OpenTable or Resy.

### Phased integration plan

**Phase 0 (weeks 0–6): zero-accreditation coverage.**
- Duffel (flights, stays, cars) and LiteAPI (hotels via MCP).
- Viator (Basic → Full + Booking) and GetYourGuide (READ → BOOKING).
- Affiliate deeplinks: Omio, 12Go, Booking.com affiliate, Kayak/Skyscanner where approved, OpenTable/Resy links, Uber/Lyft deeplinks.
- Stripe or Duffel Payments in tokenized mode.
- Email-forwarding importer plus AwardWallet Account Access.
- Legal: choose agency/disclosed-agent posture; register as seller of travel in CA, FL, WA and HI before selling there; per-component checkout to avoid package formation.

**Phase 1 (months 2–6): depth and ground.**
- Distribusion (MCP) and Mozio.
- Expedia Rapid application (compliance review; Vrbo, cars; B2B MCP when live).
- Trainline Partner Solutions.
- Flight-status data plus Duffel change webhooks driving proactive rebooking.
- Pilot HTS CFAR/Disruption or an equivalent insurer partnership.

**Phase 2 (months 6–12): accreditation and networks.**
- IATA TIDS → IATA accreditation, or a host agency, for a Sabre PCC (Sabre MCP; Mindtrip pattern) or Travelport (Trip Services API; Booked AI pattern).
- Mastercard Agent Pay / Visa VIC token checkout.
- Hotelbeds/RateHawk net rates for margin.
- Booking.com Demand API application with explicit AI approval.

**Phase 3 (12+ months): become the accountable organiser in one market.**
- In one market (e.g. UK with ATOL or one EU state with insolvency cover), offer guaranteed whole-trip packages.
- Adopt ONE Order servicing through NDC aggregators as airlines go live.
- Expose your own MCP/UCP endpoint so other agents (ChatGPT, Gemini, Claude) can book your protected trips.

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
