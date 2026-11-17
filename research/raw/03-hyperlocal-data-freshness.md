# 03 — Hyperlocal Knowledge, Place-Data Quality, Freshness & Hallucination

*Research agent 3 of 7 · compiled 2026-11-17*

**Evidence labels:** **[verified]** means confirmed in a primary or near-primary source found during this session. **[claimed]** means stated by a vendor, a secondary outlet or a single report. **[inferred]** means my analysis. **[bg]** means background knowledge from before this session (up to mid-2026) that I could not re-check here. Treat [bg] items as leads to verify.

**Method limits (read first).** WebFetch could not reach most hosts from this container (greetwell.com, monkeyeatingmango.com and keyt.com all failed DNS). The first pass ran out of shared web-search budget, so many rows rested on [bg] knowledge.

A **gap-fill pass (2026-11-17, 54 searches, search snippets only, no page fetches)** re-checked those rows. It covered:
- Beli, Corner, Mapstr, Fever, Withlocals
- The TikTok, Instagram and YouTube terms
- Citymapper, Moovit, HERE, TomTom, Mapbox, SafeGraph/Advan/Dewey
- Wikivoyage and Wikidata
- Michelin, Time Out, Lonely Planet and The Infatuation, plus the publisher AI deals
- The Mount Misen and Weldborough incidents
- Entry-rules, accessibility and safety data
- Events APIs and tourism open data (DATAtourisme, ATDW, Tokyo)
- VOYGR, Google pricing, Rome2Rio/Omio, Transitous, Navitia, NAVITIME, ferries and GTFS cable modes

Tags were updated wherever evidence was found. Several items are still unverified and are marked [bg] or "not found":
- Showaround and ToursByLocals APIs
- Resident Advisor
- iVisa
- Euan's Guide
- Jorudan
- GeoSure and Safeture pricing
- Routes API (New) transit coverage in Japan and China
- Primary-source HERE and TomTom storage clauses

Raw notes: `research/notes/03-gapfill-notes.md`.

---

## 1. Evidence of the problem

### 1.1 Documented incidents

| Incident | What happened | Root cause class | Status |
|---|---|---|---|
| **"Sacred Canyon of Humantay", Peru (2025)** | Two tourists headed into the Andes toward a canyon that does not exist and were stopped by a local guide, Miguel Angel Gongora Meza (Evolution Treks Peru). They had reportedly paid for the trip; one report puts the cost at ~£118. The name seems to blend two real local toponyms. Logged as an OECD AI incident and in the AI Incident Database. | Entity fabrication by merging real names | [verified that it was reported] (BBC-sourced, OECD.ai, AIID). One Substack questions whether the guide's account was embellished. |
| **"Kuak Skyride" cable car, Perak, Malaysia (June 2025)** | An elderly couple drove ~300–400 km to see a cable car shown in a ~3-minute AI video (reportedly made with Veo 3) styled as a "TV Rakyat" news report. Officials confirmed no such project exists. | Synthetic media treated as ground truth. This was not a planner error, but any planner that ingests social video inherits the risk. | [verified] (SCMP, NST, PetaPixel) |
| **Mount Misen ropeway, Miyajima, Japan (2025)** | A couple, named as Dana and Robert Yao, used ChatGPT to plan a sunset hike. ChatGPT reportedly gave the last ropeway as 5:30 pm, but the ropeway had already closed when they reached the summit, and they were stranded. | Wrong attraction-operational data (last-departure time) | [claimed] Logged as AI Incident Database #1635, dated 2025-09-29, citing a watson.de report. The gap-fill could **not** confirm the BBC feature ("The perils of letting AI plan your next trip") as its source. Snippets of that feature mention only Humantay. |
| **"Weldborough Hot Springs", Tasmania (Jul 2025, reported Feb 2026)** | Tasmania Tours (Australian Tours and Cruises) published an AI-generated list, "7 Best Hot Springs Tasmania Experiences for 2026". It named non-existent Weldborough Hot Springs, and also Savage River and Liawenee, which are not hot springs either. The owner said the posts went live unchecked while he was overseas. The Weldborough Hotel fielded calls and visits from people looking for the springs, and the content was later removed. | Fabrication in a "local" content source (AI-written operator blog) | [verified] (The New Daily, 2 Feb 2026) |
| **Canadian hikers, "Unnecessary Mountain", BC (2025)** | Two hikers followed a ChatGPT-planned route that ignored conditions and had to be rescued. BC search-and-rescue groups warned about AI-guided hikers. | Ignored seasonality and conditions | [claimed] (OECD.AI incident, Gigazine) |
| **Stacker roundup (Oct 2026)** | Cases include a ChatGPT-invented bar in Lisbon, which the bot admitted was invented when pressed, and Notion AI scheduling a "day trip" to Ba Na Hills (Da Nang) from a Hanoi base, several hundred km away. | Fabrication and geographic infeasibility | [claimed] (syndicated via Coast Reporter) |
| **Bolinas, CA, ChatGPT test (Fast Company)** | ChatGPT recommended "Wharf Road Restaurant & Bar", which the journalist could not find in Google, a maps app or the hotel's list. A second suggested restaurant was permanently closed. | Invented venue plus a stale closure | [claimed] (found via secondary summary) |
| **Washington, DC, ChatGPT test (Washington Post)** | The restaurant list included permanently closed venues. | Stale closure | [claimed] (secondary summary) |
| **Layla early outputs (2023–24)** | Reported an "Eiffel Tower in Beijing" and a marathon route across northern Italy that could not be run. | Fabrication and geographic infeasibility | [bg] |
| **Visa failures (2025)** | Viral cases of travelers denied boarding after ChatGPT gave wrong entry or ESTA advice. Stacker/KEYT ran a roundup in Oct 2026, "bogus bars to visa fails". | Regulatory info hallucination | [claimed] (roundup seen via the Coast Reporter syndication; original unreachable) |

No new 2026 case was found of ChatGPT or Gemini *stranding* travellers beyond those above (one extended search) [verified absence, limited].

**Pattern [inferred].** The failures fall into five classes. In rough order of how often they appear:
1. Stale status: closed or relocated venues.
2. Wrong operational times: hours, last entry, last ropeway or ferry, closed weekdays.
3. Infeasible sequencing: backtracking, overruns, double-booking.
4. Outright fabrication: invented places, often by merging two real names.
5. Synthetic or AI-generated source content poisoning retrieval.

Classes 1–3 can be fixed with data and constraint checking. Class 4 is fixed by entity grounding. Class 5 is a growing provenance problem.

### 1.2 Quantification

| Study | Sample | Key numbers | Caveat |
|---|---|---|---|
| **Greetwell AI Travel Report 2026** (Aug 2026) | 1,000 US leisure travellers; 485 had used AI for travel | **55%** met at least one inaccurate, unavailable, nonexistent or closed recommendation. **27%** saw incorrect details, **21%** unavailable bookings, **16% (~1 in 6)** a place, tour or activity that did not exist. Trust in AI rose for 34% and fell for 14%. | Company-commissioned and self-reported. [verified via syndicated press release] |
| **MonkeyEatingMango itinerary audit** (~Sep 2026) | 356 AI itineraries, 2,735 days, 268 destinations, 61 countries | **43% of planned days** have at least one verifiable fault: venue shut at the scheduled hour, visit running past closing, backtracking, or a duplicate. **53% of closed-day errors fall on Mondays.** 84% of early arrivals are off by 1 hour or less. Faults grow with trip length and complexity. | Vendor study. The six category shares were not retrievable. [claimed] |
| **Global Rescue survey** (Sep 2026) | Experienced international travellers | **27%** met incorrect or outdated AI information; **3%** said it affected their plans. In the 2025 wave, 24% used AI for planning. | [claimed via secondary] |
| **Simon-Kucher Global Travel Trends 2026** | Dissatisfied AI users | **52%** said answers were inaccurate; **47%** said they were too generic. This figure supports both our problem #1 and problem #3. | [claimed via secondary] |
| **VOYGR closure test** (Aug 2026) | 400 US places sampled from Overture | 86 confirmed closures, of which **23 (~27%) still showed as open or missing on Google Maps**. | Vendor with an interest in the result. [claimed] |
| **TravelPlanner benchmark** (Xie et al., ICML 2024) | 1,225 queries with hard and commonsense constraints | GPT-4 with tools had a **0.6%** final pass rate. This is the likely origin of the oft-quoted "90% of AI itineraries contain errors". Later LLM-Modulo and formal-solver approaches raised success sharply; one SMT-based framework reported ~90%+. | [bg] |
| **Amadeus** | Global | Gen-AI use for trip planning rose from 11% (2024) to 18% (2025). | [claimed] |
| **Layla's own comparison blog** | Several tools | "Every tool tested surfaced at least one wrong opening hour, a quietly closed restaurant, or an off distance." | Vendor. [claimed] |

**Takeaway [inferred].** At least one error per trip is close to universal. Errors per day run at roughly 40%. Outright fabrication is the minority, at about 1 in 6 users, but it is the most damaging to trust. The main failure is *operational*: time, status and feasibility. It is not hard knowledge.

---

## 2. Place / POI data sources

### 2.1 Master comparison

