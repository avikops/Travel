# 01 — AI-Native Trip Planner Startups: State of the Art (as of 2026-11-17)

**Scope:** consumer AI-native trip planners, AI travel agents, social-to-itinerary tools, and B2B/DMO conversational planners. Big-tech assistants and OTA in-house AI (Google, ChatGPT apps, Expedia Romie, etc.) appear here only where they acquired or launched AI-native startups. Other agents cover them in depth.

**Method and limits:**
- I used web search only. WebFetch could not reach any primary site I tried (mindtrip.ai, layla.ai, phocuswire.com, morningstar.com), so I couldn't read help centres or terms pages in full. Terms details come from search excerpts of those pages.
- The shared web-search budget ran out partway through. Several products got thinner coverage than planned: Tripnotes, Navi, Vacay, Boardwalk, iMean, Stippl's 2026 features and Mozio-type tools.
- **Gap-fill pass (17 Nov 2026):** a second pass used 58 web searches (no WebFetch) to check the thin items and the [prior] tags. Raw notes are in `research/notes/01-02-gapfill-notes.md`. Main changes:
  - new facts on Lola (flights via Duffel, $100M commitment, US-only), Mindtrip Stays (Jul 2026), Vayo's booking status, Holiwise's ATOL claim, Axel pricing, Stippl, Pilot, Wanderboat, Tripnotes, Vacay, Tryp.com and the PhocusWire Hot 25 for 2027;
  - corrections to the GuideGeek "spin-out" (no evidence found) and to the Mindtrip Flights date (launched 6 May 2026).
  - Most long-tail players (iMean, Wonderplan, Trip Planner AI, Plan Harmony, JourneAI, Tripnotes) still have only directory, SEO or competitor-blog coverage. Their [review] tags reflect that.
- Tags:
  - **[verified]**: primary source, press release, or reputable trade press (Skift, PhocusWire, TechCrunch, GeekWire, Expedia IR).
  - **[claimed]**: the company's own marketing.
  - **[review]**: a third-party review. Many are SEO or affiliate blogs, and some are written by competitors.
  - **[inferred]**: my own reading of the evidence.
  - **[prior]**: from my background knowledge, not re-checked in 2026.

---

## 1. Executive summary: what changed in 2025–2026

1. **Big companies bought or built the independent AI planners.**
   - **Expedia Group acquired Layla on 31 Jul 2026** (Berlin; about €5M raised; about 25 staff) [verified].
   - **OpenAI acquired Odessia on 10 Nov 2026.** Odessia is the IATA-accredited AI travel agent founded by Sonder's Francis Davidson, who is now Head of Travel at OpenAI. The Odessia service shut down about 27 days after its public launch [verified].
   - **Booking Holdings launched two AI-native startups:**
     - **Lola** (29 Sep 2026), from Kayak co-founders Steve Hafner and Paul English. It is a membership model with live booking and Ten Group human concierge. It has since added flight booking (via Duffel) and received its own conditional **$100M investment commitment** [verified, PhocusWire].
     - **Vayo** (14 Oct 2026, private beta, up to $100M committed). It is an inbox-connected agent that monitors existing bookings. As of mid-Nov it books only restaurants (via OpenTable) [verified].

   The pure independent "chat-to-itinerary" category is being hollowed out. The survivors are differentiating through B2B/DMO distribution (Mindtrip, GuideGeek), logistics depth (Airial), and agentic post-booking (Axel, Vayo, Stardrift).

2. **Booking depth moved from affiliate links (B1) to in-chat transactions (B2/B3).**
   - **Mindtrip Flights** (launched 6 May 2026) runs on Sabre's Mosaic platform: 420+ airlines including 150 LCCs, and 2M+ lodging options planned in a phased rollout. PayPal handles checkout [verified].
   - **Mindtrip Stays** (15 Jul 2026) is a conversational hotel search and booking product. It aggregates Expedia, Booking.com, Priceline, Agoda and Nuitee inventory and adds price-drop alerts [verified, trade press].
   - **Lola** books Booking.com, Priceline, Agoda, OpenTable, FareHarbor, GetYourGuide and SeatGeek inventory in chat, and now flights via Duffel [verified].
   - **Odessia** booked as an IATA agency [verified].
   - **Axel** books flights and hotels as separate bookings, after user approval [claimed].

3. **Persistent memory and background agents are the new frontier (P3→P4, L2→L3).**
   - Mindtrip's **Personal Travel Assistant** (30 Sep 2026) remembers preferences across trips and runs agents that "research, monitor and work on the traveller's behalf" after the chat ends. It had 18k+ beta users [claimed].
   - Stardrift reads your calendar.
   - Vayo and Lola read Gmail confirmations.
   - Axel monitors post-booking price drops and claims refunds.

   **Nobody has publicly shipped a verified L4**, meaning automated rebooking after a disruption, in a consumer AI-native product [inferred, absence of evidence; re-checked Nov 2026].
   - The only consumer claim found is TripAgent.ai's marketing page (Jul 2026), which says it rebooks cancelled or badly delayed flights automatically. It is unverified [claimed].
   - Automatic consumer rebooking that does exist in 2026 is **carrier-side**. American Airlines' AURA/Connect Assist moves delayed passengers onto later flights without asking, and has drawn complaints about wrong itineraries [press]. Delta Concierge offers alternatives for the traveller to approve.

4. **Hallucination and staleness are still widely reported.**
   - Third-party tests of Mindtrip (the category leader) found:
     - hotels that don't exist ("Holiday Inn Express Tokyo", "InterContinental Nagasaki");
     - a Lisbon restaurant that closed in 2024;
     - wrong Colosseum hours, and a plan that missed the free first-Sunday rule;
     - an invented rain probability and wind speed [review].
   - In one test Layla misread arrival and departure days [review].
   - There is **no independent benchmark** for the category (noted as of Aug 2026, still true in Nov 2026) [review]. The best 2026 evidence is:
     - a Greetwell survey of 1,000 US adults (Sep 2026): **1 in 6** AI-using travellers were sent to a place or tour that does not exist, and 55% hit at least one bad recommendation, most often wrong prices or hours [verified, Stacker syndication];
     - small single-trip model tests with inconsistent rankings [review].
   - Engadget warns that agents can show a "confirmed" status while a booking is still pending [verified, press].

5. **Accountability is the weakest axis everywhere.**
   - Terms push liability to suppliers. For example, Layla's terms say the chatbot "cannot in any case bind" anyone contractually, liability is capped, and third-party integrations are excluded [verified, terms excerpt].
   - The only players with a real human backstop are:
     - Layla's "human expert" booking layer;
     - Lola's paid concierge, outsourced to Ten Group;
     - Holiwise's premium concierge (Holiwise also displays an ATOL number, which would make it the only AI-native player claiming UK package protection [claimed, not checked against the CAA register]);
     - advisor-centric models (Fora, Tern), where a licensed human owns the trip.
   - A Booking.com survey found 89% of travellers want AI help planning, but **only 12% trust AI to make decisions on its own** [review, citing a Booking.com survey].

---

## 2. Product deep-dives

### 2.1 Mindtrip (USA, founded 2023, CEO Andy Moss)

**What it is**
- A map-centric conversational planner covering hotels, restaurants, attractions, collections and itineraries.
- Consumer app on web, iOS and Android.
- Plus "Mindtrip for Business": a planner embedded on DMO and tourism-board websites.

**Target user**
- Leisure travellers, mostly US.
- DMOs: Brand USA, Discover Puerto Rico, San Francisco Travel, Visit Santa Fe, Meet Boston (on WhatsApp, timed to the FIFA World Cup 2026), Meet Minneapolis (Sep 2026), Kentucky Department of Tourism (11 Nov 2026), Visit Santa Barbara, Madeira Promotion Bureau and Norwegian Travel Cluster (Europe launch, 3 Jun 2026). The Norway deal powers "Norway by Locals" across 150+ municipalities and 29 regions [verified].
- TUI partnership, and Ripe's ITA booking-platform integration [verified, trade press].

**Business model**
- Free to consumers.
- Revenue comes from affiliate and transaction commissions (hotels via partners; flights via Sabre) and B2B DMO contracts.
- DMO pricing is not public ("contact sales"; one aggregator says usage-based) [verified absence].
- Mindtrip pitches itself to DMOs as "the decision layer" now that organic search is declining (Moss) [verified].

