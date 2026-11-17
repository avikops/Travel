# Handoff: AI Trip Planner project (paste this into a new session)

You're continuing a personal project with me. Read this, then `research/REPORT.md` (the synthesis), and open `research/raw/*.md` only when you need detail.

## My goal
Build **the best AI trip planner, with no doubt about it.** The known problems with current AI trip planners:
1. **Generic, cliché picks.** The same common spots for everyone, with no hyperlocal knowledge.
2. **Poor interoperability.** They don't work with hotel, transport, activity and other booking and trip-management sites.
3. **Stale, poor-quality data.** This leads to hallucinations: closed places, wrong hours, invented places.
4. **No accountability.** Nobody supports the traveller when things go wrong.

The plan is to research the state of the art deeply first, find exactly where and how deep competitors' solutions go (personalisation, granularity, customisation, booking, live support), exploit the gaps, and then build.

## Repo
- **Repository:** GitHub `avikops/Travel`, branch `main`.
- **Layout:**
  - `research/REPORT.md`: synthesis v2, the main document.
  - `research/raw/01–07-*.md`: seven detailed research reports, about 70k words with sources.
    - 01: AI-native startups
    - 02: incumbents and AI platforms
    - 03: hyperlocal data and freshness
    - 04: booking infrastructure
    - 05: accountability and law
    - 06: traveller voice
    - 07: research frontier and market
  - `research/notes/*.md`: raw gap-fill notes with every URL.

## Done so far (Nov 2026)
- **Research pass 1:** 7 parallel agents covering startups, incumbents, data, booking infrastructure, accountability, users, and the research frontier and market.
- **Research pass 2:** about 350 searches that replaced recall-based claims with sourced facts and corrected the first pass. The corrections are listed in REPORT §13.
- **Spot-checks:** the 9 headline facts were independently re-checked.
- **Strategy drafted** in REPORT §7–§10:
  - **Positioning:** "the trip planner that stands behind its plan". The four pillars are verified plans (solver-checked feasibility and timestamped facts), real local taste (a licensed, attributed local corpus, plus an anti-cliché objective in the solver), whole-trip watch and repair, and someone accountable (an insurer-backed accuracy guarantee, a human desk, free compensation claims).
  - **Business model:** planning is free; revenue comes from a paid trip-protection product, commissions and B2B.
  - **Beachhead:** US travellers on multi-city Europe rail trips, group-first, with Japan next.
  - **Delivery plan:** a reference architecture (§8) and a phased build (§10).

## Key conclusions to keep in mind
- **No AI-native consumer product reaches G4+, B3+ and L3+ at once.** That means time-slotted routing with real transit, multi-supplier booking, and live alerts or rebooking, all in one product. G5 (door-to-door) and L4 (automatic disruption repair) exist only with human advisors, in corporate travel, or within one airline's own flights.
- **Solver-backed planning beats a model planning alone.** It passes 93.9% of the TravelPlanner benchmark versus 0.6%. No consumer product ships it.
- **Licensing shapes the data design.** Google, Yelp, Tripadvisor and Reddit data is walled off or licensed to the big AI labs, and Mapbox, HERE and TomTom don't give you a place database you can store. Build an owned base on open data (Overture, Foursquare's open places dataset, OpenStreetMap, tourism-board open data). Use Google live only to verify and display. License the local layer: Lonely Planet, Time Out, The Infatuation and Michelin have no AI deals yet.
- **Booking without airline-industry accreditation:** Duffel (identity checks only), LiteAPI, Viator, GetYourGuide, Tiqets, Distribusion, Trainline and Mozio. Restaurants are the most closed vertical. United and Delta are blocking unapproved AI agents, so use official APIs, agent payment tokens and explicit user approval for each purchase.
- **Users won't pay for planning; they pay for certainty.** 50% expect AI help to be free; about half of Hopper bookings attach a paid protection product.
- **Law (a lawyer is needed):**
  - The EU's revised package-travel directive (2026/1024) makes linked multi-supplier bookings a package, from about 2029.
  - The UK goes the opposite way from April 2027.
  - The UK competition regulator says businesses are liable for their AI agents.
  - The reformed EU flight-compensation rules (EU261) are adopted.
  - US seller-of-travel registration: California, Florida, Washington and Hawaii, plus Maryland's requirement of $1M in errors-and-omissions insurance.

## Remaining work
1. **Hands-on teardown of competitors.** This was blocked in the cloud session, which had no browser access to their sites. Run the 12-prompt test battery in REPORT §12 against ChatGPT, Gemini (AI Mode and Maps), Mindtrip, Lola, Airial, Wanderlog, Layla, Tryp.com, Stardrift and Wonderplan:
   - Use a browser (Playwright, or me signed in) to drive their flows, capture what they request and return, and score each against the rubric in REPORT §0.
   - Note what can be learned about their architecture from network calls.
   - Write the results to `research/raw/08-hands-on-teardown.md` and update REPORT §2 and §4.
2. **Fill the remaining unknowns in REPORT §11** using primary pages, which are now reachable:
   - Holiwise's ATOL number on the CAA register.
   - Axel pricing.
   - The merchant of record for Mindtrip Stays.
   - Whether Vayo books flights and hotels yet.
   - Whether Lola Plus has ended.
   - Duffel Stays approval steps.
   - Booking.com's AI-approval clause.
   - Host-agency API booking (Nexion, KHM).
   - Official Journal texts and dates for the package directive, EU261 and the AI Act.
   - Visa and Mastercard agent-liability rules.
   - Official affiliate rate cards.
   - Reddit and app-store review text.
   - Tests from The Verge, Wired, CNET, Condé Nast Traveler and The Points Guy.
3. **Then start building (REPORT §10 Phase 0–1).** Build the evaluation harness and a public "infeasible-day" and cliché benchmark across competitors, followed by the verified-planner MVP:
   - an open-data place graph;
   - a freshness ledger;
   - a CP-SAT/SMT solver plus a deterministic verifier;
   - a structured group plan editor;
   - Sherpa° entry rules.
   Start on one rail corridor (Paris–Amsterdam–Berlin).

## How I like to work
- Be direct; don't stop halfway.
- Use parallel long-running agents for big research, and have them save notes to files as they go so nothing is lost.
- If a limit is hit (for example the web-search cap of about 200 per turn shared across agents), work in waves instead of quitting.
- Commit and push to `main` as work completes.
- Tag claims [verified]/[claimed]/[inferred] and never fabricate.
