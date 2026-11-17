# 03 — Hyperlocal Knowledge, Place-Data Quality, Freshness & Hallucination

*Research agent 3 of 7 · compiled 2026-11-17*

**Evidence labels:** **[verified]** means confirmed in a primary or near-primary source found during this session. **[claimed]** means stated by a vendor, a secondary outlet or a single report. **[inferred]** means my analysis. **[bg]** means background knowledge from before this session (up to mid-2026) that I could not re-check here. Treat [bg] items as leads to verify.

**Method limits (read first).** WebFetch could not reach most hosts from this container (greetwell.com, monkeyeatingmango.com and keyt.com all failed DNS). The web-search budget is shared by all parallel agents, and it ran out partway through this work. The following areas were not searched this session and rest on [bg] knowledge only: Beli, Corner, Mapstr, Fever, Withlocals, ToursByLocals, Showaround, the TikTok/Instagram/YouTube APIs, Citymapper, Moovit, HERE, TomTom, Mapbox, SafeGraph/Dewey, Wikivoyage/Wikidata licensing, Time Out, The Infatuation, Eater and Lonely Planet. A follow-up pass should verify those rows.

---

## 1. Evidence of the problem

### 1.1 Documented incidents

| Incident | What happened | Root cause class | Status |
|---|---|---|---|
| **"Sacred Canyon of Humantay", Peru (2025)** | Two tourists headed into the Andes toward a canyon that does not exist and were stopped by a local guide, Miguel Angel Gongora Meza (Evolution Treks Peru). They had reportedly paid for the trip; one report puts the cost at ~£118. The name seems to blend two real local toponyms. Logged as an OECD AI incident and in the AI Incident Database. | Entity fabrication by merging real names | [verified that it was reported] (BBC-sourced, OECD.ai, AIID). One Substack questions whether the guide's account was embellished. |
| **"Kuak Skyride" cable car, Perak, Malaysia (June 2025)** | An elderly couple drove ~300–400 km to see a cable car shown in a ~3-minute AI video (reportedly made with Veo 3) styled as a "TV Rakyat" news report. Officials confirmed no such project exists. | Synthetic media treated as ground truth. This was not a planner error, but any planner that ingests social video inherits the risk. | [verified] (SCMP, NST, PetaPixel) |
| **Mount Misen ropeway, Miyajima, Japan (2025)** | A couple followed ChatGPT's timing for a sunset hike and found the ropeway had stopped running. They were stranded on the mountain. | Wrong attraction-operational data (last-departure time) | [bg] reported in the same 2025 BBC feature as Humantay. Not re-verified this session. |
| **"Weldborough Hot Springs", Tasmania (early 2026)** | A tour operator's AI-written blog sent tourists looking for hot springs that do not exist. | Fabrication in a "local" content source | [bg] Widely reported. Not re-verified this session. |
| **Bolinas, CA, ChatGPT test (Fast Company)** | ChatGPT recommended "Wharf Road Restaurant & Bar", which the journalist could not find in Google, a maps app or the hotel's list. A second suggested restaurant was permanently closed. | Invented venue plus a stale closure | [claimed] (found via secondary summary) |
| **Washington, DC, ChatGPT test (Washington Post)** | The restaurant list included permanently closed venues. | Stale closure | [claimed] (secondary summary) |
| **Layla early outputs (2023–24)** | Reported an "Eiffel Tower in Beijing" and a marathon route across northern Italy that could not be run. | Fabrication and geographic infeasibility | [bg] |
| **Visa failures (2025)** | Viral cases of travelers denied boarding after ChatGPT gave wrong entry or ESTA advice. Stacker/KEYT ran a roundup in Oct 2026, "bogus bars to visa fails". | Regulatory info hallucination | [claimed] (headline seen; article unreachable) |

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
| **Google Places API (New)** | Largest consumer POI graph, ~250M+ places (Google's figure in the Maps-grounding launch) [claimed]. Best for hours, business status, reviews, photos, price level, accessibility fields [bg]. | Business owners via Business Profile, user edits, Local Guides, **Duplex phone calls** (3M+ updates by 2020; target of 20M businesses' hours) [verified, dated], imagery and ML. Low-confidence hours carry a "may have changed" warning [verified]. **~27% of real closures missed in one vendor test** [claimed]. | Since 1 Mar 2025 the $200 credit is replaced by free calls per SKU: Essentials 10k, Pro 5k, Enterprise 1k per month [verified]. Fields such as hours and ratings sit in the Pro/Enterprise tiers, roughly $32–35 per 1k (secondary) [claimed]. | **No caching except place_id**, which may be stored indefinitely. lat/lng may be cached for 30 days [verified]. ToS §3.2.3 prohibits using Maps content to "train, test, validate or fine-tune" ML/AI models [verified]. The Analytics SSTs allow Maps content *only as a factual reference to validate or correct ML output* in that product [verified]. There are separate EEA terms [verified]. In practice you **cannot build your own vector index of Google content** [inferred]. | Best live lookup layer. Unusable as the substrate of a proprietary knowledge base. |
| **Grounding with Google Maps (Gemini API)** | Same graph, exposed as a tool for Gemini. GA October 2025 [verified]. | As above | Gemini 3+: 5,000 free requests per month, then **$14 per 1k** grounded queries. Gemini 2.5: $25 per 1k [verified]. | Gemini-only (lock-in). Each source must carry Google Maps attribution. An optional widget token shows place cards [verified]. Grounded output may not be used to train models [verified]. There is also a "Grounding Lite" agent/MCP offering under similar terms [verified mention]. | Fastest path to grounded answers if you run on Gemini. Strategic dependency risk. |
| **Foursquare OS Places (open)** | ~100–106M POIs, global, 22 core attributes. Releases are monthly [claimed]. | Monthly releases. Example notes: 13.7M record updates and 200k new places in one release; 500k places held back for quality. An agent-based verification system checks ingestion [claimed]. Has `date_refreshed` and `date_closed` fields [bg]. | Free | **Apache 2.0** (attribution notice) [verified]. Some rows may be CDLA-Permissive-2.0 [claimed by SafeGraph]. Since Oct 2025, available only via supported channels, not the public S3 bucket [claimed]. LLM-friendly. | A strong open spine. Thin on attributes, especially hours. |
| **Foursquare Places API (commercial)** | Same base plus Premium fields: hours, photos, tips, ratings. | Continuous | From 1 Jun 2026: Pro ~$15 per 1k; **free tier cut from 10k to 500 calls**. Premium $11.25–18.75 per 1k, no free tier. "Ask" natural-language endpoints $30–36 per 1k [claimed, secondary; Foursquare's marketing page still says 10k]. | Commercial terms. Not checked for LLM clauses this session. | Hours and tips at lower cost than Google. Tips are dated (City Guide app shut 2024 [bg]). |
| **Overture Maps (Places)** | **88.4M places** (2026-10-21 release, +8.5%). New sources: Uberall (424.6k), Birdeye, OpenTravel [verified]. Meta and Microsoft confirmed as sources; a Foursquare feed is unconfirmed. | Monthly. Each place has a 0–1 **existence confidence**, *not calibrated across providers*, so use it only as a relative filter [verified]. Earlier quality audits found location errors and outdated places [claimed, 2023]. | Free | CDLA-Permissive-2.0 for places [bg]. **GERS stable IDs** for entity joins [verified]. | Best open join key and spine. Expect noise. Filter by confidence and cross-check. |
| **OpenStreetMap** | Global and uneven; excellent in the EU and Japan. | Community edits | Free | **ODbL share-alike.** A derived *database* mixed with OSM must be ODbL; "produced works" (rendered output) need attribution only [bg]. Legal friction when merged with proprietary data. | Strongest source for long-tail structure: trails, viewpoints, stairs, toilets, water, `wheelchair=*`. `opening_hours` is filled for only **~45–49%** of restaurants in typical cities (Bordeaux 48.9%) and ~77% in Berlin [claimed]. |
| **Apple Maps Server API / MapKit** | Global. Ratings partly via partners [bg]. | Business Connect; partners | Quota-based. The daily-vs-monthly quota is ambiguous and developers report hitting limits [verified forum]. | Place IDs are available. ToS not reviewed. | Secondary. Weak developer tooling for this use case. |
| **Yelp Places API (formerly Fusion)** | Strong in US, CA and parts of the EU [bg]. | Reviews | Base $229, Enhanced $299, Premium $643 per month plus overage. No free tier beyond a 5k trial [verified]. **Yelp AI API $25 per 1k** with a 1k/day minimum [verified]. | ToS bars *training* gen-AI on Yelp content **and bars submitting or ingesting Yelp content into any gen-AI model** (e.g. ChatGPT) without written approval [verified]. Content may be kept ≤24h [claimed]. | Can enter an LLM pipeline **only via the Yelp AI API**. |
| **Tripadvisor Content API / Terra** | 8M+ businesses, 1B+ reviews [bg]. | Reviews | The legacy API had a 5k/month free tier. **Reportedly retired 31 Aug 2026**, with access moving to Terra (one-time allowance of 1,000 entities) [claimed]. | Legacy terms (Mar 2025) allow AI **only for internal, non-commercial RAG testing**. Any other AI use needs a signed agreement. AI summaries must carry a "may contain mistakes" disclosure. Selective display of reviews is banned [verified terms page plus secondary]. | Partner deal required. Good for attractions and tours. |
| **HERE / TomTom / Mapbox Search** | Global, automotive-grade addresses and POIs [bg] | Commercial feeds | Usage-based [bg] | Storage rights are generally more permissive than Google's; check per contract [bg] | Geocoding and routing backup. Weak on "experience" attributes. |
| **SafeGraph / Dewey / Advan / Placer.ai** | Mostly US (and CA) POIs plus foot traffic [bg] | Monthly | Enterprise contracts | Dataset licences [bg] | Analytics. Weak global consumer value. |
| **BestTime.app** | Claims 150+ countries. A venue needs roughly ≥100 visitors/day for a forecast [claimed]. | Hourly forecasts (0–100) plus live data where available | From ~$29/month metered [claimed] | Vendor terms | The only practical "popular times" substitute. Google does **not** expose Popular Times via the API [bg]. |
| **VOYGR** (YC W26) | US-first | Active closure detection. `/v1/validate` returns open, closed, unknown or not_exists with an existence_confidence. **PlaceCall** phone verification. Batches of 10k [claimed]. | Usage-based | REST, MCP and llms.txt [claimed] | Closest thing to a "liveness API". **No opening hours yet** [claimed]. |
| **Wikidata / Wikivoyage** | Landmarks, plus Wikivoyage's "See/Do/Eat/Sleep" text per destination [bg] | Volunteer | Free | Wikidata is CC0. Wikivoyage is **CC BY-SA**, so attribution and share-alike apply to derivative text [bg]. | Good backbone for landmarks and practicalities. Listings are often stale. |
| **National tourism open data** (e.g. DataTourisme France, ATDW Australia, Open Data Hub South Tyrol) | Official attractions and events per country [bg] | Fed by tourism boards | Free or low cost | Open licences in many cases [bg] | **Underused.** Authoritative hours and seasons for attractions. |

### 2.2 Editorial and "taste" sources

| Source | Access | AI licensing status | Note |
|---|---|---|---|
| **Michelin Guide** | **No public restaurant API**. developer.michelin.com covers tyres and mobility. Data is reached by scrapers (Apify etc.) [claimed]. | No disclosed AI licensing deal found [verified absence in search]. A Kaggle copy is CC BY-NC. | A licensing gap. Mindtrip reviewers saw Michelin data appear in its product [claimed]. |
| **Eater (Vox Media), Condé Nast Traveler, Travel + Leisure / Food & Wine (Dotdash Meredith)** | Websites | Their parent companies signed OpenAI content deals in 2024 [bg] | ChatGPT has licensed access to this editorial layer. A startup would have to negotiate. |
| **Atlas Obscura** | ~33k "odd places" [claimed] | Listed in a Dec 2024 ProRata.ai revenue-share deal [claimed]. Staff and readers pushed back on its AI plans. First annual profit in 2025 [claimed]. | A good "non-cliché" corpus. Revenue-share licensing is feasible. |
| **Lonely Planet, Time Out, The Infatuation (JPMorgan Chase)** | Websites | **No AI deal found** for Lonely Planet [verified absence]. Time Out and Infatuation not searched [bg]. | Open to licensing negotiation. |
| **Beli, Corner, Mapstr** | Consumer apps; no public data APIs [bg] | None known [bg] | They hold the richest *taste-graph* signals (ranked lists, saved places among friends), and those are walled. |
| **Fever** | Event and experience inventory [bg] | Partner APIs [bg] | Strong for city experiences. |

### 2.3 Reservations and availability

- **OpenTable:** a partner-gated API (Online Booking API, Voice AI API) behind certification. It has discovery and booking ties with OpenAI, Perplexity, Alexa+ and Google [claimed]. Its ToS bans bots and gen-AI assistants unless authorised [claimed].
- **Resy:** said in Sep 2026 that it does *not* allow unapproved third-party agents. A ChatGPT integration was reported in Aug 2026 [claimed].
- **Tock:** its API FAQ (Jul 2026) says the API cannot create reservations or read unbooked availability [claimed].
- Across all three, none offers a self-serve public write API [claimed]. Availability, which is the strongest freshness signal for a restaurant, is gated by partnerships.

### 2.4 Events and busyness

- **PredictHQ:** 19 categories, including unscheduled events (severe weather, airport delays, disasters). Search by radius or IATA code [verified]. Pricing is on request. It is built for demand forecasting, so it is good for "what's on and what's disrupting".
- **Ticketmaster Discovery API:** ~5k calls/day [claimed]. Its terms throttle non-user-driven volume [claimed].
- **Eventbrite** retired public event search years ago [bg]. **Songkick** is closed to new API users [bg]. Resident Advisor and Dice have no public API [bg].
- So hyperlocal events (gallery openings, markets, neighbourhood festivals) live in newsletters, Instagram and tourism-board feeds. **This is unserved.**

---

## 3. Hyperlocal and "insider" knowledge sources

| Source | What it holds | Legal access (2026) | Depth |
|---|---|---|---|
| **Reddit** | The best corpus for candid "skip X, go to Y instead" advice, tourist-trap warnings, safety-by-neighbourhood, and time-of-day tips | Google pays ~$60M/yr (Feb 2024 deal), which is under contentious renewal; in Jul 2026 the WSJ reported Reddit considered restricting Google's AI access and wants usage-based pricing [claimed]. OpenAI has had real-time Data API access since May 2024 [verified]. **Free API and RSS reportedly end by March 2027** [claimed]. The commercial API needs approval; paid tiers have run at ~$0.24 per 1k calls since 2023 [bg]. Reddit sued Anthropic (2025) and Perplexity and scrapers (2025) [bg]. | Street- and dish-level detail, but noisy and quickly stale. **Effectively licensed only to the large LLM labs.** |
| **TikTok** | Visual "hidden gem" content, very current | The Research API is limited to academics and is non-commercial; the Display API covers only the user's own content [bg]. | High recency, low reliability. The Kuak Skyride case shows synthetic-video risk. |
| **Instagram** | Venue and creator posts | Graph API access covers only accounts that authorise you; oEmbed for display [bg] | Same as TikTok |
| **YouTube** | Long-form walking tours and guides | The Data API allows search and metadata. Policies require refreshing or deleting stored non-authorised data roughly every 30 days [bg]. Transcripts are not an official API surface [bg]. | Good for neighbourhood "feel". Licensing is ambiguous. |
| **Google Local Guides / Maps reviews** | Huge UGC base | Only via the Places API, **max 5 reviews** per place [bg], plus Gemini-generated review and area summaries [bg]. Caching restrictions apply. | Broad and shallow |
| **Local-guide marketplaces** (Withlocals, ToursByLocals, Showaround) | Human locals with neighbourhood expertise | No public data APIs; affiliate programmes only [bg] | Deep but not machine-readable. **A partnership opportunity.** |
| **Creator and advisor platforms** (Thatch, Fora, Matador/GuideGeek) | Creator-curated guides and advisor knowledge | Their own platforms. Matador's GuideGeek runs over its own content and creators [bg]. | Authentic and attributable. Small coverage. |
| **Local blogs and newsletters** | City- and neighbourhood-level picks and events | Copyright applies. Licensing is negotiable and long-tail. | Deepest hyperlocal layer, also the least structured. **AI-generated "local" blogs** (the Tasmania case) now pollute it. |

**How current planners get "local" knowledge [inferred, from partner lists and reviews]:**
- **Mindtrip** combines an OpenAI-based model with a proprietary DB of 11M+ POIs. Its stated data partners are Google Places/Maps, Tripadvisor, OpenTable, Viator and Priceline, with Sabre, PayPal, Expedia and Booking for transactions [claimed]. Reviewers saw few hallucinations, and it declines far-future flight queries rather than guessing [claimed]. Its "local" layer is therefore *aggregated reviews*, not insider knowledge.
- **Layla** (reportedly acquired by Expedia in Jul 2026 [claimed]) uses Booking.com and Skyscanner for live prices plus GetYourGuide and Viator. Its accuracy is attributed to live web search; the model is undisclosed [claimed].
- **ChatGPT, Gemini and Perplexity** draw on pretraining plus web search. Licensed publisher deals cover Eater, CNT and T+L for OpenAI [bg], Reddit for OpenAI and Google, and Google's first-party Maps graph for Gemini.
- **No product we found** has a licensed, attributed, *recency-stamped* corpus of local insider knowledge.

Depth today [inferred]:
- **Neighbourhood-level:** partially served.
- **Street-level and dish-level:** unserved except by accident through Reddit in pretraining.
- **Time-of-day and seasonal nuance:** largely unserved (BestTime is the exception).
- **Etiquette:** generic.
- **Safety:** country-level advisories only.
- **Accessibility:** Google boolean fields plus OSM `wheelchair` tags. Shallow.

---

## 4. Transit and routing data

| Source | Coverage | Freshness | Access | Notes |
|---|---|---|---|---|
| **Mobility Database** (MobilityData) | **6,000+ GTFS, GTFS-RT and GBFS feeds in 100+ countries** (as of Oct 2026) [verified]. A third-party count gives ~4,500 schedule and ~1,900 RT feeds across ~70 countries [claimed]. One agency's RT can count as 3 feeds. | Operator-published | Free | The canonical open catalogue. TransitFeeds has shut down [claimed]. |
| **Transitland** | Thousands of GTFS, GTFS-RT, GBFS and MDS feeds [verified]. "55+ countries" is likely dated. | Fetched continuously | Free API tier plus paid [bg] | Good for a feed registry and history. |
| **Google Routes API** | Compute Routes and Route Matrix replaced the legacy Directions and Distance Matrix APIs (Legacy since Mar 2025) [verified]. Transit matrix capped at 10×10 [claimed]. Some countries' transit is unavailable through the API (Japan historically; China) [bg, verify]. | Google's merged feeds plus realtime | Pay per SKU, or a $100/mo Starter plan [verified] | The best global single call. Same caching restrictions as Places. |
| **Open routing stacks** (OpenTripPlanner, MOTIS/Transitous, Navitia) | As good as the GTFS you load [bg] | Your pipeline | Open source | Can be self-hosted and cached. Transitous runs community-wide routing [bg]. |
| **Citymapper** (Via-owned) | ~100 cities [bg] | Strong | No public third-party API today [bg] | Quality benchmark only. |
| **Moovit** (Mobileye) | Claims thousands of cities, 100+ countries [bg] | Mixed: agency data plus crowdsourcing | Enterprise APIs [bg] | Strongest for developing-market urban transit. |
| **Rome2Rio** (Omio since 2019) | Global multimodal *estimates* [verified acquisition] | Heuristic: frequencies and durations, often stale [bg] | No current public API found [verified absence] | Good for coarse "is there a bus?" answers, not schedules. |
| **12Go (Travelier group, which includes Bookaway)** | ~4,000 operators, ~50k routes, 26 Asian countries; also claims 30k+ operators worldwide [claimed] | Direct operator integrations | Affiliate (80+ countries), deep links, white label and OTA-grade API [claimed]. AirAsia super-app partner [verified]. | **The key source for buses, ferries and minivans in SE Asia.** |
| **Busbud, Distribusion, Ferryhopper, Direct Ferries** | Intercity bus (global), B2B rail/bus/ferry, Mediterranean ferries [bg] | Inventory feeds | Partner APIs [bg] | Bookable ground transport that complements GTFS. |
| **Walking, terrain and steps** | OSM (`highway=steps`, `incline`, `surface`, `sac_scale`) plus elevation DEMs [bg] | Community | Free | Routers ignore stairs, heat and hills for tourists, which is a gap. |

**Transit gaps [inferred]:**
- **Cable cars, ropeways, funiculars, small island ferries, park shuttles and seasonal services** are rarely in GTFS. This is exactly the Mount Misen failure.
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
   - VOYGR's validate API, with existence_confidence and phone calls [claimed].
   - Google Duplex calling for hours, plus "hours may have changed" flags [verified, older].
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
| ChatGPT | Web search plus publisher deals | Closed and invented restaurants documented (Fast Company, WaPo) [claimed]. |

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
 enrichment     Google Places (status, hours, currentOpeningHours) ·
                Foursquare Premium (hours/tips) · Yelp AI API (where allowed)
                · BestTime (busyness) · OpenTable partner API (availability)
 L2 Liveness    Freshness ledger per place: {field, value, source, observed_at,
 & confidence   method: api|crowd|call|editorial, confidence}
                Closure detectors: VOYGR-style validation, review-velocity drop,
                multi-source disagreement, own voice-agent calls for booked/
                critical stops (24-48h pre-visit reconfirm)
 L3 Licensed    Revenue-share licensed editorial + creator + local-guide corpus
 knowledge      (Atlas Obscura-style ProRata model; newsletters; guides; own
                local-expert network) — chunked, place-linked by GERS, dated,
                attributed; synthetic-content filter
 L4 Ops data    GTFS/GTFS-RT via Mobility Database → self-hosted OTP/MOTIS;
                Google Routes fallback; 12Go/Busbud/Distribusion/Ferryhopper
                inventories; hand-curated "special services" table (ropeways,
                funiculars, park shuttles, seasonal ferries, last-entry times)
                PredictHQ + tourism-board events; weather/daylight
 L5 Planner     LLM proposes → deterministic validator (hours × day-of-week ×
                last entry × travel time × buffers × holidays × daylight) →
                repair loop → every claim carries source + last-verified stamp
 L6 In-trip     Push alerts on status change; one-tap "it was closed" reports
 loop           feed L2; accountability log (what we said, when, from where)
```

**Key design choices:**
- **[inferred]** Do not build the knowledge base on Google content. Its ToS forbids caching and model training. Use Google only as a real-time verifier and display layer, and keep the spine open-licensed.
- **[inferred]** Choose the LLM vendor separately from the data vendor. Gemini Maps grounding is cheap at $14 per 1k but locks you to one model. Keep it as one tool among several.
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
| Intercity bus/ferry, developing regions | 12Go, Busbud, Bookaway | ◐ | Africa and South Asia thin |
| Special transport (cable cars, funiculars, seasonal) | — | ○ | Not in GTFS |
| Walking terrain, stairs, heat | OSM plus DEM | ◐ | Not used by consumer routers |
| Accessibility (step-free, toilets) | Google booleans, OSM/Wheelmap | ◐ | Shallow; no verified detail |
| Events (major) | PredictHQ, Ticketmaster | ● | |
| Events (hyperlocal: markets, openings) | Instagram, newsletters | ○ | No machine-readable feed |
| Insider "skip X, do Y", tourist-trap detection | Reddit (licensed only to big labs) | ○ | Strategic gap |
| Dish-level / what to order | Reddit, Beli, Infatuation | ○ | Walled |
| Neighbourhood vibe / who it's for | Editorial, YouTube | ◐ | Licensing needed |
| Time-of-day and seasonal nuance (light, bloom, crowds) | Scattered | ○ | |
| Cultural etiquette, dress codes, cash-only | Wikivoyage, generic LLM | ◐ | Not venue-specific |
| Safety by neighbourhood and time | Gov advisories (country level) | ○ | |
| Entry and visa rules | Gov sites; Timatic (B2B) [bg] | ◐ | Frequent hallucination class |
| Provenance / last-verified display | — | ○ | Nobody ships it |

---

## 8. Top gaps and exploitable opportunities

1. **A shipped freshness and confidence layer.** Every planner treats place facts as binary truth. Build a per-field freshness ledger, as in §6 L2, and show "last verified" and confidence to users. Re-confirm booked or critical stops 24–48h ahead with a voice agent; VOYGR's PlaceCall and Google Duplex prove the approach works. VOYGR does not cover hours yet, which is a white space. This directly answers problem #4, accountability.
2. **A deterministic feasibility validator.** 43% of AI-planned days contain a verifiable fault, and most are hours, sequencing or duplicates. These are mechanically checkable once you have hours, day-of-week closures, last entry, travel times, buffers and holidays. Research shows solver-in-the-loop planning beats pure LLMs by large margins, yet no consumer product documents one. This is cheap to build and directly measurable ("0 infeasible days").
3. **An operational long tail of attractions and special transport.** Cable cars, ropeways, funiculars, park shuttles, seasonal ferries, last-entry and timed-ticket sellouts, and seasonal hut and trail closures. None of it sits in GTFS or the POI APIs. A curated, crowd-maintained "special services" dataset fed by tourism-board open data and operator sites would be a proprietary moat.
4. **A licensed, attributed hyperlocal corpus.** Reddit is licensed to Google and OpenAI and its free API ends in 2027. TikTok and IG are inaccessible. Michelin has no API. Lonely Planet and Infatuation have no AI deals found. Opportunity: revenue-share licensing in the ProRata/Atlas Obscura style with local newsletters, guidebook publishers and local-guide marketplaces, plus an owned local-expert network paid per verified tip. Each tip is GERS-linked, dated and attributed, and screened for AI-generated content. This answers problem #1, cliché recommendations, with *rights*, not scraping.
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