**Funding**
- $7M seed (Sep 2023, Costanoa).
- $12M (Sep 2024, Forerunner).
- Strategic investments from Amex Ventures, and from Capital One Ventures and United Airlines Ventures (Dec 2025; CB Insights labels it a Series B dated 8 Dec 2025).
- About **$22.5M total** per PhocusWire (Dec 2025) [verified]. CB Insights says $19M. **No 2026 round found** (re-checked Nov 2026) [verified absence].
- PhocusWire Hot 25 for 2025.

**Key capabilities**
- **Start Anywhere / Magic Links** (Jul 2024): builds an itinerary from a photo, screenshot, TikTok or YouTube link, blog URL, PDF or Google Maps list. It comes with a creator program, where creators put Mindtrip links in their bios [verified].
- **Group Chat** (Sep 2024): invite a crew and @Mindtrip to balance everyone's preferences; likes, comments and real-time editing [verified].
- **Mindtrip Flights** (launched 6 May 2026, per Skift): conversational search and booking on Sabre's platform, which handles shopping, pricing, availability, booking and servicing. PayPal provides wallet, ID verification and Pay Later [verified]. Hotels via Sabre are "phased".
  - Date note (resolved): the Sabre–PayPal–Mindtrip partnership was *announced* in Feb 2025 (the PayPal newsroom URL dated 2025-02-12). The product *launched* on 6 May 2026 [verified].
- **Mindtrip Stays** (15 Jul 2026, PR Newswire):
  - a standalone conversational hotel search and booking product with price-drop alerts and "best-fit, best-value" optimisation;
  - it compares room-level details, not just headline rates;
  - live inventory is aggregated from **Expedia, Booking.com, Priceline, Nuitee, Agoda "and more"** [verified, Hotel Management / PR];
  - the merchant of record for Stays bookings is not stated. This replaces the earlier unconfirmed "Expedia/Hotels.com, Priceline, Viator" claim.
  - Mindtrip also sells a B2B "Mindtrip for Hotels" product, and launched an AI-visibility tool for DMOs (PhocusWire, 21 Jul 2026) [verified].
- **Personal Travel Assistant** (30 Sep 2026): cross-trip memory. A Home tab shows price alerts and "agents" you can switch on or create yourself, and these keep running after the chat ends. Examples include monitoring hotel prices and checking alternative dates for flights. 18k+ beta users [claimed].
- **Data:** "Scours thousands of data sources"; photos, maps and reviews [claimed]. No named POI provider was found. A Foursquare link is **unconfirmed**. DMO partnerships supply first-party local content, which is a structural hyperlocal advantage on partner sites [inferred].

**Rubric**
- P3–P4 (persistent assistant; no evidence yet of learning from bookings).
- G3: maps plus a day plan. Transit times are weak; a reviewer found errors in its time arithmetic.
- B2–B3: flights (Sabre) and hotels (Stays, multi-supplier) are now both bookable in-product. Activities and attraction tickets still mostly link out [review]. There is no single cross-vertical checkout.
- L2–L3 (companion chat; price-alert agents).
- Editing: good. Collections, group chat, likes and comments. No evidence of constraint locking.
- Accountability: no published human support or guarantee was found. Flight servicing sits with Sabre and the ticketing agency [inferred].

**Weaknesses**
- Hallucinated hotels, a closed restaurant, wrong hours, and invented weather numbers [review].
- Ignores dietary preferences in some reports [review, low quality].
- Clunky map filtering [review].
- 2026 accuracy evidence is still anecdotal.
  - A MonkeyTravel review cites an 11M+ POI database.
  - One informal Tokyo comparison named Mindtrip the most accurate.
  - Neither publishes a method [review, low rigour]. No rigorous independent test was found.

### 2.2 Layla (Berlin, Layla AI GmbH; merged with Roam Around in 2023 [prior]); acquired by Expedia Group on 31 Jul 2026

**What it is**
- A chat-first AI travel agent covering flights, hotels, activities and cars, with video and social inspiration. Integrations include Beautiful Destinations content [verified, terms].
- After the acquisition it still runs from Berlin and works with Expedia, Hotels.com and Vrbo. No Expedia-branded Layla product has been announced [verified].
  - Re-checked Nov 2026: no post-acquisition feature launches or integration timeline have been announced. Layla runs standalone [verified absence].
  - Expedia's own Fall 2026 release (30+ AI features, a Hotels.com AI agent) does not mention Layla (see file 02, §3.1).

**Business model**
- Freemium: Premium is about $49 a year and unlocks live pricing (Skyscanner, Booking.com) and PriceLock alerts [review].
- Reviews disagree on whether the full day-by-day itinerary is free or sits behind a 3-day trial [review].
- One review says Layla stopped naming its live-pricing partners and now sells **expert-built packages** rather than live fares [review]. That would be a notable move toward a packaged-travel or agency model [inferred].

**Traction**
- A homepage counter showed 1.1M, then more than 2.35M, trips planned [claimed].
- App store ratings: iOS 4.6, Google Play 4.7 (Sep 2026).
- Funding about €5M (First Minute Capital, M13).

**Key mechanism: a human expert layer**
- The AI drafts the plan, then a "destination expert" human reviews and books it. Reviews say this is free and you pay only for the travel [review].
- Separate "Human Expert Terms and Conditions" apply, and they override the main terms for those services [verified, terms excerpt].
- The chatbot "cannot bind" any party. Liability is capped, and indirect and third-party-integration damages are excluded [verified, terms excerpt; the terms page may be about 18 months old].

**Rubric**
- P2–P3.
- G2–G3.
- B2 (AI-assisted, human-completed booking).
- L2.
- Editing: **no manual editor and no drag-and-drop** [review].
- Accountability: better than average because of the human-expert path, but liability terms are unclear.

**Weaknesses**
- Shallow comparison logic.
- Misread arrival and departure days in one test.
- Pricing and paywall confusion.
- Concern about OTA bias after the acquisition (Expedia inventory may be favoured) [review].

### 2.3 Lola (Booking Holdings-backed; founders Hafner and English; launched 29 Sep 2026)

**What it is**
- An AI assistant for travel, dining and experiences with live prices and in-chat booking.
- Launch partners: Booking.com, KAYAK, Priceline, Agoda, OpenTable, FareHarbor, SeatGeek, GetYourGuide and others [verified].

**Post-launch changes (Oct–Nov 2026)**
- **Flight booking added.** Users search and book flights without leaving Lola, **powered by Duffel**. Direct links to airlines and travel-search sites are also offered [verified, PhocusWire].
- **$100M investment commitment from Booking Holdings**, mirroring Vayo. It is "subject to continued advancement of the product and market commitments", so it is conditional rather than paid in [verified, PhocusWire].
- Lola is wholly owned by Booking Holdings and has about 20 staff [verified].
- Users can share itineraries and link Google Calendar as well as Gmail [verified].
- **US-only.** Hafner has acknowledged this needs to change, but no expansion date has been given [verified, press].
- Pricing change: a Japanese trade outlet (travelvoice.jp, 10 Nov 2026) reports that **Lola Plus ended on 5 Nov 2026 and existing members moved to VIP**. I found no confirmation elsewhere [claimed, single outlet].

**Business model**
- **No advertising or paid placement.**
- Free tier, then Plus at $5 a month and VIP at $25 a month, both on 12-month commitments.
- VIP includes:
  - up to 15% off 4- and 5-star hotels;
  - preferred activity rates;
  - OpenTable Gold status and priority restaurant booking via ResX;
  - Aero charter credits;
  - **human concierge consultations via Ten Group** (Plus gets quarterly access; VIP gets several per quarter) [verified].
- One company-supplied example: a 4-night Miami stay at $783 vs $997 on Booking.com and Expedia [claimed].
- A critic notes Booking earns twice: hotel commission plus the member's fee [press].

**Data**
- Connects to Gmail to pull confirmation numbers and addresses [verified, privacy notice per press].

**Rubric**
- P3 (membership profile, inbox data).
- G2–G3 (unclear).
- **B3** (multi-vertical in one chat: hotels, dining, events, activities, and now flights).
- L2.
- Accountability: paid human concierge. This is the first mass-market "AI + human" subscription [inferred].

**Weaknesses:**
- Still no independent hands-on reviews as of mid-Nov 2026. One VentureBeat writer started a test booking, but I couldn't find the follow-up.
- Note: an unrelated older business-travel company, Lola.com, carries 2020-era Trustpilot reviews. Don't conflate the two.
- Engadget warns that agents can show "confirmed" while a booking is still pending [press].
- Lola is US-only.

### 2.4 Vayo (Booking Holdings; Seattle; CEO Mike Fridgen; private beta 14 Oct 2026; up to $100M)

**What it is**
- An inbox-connected agent. It pulls flight, hotel and restaurant confirmations from email, then **monitors** them for:
  - price drops;
  - openings at sold-out hotels;
  - schedule changes [verified].