| Source | Coverage | Freshness mechanism | Cost (2026) | Licensing: caching, LLM and display | Suitability |
|---|---|---|---|---|---|
| **Google Places API (New)** | Largest consumer POI graph, ~250M+ places (Google's figure in the Maps-grounding launch) [claimed]. Best for hours, business status, reviews, photos and price level [bg]. Accessibility comes as `accessibilityOptions`: wheelchair-accessible entrance, parking, restroom and seating, each a nullable boolean [verified]. | Business owners via Business Profile, user edits, Local Guides, **Duplex phone calls** (3M+ updates by 2020; target of 20M businesses' hours) [verified, dated], imagery and ML. Low-confidence hours carry a "may have changed" warning [verified]. **~27% of real closures missed in one vendor test** [claimed]. | Since 1 Mar 2025 the $200 credit is replaced by free calls per SKU: Essentials 10k, Pro 5k, Enterprise 1k per month [verified]. Fields such as hours and ratings sit in the Pro/Enterprise tiers, roughly $32–35 per 1k (secondary) [claimed]. Another secondary source puts Place Details at $5 per 1k for Essentials and $17 for Pro [claimed]. **No new 2026 Places pricing change found**; optional subscription plans now sit alongside pay-as-you-go [verified absence, 1 search]. | **No caching except place_id**, which may be stored indefinitely. lat/lng may be cached for 30 days [verified]. ToS §3.2.3 prohibits using Maps content to "train, test, validate or fine-tune" ML/AI models [verified]. The Analytics SSTs allow Maps content *only as a factual reference to validate or correct ML output* in that product [verified]. There are separate EEA terms [verified]. In practice you **cannot build your own vector index of Google content** [inferred]. | Best live lookup layer. Unusable as the substrate of a proprietary knowledge base. |
| **Grounding with Google Maps (Gemini API)** | Same graph, exposed as a tool for Gemini. GA October 2025 [verified]. | As above | Gemini 3+: 5,000 free requests per month, then **$14 per 1k** grounded queries. Gemini 2.5: $25 per 1k [verified]. | Gemini-only (lock-in). Each source must carry Google Maps attribution. An optional widget token shows place cards [verified]. Grounded output may not be used to train models [verified]. There is also a "Grounding Lite" agent/MCP offering under similar terms [verified mention]. | Fastest path to grounded answers if you run on Gemini. Strategic dependency risk. |
| **Foursquare OS Places (open)** | ~100–106M POIs, global, 22 core attributes. Releases are monthly [claimed]. | Monthly releases. Example notes: 13.7M record updates and 200k new places in one release; 500k places held back for quality. An agent-based verification system checks ingestion [claimed]. Has `date_refreshed` and `date_closed` fields [bg]. | Free | **Apache 2.0** (attribution notice) [verified]. Some rows may be CDLA-Permissive-2.0 [claimed by SafeGraph]. Since Oct 2025, available only via supported channels, not the public S3 bucket [claimed]. LLM-friendly. | A strong open spine. Thin on attributes, especially hours. |
| **Foursquare Places API (commercial)** | Same base plus Premium fields: hours, photos, tips, ratings. | Continuous | From 1 Jun 2026: Pro ~$15 per 1k; **free tier cut from 10k to 500 calls**. Premium $11.25–18.75 per 1k, no free tier. "Ask" natural-language endpoints $30–36 per 1k [claimed, secondary; Foursquare's marketing page still says 10k]. | **FSQ Supplemental AI Terms** apply to Places API AI features (search, matching, summaries). They list prohibited uses, which were not read in full, and allow third-party AI providers to process inputs and outputs [verified exists]. The self-service EULA grants no right to create derivative works. Pages that display Places Data must be protected from crawling. The AUP has a caching section [verified snippets]. | Hours and tips at lower cost than Google. Tips are dated (City Guide app shut 2024 [bg]). |
| **Overture Maps (Places)** | **88.4M places** (2026-10-21 release, +8.5%). New sources: Uberall (424.6k), Birdeye, OpenTravel [verified]. Meta and Microsoft confirmed as sources; a Foursquare feed is unconfirmed. | Monthly. Each place has a 0–1 **existence confidence**, *not calibrated across providers*, so use it only as a relative filter [verified]. Earlier quality audits found location errors and outdated places [claimed, 2023]. | Free | CDLA-Permissive-2.0 for places [bg]. **GERS stable IDs** for entity joins [verified]. | Best open join key and spine. Expect noise. Filter by confidence and cross-check. |
| **OpenStreetMap** | Global and uneven; excellent in the EU and Japan. | Community edits | Free | **ODbL share-alike.** A derived *database* mixed with OSM must be ODbL; "produced works" (rendered output) need attribution only [bg]. Legal friction when merged with proprietary data. | Strongest source for long-tail structure: trails, viewpoints, stairs, toilets, water, `wheelchair=*`. `opening_hours` is filled for only **~45–49%** of restaurants in typical cities (Bordeaux 48.9%) and ~77% in Berlin [claimed]. |
| **Apple Maps Server API / MapKit** | Global. Ratings partly via partners [bg]. | Business Connect; partners | Quota-based. The daily-vs-monthly quota is ambiguous and developers report hitting limits [verified forum]. | Place IDs are available. ToS not reviewed. | Secondary. Weak developer tooling for this use case. |
| **Yelp Places API (formerly Fusion)** | Strong in US, CA and parts of the EU [bg]. | Reviews | Base $229, Enhanced $299, Premium $643 per month plus overage. No free tier beyond a 5k trial [verified]. **Yelp AI API $25 per 1k** with a 1k/day minimum [verified]. | ToS bars *training* gen-AI on Yelp content **and bars submitting or ingesting Yelp content into any gen-AI model** (e.g. ChatGPT) without written approval [verified]. Content may be kept ≤24h [claimed]. **Yelp licensed reviews, ratings, photos and business data (330M reviews, 8M+ listings) to OpenAI for ChatGPT** (Axios, 23 Jul 2026). The deal is non-exclusive, so Yelp can sign other AI firms; terms were not disclosed [verified]. | Can enter an LLM pipeline **only via the Yelp AI API or a negotiated licence**. The lab-level licence route that OpenAI used is now proven. |
| **Tripadvisor Content API / Terra** | 8M+ businesses, 1B+ reviews [bg]. | Reviews | The legacy API had a 5k/month free tier. **Reportedly retired 31 Aug 2026**, with access moving to Terra (one-time allowance of 1,000 entities) [claimed]. | Legacy terms (Mar 2025) allow AI **only for internal, non-commercial RAG testing**. Any other AI use needs a signed agreement. AI summaries must carry a "may contain mistakes" disclosure. Selective display of reviews is banned [verified terms page plus secondary]. | Partner deal required. Good for attractions and tours. |
| **HERE / TomTom / Mapbox Search** | Global, automotive-grade addresses and POIs [bg]. TomTom's Orbis Maps Search API is in public preview [verified]. | Commercial feeds | **Mapbox:** permanent geocoding $5 per 1k with no free tier [claimed]; Search Box ~$11.50 per 1k sessions at standard rates [claimed]. **HERE:** commercial terms v2.5 (1 Jul 2026) and a pricing update (1 Apr 2026); Places rates not extracted [verified page dates]. TomTom: usage-based [bg]. | **Corrected: not more permissive than Google for POIs.** Mapbox allows permanent storage *only* through the permanent Geocoding endpoint, which **does not return POIs**. Search Box (POI) results are temporary [verified docs]. HERE's 2020 platform terms bar building a derivative POI database from HERE Content [verified, 2020]. A secondary source gives a 30-day storage cap [claimed]. TomTom: no storage, caching only as response headers allow, no derivative databases [claimed, geocod.io]. | Geocoding and routing backup. Weak on "experience" attributes. **Not a storable POI spine.** |
| **SafeGraph / Dewey / Advan / Placer.ai** | **SafeGraph: 80M+ POIs worldwide in four country coverage tiers** [claimed, vendor], which corrects "mostly US". It is the base of Esri ArcGIS Places. Advan foot traffic (Weekly Patterns+) covers US and CA from 2018 [verified vendor docs]. | Monthly (SafeGraph). Weekly (Advan, delivered the following Wednesday). | Paid, usage-based commercial contracts | SafeGraph: commercial licence [claimed]. Advan via **Dewey**: academic research licence; commercial use needs a separate licence [verified]. | Analytics and a possible paid spine supplement. Weak on consumer "experience" value. |
| **BestTime.app** | Claims 150+ countries. A venue needs roughly ≥100 visitors/day for a forecast [claimed]. | Hourly forecasts (0–100) plus live data where available | From ~$29/month metered [claimed] | Vendor terms | The only practical "popular times" substitute. Google does **not** expose Popular Times via the API [bg]. |
| **VOYGR** (YC W26) | US-first | Active closure detection. `/v1/validate` returns open, closed, unknown or not_exists with an existence_confidence. **PlaceCall** phone verification. Batches of 10k [claimed]. | **Credits:** a free key includes 2.5k credits with no card. Validate costs 1 credit; standard enrichment, **including opening hours**, costs 1 credit per place. PlaceCall is **$0.10 per successful call**, or $0.09–0.096 in packs [claimed, dev repo and Apify listing]. One aggregator lists "from $49/mo" [claimed]. | REST, MCP and llms.txt [claimed]. Dev CLI on GitHub [verified]. | Closest thing to a "liveness API". **Correction:** the first pass said "no opening hours yet". VOYGR's dev tooling now documents an hours-enrichment field [claimed]. |
| **Wikidata / Wikivoyage** | Landmarks, plus Wikivoyage's "See/Do/Eat/Sleep" text per destination [bg] | Volunteer | Free, or paid bulk and real-time access via **Wikimedia Enterprise**. Enterprise deals announced 15 Jan 2026 with Amazon, Meta, Microsoft, Mistral and Perplexity, plus Ecosia, Pleias and ProRata. Enterprise covers Wikivoyage datasets [verified]. | Wikidata structured data is **CC0**. Wikivoyage text is **CC BY-SA 4.0**, so attribution and share-alike apply to derivative text [verified]. An Enterprise contract does not override the open licence [claimed]. | Good backbone for landmarks and practicalities. Listings are often stale. |
| **National and regional tourism open data** | **DATAtourisme (France):** a national platform of geolocated POIs **and events**. It uses **Licence Ouverte 2.0**, is free, has an API with a key, and syncs ~daily [verified]. **ATDW (Australia):** a distributor API. Access requires signing a Distribution Licence Agreement (updated 24 Jun 2024). **Cached data must be refreshed at least twice a week**, and tracking must be in place within 30 days. Pricing is on request [verified]. **Tokyo:** the Metropolitan Government API catalogue serves ward-level tourist-spot datasets in the national "recommended dataset" format [verified]. **JNTO has no attractions API** [verified absence]. Open Data Hub South Tyrol [bg]. | Fed by tourism boards | Free (DATAtourisme, Tokyo). Licensed (ATDW). | Open licences in FR and JP. ATDW is contractual, with refresh duties. | **Underused.** Authoritative hours and seasons for attractions, plus events (DATAtourisme). |

### 2.2 Editorial and "taste" sources

| Source | Access | AI licensing status | Note |
|---|---|---|---|
| **Michelin Guide** | **No public restaurant API**. developer.michelin.com covers tyres and mobility. Data is reached by scrapers (Apify etc.) [claimed]. | **No AI licensing deal with Google, OpenAI or Perplexity found** in a 2026 re-check [verified absence]. Michelin has an international content and licensing partnership with **Tripadvisor/TheFork** [verified, Michelin page; date unconfirmed]. In Oct 2026 Michelin denied that AI wrote its Dallas descriptions (D Magazine) [verified]. A Kaggle copy is CC BY-NC. | A licensing gap. Mindtrip reviewers saw Michelin data appear in its product [claimed]. A citation study says Perplexity leans heavily on Michelin and 50 Best, and that **Eater has overtaken Michelin** as the top US fine-dining source in AI answers [claimed]. |
| **Eater (Vox Media), Condé Nast Traveler, Travel + Leisure / Food & Wine (Dotdash Meredith)** | Websites | **OpenAI deals:** Dotdash Meredith (May 2024; reportedly ≥$16M/yr; Food & Wine among the brands), Vox Media, which owns Eater (May 2024), and Condé Nast (Aug 2024; Traveler not named specifically) [verified]. Perplexity runs a separate ad revenue-share **Publishers Program** (Jul 2024). Condé Nast sent Perplexity a cease-and-desist [verified]. | ChatGPT has licensed access to this editorial layer. A startup would have to negotiate. |
| **Atlas Obscura** | ~33k "odd places" [claimed] | Listed in a Dec 2024 ProRata.ai revenue-share deal [claimed]. Staff and readers pushed back on its AI plans. First annual profit in 2025 [claimed]. | A good "non-cliché" corpus. Revenue-share licensing is feasible. |
| **Lonely Planet (Red Ventures), Time Out Group, The Infatuation (JPMorgan Chase)** | Websites | **No AI licensing deal found for any of the three** in 2026 deal trackers, which count 100+ publisher–AI deals by mid-2026 [verified absence]. Time Out's 2025–26 deal news is franchising, e.g. Time Out Market Delhi [verified]. Note that "Time" (the magazine) does have an OpenAI deal (Jun 2024); do not confuse the two. | **Unclaimed by AI labs.** These are open to licensing negotiation. |
| **Yelp, Tripadvisor (as AI licensors)** | APIs | **Yelp → OpenAI** (Jul 2026, see §2.1). **Tripadvisor → Perplexity** (Jan 2025): reviews, AI summaries and Viator experiences power Perplexity's hotel and travel answers, as Perplexity's first travel partnership, with a three-year collaboration [verified]. | The UGC review layer is being locked up through lab-level deals. |
| **Beli, Corner, Mapstr** | Consumer apps. **No public data APIs** found [verified absence]. Beli: 120M+ ratings, 2M venues, 50k+ cities (Aug 2026) [claimed]. Mapstr imports from Google, Foursquare, Apple, CSV and KML. Its 2016 API plan never appeared [verified]. Corner turns TikTok and IG links into map pins [claimed]. | **Beli's integrations are inbound:** Resy reservations in-app, Grubhub ordering (Jun 2026) and OpenTable earlier [verified]. The Beli CEO talks of a diner-preference database and a planned restaurant "Insight Suite" [claimed]. **No outbound data-licensing deal found.** | They hold the richest *taste-graph* signals (ranked lists, saved places among friends), and those are walled. Beli is a possible future data seller [inferred]. |
| **Fever** | Event and experience inventory | **Developer portal** (developer.feverup.com). The **Experience Distribution Platform** offers catalogue API access with real-time availability and wholesale pricing for resellers. The **Affiliate Program** is free to join; commission varies (8% per one network listing); larger partners get feeds or custom APIs [verified, vendor pages]. | **An accessible, licensed experiences and events feed.** Strong for city experiences. |

### 2.3 Reservations and availability

- **OpenTable:** a partner-gated API (Online Booking API, Voice AI API) behind certification. It has discovery and booking ties with OpenAI, Perplexity, Alexa+ and Google [claimed]. Its ToS bans bots and gen-AI assistants unless authorised [claimed].
- **Resy:** said in Sep 2026 that it does *not* allow unapproved third-party agents. A ChatGPT integration was reported in Aug 2026 [claimed].
- **Tock:** its API FAQ (Jul 2026) says the API cannot create reservations or read unbooked availability [claimed].
- Across all three, none offers a self-serve public write API [claimed]. Availability, which is the strongest freshness signal for a restaurant, is gated by partnerships.

### 2.4 Events and busyness

- **PredictHQ:** 19 categories, including unscheduled events (severe weather, airport delays, disasters). Search by radius or IATA code [verified]. It is built for demand forecasting, so it is good for "what's on and what's disrupting".
  - **Access:** a 14-day full trial with no card, then a **free-forever plan** limited to 2 locations within a 2-mile radius [verified]. A "Starter" plan sells city access [verified mention].
  - **Price:** third-party listings say Basic is ~$500/user/yr, customised by category and city coverage [claimed]. No startup programme was found.
- **Ticketmaster Discovery API:**
  - **Rate limit:** 5,000 calls/day by default. Higher limits are granted case by case after a compliance and branding review [verified].
  - **Terms (last updated 27 Jun 2023):** Ticketmaster may **throttle or block calls not primarily driven by direct user actions**, which is relevant for autonomous agents. The terms also bar selling, sublicensing or otherwise monetising the API [verified].
- **Eventbrite:** public event search was shut down on 12 Dec 2019. The API now serves only your own events, or events by ID or venue [verified].
- **Songkick:** API access only under a partnership and licence fee. Reportedly no keys for general developers [claimed]. JamBase sells concert data as an alternative [claimed].
- **DICE:** a partner-only GraphQL API covering events, tickets and orders [claimed].
- **Resident Advisor:** no API information found [unverified].
- **Fever:** a catalogue API plus affiliate access (§2.2) [verified]. This is the most open of the experience and event inventories.
- **Tourism-board feeds:** DATAtourisme publishes events under an open licence [verified]. ATDW has events under a distributor licence [verified].
- So hyperlocal events (gallery openings, markets, neighbourhood festivals) live in newsletters, Instagram and tourism-board feeds. **This is still unserved outside France-style national feeds.**

### 2.5 Entry rules, accessibility and safety data *(new in gap-fill)*

| Domain | Source | Access and licensing | Notes |
|---|---|---|---|
| **Entry and visa rules** | **IATA Timatic** (Web, API, AutoCheck) | **No published startup pricing or programme found.** The API targets large airlines and OTAs. AutoCheck verifies documents for the whole journey [verified absence of pricing; product verified]. | The industry gold standard, but enterprise-gated. |
| | **Sherpa°** | One API call returns visa, passport, transit, country restrictions and vaccination requirements. A Trips endpoint takes origin, destination and date. Also offers widgets and a white-label WebApp. **Revenue share on eVisa sales**, with enterprise pricing [verified, vendor]. | **The most startup-accessible requirements API** found. It also monetises through eVisa ancillaries. |
| | **VisaHQ** | A developer programme with a "travel API", widgets and an affiliate commission on every visa application. Developer sign-up is free [verified, vendor]. Endpoint detail was not found. | An affiliate-style option. |
| | eVisas.io; Smartvel; EntryDocs | eVisas.io has a partner API in early access, for approved B2B partners only [claimed]. Smartvel and EntryDocs are requirements-content vendors [claimed]. | |
| | **iVisa** | No partner API found [unverified]. | |
| **Accessibility** | **Google Places `accessibilityOptions`** | Four nullable booleans: entrance, parking, restroom and seating. Google caching terms apply [verified]. | Broad but shallow. |
| | **accessibility.cloud / Wheelmap** (Sozialhelden e.V., non-profit) | A JSON API with a free token and the **a11yJSON** exchange standard. It aggregates partner sources: ~1.3M places from 79 organisations plus 3.8k real-time elevator statuses (presentation figure, date uncertain). Copyrighted sources (e.g. HERE) are harmonised but not redistributed. The Wheelmap REST API runs on OSM data [verified]. | **The best open, structured accessibility layer**, with a licence that varies by source. |
| | **AccessNow** | Built on Google Maps Platform. ~2M places in 100 countries (Google case study). Runs the paid **"AccessNow Verified"** business programme. **No public API or licensing terms found** [verified/absence]. | A partnership candidate. |
| | **Euan's Guide** (UK charity) | Crowd reviews written by disabled people. **No API found** [unverified]. | Deep UK review text. Would need a licence. |
| **Safety** | **US State Dept advisories** | A Consular Affairs API (`cadataapi.state.gov`, TravelAdvisories) with no authentication, per a third-party API listing [claimed]. Data.gov datasets exist [verified]. Level 1–2 advisories are reviewed at least every 12 months, Level 3–4 at least every 6 months [claimed]. | Country level only. US government work is generally public domain [bg]. |
| | **GeoSure** | Neighbourhood-level safety scores (tens of thousands of neighbourhoods, 400k+ locations), including LGBTQ+ and women's sub-scores. Delivered as API-as-a-service. Used by **TripIt** (Neighborhood Safety Scores) and Deem/Travelport [claimed, vendor/partner]. Proprietary; no public pricing. | **The only neighbourhood-level safety source found.** |
| | **Safeture** | A B2B duty-of-care platform with a JSON REST API (2019 sheet). Partners include Riskline, International SOS, BCD, Amadeus Cytric (2-yr deal), Perk/TravelPerk and Aries Risk (Jul 2026) [verified]. | Corporate travel; not consumer-priced. |

---

## 3. Hyperlocal and "insider" knowledge sources

| Source | What it holds | Legal access (2026) | Depth |
|---|---|---|---|
| **Reddit** | The best corpus for candid "skip X, go to Y instead" advice, tourist-trap warnings, safety-by-neighbourhood, and time-of-day tips | Google pays ~$60M/yr (Feb 2024 deal), which is under contentious renewal; in Jul 2026 the WSJ reported Reddit considered restricting Google's AI access and wants usage-based pricing [claimed]. OpenAI has had real-time Data API access since May 2024 [verified]. **Free API and RSS reportedly end by March 2027** [claimed]. The commercial API needs approval; paid tiers have run at ~$0.24 per 1k calls since 2023 [bg]. Reddit sued Anthropic (2025) and Perplexity and scrapers (2025) [bg]. | Street- and dish-level detail, but noisy and quickly stale. **Effectively licensed only to the large LLM labs.** |
| **TikTok** | Visual "hidden gem" content, very current | The **Research API** FAQ states that creators, advertisers and **commercial users are not eligible** [verified]. The **Commercial Content API** is an *ad-transparency* library covering EU/EEA ads, not organic posts [verified]. The Display API covers only the user's own content [bg]. | High recency, low reliability. The Kuak Skyride case shows synthetic-video risk. **No licit commercial ingestion path.** |
| **Instagram** | Venue and creator posts | Graph API access covers only accounts that authorise you; oEmbed for display [bg]. **Hashtag Search** needs App Review plus the *Instagram Public Content Access* feature and is capped at **30 unique hashtags per rolling 7 days** [verified]. Meta's Automated Data Collection Terms bar scraping without written permission [claimed]. | Same as TikTok |
| **YouTube** | Long-form walking tours and guides | The Data API allows search and metadata.<br>**Retention [verified]:**<br>• Don't store data indefinitely.<br>• Delete within 30 days when a user asks or authorisation can't be verified.<br>• Non-statistic data (titles, descriptions, comments) follows the 30-day refresh-or-delete rule.<br>• Approved clients may keep statistics (views, likes, subscribers) for up to **36 months** under the derived-metrics amendment.<br>Transcripts are not an official API surface [bg]. | Good for neighbourhood "feel". **A persistent RAG index of YouTube metadata is not allowed** [inferred]. |
| **Google Local Guides / Maps reviews** | Huge UGC base | Only via the Places API, **max 5 reviews** per place [bg], plus Gemini-generated review and area summaries [bg]. Caching restrictions apply. | Broad and shallow |
| **Local-guide marketplaces** (Withlocals, ToursByLocals, Showaround) | Human locals with neighbourhood expertise | **Withlocals:** an in-house and Awin affiliate programme (~10% commission, 30-day cookie), with **an API and XML data feed for selected partners** [verified, network listing]. ToursByLocals and Showaround: no API or affiliate details found [unverified]. | Deep but not machine-readable. **A partnership opportunity.** Withlocals is the most integrable. |
| **Creator and advisor platforms** (Thatch, Fora, Matador/GuideGeek) | Creator-curated guides and advisor knowledge | Their own platforms. Matador's GuideGeek runs over its own content and creators [bg]. | Authentic and attributable. Small coverage. |
| **Local blogs and newsletters** | City- and neighbourhood-level picks and events | Copyright applies. Licensing is negotiable and long-tail. | Deepest hyperlocal layer, also the least structured. **AI-generated "local" blogs** (the Tasmania case) now pollute it. |

**How current planners get "local" knowledge [inferred, from partner lists and reviews]:**
- **Mindtrip** combines an OpenAI-based model with a proprietary DB of 11M+ POIs. Its stated data partners are Google Places/Maps, Tripadvisor, OpenTable, Viator and Priceline, with Sabre, PayPal, Expedia and Booking for transactions [claimed]. Reviewers saw few hallucinations, and it declines far-future flight queries rather than guessing [claimed]. Its "local" layer is therefore *aggregated reviews*, not insider knowledge.
- **Layla** (reportedly acquired by Expedia in Jul 2026 [claimed]) uses Booking.com and Skyscanner for live prices plus GetYourGuide and Viator. Its accuracy is attributed to live web search; the model is undisclosed [claimed].
- **ChatGPT, Gemini and Perplexity** draw on pretraining plus web search. Their licensed sources:
  - **OpenAI:** Vox (Eater), Condé Nast and Dotdash Meredith (T+L, Food & Wine) [verified]; Reddit; **Yelp reviews and business data (Jul 2026)** [verified].
  - **Perplexity:** **Tripadvisor and Viator** (Jan 2025) and Wikimedia Enterprise (Jan 2026) [verified].
  - **Google:** Reddit, plus its first-party Maps graph for Gemini.
- **No product we found** has a licensed, attributed, *recency-stamped* corpus of local insider knowledge.

Depth today [inferred]:
- **Neighbourhood-level:** partially served.
- **Street-level and dish-level:** unserved except by accident through Reddit in pretraining.
- **Time-of-day and seasonal nuance:** largely unserved (BestTime is the exception).
- **Etiquette:** generic.
- **Safety:** country-level advisories in consumer planners. Neighbourhood scores exist B2B (GeoSure, used by TripIt) [claimed].
- **Accessibility:** Google boolean fields, OSM `wheelchair` tags and accessibility.cloud aggregation. Shallow; no verified step-by-step detail.

---

## 4. Transit and routing data

| Source | Coverage | Freshness | Access | Notes |
|---|---|---|---|---|
| **Mobility Database** (MobilityData) | **6,000+ GTFS, GTFS-RT and GBFS feeds in 100+ countries** (as of Oct 2026) [verified]. A third-party count gives ~4,500 schedule and ~1,900 RT feeds across ~70 countries [claimed]. One agency's RT can count as 3 feeds. | Operator-published | Free | The canonical open catalogue. TransitFeeds has shut down [claimed]. |
| **Transitland** | Thousands of GTFS, GTFS-RT, GBFS and MDS feeds [verified]. "55+ countries" is likely dated. | Fetched continuously | Free API tier plus paid [bg] | Good for a feed registry and history. |
| **Google Routes API** | Compute Routes and Route Matrix replaced the legacy Directions and Distance Matrix APIs (Legacy since Mar 2025) [verified]. Transit matrix capped at 10×10 [claimed]. **Japan:** the legacy Directions and Distance Matrix APIs return `ZERO_RESULTS` for transit in Japan while other modes work, per developer forum reports and a tutorial [claimed, consistent]. Routes API (New) transit coverage for Japan and China is still unconfirmed [bg, verify]. | Google's merged feeds plus realtime | Pay per SKU, or a $100/mo Starter plan [verified] | The best global single call outside Japan. Same caching restrictions as Places. |
| **NAVITIME** (Japan) | Japan car, train, bus and bicycle routing; business APIs and SDKs [verified] | **The Rakuten RapidAPI "Route (totalnavi)" tier uses NAVITIME-estimated train times, not real timetables.** Timetable and bus data need a direct contract [verified]. | Self-serve via RapidAPI; enterprise contract for timetables | **The fallback for Japanese transit.** Jorudan not checked. |
| **Open routing stacks** (OpenTripPlanner, MOTIS/Transitous, Navitia) | As good as the GTFS you load [bg]. **Transitous:** 1,800+ static datasets from 55 countries (Jun 2025) [verified, dated]. | Your pipeline | Open source. **Transitous** offers a free MOTIS 2 API (api.transitous.org), volunteer-run and best-effort, with a usage policy [verified]. **Navitia** (Hove, a Keolis subsidiary) is AGPL-3.0 and still active in 2026. Hosted api.navitia.io has a free key and paid tiers of ~$49–199/mo [claimed]. | Can be self-hosted and cached. Do not build production on Transitous's public endpoint. Self-host MOTIS instead [inferred]. |
| **Citymapper** (Via-owned since 2023) | ~100 cities [bg] | Strong | **Self-serve developer products discontinued 23 Jun 2023** [claimed]. A partner-key "Citymapper API" (v1.8.3) is still documented, and its APIs and SDKs were folded into Via's platform for agencies and cities [verified]. | Quality benchmark. Partner-only. |
| **Moovit** (Mobileye) | 7,500+ transit agencies and operators [claimed, Mobileye IR] | Mixed: agency data plus crowdsourcing | **No self-serve.** Transit API suite (trip planning, stops, real-time, alerts, GTFS-RT); pricing negotiated per customer [claimed]. A single Apr 2026 report says Mobileye put Moovit up for sale at $300–400M [claimed]. | Strongest for developing-market urban transit. **Ownership risk.** |
| **Rome2Rio** (Omio since 2019) | Global multimodal *estimates* [verified acquisition] | Heuristic: frequencies and durations, often stale [bg] | **No public developer sign-up in 2026** [verified absence]. Omio B2B offers API and white-label access to 3,000+ operators (train, bus, flight, ferry) through private partnerships [verified, vendor]. | Good for coarse "is there a bus?" answers, not schedules. Bookable inventory goes through Omio B2B. |
| **12Go (Travelier group, which includes Bookaway)** | ~4,000 operators, ~50k routes, 26 Asian countries; also claims 30k+ operators worldwide [claimed] | Direct operator integrations | Affiliate (80+ countries), deep links, white label and OTA-grade API [claimed]. AirAsia super-app partner [verified]. | **The key source for buses, ferries and minivans in SE Asia.** |
| **Busbud, Distribusion** | Intercity bus (global), B2B rail, bus and ferry [bg] | Inventory feeds | Partner APIs [bg] | Bookable ground transport that complements GTFS. |
| **Ferryhopper** | **130+ ferry operators, 30+ countries** [claimed, vendor] | Live itineraries and prices | **FerryhAPI** B2B API; affiliate programme (30-day cookie); **an MCP server for AI agents** with real-time itineraries, indicative prices and booking deep links; a widget with an API key [verified, vendor] | **The most agent-ready ferry source.** |
| **Direct Ferries** | Global ferry aggregator. 2,000+ routes reached via the Omio partnership [verified] | Live fares via the booking API | **Direct Ferries Connect:** booking API, widget, affiliate links and agent portal. Claims 4,500+ agencies and sites. Bookaway integrates via API [verified, vendor]. | Fills small-ferry gaps that GTFS misses. |
| **Walking, terrain and steps** | OSM (`highway=steps`, `incline`, `surface`, `sac_scale`) plus elevation DEMs [bg] | Community | Free | Routers ignore stairs, heat and hills for tourists, which is a gap. |

**Transit gaps [inferred]:**
- **Cable cars, ropeways, funiculars, small island ferries, park shuttles and seasonal services** are rarely in GTFS. This is exactly the Mount Misen failure.
  - The *schema* is not the problem. GTFS has `route_type` 5 (cable tram), 6 (aerial lift) and 7 (funicular), plus extended types 1300–1302 and 1400 [verified].
  - Some feeds already use them, e.g. the Roosevelt Island Tramway, Montjuïc and a Mountain Village gondola [verified].
  - The gap is *coverage*: tourist ropeways run by private or attraction operators rarely publish feeds [inferred].
- **Last-departure risk.** No planner warns that a leg is the final service of the day.
- **Intercity schedules in Africa, South Asia and Latin America** exist only in booking inventories (12Go, Busbud, Bookaway) or not online at all.

---

## 5. Technical state of the art: grounding and verification

### 5.1 What exists

1. **Tool-grounded generation.**
   - Gemini plus Maps grounding: the model calls the Maps tool and returns cited sources and a widget [verified].
   - Foursquare "Ask" endpoints and the Yelp AI API move the LLM step to the data owner [claimed/verified].
   - **Trend [inferred]:** POI owners now sell *premium "AI" SKUs* ($14–36 per 1k) and forbid ingesting their raw API output into third-party LLMs. Raw data plus your own LLM is becoming legally harder than buying their grounded answer.
2. **Existence and closure scoring.**
   - Overture's per-place confidence, uncalibrated across sources [verified].
   - Foursquare's agent-based ingestion verification [claimed].
   - VOYGR's validate API, with existence_confidence. PlaceCall phone verification costs ~$0.10 per successful call, and an hours-enrichment field is now documented [claimed].
   - Google Duplex calling for hours, plus "hours may have changed" flags [verified, older].
   - **Google "Call for Me"** in the Gemini app (announced 24 Sep 2026; first for US Pixel 11 Gemini subscribers) calls businesses for hours and bookings on a *consumer's* behalf [claimed, secondary]. Google Business Profile still places automated hours-check calls, which businesses can opt out of [claimed].
   - No other dedicated "hours-verification by phone" API was found in 2026 beyond VOYGR PlaceCall. General voice-agent platforms (Synthflow, Trillet and others) could be used to build one [verified absence, 1 search].
3. **Entity resolution.** Overture GERS IDs provide a stable cross-source join key [verified]. Google place_id may be stored [verified]. Yelp business IDs may be kept for matching [claimed]. Apple offers alternate Place-ID lookup [verified]. An open OSM↔Foursquare category crosswalk was published (Scientific Data, 2026) [claimed].
4. **Constraint verification of plans.** Research: LLM-Modulo and SMT/formal-solver planners on TravelPlanner beat pure LLMs by orders of magnitude [bg]. Production: **no consumer planner publicly documents a deterministic feasibility validator** [inferred from absence]. The MonkeyEatingMango 43% fault rate suggests none ships one at scale.
5. **Provenance shown to users.**
   - Gemini Maps grounding must display Google Maps attribution [verified].
   - Tripadvisor requires an "AI-generated, may contain mistakes" label [verified].
   - Mindtrip and Layla show place cards with photos and ratings, but **no "last verified" timestamp or confidence** [inferred from reviews].
6. **Human and local verification networks.** Google Local Guides (UGC). Duplex and VOYGR PlaceCall (automated calls). Kimkim, Fora and similar advisors (human review of AI drafts) [claimed via Kimkim survey]. None is exposed as a guarantee to the traveller.

### 5.2 How the leaders ground (claims vs reality)

| Product | Claim | Observed reality |
|---|---|---|
| Google (Gemini, AI Mode, Ask Maps) | Grounded in 250M+ Maps places | Strongest live status, but ~27% of closures can lag (vendor test) [claimed]. Ask Maps launched in 2026; Gemini moderates Maps edits [claimed]. |
| Mindtrip | 11M+ POI DB plus Google, Tripadvisor and OpenTable partners | Reviewers report few hallucinations, but it is generic (Afar: it struggled with compound constraints) [claimed]. |
| Layla | Live prices from Booking and Skyscanner | Accuracy relies on live search. Earlier fabrications on record [claimed/bg]. |
| ChatGPT | Web search plus publisher deals, and **Yelp local data since Jul 2026** [verified] | Closed and invented restaurants documented (Fast Company, WaPo), mostly before the Yelp deal [claimed]. |
| Perplexity | Web search plus Tripadvisor/Viator (Jan 2025) and Wikimedia Enterprise [verified] | Citation patterns anchored on Michelin and 50 Best lists [claimed]. |

---

## 6. Recommended data-stack architecture

The design is shaped by the licensing constraints in §2, not only by technology.

```
                ┌──────────────────────────────────────────────────────────┐
 L0 Canonical   │ Own Place Graph keyed by Overture GERS ID                │
 spine (owned,  │  ← Overture Places (CDLA-P) + FSQ OS Places (Apache 2.0) │
 storable)      │  ← Wikidata (CC0) + national tourism open data           │
                │  ← OSM (ODbL; kept in a separate ODbL "produced work"    │
                │     layer for trails/steps/accessibility)                │
                │  Store external IDs only: google place_id, yelp id, apple│
                └──────────────────────────────────────────────────────────┘
 L1 Live        Query-time, display-only, never cached (except IDs):
 enrichment     Google Places (status, hours, currentOpeningHours,
                accessibilityOptions) · Foursquare Premium (hours/tips;
                check FSQ AI Terms) · Yelp AI API (where allowed)
                · BestTime (busyness) · OpenTable partner API (availability)
                · VOYGR validate/enrich (US) · Fever catalogue API
                (experiences availability)
                Mapbox/HERE/TomTom: geocoding & routing only — not a
                storable POI source
 L2 Liveness    Freshness ledger per place: {field, value, source, observed_at,
 & confidence   method: api|crowd|call|editorial, confidence}
                Closure detectors: VOYGR-style validation, review-velocity drop,
                multi-source disagreement, own voice-agent calls for booked/
                critical stops (24-48h pre-visit reconfirm)
 L3 Licensed    Revenue-share licensed editorial + creator + local-guide corpus
 knowledge      (Atlas Obscura-style ProRata model; newsletters; guides; own
                local-expert network; unclaimed publishers: Lonely Planet,
                Time Out, Infatuation, Michelin; Withlocals feed) — chunked,
                place-linked by GERS, dated, attributed; synthetic-content
                filter. Wikivoyage (CC BY-SA 4.0) kept share-alike-separate.
                NOT: TikTok/IG/YouTube content (no commercial ingest path)
 L4 Ops data    GTFS/GTFS-RT via Mobility Database → self-hosted OTP/MOTIS;
                Google Routes fallback (not Japan transit → NAVITIME);
                12Go/Busbud/Distribusion/Ferryhopper (MCP)/Direct Ferries
                inventories; hand-curated "special services" table (ropeways,
                funiculars, park shuttles, seasonal ferries, last-entry times)
                — emitted as GTFS route_type 6/7 so routers consume it
                PredictHQ (free tier to start) + Ticketmaster (user-driven
                calls only) + Fever + DATAtourisme/ATDW events;
                weather/daylight
 L4b Trip       Entry rules: Sherpa° API (rev-share) → Timatic later;
 rules          safety: State Dept advisories + GeoSure (neighbourhood);
                accessibility: accessibility.cloud + Google booleans + OSM
 L5 Planner     LLM proposes → deterministic validator (hours × day-of-week ×
                last entry × travel time × buffers × holidays × daylight) →
                repair loop → every claim carries source + last-verified stamp
 L6 In-trip     Push alerts on status change; one-tap "it was closed" reports
 loop           feed L2; accountability log (what we said, when, from where)
```

**Key design choices:**
- **[inferred]** Do not build the knowledge base on Google content. Its ToS forbids caching and model training. Use Google only as a real-time verifier and display layer, and keep the spine open-licensed.
- **[inferred]** Choose the LLM vendor separately from the data vendor. Gemini Maps grounding is cheap at $14 per 1k but locks you to one model. Keep it as one tool among several.
- **[inferred]** The commercial map vendors (Mapbox, HERE, TomTom) do **not** solve the storage problem for POIs. Mapbox allows permanent storage only for non-POI geocodes, and HERE and TomTom restrict derivative databases. So the open spine (Overture, FSQ OS, OSM, Wikidata, tourism open data) is the only storable base unless you buy SafeGraph.
- **[inferred]** UGC review layers are being licensed to the labs: Yelp to OpenAI, Tripadvisor to Perplexity, Reddit to Google and OpenAI. A startup should not plan to differentiate on aggregated reviews. Differentiate on freshness, feasibility and owned local knowledge instead.
- **[inferred]** Treat confidence as a *product feature*. Show "Hours confirmed by phone 2 days ago" or "Last verified 9 months ago, check before going." Nobody does this today.

---

## 7. Knowledge-dimension coverage matrix

Legend: ● well served · ◐ partially served · ○ unserved / walled

| Dimension | Best available source | Served? | Notes |
|---|---|---|---|
| Place existence (major venues) | Google, Overture, FSQ | ● | Long tail and closures lag (~27% missed) |
| Regular opening hours | Google, FSQ Premium | ◐ | OSM ~45–77%. Holiday and seasonal exceptions are weak. |
| Attraction ops (last entry, timed tickets, ropeway/ferry last run) | Tourism boards, operator sites | ○ | The root cause of the Mount Misen-type failures |
| Day-of-week closures (e.g. Monday museums) | Google hours | ◐ | 53% of closed-day errors fall on Mondays: data exists, planners ignore it |
| Price level / menu prices | Google price_level, Yelp | ◐ | Coarse $–$$$$ only |
| Reservation availability | OpenTable partner, Resy/Tock closed | ○/◐ | Partner-gated |
| Busyness by hour / queues | BestTime; Google Popular Times (no API) | ◐ | Queue times unserved |
| Urban transit schedules | GTFS (6k+ feeds), Google Routes | ● | Developed markets |
| Urban transit, Japan | NAVITIME (contract), Google app (not API) | ◐ | Google API transit returns ZERO_RESULTS in Japan (legacy); NAVITIME RapidAPI tier uses estimated times |
| Intercity bus/ferry, developing regions | 12Go, Busbud, Bookaway; Ferryhopper, Direct Ferries for ferries | ◐ | Africa and South Asia thin. Ferries are better served than buses (Ferryhopper offers an MCP server). |
| Special transport (cable cars, funiculars, seasonal) | — | ○ | GTFS *supports* route_type 6/7, but tourist operators rarely publish feeds |
| Walking terrain, stairs, heat | OSM plus DEM | ◐ | Not used by consumer routers |
| Accessibility (step-free, toilets) | Google booleans, OSM/Wheelmap, accessibility.cloud, AccessNow (no API) | ◐ | Shallow; no verified detail |
| Events (major) | PredictHQ (free tier), Ticketmaster (user-driven only), Fever API | ● | Ticketmaster may throttle agent-driven calls |
| Events (hyperlocal: markets, openings) | Instagram, newsletters; DATAtourisme in France | ○ | No machine-readable feed outside national open-data platforms |
| Insider "skip X, do Y", tourist-trap detection | Reddit (licensed only to big labs) | ○ | Strategic gap |
| Aggregated reviews and ratings | Yelp (licensed to OpenAI), Tripadvisor (licensed to Perplexity), Google (5 reviews via API) | ◐ | Served for the labs; gated for startups |
| Dish-level / what to order | Reddit, Beli, Infatuation | ○ | Walled. Beli has 120M+ ratings and no outbound API. |
| Neighbourhood vibe / who it's for | Editorial, YouTube | ◐ | Licensing needed |
| Time-of-day and seasonal nuance (light, bloom, crowds) | Scattered | ○ | |
| Cultural etiquette, dress codes, cash-only | Wikivoyage, generic LLM | ◐ | Not venue-specific |
| Safety by neighbourhood and time | Gov advisories (country level); GeoSure (neighbourhood, B2B) | ○/◐ | Neighbourhood scores exist B2B (TripIt uses GeoSure). Time-of-day is unserved. |
| Entry and visa rules | Sherpa° API (rev-share), VisaHQ API, Timatic (enterprise) | ◐ | Frequent hallucination class. **Startup-accessible APIs exist (Sherpa°)**, so planners that hallucinate here are choosing not to ground. |
| Provenance / last-verified display | — | ○ | Nobody ships it |

---

## 8. Top gaps and exploitable opportunities

1. **A shipped freshness and confidence layer.** Every planner treats place facts as binary truth. Build a per-field freshness ledger, as in §6 L2, and show "last verified" and confidence to users. Re-confirm booked or critical stops 24–48h ahead with a voice agent; VOYGR's PlaceCall (~$0.10 per call) and Google Duplex prove the approach works. Google's consumer "Call for Me" (Sep 2026) shows the pattern is going mainstream. VOYGR now documents hours enrichment, but it is US-first, so **non-US hours verification is the white space** [inferred]. This directly answers problem #4, accountability.
2. **A deterministic feasibility validator.** 43% of AI-planned days contain a verifiable fault, and most are hours, sequencing or duplicates. These are mechanically checkable once you have hours, day-of-week closures, last entry, travel times, buffers and holidays. Research shows solver-in-the-loop planning beats pure LLMs by large margins, yet no consumer product documents one. This is cheap to build and directly measurable ("0 infeasible days").
3. **An operational long tail of attractions and special transport.** Cable cars, ropeways, funiculars, park shuttles, seasonal ferries, last-entry and timed-ticket sellouts, and seasonal hut and trail closures. None of it sits in GTFS or the POI APIs. A curated, crowd-maintained "special services" dataset fed by tourism-board open data and operator sites would be a proprietary moat. Publish it internally as GTFS `route_type` 6/7 so standard routers consume it. ATDW-style licences require refreshing cached data at least twice a week, which sets a useful benchmark for the refresh cadence.
4. **A licensed, attributed hyperlocal corpus.** Reddit is licensed to Google and OpenAI and its free API ends in 2027. Yelp is licensed to OpenAI and Tripadvisor to Perplexity. TikTok's research API excludes commercial users, IG hashtag search is capped at 30 per week, and YouTube data must be refreshed or deleted every 30 days. Michelin has no API. **Lonely Planet, Time Out and Infatuation have no AI deals found** (re-verified Nov 2026), so they are licensable. Opportunity: revenue-share licensing in the ProRata/Atlas Obscura style with local newsletters, guidebook publishers and local-guide marketplaces, plus an owned local-expert network paid per verified tip. Each tip is GERS-linked, dated and attributed, and screened for AI-generated content. This answers problem #1, cliché recommendations, with *rights*, not scraping.
5. **Ground transport in developing regions, plus last-service risk.** Combine GTFS with 12Go, Busbud and Distribusion inventories and flag "this is the last departure; miss it and you're stuck". Add terrain and accessibility-aware walking times from OSM steps and inclines plus heat. No incumbent planner does this.

Smaller opportunities:
- Busyness-aware sequencing using BestTime.
- A hyperlocal events feed built from newsletters and tourism-board data.
- An in-trip loop where a "closed" report updates everyone, giving a Waze-style network effect on place truth.

---

## Sources

- OECD.AI incident, Humantay: https://oecd.ai/en/incidents/2025-09-29-8b4f
- AI Incident Database, Humantay: https://incidentdatabase.ai/entities/tourists-seeking-the-supposed-sacred-canyon-of-humantay/
- AI Incident Database, Malaysia cable car: https://incidentdatabase.ai/cite/1634
- CO/AI coverage: https://getcoai.com/news/ai-travel-tools-send-tourists-to-fake-dangerous-destinations
- Skeptical take: https://fialka.substack.com/p/ai-didnt-ruin-your-trip-you-did
- Futurism: https://futurism.com/artificial-intelligence/ai-hallucination-landmarks-tourists
- SCMP, Malaysia couple: https://www.scmp.com/news/people-culture/article/3317337/malaysia-couple-travel-hours-tour-site-after-watching-ai-created-video-unaware-its-unreal
- NST: https://www.nst.com.my/amp/news/nst-viral/2025/07/1238897/nstviral-elderly-couple-duped-ai-generated-cable-car-video
- PetaPixel: https://petapixel.com/2025/07/14/malaysian-couple-tricked-by-ai-video-travel-hours-to-fake-tourist-attraction
- Stacker/KEYT roundup: https://keyt.com/lifestyle/travel/stacker-travel/2026/10/03/bad-travel-advice-from-ai-from-bogus-bars-to-visa-fails/
- Greetwell AI Travel Report 2026: https://www.greetwell.com/us/research/ai-travel-survey-2026
- Greetwell syndication: https://krdo.com/stacker-travel/2026/09/15/survey-ai-hallucinated-travel-destinations-for-1-in-6-users/
- MonkeyEatingMango 356-trip study: https://monkeyeatingmango.com/research/ai-itinerary-errors-data-study/
- Forbes, AI travel accuracy: https://www.forbes.com/sites/garystoller/2026/03/23/how-accurate-is-ai-for-planning-travel-and-vacations/
- Kimkim survey: https://recommend.com/travel-interests/kimkim-survey-finds-ai-drafted-itineraries-reshaping-bookings
- Afar app test: https://www.afar.com/magazine/we-tested-ai-travel-planning-apps-here-are-the-3-that-actually-worked
- Layla blog comparison: https://layla.ai/blog/news-and-tips/best-ai-for-luxury-travel-planning
- Travel Anywhere tests: https://www.travelanywhere.blog/blog/chatgpt-vs-gemini-vs-claude-trip-planning-2026-tested-comparison
- Google Maps Platform ToS: https://cloud.google.com/maps-platform/terms
- GMP Service Specific Terms: https://cloud.google.com/maps-platform/terms/maps-service-terms
- GMP EEA terms: https://cloud.google.com/terms/maps-platform/eea
- GMP Analytics SSTs: https://cloud.google.com/archive/terms/maps-platform/maps-analytics-service-terms-20260630
- Geocoding policies (place_id storage): https://developers.google.com/maps/documentation/geocoding/policies
- GMP March 2025 pricing changes: https://developers.google.com/maps/billing-and-pricing/march-2025
- GMP pricing: https://mapsplatform.google.com/pricing
- Places pricing (secondary): https://openplacesapi.com/blog/google-places-api-pricing
- Grounding with Google Maps launch: https://blog.google/innovation-and-ai/technology/developers-tools/grounding-google-maps-gemini-api/
- Maps grounding docs: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-maps
- Gemini API pricing: https://aistudio.google.com/docs/pricing
- Google Duplex 3M updates (2020): https://techcrunch.com/2020/10/15/duplex-googles-conversational-a-i-has-updated-3m-business-listings-since-pandemic
- Google self-updating map: https://blog.google/products-and-platforms/products/maps/how-ai-and-imagery-build-self-updating-map/
- Duplex updates: https://blog.google/innovation-and-ai/products/duplex-helpful-updates/
- VOYGR closure test: https://dev.to/voygr/is-google-maps-accurate-for-closed-businesses-we-checked-400-places-50k2
- VOYGR Launch HN: https://news.ycombinator.com/item?id=47401042
- VOYGR agent API: https://dev.to/voygr/a-place-data-api-for-ai-agents-llmstxt-mcp-and-rest-1nb
- VOYGR KYB/PlaceCall: https://dev.to/voygr/best-kyb-and-business-verification-apis-in-2026-agd
- Foursquare OS Places launch: https://foursquare.com/resources/blog/products/foursquare-open-source-places-a-new-foundational-dataset-for-the-geospatial-community/
- FSQ OS Places release notes: https://docs.foursquare.com/data-products/docs/fsq-os-places-release-notes
- Evolving FSQ OS Places: https://foursquare.com/resources/blog/data/evolving-fsq-open-source-places/
- FSQ OS Places notice: https://opensource.foursquare.com/places-notice-txt/
- Foursquare Places API: https://foursquare.com/products/places-api/
- Foursquare pricing (secondary): https://openplacesapi.com/compare/foursquare-places-api
- Foursquare free tier change: https://agentdeals.dev/vendor/foursquare
- SafeGraph vs OSM: https://www.safegraph.com/blog/comparing-safegraph-and-openstreetmap/
- Overture Places guide: https://docs.overturemaps.org/guides/places/
- Overture 2026-10-21 release: https://docs.overturemaps.org/blog/2026/10/21/release-notes/
- Overture 2026-04-15 release: https://docs.overturemaps.org/blog/2026/04/15/release-notes/
- Overture quality 2023: https://latlong.blog/2023/08/a-look-at-overtures-data-quality.html
- OSM vs Overture restaurants: https://surprisedatespot.com/blog/comparing-overture-osm-restaurants/
- OSM–Foursquare taxonomy: https://arxiv.org/pdf/2511.13369
- OSM completeness: https://www.spatialworkflow.io/osm-data-completeness-explained/
- OSM restaurant dataset: https://overspan.dev/blog/build-poi-dataset
- Apple Maps Server API docs: https://developer.apple.com/documentation/applemapsserverapi.md
- Apple Server API limits forum: https://developer.apple.com/forums/thread/834089
- Yelp API Terms: https://terms.yelp.com/developers/api_terms/20250113_en_us/
- Yelp pricing: https://business.yelp.com/data/resources/pricing/
- Yelp AI API: https://fusion.yelp.com/fusion-ai/
- Tripadvisor API master terms: https://docs.terra.tripadvisor.com/docs/api-master-terms
- Tripadvisor partner terms: https://developer-tripadvisor.com/partner/master-partnerships-terms-and-conditions/index.html
- Tripadvisor Content API to Terra (secondary): https://vorplabs.com/agent-tools/tripadvisor-content-api
- Tripadvisor API shutdown (secondary): https://stayapi.com/blog/tripadvisor-reviews-api
- Michelin data access: https://scraperly.com/scrape/michelin-guide
- Atlas Obscura: https://en.wikipedia.org/wiki/Atlas_Obscura
- AI licensing deals tracker: https://aidata.broker/figures/deals-disclosed
- OpenTable/Resy/Tock agent audit: https://ainora.lt/blog/restaurant-booking-api-for-ai-agents-2026
- Resy agent policy: https://platform.simular.ai/use-cases/restaurant-reservation-bot
- OpenTable vs Resy: https://forktime.ai/compare/opentable-vs-resy
- Restaurant APIs for agents: https://hyperleap.ai/blog/restaurant-booking-apis-ai-agents
- BestTime docs: https://documentation.besttime.app/
- BestTime pricing: https://besttime.app/subscription/pricing
- PredictHQ categories: https://docs.predicthq.com/getting-started/predicthq-data/event-categories
- PredictHQ travel: https://predicthq.com/events/travel
- Ticketmaster Discovery API: https://jentic.com/apis/ticketmaster.com/discovery-api
- Reddit–Google renewal: https://winbuzzer.com/2026/07/23/reddit-weighs-tighter-google-ai-access-in-renewal-talks-xcxwbn/
- Reddit free API ending: https://startupfortune.com/reddit-is-cutting-off-free-api-and-rss-access-while-keeping-google-and-openai-paying/
- OpenAI–Reddit deal: https://techcrunch.com/2024/05/16/openai-inks-deal-to-train-ai-on-reddit-data
- Reddit deal value forecast: https://www.tikr.com/blog/reddit-fell-6-as-its-550m-ai-deal-renewal-looms-heres-where-the-stock-could-go-in-2026
- Mindtrip partners: https://www.tourmag.com/Mindtrip-les-folles-ambitions-du-futur-super-agent-de-voyages-dope-a-l-IA_a132074.html
- Mindtrip homepage: https://mindtrip.ai/homepage
- Mindtrip review: https://aitravel.tools/mindtrip-review/
- AI planners compared: https://monkeytravel.app/blog/best-ai-trip-planners-2026-compared
- Layla data sources: https://techcrunch.com/2024/02/12/travel-startup-layla-acquires-flyr-backed-ai-itinerary-building-bot
- Layla review: https://aitravel.tools/layla-ai-review/
- Layla–Expedia: https://www.endlesstravelplans.com/guides/planning-tools/layla-ai-review
- Mobility Database: https://mobilitydatabase.org/
- Mobility DB MCP counts: https://github.com/pipeworx-io/mcp-mobility-database
- Transitland feeds: https://www.transit.land/feeds
- TransitFeeds shutdown: https://www.gtfsx.com/transitfeeds/
- Routes API launch: https://mapsplatform.google.com/resources/blog/announcing-routes-api-new-enhanced-version-directions-and-distance-matrix-apis/
- Routes API coverage: https://developers.google.com/maps/documentation/routes/coverage
- TravelTime vs Google: https://traveltime.com/compare/google-maps-api-alternative
- Rome2Rio: https://en.wikipedia.org/wiki/Rome2Rio
- 12Go about: https://12go.asia/en/about
- 12Go–AirAsia: https://www.phocuswire.com/airasia-partners-12go-ground-transportation
- 12Go affiliate: https://www.travelpayouts.com/blog/12go-asia/
- 12Go white label: https://newswav.com/article/how-12go-built-a-white-label-system-behind-travel-brands-A2602_CdVfIo

### Sources added in gap-fill pass (2026-11-17)

*Incidents*
- AIID #1635, Mount Misen: https://incidentdatabase.ai/cite/1635/
- OECD.AI, BC hikers / ChatGPT: https://oecd.ai/en/incidents/2025-05-26-63e6
- Gigazine, SAR warnings on AI hikes: https://wbgsv0a.gigazine.net/gsc_news/en/20250607-search-and-rescue-groups-warn-ai-hike
- The New Daily, Weldborough Hot Springs: https://www.thenewdaily.com.au/travel/2026/02/02/tasmania-hot-springs
- Stacker roundup (Coast Reporter syndication): https://www.coastreporter.net/bc-news/bad-travel-advice-from-ai-from-bogus-bars-to-visa-fails-12868919

*Place data and terms*
- Google Places accessibilityOptions: https://developers.google.com/maps/documentation/places/ios-sdk/reference/swift/Structs/AccessibilityOptions
- Google Places pricing 2026 (secondary): https://www.woosmap.com/blog/google-places-api-pricing
- FSQ Supplemental AI Terms: https://foursquare.com/legal/fsq-supplemental-ai-terms/
- FSQ Places API EULA: https://foursquare.com/legal/terms/apilicenseagreement
- Axios, Yelp–ChatGPT: https://axios.com/2026/07/23/yelp-reviews-chatgpt-geo-partnership
- Search Engine Land, OpenAI–Yelp: https://searchengineland.com/openai-yelp-deal-483326
- Mapbox temporary vs permanent geocoding: https://docs.mapbox.com/help/dive-deeper/understand-temporary-vs-permanent-geocoding/
- Mapbox search overview: https://docs.mapbox.com/help/getting-started/search/
- HERE platform terms 2020: https://legal.here.com/terms/here-platform/terms-2020
- HERE commercial terms v2.5: https://www.here.com/pricing/commercial-terms
- Geocoder ToS comparison (TomTom/HERE): https://www.geocod.io/geocoding-terms-of-use-comparison
- Places caching policies compared: https://openplacesapi.com/blog/can-you-store-places-api-results
- TomTom Orbis Search API: https://developer.tomtom.com/search-api/documentation/tomtom-orbis-maps/product-information/introduction
- SafeGraph places technical guide: https://safegraph.com/guides/places-data-technical-guide
- Esri ArcGIS Places (SafeGraph): https://doc.esri.com/en/arcgis-data/latest/arcgis-places/safegraph.html
- Advan data dictionaries: https://docs.advanresearch.com/
- Dewey Data (Cornell): https://johnson.library.cornell.edu/database/dewey/
- VOYGR dev tools: https://github.com/voygr-tech/dev-tools
- VOYGR CLI PR (pricing/hours): https://github.com/voygr-tech/dev-tools/pull/10
- VOYGR PlaceCall: https://voygr.tech/placecall/
- PlaceCall on Apify: https://apify.com/voygr/placecall/api
- Wikidata licensing: https://www.wikidata.org/wiki/Wikidata:Licensing
- Wikivoyage copyright: https://en.wikivoyage.org/wiki/Copyvio
- Wikimedia Enterprise AI deals: https://decrypt.co/354902/wikipedia-reveals-multiple-deals-with-ai-giants-to-use-its-content
- DATAtourisme: https://www.data.gouv.fr/datasets/datatourisme-la-plateforme-nationale-des-donnees-touristiques
- ATDW Distribution Licence: https://support.atdw.com.au/en/articles/44011-distribution-licence-agreement
- ATDW developer guide: https://support.atdw.com.au/en/articles/64809-developer-api-integration-guide
- Tokyo open-data tourist spots: https://spec.api.metro.tokyo.lg.jp/spec/t131041d0000000007-0a8f084b94f2dd4ef2b011fc5f3b33a1-0?lang=en

*Editorial, taste and experiences*
- Michelin–Tripadvisor/TheFork: https://guide.michelin.com/sg/en/article/news-and-views/the-michelin-guide-tripadvisor-and-thefork-launch-an-international-strategic-partnership
- D Magazine, Michelin Dallas AI: https://www.dmagazine.com/food-drink/2026/10/michelin-guide-dallas-ai-reviews/
- Restaurant AI citation index: https://everything-pr.com/restaurants-citation-share-index-2026
- Vox/Atlantic–OpenAI: https://venturebeat.com/ai/openai-partners-with-the-atlantic-and-the-verge-publisher-vox-media
- Condé Nast–OpenAI: https://the-decoder.com/openai-partners-with-conde-nast-to-add-content-to-chatgpt-and-searchgpt
- Perplexity Publishers Program: https://techcrunch.com/2024/07/30/perplexitys-plan-to-share-ad-revenue-with-outlets-cited-by-its-ai-chatbot
- 2024 publisher–AI deal timeline: https://digiday.com/media/2024-in-review-a-timeline-of-the-major-deals-between-publishers-and-ai-companies
- AI licensing tracker, Jun 2026: https://presenc.ai/research/ai-content-licensing-deals-tracker-june-2026
- Tripadvisor–Perplexity: https://skift.com/2025/01/14/tripadvisor-exec-explains-partnership-with-chatgpt-competitor-perplexity/
- Time–OpenAI (not Time Out): https://www.axios.com/2024/06/27/openai-time-licensing-deal-chatgpt
- Time Out Market Delhi: https://www.investegate.co.uk/announcement/rns/time-out-group--tmo/time-out-market-delhi-franchise-agreement-signed-/9606745
- Resy in Beli: https://blog.resy.com/newsroom/resy-launches-reservations-in-beli/
- Grubhub in Beli: https://www.nrn.com/restaurant-delivery/diners-can-now-order-grubhub-on-eater-beli-and-more
- Boston Globe, Beli scale: https://www.bostonglobe.com/2026/08/04/lifestyle/beli-restaurant-rating-app/
- BU, Beli CEO: https://www.bu.edu/hospitality/2026/04/15/expedite-beli-ceo-highlights-data-driven-dining-at-hospitality-leadership-summit/
- Mapstr App Store: https://apps.apple.com/us/app/id917288465
- Corner App Store: https://apps.apple.com/app/id1668282277
- Fever developer portal: https://developer.feverup.com/
- Fever distribution: https://business.feverup.com/en/partner-programs/experience-distribution-platform/
- Fever affiliates: https://business.feverup.com/en/partner-programs/affiliate-program/
- Withlocals partners: https://storefront.withlocals.com/info/partners/
- Withlocals on Awin: https://ui.awin.com/merchant-profile/37836

*Social platforms*
- TikTok Research API FAQ: https://developers.tiktok.com/docs/en/research-api-faq
- TikTok Commercial Content API: https://developers.tiktok.com/products/commercial-content-api
- TikTok terms memo (Open Terms Archive): https://opentermsarchive.org/en/memos/tiktok-updates-its-developer-terms-to-introduce-commercial-content-library-access-clarify-research-purposes-and-reorganize-core-definitions/
- YouTube developer policies: https://developers.google.com/youtube/terms/developer-policies
- YouTube policies guide: https://developers.google.com/youtube/terms/developer-policies-guide
- YouTube derived metrics: https://developers.google.com/youtube/terms/derived-metrics-policy
- Instagram Hashtag Search: https://developers.facebook.com/documentation/instagram-platform/instagram-api-with-facebook-login/hashtag-search
- Instagram Public Content Access: https://developers.facebook.com/documentation/development/features-reference/instagram-public-content-access

*Events*
- PredictHQ trial and free plan: https://www.predicthq.com/support/learn-about-our-trial-and-free-plan
- PredictHQ free plan blog: https://www.predicthq.com/blog/free-plan-access-predicthq-data-for-free-forever
- PredictHQ on Capterra: https://www.capterra.com/p/153702/PredictHQ/
- Ticketmaster terms: https://developer.ticketmaster.com/support/terms-of-use/
- Ticketmaster getting started: https://developer.ticketmaster.com/products-and-docs/apis/getting-started/
- Eventbrite search shutdown: https://groups.google.com/g/eventbrite-api/c/FT2MsDswdrA
- JamBase vs Songkick: https://data.jambase.com/compare/songkick
- DICE (API Evangelist): https://providers.apievangelist.com/providers/dice-fm/

*Entry rules, accessibility and safety*
- Timatic (AltexSoft): https://www.altexsoft.com/blog/timatic/
- IATA developer portal: https://developer.iata.org/en/api
- Sherpa travel requirements: https://joinsherpa.com/products/travel-requirements
- Sherpa API docs: https://joinsherpa.readme.io/docs/travel-restrictions
- VisaHQ suppliers/API: https://www.visahq.ca/travel_suppliers.php
- VisaHQ partnership: https://www.visahq.ca/partnership.php
- eVisas.io partner API: https://evisas.io/partners/api.md
- accessibility.cloud: https://github.com/sozialhelden/accessibility-cloud
- Wheelmap / accessibility.cloud W3C talk: https://www.w3.org/2020/maps/supporting-material-uploads/presentations/Sebastian_Felix_Zappe_Holger_Dieteric.pdf
- AccessNow Google case study: https://services.google.com/fh/files/misc/accessnow_casestudy_en.pdf
- Euan's Guide: https://en.wikipedia.org/wiki/Euan%27s_Guide
- State Dept advisories API (listing): https://apis.io/apis/state-dept/state-dept-travel-advisories-api/
- Data.gov travel warnings: https://catalog.data.gov/dataset/travel-warnings
- GeoSure (Cherre): https://cherre.com/vendors/geosure/
- Safeture–Riskline: https://riskline.com/riskline-partners-with-swedish-based-employee-safety-platform-safeture/
- Safeture–Amadeus: https://www.itij.com/latest/news/safeture-partners-amadeus

*Freshness and AI calling*
- AI calling agents explainer ("Call for Me"): https://ud.hk/en/blogs/insight/article/ai-calling-agents-explained-2026-10-02

*Transit*
- Citymapper joins Via: https://citymapper.com/i/2582/citymapper-joins-via
- Citymapper API docs: https://docs.external.citymapper.com/api
- Citymapper (API Evangelist): https://providers.apievangelist.com/providers/citymapper/
- Moovit transit APIs: https://moovit.com/it/maas-solutions-it/transit-apis/
- Moovit (API Evangelist): https://github.com/api-evangelist/moovit
- Moovit sale report: https://www.newsru.co.il/finance/24jul2026/moovit306.html
- Omio corporate: https://www.omio.co.uk/corporate
- Rome2Rio (API Evangelist): https://providers.apievangelist.com/providers/rome2rio/
- Transitous API: https://transitous.org/api/
- Transitous coverage, Jun 2025: https://planet.kde.org/volker-krause-2025-06-14-adding-public-transport-data-to-transitous
- Navitia repo: https://github.com/hove-io/navitia
- Navitia docs: https://doc.navitia.io
- NAVITIME RapidAPI: https://rapidapi.com/navitimejapan-navitimejapan/api/navitime-route-totalnavi
- NAVITIME business: https://corporate.navitime.co.jp/en/service_biz
- Google transit ZERO_RESULTS, Japan: https://discuss.google.dev/t/directions-api-transit-mode-returns-zero-results/378267
- GTFS extended route types: https://developers.google.com/transit/gtfs/reference/extended-route-types
- FerryhAPI: https://partners.ferryhopper.com/ferryhapi
- Ferryhopper MCP: https://partners.ferryhopper.com/mcp
- Direct Ferries affiliate: https://ca.directferries.com/affiliate.htm
- Omio–Direct Ferries: https://www.cruiseandferry.net/articles/omio-partners-with-direct-ferries-to-add-over-2000-ferry-routes-to-travel-platform