- It reads only travel confirmations, and says personal data won't train its wider model [claimed].
- At launch it organised and monitored trips.
  - **Restaurant reservations are bookable via OpenTable** during the beta.
  - Flights and hotels can be searched, but the user is **handed off to the supplier** to book [verified, PhocusWire 14 Oct 2026].
  - CEO Mike Fridgen promised transactional flight and hotel booking "in the coming weeks", followed by group planning and a native app.
  - Re-checked mid-Nov 2026: **no report confirms flight or hotel booking has shipped** [verified absence].
- Free, invite-only beta with a waitlist at vayo.com.
- It is an "open" system. It monitors bookings made on rival platforms or directly with airlines and hotels, not just Booking Holdings brands [verified].

**Rubric:** P4 (behavioural, from booking history), G1–G2, B1–B2 (restaurants only; flights and hotels planned), **L3**.

**Gap:** Monitoring without automatic re-planning or rebooking (no L4).

### 2.5 Odessia (Canada/US; Francis Davidson; $6M pre-seed led by Sequoia, Jun 2026; public 14 Oct 2026; acquired by OpenAI and shut down 10 Nov 2026)

**What it was**
- A text-message concierge. It compared flights and hotels, watched prices and **award seats**, and booked as an **IATA-accredited travel agent**.
- Accreditation gave it agency/private hotel rates and perks at about 2,000 hotels: breakfast, a $100 credit, upgrades, late checkout [verified/press].
- Built itinerary panels with property previews.
- Claimed more than $60M in annualised planned travel (unverified) [claimed].
- Named to the **PhocusWire Hot 25 Travel Startups for 2027** (published 9 Nov 2026, the day before the OpenAI deal) [verified].
- OpenAI has not announced any travel-booking product for ChatGPT. Davidson joins "to focus on the future of travel". Existing customers were told to email support@odessia.com [verified].

**Weaknesses**
- Never said how 24/7 human support worked.
- Hotel support was run by a wholesale supplier.
- Some bookings were handed off to third-party sites [press/review].
- On shutdown, users were told to contact support about existing bookings. Gmail-connected users were advised to revoke access [press].

**Lesson [inferred]:** the defensible asset was the *licence and supply stack* (IATA, rates, servicing), not the LLM. A shutdown that leaves travellers with live bookings is exactly the accountability failure our product should design against.

### 2.6 Airial (USA; founders Archit Karandikar, ex-Meta/Google/Waymo, and Sanjeev Shenoy, ex-Instagram Reels; $3M seed Jun 2025 led by Montage Ventures, with South Park Commons, Peak XV and angels)

**What it is**
- A "logistics-correct" multi-city itinerary generator from a single prompt [verified, TechCrunch].
- Flight search across multiple dates and airports.
- **Multi-modal transit embedded in the itinerary**: high-speed and regional trains, buses, metros, trams, ferries, e-bikes and driving. It gives which train serves each leg, recommended departure times and transfer durations, and re-computes connections when you edit [claimed, blog].
- Turns TikTok and Instagram links into trip plans, and shows TikTok videos filmed at suggested places.
- Collaborative editing and comments.
- "Airial for travel businesses" B2B offering.

**Business model:** Free or freemium. One source says it isn't monetised yet and affiliate revenue is likely [review]. No 2026 funding or booking news was found. The last round is still the $3M seed (Jun 2025), and the public beta dates from Dec 2024 [verified absence].

**Rubric**
- P2.
- **G4**: the strongest transit and routing claim among consumer AI planners.
- B1 (the blog calls them "bookable-style" routes; no evidence of ticketing).
- L0–L1.
- Collaboration: yes.

**Weaknesses:** English only, no public API, weaker on niche preferences [review]. No evidence of real-time timetable feeds (GTFS-RT or operator APIs) behind the transit data [inferred gap].

### 2.7 Stardrift (YC S24; backed by Bain Capital Ventures; launched 4 Dec 2025)

**What it is**
- A "personal travel assistant" for frequent and business travellers.
- **Calendar integration** checks for conflicts.
- Searches and books flights, trains, hotels and activities in chat with current prices.
- Remembers preferred airlines and seats across trips.
- Can enforce corporate travel policy and route manager approvals [review/claimed].
- A Kernel (browser-infrastructure) customer story suggests **browser automation** is part of its booking stack [inferred].
- Free, no waitlist. An iOS app has launched on Product Hunt. YC's $500K investment is dated Dec 2025 (Crustdata) [review].
- **Booking mechanics are still undocumented** (re-checked Nov 2026).
  - Sources describe live pricing for flights, **Amtrak rail** and hotels, ranked by user rules (airlines, seats, times).
  - No source describes the checkout or ticketing step, or who the merchant of record is.
  - One guide says the product "focuses on planning and search" and lists booking limitations [review].
  - Coverage is US-domestic plus major international destinations.

**Rubric:** P3–P4 (calendar plus remembered preferences), G2–G3, B1–B2 (in-chat booking claimed, checkout unverified), L2.

**Weaknesses:** Early stage and logistics-focused, with weak experiential itineraries and little group or multi-city support [review]. Stardrift also publishes competitor reviews (for example, of Layla) as SEO content.

### 2.8 Axel (Gordian Software, YC W19; CEO Stephen Grabowski, ex-Skyscanner)

**What it is**
- A free AI travel agent with **private rates** (it claims 10–40% savings).
- Books flights and hotels **after the user approves**; they are separate bookings, not a package.
- Its signature feature is **post-booking monitoring that automatically secures refunds when prices drop** [claimed].
- Exposes an MCP server so that *other AI assistants* can use Axel's rates [verified, MCP listing].
- Gordian's heritage is B2B airline ancillaries APIs (seats, bags), so it has deep air servicing know-how [verified/prior].

**Rubric:** P2–P3, G1, B2, **L3** (price monitoring), with a partial B4 (price-drop rebooking or refunds).

**Company:** Gordian Software, Inc. (founded 2017, Seattle area) [verified, YC listing]. It claims an average saving of $327 a year per user (GWU media tip sheet) [claimed].

**Pricing (conflicting):**
- Axel's FAQ ("How much does Axel cost?") says there is **no membership fee**.
- Axel's own Trustpilot company description says members pay **$35 a year**.
- The help centre has a "How do I cancel my membership" article, which suggests a paid or registered membership exists [claimed, conflicting].
- Price-drop savings are paid as a refund, and the itinerary does not change.

**Accountability:**
- Has an FAQ entry titled "Is Axel a travel agent?". I still couldn't read the body, and I found no seller-of-travel registration.
- Trustpilot shows 25 reviews, including complaints that price drops were missed [review].

### 2.9 GuideGeek (Matador Network)

**Correction:** the first pass said a spin-out had been announced. The gap-fill found **no evidence of a GuideGeek spin-out**. The 2026 "Matador spin-out" news concerns Matador Technologies, an unrelated Toronto-listed bitcoin company spinning out GODL Corp. GuideGeek remains a Matador Network product [verified absence].

**What it is**
- An AI travel assistant that started on WhatsApp, Instagram and Messenger. Matador's Messenger launch press release confirms the channels [verified, PR Newswire]. A 2026 profile claims more than 1M consumer users [claimed].
- Now mainly a **B2B white-label "AI travel genius" for DMOs**. Each build prioritises the DMO's own content, website and social channels.
- Partners include:
  - NYC Tourism + Conventions ("Libby" for visitors, Mar 2026; "Ellis" for meeting planners);
  - Destination Toronto ("6ix");
  - Colorado ("Colorado Concierge", Aug 2025);
  - Visit Idaho, Reno Tahoe, Tourism Greece, Aruba, Fort Lauderdale, Manitoba, Richmond, Estes Park, Snowmass and Discover Halifax [verified].
- **Ripe** booking integration gives DMOs real-time booking and attribution [verified].
- Skift IDEA Awards 2025 finalist or winner for "Best Use of AI".
- Says it won't sell user data; DMOs get access to their own data [verified].

**Rubric:** P1–P2, G2, B1 (B2 via Ripe for some DMOs), L2 (chat on messaging apps).

**Data angle:** DMO first-party content is a credible route to hyperlocal and verified information, though it is promotional by nature [inferred].

### 2.10 Wanderlog (YC; popular manual planner with AI layered on)

**What it is**
- Collaborative planner with map plus list, drag-and-drop, route optimisation, offline mode, Google Maps export, and flight and car deals.
- **Reservation import from Gmail** and forwarding [prior].
- AI assistant: Pro is $39.99 a year with no monthly option. The free tier has capped AI (one source says 5 messages) [review].
- 2026 comparisons describe the AI trip builder as capped on free and "better as a refinement tool". They rate its map interface and group collaboration highest [review, mostly competitor blogs]. No 2026 Wanderlog AI launch was found.

**Rubric**
- P1–P2.
- **G3–G4** (opening hours, route optimisation, distances and times between stops).
- B1 (hotel affiliate).
- L1 (offline).
- Editing and collaboration: best in class.

**Weakness:** AI is an add-on, not the core; recommendation quality is generic [review/inferred].

### 2.11 Wonderplan

- A free generator. It factors travel time between locations and estimated transport and entrance costs [review].
- Fast first drafts. Weak on complex or group trips and shallow on detail about places [review].
- Pricing is inconsistent across 2026 sources.
  - A MonkeyTravel review (Jul 2026) says it is free with no paywall on core features, but that free-tier limits shifted during 2026.
  - Earlier analyses put day-by-day detail behind a premium of about $49 a year [review].
- Rubric: P1, G3, B0–B1, L0.
- Thin coverage, with a Trustpilot rating based on one review.

### 2.12 Trip Planner AI (tripplanner.ai)

- Free plus a premium tier. Directories list "Free + Premium". The one price found ($9 a month, InsideA) appears to be mixed up with Wonderplan's listing, so no reliable price is known [review].
- Built-in maps with routes, a day-by-day planner, editable and shareable schedules, PDF export, and a library of public itineraries [review].
- Rubric: P1, G2–G3, B1, L1.
- One directory confuses it with "Layla (formerly Trip Planner AI)". Unverified.

### 2.13 Wanderboat (founded by ex-Bing search scientists)

- Repositioned in **Jan 2026 as an "AI-powered local discovery platform"** with an AI Concierge, a "Hands Off" mode that builds journey blueprints, a community of shared itineraries, and an AI tour guide [press release/review].
- Funding unclear: the $23.84M figure on CB Insights is listed under "uta-ai", so treat it as unverified.
- 2026 status [review/claimed]:
  - a free iOS and Android local-discovery app covering dining, nightlife, events and outdoors, linking out to reservation and delivery services;
  - live in New York, Los Angeles, San Francisco, Chicago and Boston;
  - HQ in Sunnyvale, founded 2023, 2–10 employees (RankMyAI);
  - ran a holiday ad campaign across the SF BART system.
  - It is now closer to a city-discovery app than a trip planner.
- Rubric: P2, G2, B0–B1, L2.
- Limited booking integrations [review].

### 2.14 iMean

- A chat planner for flights, hotels and itineraries. Pitched for complex multi-origin group trips, with a Chrome extension that works across 100+ booking sites. Some describe it as a "Language-Action Model" agent that executes bookings in the browser.
- Product Hunt launch Apr 2025. Trustpilot 3.2.
- Booking partnership claims are unverified [review/claimed].
- 2026 coverage is directory-only [review].
  - One tutorial says "Book Now" **redirects to the airline or hotel partner with details pre-filled**, so it is a hand-off, not an in-product booking.
  - It also claims post-booking monitoring of flights and stays for changes.
  - A ranking site lists 51–200 employees, US-based.
  - No primary source was found.
- Rubric: P2, G2, B1 (hand-off; the browser-agent booking claim is unverified), L0–L1.

### 2.15 Holiwise (London; founded 2024; €1.45M pre-seed, Aug 2025)

- An "AI-powered travel agency" for premium travel. Funds go to its AI travel agent, **dynamic packaging** and a **premium human concierge** [verified].
- Investors include execs from Bank of America and DHL (DHL's exec joined the board). Bobby Previti (Bank of America) led the round [verified, startup press].
- Founders: Albin Eriksson Lippe and Kristian Lexeklint (Swedish). Initial focus is **Europe and the Middle East**, from a London base [verified].
- **ATOL:** Holiwise's trust-and-safety page lists **ATOL No. Y6864**.
  - The page I found was on a dev subdomain.
  - The same number is also presented as an ABTA number, which is unusual because the two are separate schemes.
  - I couldn't check it against the CAA's ATOL register [claimed, unverified].
- The FAQ says Holiwise is currently free to use. One review site mentions a Premium concierge tier [claimed/review].
- No 2026 launch or funding news was found.
- Rubric: P2–P3, G2–G3, B2–B3 (packaging), L2. If the ATOL claim holds, Holiwise is the only AI-native consumer player here offering UK package-style financial protection. That would be **above-average accountability** [inferred].

### 2.16 Stippl (Amsterdam)

- A social, visual trip planner with a drag-and-drop timeline, AI planning and trip sharing. About 250k users in 160 countries.
- Pre-seed rounds totalling about €1–1.3M (latest disclosed 2024) [verified].
- No 2026 raise found (re-checked Nov 2026).
- **No social-import feature (Instagram/TikTok → itinerary) was found.** Stippl's social features run the other way [claimed, stippl.io]:
  - **Travel Reels** turn the itinerary's map data plus trip-journal photos into a 3D reel to post on Instagram Reels, TikTok or YouTube Shorts (free);
  - a creator programme makes branded reels from itineraries.
- Other features: reservation and document **forwarding import** (app v2.0.24), a scratch map, and AI day-by-day generation from a description [claimed].
- Premium is about **€24.99 a year** (Stippl's own comparison blog) [claimed].
- Rubric: P1–P2, G3, B1, L1. Strong editing.

### 2.17 Pilot (Vancouver; launched 2023)

- A social, group trip planner. AI day-by-day itineraries, co-planning, and **in-app hotel booking at private rates**. Revenue comes from hotel bookings, "not sponsored placement" [claimed].
- Claims 23k+ travellers. Third-party install data is much lower (Android about 1.7K, iOS about 450 in one tracker).
- Publishes a "for AI assistants" page and many competitor-comparison SEO pages.
- Founders: Connor Wilson, Yu-Wei Hung and Avinash VK [claimed, About page].
- Pricing: the planner is free; sourcing group hotel rates costs $0; the business planner is pay-what-you-want. It promises "no sponsored results, no upsells, no hidden fees" [claimed].
- Published a 2026 "booking and planning" report (Apr 2026), which it says draws on a two-year study of 40,000 travellers using its own app data [claimed].
- Trustpilot score is 3.5/5 from 11 reviews. One Feb–Mar 2026 review alleges a charge for a stay whose booking status was unclear [review].
- Rubric: P2, G2–G3, B2 (hotels), L1.

### 2.18 Social-to-itinerary specialists (2025–2026 wave)

| Tool | Mechanism | Output | Evidence |
|---|---|---|---|
| Mindtrip Start Anywhere | Photo, URL, TikTok/YouTube, PDF or Google Maps list → LLM plus Mindtrip place data | Chat, collection or itinerary, bookable | [verified] |
| Airial | TikTok/Instagram links → logistics-aware plan | Multi-city plan with transit | [verified/claimed] |
| Plotline (iOS) | Share sheet → extracts every place mentioned and pins it on a map | Route-optimised plan from saves plus AI suggestions | [claimed] |
| Triply Planner | IG, TikTok, YouTube or screenshot saves → day-by-day itinerary with routes | Web, iOS, Android | [claimed] |
| feedtrip | Paste link → extract restaurants, cafés, landmarks → map → day plan | Free | [claimed] |
| Strollio | Reels, TikToks, screenshots → map plus flexible itinerary | — | [claimed] |
| ReelTravel | Share reel → research → map | Few ratings | [claimed] |
| Layla | Video and creator content (Beautiful Destinations) in the planning chat | — | [verified, terms] |
| Tripadvisor (demo, Nvidia GTC 2026) | Video → find featured places → cross-reference with Tripadvisor data → itinerary | Experimental | [verified] |
| Also named | Rhyme, DocentPro, Yaay, Map Your Voyage | — | [review] |

**Observation [inferred]:**
- Extracting places from video is now commoditised: there are 8+ apps and an OTA demo.
- Nobody publishes accuracy for entity resolution, meaning how reliably a TikTok mention gets matched to the right place ID and checked that it is still open.
- Nobody uses the creator's *context*: why the place was recommended, the time of day, the dish to order.

### 2.19 Group-planning AI tools

- **Plan Harmony** (v2.0 with an AI planner, Feb 2025): shared calendar, expense tracking, activity voting, "off-the-beaten-path" suggestions [claimed].
- **Hoku**: real-time collaboration and expenses.
- **Voyagr**: analyses group-chat conversations to recommend [review].
- Mindtrip Group Chat and Wanderlog collaboration remain the reference products.
- **JourneAI** is single-user and in free beta (listing dated late 2024) [review].
- Re-checked Nov 2026: **no 2026 news, pricing or status updates were found for Plan Harmony or JourneAI** [verified absence]. Treat both as dormant or very small.
- **Boardwalk:** I couldn't find any AI trip planner by this name.

### 2.20 Advisor-centric AI (the accountability benchmark)

- **Fora**:
  - AI-powered host agency; raised a $60M Series D at a **$1B valuation** (Jul 2026, Forerunner and Tactile).
  - Its AI "Via" helps human advisors research and build itineraries [verified].
- **Tern**:
  - Advisor operating platform; $13M Series A (May 2025); about $17M total.
  - 2026 agentic AI triages advisor inboxes, drafts cruise proposals and client messages, and **flags missing transfers or lodging gaps before an itinerary is sent**. Nothing goes out without the advisor's approval [verified].
  - Claims its advisors went from $100M to $2B in travel sales in 12 months [claimed].

**Lesson [inferred]:** the market is paying unicorn multiples for *AI + accountable human*, not for pure AI planners.

### 2.21 Other 2026 entrants and signals

- **Vuelo** (London): £56M seed for an AI-native travel booking plus **financing** platform [verified, fintech press].
- **Voyagier** (Baltimore): AI luxury platform; $1.25M raised at a $7M valuation; raising a seed round in late 2026 [verified].
- **BizTrip AI**: corporate agentic AI; $2.5M pre-seed total; Hot 25 2026 [verified].
- **PhocusWire Hot 25 for 2026** (published Nov 2025) is dominated by AI infrastructure rather than consumer planners:
  - DirectBooker: AI-native, supplier-aligned hotel aggregator from ex-Google Travel and Tripadvisor staff.
  - Kismet: AI-facing storefronts for hotels.
  - Kaiban: AI agent management for airlines.
- **PhocusWire Hot 25 Travel Startups for 2027** (published 9 Nov 2026; the ninth cohort; the previous eight cohorts raised about $4.1B) [verified].
  - Confirmed honorees: **Odessia** (acquired by OpenAI the next day), **Folio** (hospitality financial operations) and **OneJourney** (hospitality payments).
  - I couldn't retrieve the full list. Check it for any other consumer AI planners.
- **Tryp.com** (Copenhagen):
  - a multi-modal booking platform with a 24/7 AI travel companion called "Sandra";
  - $1.9M seed (Oct 2026) led by Point Capital Partners, $5.9M raised in total [verified, FinSMEs];
  - relevant to the rail and ground-transport gap (gap 3 in §5).
- **Chaty AI**: $1.15M seed, but it sells an AI assistant to tour and activity operators (B2B), not to travellers [verified, PhocusWire].
- **Veeza AI** (YC F26, per a third-party page): agentic visa applications [review]. No other 2026 YC consumer trip planner was found.
- **Product Hunt 2026 AI-planner launches** are all tiny: Trip Planner: AI Travel Guide (11 Jan), Lowkeytion (24 Jan), Vacay (11 Feb), Wanderloom, ChillTrip ("adapts plans when travel changes"), RabbitTravel [claimed]. None showed meaningful traction.
- **Funding climate** is a multi-year low:
  - Skift counted 57 travel funding rounds in Q3 2026, against 75 in Q2 and 110 in Q1;
  - Crunchbase data puts the Jan–Sep 2026 total at $2.2B [verified, press].
- **TripAgent.ai**: its marketing page (Jul 2026) claims automatic rebooking of cancelled or badly delayed flights [claimed, unverified]. It is the only consumer L4 claim found.
- **Tripadvisor**: no acquisition found. It built an OpenAI-powered itinerary generator and a ChatGPT app, and demoed video-to-itinerary at GTC 2026 [verified]. See file 02, §3.6, for its 2026 strategy.
- **Tripnotes** (founded 2023 by Matthew Rosenberg; generated 40k itineraries on its first day) [review]:
  - a 2026 review on a competitor's blog (iWeaver) says the web version has stopped and the product lives on mainly as a mobile app for organising inspiration and notes;
  - the same review claims it was "acquired by Dorsia" (unconfirmed);
  - directory listings still describe a web itinerary generator.
  - Status is unclear. It is probably no longer a meaningful AI-planner competitor [inferred].
- **Vacay**: several unrelated products share the name.
  - A Product Hunt "Vacay" AI planner launched on 11 Feb 2026.
  - An iOS "swipe-first" planner is priced from $49.99 a year (iTechGuides scores its editor 3.0/10).
  - usevacay.com is a web chatbot with advisor tools.
  - Layla's tier list quotes $9.99 a month.
  - None is a meaningful competitor [review].
- **Navi**: no AI trip planner by this name was found. The closest is "Navica", a Product Hunt listing with 11 followers [verified absence].
- **Couldn't verify or find:** "Iris" and other Mozio-type AI ground-transport planners. Mozio itself is a B2B ground-transfer aggregator API [prior] and is better treated as a supply partner than a competitor.

---

## 3. Comparison table (shared rubric)

P = personalisation, G = itinerary granularity, B = booking depth, L = live/on-trip.

| Product | Status (Nov 2026) | Model | P | G | B | L | Data grounding | Editing / collab | Accountability |
|---|---|---|---|---|---|---|---|---|---|
| Mindtrip | Active, growing B2B; no 2026 round | Free consumer; affiliate/transaction; DMO SaaS | P3–4 | G3 | B2–3 (flights May 2026 + Stays hotels Jul 2026) | L2–3 | "Thousands of sources"; Sabre for air; Expedia/Booking/Priceline/Agoda/Nuitee for hotels; DMO content | Collections, group chat, likes and comments | None published; Sabre servicing |
| Layla | Acquired by Expedia (Jul 2026); standalone, no changes announced | Freemium ($49/yr); human-expert booking; packages? | P2–3 | G2–3 | B2 (human-completed) | L2 | Skyscanner, Booking.com, Beautiful Destinations | Weak (no manual editor) | Human experts; liability capped |
| Lola | Launched Sep 2026 (Booking Holdings); US-only; $100M conditional commitment | Free / $5 (Plus reportedly ended 5 Nov) / $25 a month; no ads | P3 | G2–3 | B3 (now incl. flights via Duffel) | L2 | Booking.com, Agoda, Priceline, KAYAK, OpenTable, FareHarbor, GYG, Duffel; Gmail, Google Calendar | Itinerary sharing | Ten Group human concierge (paid) |
| Vayo | Private beta (Oct 2026); flights/hotels booking not yet shipped | TBD; Booking-funded | P4 | G1–2 | B1–2 (restaurants via OpenTable; flights/hotels hand-off) | L3 | Inbox confirmations, incl. non-Booking bookings | Group planning promised | Unknown |
| Odessia | **Shut down; acquired by OpenAI (Nov 2026)**; Hot 25 for 2027 | IATA agency commissions | P3 | G3 | B3 | L3 | Agency rates; wholesaler | — | Wholesaler support; service ended |
| Airial | Active, $3M seed (no 2026 news) | Free; affiliate likely; B2B | P2 | **G4** | B1 | L0–1 | Multi-modal routing (sources undisclosed) | Shared editing, comments | None |
| Stardrift | Active, YC/BCV; iOS app | Free | P3–4 | G2–3 | B1–2 (checkout undocumented) | L2 | Live prices incl. Amtrak; calendar | Limited | Unknown |
| Axel | Active (Gordian) | Free per FAQ vs $35/yr per Trustpilot profile; private-rate margin | P2–3 | G1 | B2 (+partial B4) | L3 | Private/net rates; air ancillaries APIs | — | Price-drop refunds |
| GuideGeek | Active; DMO white label (no spin-out found) | B2B SaaS | P1–2 | G2 | B1–2 (Ripe) | L2 | DMO first-party content | — | DMO-branded |
| Wanderlog | Active | Freemium ($39.99/yr) | P1–2 | G3–4 | B1 | L1 | Google-style place data; Gmail import | **Best** (drag-and-drop, real-time) | None |
| Wonderplan | Active | Free (limits shifted in 2026; earlier ~$49/yr premium claims) | P1 | G3 | B0–1 | L0 | Undisclosed | Basic | None |
| Trip Planner AI | Active | Free + premium (price unknown) | P1 | G2–3 | B1 | L1 | Undisclosed | Editable, PDF | None |
| Wanderboat | Active; local-discovery app in 5 US cities | Free | P2 | G2 | B0–1 | L2 | Search/community | Community sharing | None |
| iMean | Active, small (directory-only coverage) | Freemium | P2 | G2 | B1 (partner hand-off) | L0–1 | Live web via extension | — | None |
| Holiwise | Active, pre-seed (no 2026 news) | AI agency, packages, concierge; free per FAQ | P2–3 | G2–3 | B2–3 | L2 | Dynamic packaging | — | Human concierge; **ATOL claimed** (unverified) |
| Stippl | Active | Freemium (~€24.99/yr Premium) | P1–2 | G3 | B1 | L1 | Undisclosed; forwarded reservations | Drag-and-drop, social, Travel Reels export | None |
| Pilot | Active, small | Hotel commission; "no sponsored results" | P2 | G2–3 | B2 (hotels) | L1 | Private hotel rates | Group co-planning | None (Trustpilot 3.5, 11 reviews) |
| Tryp.com | Active, $5.9M raised (Oct 2026 seed) | Booking commissions | — | G3–4? | B2–3 (multi-modal) | L2–3 ("Sandra" 24/7 AI companion) | Multi-modal supply (undisclosed) | — | Unknown (thin coverage) |
| Social-to-map apps (Plotline, Triply, feedtrip, Strollio) | Active, early | Free / freemium | P1–2 | G2–3 | B0 | L0–1 | Place extraction from video | Map-based | None |
| Fora (reference) | $1B unicorn | Advisor commissions | P4 (human) | G5 (human) | B4 (human) | L4 (human) | GDS and supplier partners | Advisor-led | **Licensed human advisor** |
| Tern (reference) | Active | Advisor SaaS | — | G4–5 | B2–4 | — | Supplier data; gap-checker | Advisor tools | Advisor approval gate |

**Reading the table [inferred]:**
- **No AI-native consumer product combines G4+, B3+ and L3+ in one place** (re-checked Nov 2026).
- G4 (Airial, Wanderlog) does not come with booking.
- B3 (Lola, now with flights; Mindtrip with flights plus Stays) does not come with verified routing granularity. Tryp.com claims multi-modal booking plus an AI companion, but evidence is thin.
- L3 (Vayo, Axel, Mindtrip agents) is limited to monitoring prices and schedules, with no re-planning.
- G5 and L4 exist only where a human advisor does the work (Fora, Tern).

---

## 4. Patterns: how the leaders solve each known problem

| Problem | Best current mechanism | Who | Depth |
|---|---|---|---|
| (1) Generic, cliché picks | DMO first-party content (local businesses, events); social and creator video ingestion; community itineraries | Mindtrip DMO, GuideGeek, Wanderboat, social-to-map apps | Shallow. DMO content is promotional and biased toward members. Creator ingestion extracts *names*, not *reasons*. Nobody exposes "why this pick" provenance or a locals-only signal [inferred]. |
| (2) Booking interoperability | GDS (Sabre Mosaic) plus wallet (PayPal); OTA family inventory (Booking Holdings, Expedia); IATA agency licence; browser agents; MCP endpoints | Mindtrip, Lola, Layla/Expedia, Odessia, iMean, Stardrift, Axel | Flights and hotels are covered. Duffel is now a common flight rail: Lola, and Meta Muse per file 02. **Trains, local transit passes, ferries, restaurant and activity bookings stitched into one itinerary-level checkout are missing.** Lola comes closest. |
| (3) Stale data / hallucination | Live pricing APIs; Sabre real-time availability; Tripadvisor data cross-referencing; DMO-curated listings | Mindtrip, Layla, Lola | No product publishes a freshness timestamp, a verification status per place, or an opening-hours check against a source of truth. Hallucinated hotels and closed restaurants still occur at the category leader [review]. |
| (4) Accountability / support | Human expert booking (Layla); outsourced concierge (Lola via Ten Group); premium concierge (Holiwise); price-drop refunds (Axel); advisor-in-the-loop (Fora, Tern) | — | Terms universally disclaim (Layla: the chatbot cannot bind; liability capped). No AI-native product offers a published itinerary guarantee or a 24/7 disruption desk. The only package-protection signal is Holiwise's displayed ATOL number, which is unverified. The Odessia shutdown shows the risk. |

---

## 5. Ranked gaps and exploitable opportunities

1. **An accountable "itinerary-level guarantee" with a 24/7 disruption desk (L4 + B4).**
   - Nobody AI-native owns the outcome. Terms disclaim; concierge is paid and add-on (Lola); human booking is a hand-off (Layla); Odessia died with live bookings.
   - Opportunity:
     - become the merchant of record or package organiser (EU PTD / UK ATOL style) for AI-built trips;
     - publish an SLA;
     - pair agentic monitoring (as Vayo and Axel do) with automatic re-planning of the *downstream* itinerary. A delayed flight should cascade to the hotel check-in note, the dinner reservation and the train ticket.
   - Fora's $1B valuation shows the market pays for accountability.

2. **Verifiable freshness: per-item provenance and "last verified" metadata.**
   - Hallucinated hotels and closed venues persist even at Mindtrip. No one shows sources or verification timestamps, and there is no independent benchmark.
   - Opportunity:
     - every place resolves to a canonical ID (Google, Foursquare, OSM or an operator ID);
     - every itinerary is checked against hours, closures and holidays at generation time *and* again 24h before;
     - a visible "verified on {date} via {source}" badge;
     - publish an accuracy benchmark and turn it into marketing.

3. **Door-to-door G5 including ground transport and rail ticketing.**
   - Airial does multi-modal routing (G4) without tickets. Mindtrip and Lola book air, hotels and restaurants but not trains, ferries, transit passes or transfers.
   - Opportunity: integrate rail (Trainline/Silvercore/national operators), ferries, transfers (Mozio-type APIs) and real-time GTFS-RT, with buffer-aware timing and one checkout.

4. **Hyperlocal intelligence beyond "places named in a TikTok".**
   - Social-to-itinerary is commoditised (8+ apps). The value lost is the *context*: the dish, the time of day, the local tip, recency, and creator credibility.
   - DMO content is promotional.
   - Opportunity:
     - a hyperlocal knowledge graph that stores *why* and *when* for each pick, with source attribution;
     - recency-weighted local signals (local-language reviews, local press, local creator networks);
     - a "tourist-trap score"; and preference for neighbourhood-level picks over hero sights.

5. **Learning profile + neutral ranking (P4 without OTA bias).**
   - The leading AI planners are now owned by OTAs (Expedia/Layla, Booking/Lola and Vayo) or by OpenAI (Odessia). Critics already flag self-preferencing and double-dipping.
   - Mindtrip's memory is new and unproven. Stardrift and Vayo learn only from calendar and inbox.
   - Opportunity:
     - an independent, transparent ranking ("no paid placement", as Lola claims, but across *all* suppliers);
     - a portable, user-owned travel profile that learns from past trips, bookings, loyalty programmes and saves;
     - real edit controls: lock items, hard constraints (dietary, mobility, pace) that the AI must respect. One reviewer saw Mindtrip ignore dietary preferences.

Honourable mentions:
- **Group decision-making.** Voting, budget reconciliation and preference balancing exist piecemeal: Mindtrip Group Chat, Plan Harmony, Voyagr.
- **Distribution via AI assistants.** Axel's MCP server and Pilot's "for AI assistants" page show planners positioning as tools *inside* ChatGPT, Gemini and Claude, which matters now that OpenAI has bought Odessia.
- **B2B white label.** Mindtrip and GuideGeek prove DMOs pay. TripCreator offers true unbranded white label; Mindtrip apparently doesn't.

---

## Sources

- Mindtrip press page: https://mindtrip.ai/press
- Sabre: Mindtrip Flights launch: https://investors.sabre.com/news-releases/news-release-details/mindtrip-launches-travels-first-all-one-agentic-ai-flight
- Mindtrip Personal Travel Assistant (PR): https://www.morningstar.com/news/pr-newswire/20260930ph59638/mindtrip-launches-personal-travel-assistant-that-knows-the-traveler-not-just-the-trip
- Mindtrip PTA (Yahoo): https://finance.yahoo.com/technology/ai/articles/mindtrip-launches-personal-travel-assistant-123400314.html
- Travel and Tour World on the Mindtrip PTA: https://www.travelandtourworld.com/news/article/274ga1edrk9e/
- Mindtrip Europe: https://www.phocuswire.com/news/startups/mindtrip-expands-europe-dmos-ai-trip-planning
- Mindtrip Norway: https://mindtrip.ai/press/mindtrip-partners-with-norway-by-locals-to-power-ai-driven-discovery-across-norways-29-destination-regions
- Meet Boston × Mindtrip: https://www.prnewswire.com/news-releases/meet-boston-partners-with-mindtrip-to-deliver-personalized-ai-trip-planning-timed-to-fifa-world-cup-2026-302814280.html
- Meet Minneapolis × Mindtrip: https://www.prnewswire.com/news-releases/mindtrip-partners-with-meet-minneapolis-to-power-ai-driven-trip-planning-across-the-city-of-lakes-302867099.html
- Kentucky × Mindtrip: https://www.prnewswire.com/news-releases/mindtrip-teams-up-with-the-kentucky-department-of-tourism-to-reimagine-how-travelers-discover-the-bluegrass-state-302936706.html
- Mindtrip for destinations: https://mindtrip.ai/business/destinations
- Mindtrip DMO playbook: https://resources.mindtrip.ai/business/dmo-playbook/mindtrip-launch-toolkit
- Sabre/PayPal/Mindtrip (AltexSoft): https://www.altexsoft.com/travel-industry-news/sabre-paypal-power-ai-bookings-flights-q2-2026/
- Sabre/PayPal/Mindtrip (PayPal newsroom): https://newsroom.paypal-corp.com/2025-02-12-Sabre-PayPal-and-Mindtrip-Partner-To-Deliver-the-Industrys-First-End-to-End-Agentic-AI-Experience-for-Travel
- Mindtrip in-chat flights (AltexSoft): https://www.altexsoft.com/travel-industry-news/mindtrip-adds-in-chat-flights-as-ai-moves-to-action/
- Mindtrip Start Anywhere (TechCrunch): https://techcrunch.com/2024/07/31/travel-startup-mindtrips-new-feature-lets-you-build-an-itinerary-from-a-screenshot-youtube-or-tiktok-video
- Mindtrip Start Anywhere (Axios): https://www.axios.com/2024/07/31/ai-trip-planner-travel-itinerary-mindtrip
- Mindtrip funding (PhocusWire): https://www.phocuswire.com/mindtrip-ai-travel-planning-capital-one-ventures-united-airlines-ventures
- Mindtrip $12M round (Skift): https://skift.com/2024/09/17/mindtrip-raises-12-million-in-tough-funding-environment-for-ai-trip-planners/
- Mindtrip Group Chat launch: https://globetrender.com/2024/09/24/mindtrip-launches-group-chat-feature/
- Mindtrip about page: https://mindtrip.ai/about
- Mindtrip review: https://aitravel.tools/mindtrip-review/
- Layla vs Mindtrip vs Wonderplan test: https://aitravel.tools/layla-vs-mindtrip-vs-wonderplan/
- Best AI trip planners tested (GuruWalk): https://www.guruwalk.com/mkt/best-ai-for-travel-planning
- Mindtrip and dietary preferences: https://www.newwinningcasinos.com/2026/08/10/why-does-mindtrip-ai-ignore-dietary-preferences-in-itinerary/
- Expedia IR: Layla acquisition: https://ir.expediagroup.com/news-and-events/news/news-details/2026/Expedia-Group-acquires-Layla-accelerating-its-AI-powered-trip-planning-and-booking-strategy/default.aspx
- Skift: Expedia acquired Layla: https://skift.com/2026/07/31/expedia-acquired-ai-trip-planner-layla-exclusive/
- WiT on the Layla acquisition: https://www.webintravel.com/expedia-group-acquires-layla-to-bolster-its-ai-powered-trip-planning-and-booking-strategy/
- Layla terms: https://layla.ai/terms
- Layla "best AI travel agent" blog post: https://layla.ai/blog/news-and-tips/best-ai-travel-agent
- Layla review (Endless Travel Plans): https://www.endlesstravelplans.com/guides/planning-tools/layla-ai-review
- Layla review (MonkeyTravel): https://monkeytravel.app/blog/layla-ai-review-2026
- Layla review (Stardrift): https://stardrift.ai/resources/layla-ai
- Layla review (aitravel.tools): https://aitravel.tools/layla-ai-review/
- Layla acquisition, traveller view (Ribbit): https://tryribbit.com/blog/layla-ai-was-acquired-by-expedia-heres-what-that-means-for-travelers
- OpenAI acquires Odessia (Skift): https://skift.com/2026/11/10/a-year-after-sonders-collapse-francis-davidson-sells-his-ai-travel-startup-to-openai/
- OpenAI acquires Odessia (PhocusWire): https://www.phocuswire.com/news/startups/openai-acquires-ai-travel-agent-odessia
- OpenAI acquires Odessia (The Next Web): https://thenextweb.com/news/openai-acquires-odessia-ai-travel-agent
- Odessia service closure: https://www.beri.net/article/openai-odessia-acquisition-travel-agent-service-shut-down-gmail-access-bookings-customer-continuity
- Odessia and the IATA licence: https://daily.dev/posts/odessia-s-real-trick-isn-t-the-ai-it-s-the-travel-agent-license-hawh3vt8j
- Odessia $6M funding announcement: https://www.phocuswire.com/odessia-ai-trip-planner-funding-sonder
- OTA shares after the Odessia deal: https://www.pymnts.com/news/artificial-intelligence/2026/online-travel-agencies-shares-drop-following-openai-acquisition-of-travel-startup-odessia/
- Lola launch (Skift): https://skift.com/2026/09/29/kayak-co-founders-launch-lola-booking-holdings-new-ai-assistant-exclusive/
- Lola launch (PhocusWire): https://www.phocuswire.com/news/technology/steve-hafner-paul-english-launch-ai-assistant-lola
- Lola launch (Engadget): https://www.engadget.com/2271730/lola-is-bookingcoms-new-ai-travel-agent/
- Lola launch blog post: https://lola.com/blog/lola-launches-ai-powered-experiences-memberships-and-new-partners
- Lola critique (Hospitality.today): https://www.hospitality.today/article/booking-com-now-gets-paid-by-both-sides
- Lola early scoop (Skift): https://skift.com/2026/05/06/kayak-co-founders-reunite-booking-holdings-agentic-ai-startup-lola-scoop/
- Vayo launch (GeekWire): https://www.geekwire.com/2026/booking-holdings-unveils-ai-travel-startup-vayo-based-in-seattle-with-a-planned-100m-investment/
- Vayo launch (Skift): https://skift.com/2026/10/14/booking-holdings-second-ai-startup-vayo-launches-in-private-beta/
- Airial (TechCrunch): https://techcrunch.com/2025/06/30/former-meta-engineers-airial-travel-tool-helps-travelers-solve-logistics-planning-with-ai
- Airial transit blog post: https://airial.travel/blog/?p=361
- Airial (Tracxn): https://tracxn.com/d/companies/airial-travel/__wiwzmETPxRWgi4w_-s2mWC8U7qWrW1lsLtxZafduVew
- Airial review (AIChief): https://aichief.com/ai-business-tools/airial/
- Stardrift launch post (X): https://x.com/leilavclark/status/1996641098916327724
- Stardrift (Crunchbase): https://www.crunchbase.com/organization/moonglow
- Stardrift × Kernel: https://www.kernel.sh/customers/stardrift
- Stardrift (SaaSworthy): https://www.saasworthy.com/product/stardrift-ai
- Axel (YC launch): https://www.ycombinator.com/launches/WAo-axel-ai-travel-agent-that-saves-you-money-on-flights-and-hotels
- Axel FAQ: https://helloaxel.com/en/faq/is-axel-a-travel-agent
- Axel MCP server: https://mcpservers.org/servers/helloaxel-com-en-ai-api
- GuideGeek for destinations: https://guidegeek.com/destinations
- GuideGeek × Colorado: https://brands.guidegeek.com/press/colorado-tourism-office-partners-with-guidegeek-to-launch-new-ai-travel-genius-colorado-concierge
- Ripe × GuideGeek: https://www.breakingtravelnews.com/news/article/ripe-and-guidegeek-announce-partnership-to-power-ai-driven-real-time-bookin/
- Skift on AI and DMOs: https://skift.com/2024/11/14/ai-could-be-an-existential-threat-to-dmos-how-some-are-getting-ahead-of-the-curve
- Wanderlog alternatives (MonkeyTravel): https://monkeytravel.app/blog/wanderlog-alternative-2026
- Stippl vs Wanderlog: https://www.stippl.io/blog/stippl-vs-wanderlog
- Wonderplan review (iWeaver): https://www.iweaver.ai/guide/wonderplan-ai-review-best-ai-travel-planner-alternative/
- Trip Planner AI review (MSPowerUser): https://mspoweruser.com/trip-planner-ai-review
- Wanderboat (Travolution): https://www.travolution.com/news/technology/wanderboat-launches-ai-travel-companion/
- Wanderboat (CB Insights): https://www.cbinsights.com/company/uta-ai
- iMean (Product Hunt): https://www.producthunt.com/products/imean-ai-travel-planner/launches
- Holiwise funding (tech.eu): https://tech.eu/2025/08/26/holiwise-raises-eur145m-pre-seed-to-reinvent-premium-travel/
- Stippl funding (PhocusWire): https://www.phocuswire.com/stippl-funding-ai-travel-planning-expansion
- Pilot (TechCrunch): https://techcrunch.com/2023/09/28/pilot-is-a-social-travel-hub-that-uses-ai-to-help-you-plan-book-and-share-trips
- Pilot about page: https://www.pilotplans.com/about
- Pilot "for AI assistants": https://www.pilotplans.com/for-ai-assistants
- Social-to-itinerary apps compared (Map Your Voyage): https://mapyourvoyage.com/blog/best-apps-to-plan-trips-from-social-media
- Plotline: https://getplotline.app/
- Triply Planner: https://triplyplanner.com/
- feedtrip: https://www.feedtrip.app/
- Strollio: https://strollio.app/what-is-strollio
- Plan Harmony relaunch: https://www.travelmassive.com/posts/plan-harmony-revamps-trip-planning-with-new-design-and-ai-features-175907140
- Tern agentic AI launch: https://www.phocuswire.com/news/technology/tern-launches-agentic-ai-travel-advisor-efficiency
- Tern AI tools (Travel Weekly): https://www.travelweekly.com/Travel-News/Travel-Agent-Issues/Tern-launches-AI-tools-for-travel-advisors?ct=tech
- Tern Series A (Travel Weekly): https://www.travelweekly.com/Travel-News/Travel-Agent-Issues/Travel-agency-platform-Tern-secures-13-million-funding
- Fora unicorn round (TechCrunch): https://techcrunch.com/2026/07/16/ai-powered-travel-agency-fora-hits-unicorn-status-raises-60m/
- Vuelo funding: https://fintech.global/2026/03/25/vuelo-raises-56m-to-launch-ai-native-travel-booking-platform/
- Voyagier: https://technical.ly/entrepreneurship/voyagier-ai-travel-startup-seed-round/
- BizTrip AI funding: https://www.businesswire.com/news/home/20260202904313/en/BizTrip-AI-Raises-$1.5-Million-in-New-Pre-Seed-Funding
- PhocusWire Hot 25 for 2026: https://www.phocuswire.com/hot-25-travel-startups-2026
- Tripadvisor AI planning demo (PhocusWire): https://www.phocuswire.com/news/technology/tripadvisor-ai-travel-planning-tool
- Tripadvisor × OpenAI itinerary generator (Hotel Dive): https://www.hoteldive.com/news/tripadvisor-openai-ai-travel-trip-itinerary/688500/
- YC travel companies: https://www.ycombinator.com/companies/industry/travel-leisure-and-tourism
- Foursquare Places (POI data reference): https://docs.foursquare.com/data-products/docs/how-does-places-work

### Sources added in the gap-fill pass (17 Nov 2026)
- Lola flights and $100M commitment (PhocusWire): https://www.phocuswire.com/news/startups/bookings-lola-gets-flight-booking-capabilities-100-million-dollar-planned-investment
- Lola Plus ended (travelvoice.jp, single source): https://www.travelvoice.jp/20261110-160813
- Lola US-only (tbreak): https://tbreak.com/lola-ai-travel-agent-booking-holdings-launch/
- Lola and metasearch (TravelMole): https://travelmole.com/news/bookings-lola-ai-play-buried-metasearch
- Vayo launch, booking status (PhocusWire): https://www.phocuswire.com/news/startups/booking-holdings-launches-vayo-for-leisure-travel-planning
- Vayo (Travelers Today, 17 Oct 2026): https://www.travelerstoday.com/articles/61131/20261017/booking-holdings-plans-100m-vayo-ai-that-monitors-all-your-travel-bookings.htm
- Mindtrip Flights launch, 6 May 2026 (Skift): https://skift.com/2026/05/06/sabre-mindtrip-paypal-launch-agentic-ai-travel-booking/
- Mindtrip Stays (Hotel Management): https://www.hotelmanagement.net/tech/mindtrip-launches-ai-powered-hotel-search-booking-platform
- Mindtrip Stays (PR via Webull): https://www.webull.com/news/15231413233148928
- Mindtrip Stays page: https://mindtrip.ai/stays
- Mindtrip review roundup 2026 (MonkeyTravel): https://monkeytravel.app/blog/best-ai-trip-planners-2026-compared
- Odessia, Hot 25 for 2027 (PhocusWire): https://www.phocuswire.com/interviews/startups/hot-25-travel-startups-2027-odessia
- Hot 25 for 2027 list: https://www.phocuswire.com/news/startups/hot-25-travel-startups
- Folio, Hot 25 for 2027 (Hotel-Online): https://www.hotel-online.com/news/folio-named-one-of-phocuswires-hot-25-travel-startups-for-2027-amid-rapid-expansion-adoption-and-ai-innovation
- Stardrift for iOS (Product Hunt): https://www.producthunt.com/posts/stardrift-for-ios
- Stardrift overview: https://www.scriptbyai.com/ai-trip-assistant-stardrift
- Axel pricing FAQ: https://helloaxel.com/en/faq/how-much-does-axel-cost
- Axel (Trustpilot): https://ca.trustpilot.com/review/helloaxel.com
- Axel: cancel membership (help centre): https://help.helloaxel.com/en/articles/11429068-how-do-i-cancel-my-membership
- Axel (Fondo): https://fondo.com/blog/axel-brings-private-travel-rates-to-people-and-ai-assistants
- Axel (Luxury Travel Magazine): https://www.luxurytravelmagazine.com/news-articles/axel-introduces-an-ai-powered-way-for-travelers-to-get-money-back-when-prices-drop
- GWU media tip sheet: https://mediarelations.gwu.edu/node/16206
- GuideGeek (Wikipedia): https://en.wikipedia.org/wiki/GuideGeek
- Matador Network profile: https://yespress.io/matador-network
- Holiwise FAQ: https://holiwise.com/faq
- Holiwise trust and safety (dev subdomain): https://mapi-dev.holiwise.com/trust-and-safety
- Holiwise (PhocusWire startup stage): https://www.phocuswire.com/startup-stage-holiwise
- Stippl Travel Reels: https://app.stippl.io/travel-reel
- Stippl for creators: https://app.stippl.io/creators
- Stippl (App Store): https://apps.apple.com/gb/app/id6443617088?l=en-gb
- Pilot 2026 report: https://pilotplans.com/insights/2026-booking-planning
- Pilot (Trustpilot): https://se.trustpilot.com/review/pilotplans.com
- Wanderboat (Freedom251): https://freedom251.com/apps/wanderboat-ai/
- Wanderboat BART campaign: https://www.barchart.com/story/news/36780265/wanderboat-ai-takes-over-san-francisco-bart-system-with-holiday-season-advertising-campaign
- Wonderplan review 2026 (MonkeyTravel): https://monkeytravel.app/blog/wonderplan-review-2026
- Tripnotes review (iWeaver, competitor): https://iweaver.ai/guide/tripnotes-ai-review-and-best-alternative-ai-trip-planner
- Vacay (Product Hunt): https://www.producthunt.com/products/vacay/launches
- Vacay (iTechGuides): https://www.itechguides.com/products/vacay/
- Layla AI tier list (competitor content): https://layla.ai/blog/destinations/ai-trip-planners-tier-list
- Tryp.com seed (FinSMEs): https://www.finsmes.com/2026/10/tryp-com-raises-usd1-9m-in-seed-funding.html
- Chaty AI seed (PhocusWire): https://www.phocuswire.com/news/finance/chaty-ai-raises-seed-round-expand-ai-assistant-travel-experiences
- Travel tech funding 2026 (Tech Insider): https://tech-insider.org/travel-tech-funding-2-2b-302-rounds-multiyear-low-ai-2026/
- TripAgent.ai automated rebooking claim: https://tripagent.ai/automated-flight-booking
- American Airlines auto-rebooking (TravelPulse): https://www.travelpulse.com/news/airlines-airports/american-airlines-rebooking-tool-is-changing-passengers-flights-without-their-knowledge
- Greetwell AI hallucination survey (Stacker/KEYT): https://keyt.com/lifestyle/travel/stacker-travel/2026/09/16/survey-ai-hallucinated-travel-destinations-for-1-in-6-users/
- Five-model Tokyo test (talkory): https://www.talkory.ai/blog/best-ai-for-travel-planning-5-models-tested
