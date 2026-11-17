# 05 — Accountability, Support, Liability & Disruption Handling

*Research agent 5 of 7. Date: 2026-11-17. Not legal advice. Items marked "lawyer needed" call for qualified counsel in each jurisdiction.*

## 0. Method, confidence labels, and limits (read first)

- **Labels.** **[verified]** means I confirmed it this session in a primary or near-primary source (the official page or a quote from it surfaced in search). **[reported]** means it comes from secondary or trade press found this session. **[claimed]** means it is a company's own marketing or performance claim. **[prior]** means it comes from my training knowledge (cutoff mid-2026) and was **not re-verified this session**, so its current status may have changed. **[inferred]** means it is my analysis.
- **Tooling limits this session.** WebFetch could not reach any host (DNS blocked: mindtrip.ai, layla.ai, expedia.com, morganlewis.com all failed), so I could not read full ToS pages or rulings. I could only see the excerpts that search engines surfaced. The 200-search budget shared by all 7 agents also ran out after about 20 of my searches. As a result, these could not be re-verified this session and rest on [prior]: EU261 reform status, US DOT rules, the CMA guidance text, AI Act Article 50 timing, seller-of-travel statutes, insurers' fine print, and human-backed agencies' SLAs. **Before any of these feed a product or legal decision, re-check them with a follow-up search pass. They are listed in §10.**

---

## 1. Executive summary

1. **Every consumer AI trip planner disclaims accountability.** None that I found stands behind its itinerary. The standard approach has four parts: (a) "as is / as available" with no warranty of accuracy; (b) "we are not a travel agent, booking partner terms govern"; (c) liability capped or excluded for third-party and indirect loss; (d) support by email or chat only, with no rebooking power. Mindtrip, GuideGeek, Layla, Wanderlog, Expedia's AI terms and Google AI Mode all follow some version of this [verified/reported, §2].
2. **The law is moving the other way.** *Moffatt v Air Canada* (2024 BCCRT 149) held that a company cannot treat its chatbot as a separate entity and is liable for its negligent misrepresentations [verified]. The UK CMA reportedly said in March 2026 that businesses are responsible for their AI agents as they are for employees [reported]. The revised EU Package Travel Directive (provisional deal 2 Dec 2025; EP vote 12 Mar 2026; reportedly adopted as Directive (EU) 2026/1024) **abolishes "linked travel arrangements"** and widens the definition of "package." Separate traders' services booked through linked online processes, with data passed on and contracts concluded within 24 hours, become a package [verified for deal/vote; reported for final number]. **An AI planner that orchestrates multi-supplier bookings in the EU is at real risk of becoming an "organiser"**, with full performance liability and an insolvency-protection duty [inferred, lawyer needed].
3. **Industry now openly names "who pays when the agent is wrong?" as unsolved.** Skift ran "Trust fall" (Mar 2026) and the Decision Brief "Who's in charge when a trip goes wrong?" (Sep 2026). Morgan Lewis published "AI concierge services: who is liable when a bot books the wrong vacation?" (Aug 2026). Faye's co-founder argued that AI booking agents should carry E&O cover like human agents [reported]. Expedia research found that 66% would not trust an AI assistant to book on their behalf [reported].
4. **Real accountability today comes from humans plus money: card issuers, TMCs, human advisors and fintech guarantees.** Examples are Amex/Chase travel desks and card trip-delay insurance, Navan and TravelPerk 24/7 support, Hopper's Disruption Guarantee and CFAR, Airbnb AirCover, and Booking.com's price match [prior/reported]. These are funded by margin, subscription/annual fees or ancillary premiums, not by the AI.
5. **Gap.** No one offers an AI planner that (a) **guarantees** that the facts in its itinerary are correct (opening hours, last cable car, visa/ESTA, transfer feasibility) and pays if they are wrong; (b) **acts as one accountable party** across all bookings; and (c) **monitors the trip and actually rebooks** during disruption, with a human who has GDS access behind it. Slicktrip summarises the current market as "AI can book your flight but not rebook it" [reported].

---

## 2. What current AI trip planners actually promise

| Player | Role in transaction | Accuracy / AI disclaimer | Liability posture | Human support / disruption | Confidence |
|---|---|---|---|---|---|
| **Mindtrip** | Not a seller. ToS (rev. 1 May 2026) says it "does not sell any products or services directly"; bookings go via "Booking Partners" whose terms govern payment, cancellations, changes, refunds. Pestronk (Travel Weekly) reports the ToS says it does *not* act as travel agency, booking agent or tour operator; links route to Viator, Kayak, Klook | "THE SERVICE IS PROVIDED ON AN 'AS IS' AND 'AS AVAILABLE' BASIS"; reportedly disclaims any warranty that results will be accurate or reliable | Disclaims liability for payments "except where applicable law requires otherwise." The only cap found was in the *Creator* agreement (commissions paid in prior 6 months); consumer cap not confirmed | No evidence of disruption handling; partner handles | verified (as-is, partner model); reported (no-agent clause) |
| **Layla** (Expedia Group acquired it Jul 2026) | Layla AI GmbH (Berlin). Marketing mentions "human travel experts available for booking help and trip support" | Not retrieved | Terms (eff. 21 May 2025) reportedly cap liability as far as law allows and exclude indirect damages and damages from third-party integrations | Claimed human experts; scope unknown. Post-acquisition, likely to sit on Expedia's service stack [inferred] | reported/claimed |
| **GuideGeek** (Matador) | Info only | Chatbot ToS (eff. 7 Jan 2024): "Matador makes no claims or warranties as to the accuracy of information provided by Chatbot"; the bot cannot bind anyone to contract terms. Human curators review conversations. CEO claimed accuracy of about 98% | Folds in Matador general terms | No human escalation clause found | verified (quote) / claimed (98%) |
| **Wanderlog** | Planner; booking via affiliates | tosdr: "provided 'as is' and to be used at your sole risk"; terms amendable at any time; California courts | Standard | Email support [prior] | reported (tosdr) |
| **Wonderplan, Trip Planner AI** | Planners/affiliates | Could not retrieve | — | — | not found |
| **Expedia (AI Terms / Romie)** | Expedia is the OTA (agent or merchant, depending on product) | AI Terms: responses "generally based on publicly available information, the accuracy of which Expedia has not verified"; "no representations about the relevancy, accuracy, or completeness"; responses "do not necessarily reflect Expedia's views." Main ToS treats AI content as "as-is," with no responsibility for "use of or reliance on such content." Also: "we do not exclude our liability where we are not permitted to do so under the laws of your country of residence" | Section 8 of main ToS | 24/7 OTA service. Skift reports Expedia found the end-to-end Romie concierge impractical and shifted to multi-agent | verified (quotes via search) |
| **Booking.com AI Trip Planner** | Launched 2023 (US) on ChatGPT; deep-links into normal search. Booking.com is the agent for most stays | Disclaimer not retrieved | "We Price Match" refunds price difference (hotels; not flights or cars), claimable up to 24h before arrival | 24/7 CS [prior] | reported |
| **Kayak** (AI Mode Oct 2025; "Ask AI" Apr 2026) | Metasearch; mostly redirects (some "Book on Kayak") | Not retrieved | Metasearch disclaimers [prior] | Kayak price alerts and trip status [prior] | reported (features) |
| **ChatGPT** | Instant Checkout scaled back in Mar 2026; booking now completes in partner apps (Expedia, Booking.com, hotel brands), and partner is merchant of record. Payments, fraud and complaints liability reportedly drove the change | OpenAI ToS: output may be inaccurate, user must evaluate [prior] | OpenAI ToS cap: greater of fees paid in 12 months or $100 [prior] | None for travel | reported/prior |
| **Google AI Mode / Gemini** | Hotel booking live in US since 27 Aug 2026 (Marriott, Hilton, Booking.com, Expedia); **Google not merchant of record**, "the hotel or booking platform will handle the booking and any customer service"; flights search/track only | Gemini/AI Mode "can make mistakes" [prior] | Partner liable | Partner handles | reported |
| **Airbnb AI agent** | Airbnb is the platform/payment collector | Reported dedicated disclaimer page that machine-generated responses may be inaccurate | AirCover (see §4) | AI support assistant resolved about 1/3 of issues (Q4'25), >40% (Q1'26), ~45% of assistant-started (Q2'26), ~40% of all issues (Q3'26). Support cost per booking down ~16% YoY (Q2'26). Chesky: "You have to escalate to a human accurately, especially if it's timely or there's a trust and safety incident" | reported (earnings coverage) |

**Pattern [inferred].** Planners that *only plan* disclaim everything and sell nothing, so they have little to stand behind. OTAs that *sell* offer real support and some guarantees, but wall their AI off with "unverified, as-is" language. The industry has therefore split into two kinds of liability. **Transaction liability** is accepted by OTAs and suppliers. **Advice liability**, meaning the itinerary's facts, sequencing and feasibility, is accepted by nobody. Most real-world AI travel harm (§7) falls into the advice category.

Mark Pestronk (travel-law columnist, Travel Weekly) notes that OTAs are agents of both supplier and traveller and in principle owe advisor-like duties, but they disclaim them in their terms. Agentic AI companies go further and disclaim being anyone's agent at all [reported]. Pestronk's separate column "Advice from ChatGPT is advice from you" warns human advisors that relaying AI output makes it *their* advice [reported, title only]. This is the same principle as *Moffatt*.

---

## 3. Legal landscape

### 3.1 Chatbot liability: *Moffatt v Air Canada*, 2024 BCCRT 149 (14 Feb 2024) [verified]
- Air Canada's website chatbot told Mr Moffatt he could claim a bereavement fare retroactively. Policy said otherwise, and a linked policy page contradicted the bot.
- The BC Civil Resolution Tribunal found **negligent misrepresentation**. It rejected the argument that the chatbot was "a separate legal entity responsible for its own actions," held that Air Canada failed to take reasonable care that the bot was accurate, and held that the customer's reliance was reasonable. **Linking to the correct policy did not cure the error.**
- Award: about C$812 total (fare differential, interest, fees). The case set no contractual-promise doctrine, but it is the leading cited precedent.
- **Later cases:** I found **no appellate or later court decision** on consumer chatbot liability in travel. Commentators (UBC Law Review 2025, SAL Practitioner Jun 2025) still treat *Moffatt* as the reference point [verified absence in search results only, not exhaustive].
- **Implication [inferred].** "AI-generated, may be inaccurate" disclaimers are weak against negligent misrepresentation where the product is designed and marketed to be relied on, such as a planner that says "the last ropeway is at 17:30." In the EU and UK, unfair-terms law (Directive 93/13; UK CRA 2015 Part 2) further limits blanket exclusions in consumer contracts. Expedia's AI terms concede this ("we do not exclude our liability where we are not permitted to").

### 3.2 UK: CMA on AI agents [reported]
CIOReview reports that the CMA said in March 2026 that **businesses are responsible for their AI agents as they are for employees, even when a third party built them**. This sits alongside the DMCC Act 2024, which since April 2025 lets the CMA directly fine up to 10% of global turnover for consumer-law breaches [prior]. *Not re-verified; read the primary CMA document.*

### 3.3 EU Package Travel Directive (PTD) — the biggest structural risk/opportunity
- **Current law (Directive (EU) 2015/2302) [prior].** An "organiser" combining at least 2 types of travel service (transport, accommodation, car rental, other tourist services) for the same trip is **liable for performance of all services** (Art 13), whoever supplies them. The organiser must give price-reduction or damages remedies, provide assistance to travellers in difficulty (Art 16), and hold **insolvency protection** (Art 17). "Click-through" packages already exist where traveller data passes between traders and the second contract is concluded within 24 hours (Art 3(2)(b)(v)). "Linked travel arrangements" (LTAs) carried lighter duties: insolvency protection for payments received, plus information.
- **Revision status.** Commission proposal Nov 2023. **Provisional Council–Parliament agreement 2 Dec 2025** [verified, Consilium]. **EP plenary approval 12 Mar 2026 (537–2–24)** [verified, Agence Europe/Legislative Train]. HFW reports formal adoption as **Directive (EU) 2026/1024 dated 29 Apr 2026** [reported, single source; confirm in OJ]. Key changes [reported]:
  - **LTAs abolished.** Services bought from separate traders through **linked online booking processes**, where personal data moves between traders and **all contracts are concluded within 24 hours**, are **a package**.
  - Adjusted package definition, plus new **information duties** where no package arises.
  - **14-day refunds** for cancelled packages; vouchers voluntary, and travellers may refuse them.
  - Transposition period: typically about 2 years plus an application date. Exact dates not verified (**lawyer needed**).
- **What this means for an AI planner [inferred, lawyer needed]:**
  - If the planner **takes payment or passes traveller data to a second trader** (for example, booking a flight and then pushing the traveller's details to a hotel API) within 24h, it is likely the **organiser** of a package. That carries strict performance liability, an insolvency-protection requirement and a duty to assist.
  - Pure **referral/deep-link** models where the traveller re-enters data at each supplier are the classic way to avoid package status. Most AI planners do this today (Mindtrip, Google AI Mode, ChatGPT apps).
  - "Agentic" one-click multi-booking is precisely the conduct the revision targets. A product that bundles bookings to be "the accountable one" must either **embrace organiser status** (with bonding/insurance, which is how tour operators, Tourlane and similar work) or deliberately structure flows to stay outside it.

### 3.4 UK ATOL & Package Travel Regulations [prior]
- Selling flight-inclusive packages, or "Flight-Plus" (flight plus accommodation/car within 2 days of each other), to UK consumers requires an **ATOL** from the CAA. That brings financial-protection contributions (the ATOL Protection Contribution, about £2.50 per passenger), bonding/financial tests and Air Travel Trust coverage. Agents who sell as **agent for an ATOL holder** use an "Agent for ATOL holder" arrangement.
- The UK PTRs 2018 mirror the 2015 PTD. DBT consulted (2024–25) on simplifying them, including removing LTAs and possibly domestic packages. Outcome not verified this session.
- **Implication:** UK multi-booking with flights = ATOL question. **Lawyer needed.**

### 3.5 US seller-of-travel laws [prior; verify current statutes]
| State | Key requirement | Trigger |
|---|---|---|
| **California** (Bus. & Prof. Code §17550 et seq.) | Registration with AG; trust account or bond; **Travel Consumer Restitution Fund** participation; disclosures | Selling travel to CA residents or from CA, including online |
| **Florida** (Fla. Stat. ch. 559 Part XI) | Registration with FDACS; bond (typically $25k, up to $50k for vacation certificates); disclosures | Sells to or offers to Florida consumers |
| **Washington** (RCW 19.138) | Registration; trust account or bond; disclosures | Sells to/from WA |
| **Hawaii** (HRS 468L) | Registration; **client trust account**; disclosures | Sells to HI residents |
Exemptions exist (for example airlines, certain ARC/IATA-accredited or hotel-only sellers in some states) and vary. **An AI planner that becomes merchant of record, or even "arranges" travel for compensation, may trigger these laws. Lawyer needed.** Affiliate-link-only models have historically argued they are not "sellers of travel" [inferred].

US federal law adds two layers [prior]. The **FTC Rule on Unfair or Deceptive Fees** (effective May 2025) requires all-in pricing for **short-term lodging** (and live-event tickets), so an AI quoting hotel prices without mandatory fees is exposed. The **FTC Consumer Reviews rule** (2024) bans fake/AI-generated fake reviews. FTC "Operation AI Comply" (Sep 2024, including the DoNotPay "robot lawyer" order) shows the FTC treats **overstated AI capability claims** as deception. An "AI travel agent that handles everything" marketed without the backing to deliver it is a target [inferred]. US DOT has aviation consumer-protection jurisdiction over ticket agents, including online ones, under 49 U.S.C. §41712 [prior].

### 3.6 EU AI Act [prior; timing not re-verified]
- Travel planners are **not high-risk** under Annex III. **Art 50(1)** obliges providers to ensure people are informed they are interacting with an AI system, and Art 50(2) requires machine-readable marking of synthetic content. These transparency obligations apply from **2 Aug 2026**. The Commission's late-2025 "Digital Omnibus" proposed delays mainly for high-risk obligations, and possibly grace periods for 50(2); status unverified.
- Edge case: **AI-driven risk assessment/pricing for life and health insurance** is high-risk (Annex III 5(c)). Embedding travel *medical* insurance with AI underwriting or pricing could arguably be caught. **Lawyer needed.**
- The **AI Liability Directive** was withdrawn (Commission 2025 work programme) [prior]. The **new Product Liability Directive (EU) 2024/2853** explicitly covers **software including AI**. It must be transposed by **9 Dec 2026** and applies to products placed on the market after that. It covers death or personal injury, property damage and data loss, **but not pure economic loss** [prior]. A hallucinated trail that injures someone is in scope. A missed non-refundable hotel is not, and stays under contract/negligence/consumer law.

### 3.7 Passenger rights: what AI can claim for users [prior unless noted]
- **EU261/2004 (and UK261).** €250/€400/€600 compensation for delays ≥3h at arrival, cancellations with <14 days' notice, or denied boarding, unless "extraordinary circumstances" apply. Also duty of care (meals, hotel) and the right to refund or re-routing. **Reform:** the Council adopted a position in June 2025 raising thresholds (reportedly to 4h/6h, with €300/€500). Parliament opposed this, and its status in 2026 was **not verified this session**.
- **US DOT automatic refund rule** (Apr 2024; refund provisions effective Oct 2024). Automatic cash refunds for cancellations and "significant changes" (domestic delay ≥3h, international ≥6h), within 7 business days (card) or 20 calendar days (other). The proposed **cash compensation for controllable delays** rulemaking was, per my knowledge, abandoned by DOT in 2025. **Re-verify.** DOT's airline Customer Service Dashboard lists airline *commitments* (meals, hotel vouchers) that are enforceable as representations.
- **Canada APPR.** Amended regime in force Sept 2023; compensation C$125–1,000 [prior].
- **Automation opportunity [inferred].** Most of this is mechanically determinable: route, carrier, actual arrival time (FlightAware/Cirium/OAG), cause codes (weak; airlines dispute them). Claim services (AirHelp, Flightright) charge about 30–35% + VAT, with extra legal-action fees [prior]. A planner that **files EU261/DOT/APPR claims for free, inside the subscription,** is a concrete accountability feature that costs little and is visible to users.

---

## 4. Who does accountability well today (and how)

| Player | Mechanism | Fine print / limits | Funding model | Confidence |
|---|---|---|---|---|
| **Fora** (host agency, ~thousands of advisors) | Human advisor of record; IATA/supplier relationships; advisor intervenes in disruption | Not 24/7 by default; quality varies by advisor | Supplier commissions (hotel ~10%+), advisor split; Fora Pro subscription | prior |
| **Tern / Pilot / Origin** | Software for advisors (CRM, itinerary, AI), not consumer accountability; Pilot also a consumer/social planner | Accountability lives with the advisor | SaaS/commission | prior; Origin not verified |
| **Going (ex-Scott's Cheap Flights)** | Deal alerts; does **not** book, so no transaction accountability | — | Subscription | prior; no concierge product verified |
| **Amex Travel / Centurion & Platinum** | 24/7 human travel service; Fine Hotels + Resorts benefits; **card-embedded trip delay, cancellation and baggage insurance** | Insurance only if paid on card; delay thresholds (e.g. 6h/12h) and caps per trip | Annual fees + interchange + travel margin | prior |
| **Chase Travel (Sapphire)** | OTA (historically powered by Expedia/CxLoyalty) + card protections: trip delay (Reserve: 6h, up to $500), trip cancellation/interruption (up to $10k), primary CDW | Claims via Card Benefit Services; documentation-heavy | Annual fee + interchange | prior |
| **Capital One Travel** (Hopper tech) | Price match, price-drop protection, missed-connection rebooking guarantee, CFAR | Eligibility windows, partial refunds as travel credit in some cases | Fintech ancillaries + card economics | prior |
| **Navan** | 24/7 human + AI (Ava) support; duty-of-care traveller tracking; risk alerts; rebooking by agents with GDS access | Corporate only | SaaS + supplier margin; claimed fast response (minutes) | claimed/prior |
| **TravelPerk (Perk)** | 24/7 support; **FlexiPerk**: claimed refund of at least 80% of cost if a trip is cancelled for any reason (fee per booking) | Corporate; fee about 10–15% of trip cost | Ancillary fee + subscription | prior/claimed |
| **Spotnana** | Travel-as-a-service platform; servicing by TMC partners | B2B | Platform fees | prior |
| **Hopper** | **Flight Disruption Guarantee** (rebook on any airline at no cost, or refund, for delays/cancellations/missed connections); **Cancel For Any Reason**; Price Freeze; Price Prediction | Fee-based; refunds often as Hopper credit for some products; product-specific triggers (e.g. ≥2h delay). Canada's Competition Bureau reportedly secured a ~C$9M penalty (2025) over drip pricing of fees | **Fintech ancillaries are a large share of revenue**; risk priced via data | prior (re-verify penalty) |
| **Airbnb AirCover (guests)** | Booking Protection Guarantee (host cancels within 30 days, so Airbnb rebooks similar/better or refunds), Check-In Guarantee, Get-What-You-Booked Guarantee, 24h Safety Line | Must report within 72h of discovering an issue; Airbnb's discretion on "similar" | Service fees | prior; AI assistant stats reported |
| **Booking.com** | 24/7 CS; **"We Price Match"** (refund the difference; hotels only, until 24h before arrival) | Excludes flights/cars; must be same property/dates/conditions | Commission | reported |
| **Expedia** | 24/7; Expedia Help virtual agent; flight price-drop protection (US) and add-on "flexibility" products | Varies by market | Commission/merchant margin | prior |
| **Google Flights** | **Price guarantee pilot** (2023, US): if a "price guaranteed" fare drops before departure, Google refunds the difference via Google Pay. Delay predictions | Selected itineraries only; capped per year; current status unknown | Ads/Google Pay | prior |
| **Embedded insurers** | **Cover Genius (XCover)**: embedded protection for OTAs/airlines, claims fast-tracked/instant for some covers. **Faye**: app-first travel insurance, in-trip reimbursements to a "Faye Wallet," 24/7 support. **Battleface**: embedded/specialist. **Allianz Partners**: fixed-benefit delay payouts without receipts on some plans. **Parametric delay** products (Blink and others) pay automatically on verified delay | Exclusions (pre-existing conditions, known events), sub-limits; parametric pays fixed sums only | Premium share/commission to distributor (often 20–40% of premium) | prior/claimed |

**Lessons [inferred]:**
1. **Accountability that works is pre-funded.** It comes from a fee (Hopper, TravelPerk), an annual card fee (Amex/Chase), service fees (Airbnb) or insurance premiums. Nobody funds it out of an LLM subscription.
2. **The best experiences combine a guarantee with execution power.** Hopper's guarantee matters because Hopper *rebooks*. A refund promise without rebooking capability is half a solution.
3. **Humans remain the escalation backstop.** Airbnb, with the best AI support resolution rate reported, still resolves at most about 45%. It explicitly preserves "accurate" escalation for time-critical and safety issues. Klarna's 2025 partial reversal back toward human agents is a cautionary data point [prior].

---

## 5. Disruption-management technology

| Layer | State of the art | Automatable? | Notes |
|---|---|---|---|
| **Flight status & prediction** | FlightAware (Foresight ML predictions; AeroAPI), Cirium (flight status, on-time analytics), OAG (schedules/status); Google Flights delay predictions | Fully automatable via API | Licensing costs scale with tracked flights; predictions are probabilistic [prior] |
| **Proactive alerts** | Airline apps, TripIt Pro, Kayak Trips, Flighty (consumer favourite), Navan | Fully | Commodity. Differentiation is in *what you do next* [inferred] |
| **Airline self-service rebooking** | Major US carriers auto-rebook on cancellation and offer in-app alternatives; United "Agent on Demand" video/chat; airline NDC servicing APIs are maturing | Partly. Airline-controlled, and works best for direct bookings | Third parties can't easily trigger involuntary reaccommodation; OTA-booked tickets often must go through the OTA [prior] |
| **Third-party rebooking** | Hopper (books new ticket on any airline, absorbs cost), TMCs via GDS (Amadeus/Sabre/Travelport) with agents doing exchanges/reissues | Partly. Exchanges and reissues need ticketing authority (IATA/ARC accreditation or consolidator) and often humans for complex fares | "Why AI can book your flight but not rebook it" (Slicktrip): no consumer AI reliably rebooks a cancelled flight, changes a hotel night or claims fare-difference refunds [reported]. Sabre reports AI-agent booking customers (~80) [reported] |
| **Hotel/ground re-planning** | Mostly manual; some OTAs offer late-arrival messaging | Messaging to hotel automatable; cancellation-fee waivers need negotiation | A big gap for multi-supplier trips: a delayed flight cascades into a missed night, transfer and tour [inferred] |
| **Compensation claims** | AirHelp, Flightright, ClaimCompass (EU261/UK261/APPR), ~30–35% fees; airlines' own web forms (some faster, e.g. Lufthansa Group online claims) | Eligibility check + form submission automatable. Litigation needs lawyers | Some airlines (e.g. Ryanair) resist agencies and require direct claims [prior] |
| **Insurance claims** | Parametric (auto-pay on verified delay); Faye/XCover in-app claims | Parametric fully automatable; indemnity claims need documents | Strong fit for an AI planner that already holds the itinerary and flight data [inferred] |

**What needs a human/agent with GDS access [inferred/prior]:** involuntary reroutes onto other carriers (interline/endorsement), split-ticket protection, award tickets, group bookings, irregular-ops negotiation (hotel late arrival, tour rescheduling), medical/safety incidents, and anything where the airline's cause code is disputed.

---

## 6. Trust mechanisms in AI products generally

| Mechanism | Who does it | Strength |
|---|---|---|
| **Citations / sources** | Perplexity, Google AI Overviews, ChatGPT search | Helps users verify, but shifts burden to the user. *Moffatt*: a link to correct info did not cure the misstatement [verified] |
| **Human curation / review** | GuideGeek (curators review chats; claimed 98% accuracy) [claimed]; Layla (human experts) [claimed] | Rarely scoped, priced or guaranteed |
| **"Verified by local / human" tiers** | Tour/experience marketplaces (Viator, GetYourGuide "verified booking" reviews); expert-curated guides | Not applied to AI itineraries as a guarantee [inferred: gap] |
| **Price guarantees** | Booking.com We Price Match; Google Flights price guarantee (pilot); Capital One/Hopper price-drop | Mature, priced risk. Proves that guarantees on *data* (price) are feasible |
| **Accuracy guarantees / "hallucination insurance"** | **No consumer travel product found offering money-back for wrong AI information** [verified absence within searches; not exhaustive]. In enterprise AI, some vendors offer IP indemnities (Microsoft, Google, OpenAI copyright shields) [prior], and a specialist AI-insurance market exists (e.g. Armilla AI, Lloyd's-backed AI performance cover, 2025) [prior] | **Unoccupied in travel** |
| **E&O cover for AI agents** | Proposed by Faye co-founder Daniel Green: "Every human who books travel for someone else carries it. The companies deploying software to do the same job should carry it too" [reported] | Proposal, not a product |
| **Confirm-before-buy + audit trail** | Recommended by Morgan Lewis: affirmative confirmation of key details before non-refundable purchase, transaction records, human access for disputes [reported] | Low-cost legal hygiene |
| **Escalation to humans** | Airbnb, Expedia, Navan, TravelPerk | Usually not time-bound in consumer ToS |
| **Payment-network protection** | Card chargebacks (Reg Z/FCBA in US); Citi argued in Nov 2026 that **liability should fall on the AI agent's company**, not issuers, hotels or airlines [reported, Skift headline] | Signals that issuers will push risk onto agent operators. Visa/Mastercard agentic-commerce frameworks (2025) are building "agent tokens" and dispute rules [prior] |

---

## 7. Evidence of user harm

| Incident | Date | What happened | Company response | Confidence |
|---|---|---|---|---|
| **Moffatt v Air Canada** | 2022 bot answer; ruling Feb 2024 | Chatbot invented a retroactive bereavement-refund procedure | Air Canada argued the bot was a separate entity; lost; paid ~C$812 | verified |
| **Spanish influencers (Mery Caldass) denied boarding to Puerto Rico** | Aug 2025 | ChatGPT said no visa was needed (correct) but omitted the **ESTA**; denied boarding | None from OpenAI. Commentators split on the user's question framing | reported (multiple outlets) |
| **"Sacred Canyon of Humantay," Peru** | Reported Sep 2025 (BBC, via OECD AI incident monitor) | AI-generated route to a non-existent site; tourists heading alone to high-altitude rural area | None; tool unnamed | reported; one sceptical Substack disputes authenticity |
| **Mount Misen, Japan** | 2025 | ChatGPT gave wrong last-ropeway time; couple stranded at sunset | None | reported |
| **Layla: "Eiffel Tower in Beijing," infeasible marathon route in N. Italy** | Reported 2025 (BBC, slate.fr) | Hallucinated landmarks/routes | Layla reportedly said it improved the product [prior] | reported |
| **Stacker roundup "Bad travel advice from AI: From bogus bars to visa fails"** | Oct 2026 | Syndicated compilation of incidents | — | reported (title) |
| **MSN AI travel guide listing Ottawa Food Bank as an attraction** | Aug 2023 (older) | Generative content error | Microsoft removed the article | prior |
| **Cursor AI support agent invented a policy** (non-travel) | Apr 2025 | Shows the support-bot failure mode | Apology, refunds | reported |

**Patterns [inferred]:**
- Harms cluster around **entry requirements, timing/opening hours/last departures, feasibility of connections, and non-existent places**. These are exactly the facts that a verification layer can check against authoritative sources (Timatic/IATA Travel Centre, official transport timetables, Google Places business status).
- **No documented case of an AI trip-planner company compensating a user** was found. The only compensation in the record is court-ordered (Air Canada).
- **Data gap:** no published rate of wrong AI rebookings, and no complaint statistics specific to AI planners (DOT, CMA, EU ECC). Ask a parallel agent or a later pass to check ECC-Net, DOT Air Travel Consumer Reports and FTC Sentinel.

---

## 8. Accountability matrix

Scale: 0 = none, 1 = disclaimed/info only, 2 = transaction support via partner, 3 = own support + some guarantees, 4 = guarantees + active disruption execution, 5 = full organiser-level, stands behind whole trip.

| Player | Advice accuracy | Transaction / booking | Human support | Disruption execution | Financial guarantee | Overall |
|---|---|---|---|---|---|---|
| ChatGPT / Gemini (consumer) | 1 | 1 (partner MoR) | 0 | 0 | 0 | **0.5** |
| Mindtrip, Wanderlog, Wonderplan, Trip Planner AI, GuideGeek | 1 | 1 | 1 (email) | 0 | 0 | **~1** |
| Layla (pre/post Expedia) | 1 | 2 (claimed human experts) | 2 | 1 | 0 | **~1.5** |
| Google AI Mode hotels | 1 | 2 | 0 (partner) | 0 | 0–1 (Flights price guarantee pilot) | **~1** |
| Kayak | 1 | 2 | 1 | 1 (alerts) | 0 | **~1** |
| Booking.com / Expedia (incl. AI tools) | 1 (AI walled off) | 3 | 3 (24/7) | 2 | 2 (price match / price-drop) | **~2.5** |
| Airbnb | 1 | 3 | 3 (AI + human) | 2 (rebook on host cancel) | 3 (AirCover) | **~3** |
| Hopper / Capital One Travel | 1 | 3 | 2 | 4 (any-airline rebook) | 4 (paid guarantees) | **~3** |
| Card travel desks (Amex/Chase) | 2 (human) | 3 | 4 (24/7) | 3 | 4 (card insurance) | **~3.5** |
| Navan / TravelPerk (corporate) | 2 | 3 | 5 (24/7, fast) | 4 (agents with GDS) | 3 (FlexiPerk) | **~4** |
| Human advisor (Fora etc.) | 3 (advisor answers) | 3 | 3 (business hours, advisor-dependent) | 3 | 1 (insurance sold) | **~3** |
| Tour operator / package organiser (EU) | 3 | 5 (legal organiser) | 3 | 3 | 5 (insolvency protection) | **~4** |

**Unoccupied cell [inferred]:** *consumer + AI-native + advice accuracy ≥3 + disruption execution ≥4 + financial guarantee ≥3*. No one combines a verified, guaranteed itinerary with active disruption execution for leisure travellers at an AI price point.

---

## 9. Positioning, mechanisms, business models, risks

### 9.1 Unoccupied positioning
**"The AI planner that stands behind its itinerary."** Concretely:
1. **Verified itinerary.** Every load-bearing fact (entry docs, opening hours, last departures, transfer times, closures) is checked against authoritative sources and time-stamped, with a visible "verified at T" badge. Unverified items are visibly flagged.
2. **Itinerary Guarantee.** If a *verified* fact is wrong and it costs you money (missed ropeway, closed attraction, wrong visa document), we reimburse up to $X. Insurance backs this.
3. **Trip watch + act.** 24/7 monitoring of flights and bookings. On disruption, the AI proposes and executes a re-plan, and a human with GDS access handles what the AI can't, with a published response SLA.
4. **Claims on autopilot.** EU261/UK261/DOT refunds/APPR and insurance claims are filed for the user at **0% commission** (included in the plan).

### 9.2 Product mechanisms (cost-ordered)
| Mechanism | Cost to run | Legal exposure | Notes |
|---|---|---|---|
| Confirm-before-buy for non-refundable items; immutable audit log of what the AI said and showed | Low | Reduces | Morgan Lewis recommendation; evidence in disputes (cf. *Moffatt*) |
| "Load-bearing facts" verifier (Timatic/IATA Travel Centre for entry; official timetables; Places API; FlightAware/Cirium) with confidence tiers | Medium (data licences) | Reduces negligence risk; increases reliance (double-edged) | Shared with research agent on stale data/hallucinations |
| Free compensation-claim filing (EU261/DOT/APPR) | Low–medium (some human ops) | Low; check claims-management rules (UK FCA-regulated claims management only applies to certain sectors; EU261 agencies operate freely) | Visible "we fight for you" proof point |
| Proactive disruption alerts + AI re-plan suggestions | Low (API costs) | Low | Commodity alone; value comes from pairing with execution |
| **Itinerary Accuracy Guarantee** (capped, e.g. $250–$1,000/trip) | Insurance premium or self-insured reserve | **Creates a contractual promise; must be drafted tightly** | Novel; insurers (Faye, Cover Genius, Armilla-style AI cover) are likely partners |
| Embedded travel insurance + parametric delay cover | Revenue-positive (commission) | Insurance distribution licensing (EU IDD; US producer licences; UK FCA) | Funds the guarantee |
| Human escalation with GDS access (via host agency/TMC partner or in-house IATA/ARC accreditation) | High (24/7 staffing) | Becoming an agent brings duties and seller-of-travel registration | Start with partner TMC/host agency; tiered SLA |
| Disruption Guarantee (Hopper-style any-airline rebook) | Priced per booking; actuarial risk | Insurance-like product; may be regulated as insurance in some jurisdictions | Requires being in the booking path |
| Becoming EU package organiser / ATOL holder | High (bonding, compliance) | Full PTD liability | Strongest promise ("one party responsible for the whole trip"); later stage |

### 9.3 Business models that can fund real accountability
1. **Subscription concierge tier** (e.g. $10–30/month or per-trip $49–149). Funds 24/7 human escalation, claims filing and the accuracy guarantee. Analogues: Amex/Chase annual fees, Navan/TravelPerk SaaS, Fora Pro [inferred pricing].
2. **Merchant-of-record margin** on hotels and activities (merchant rates often 15–25%+ vs 10–15% agency commissions) [prior, approximate]. Funds service but triggers seller-of-travel, PTD and chargeback exposure.
3. **Ancillary/fintech products** (disruption guarantee, CFAR, price freeze): Hopper's model, high-margin if priced well. Watch for drip-pricing enforcement (Canada's Hopper case; FTC fees rule).
4. **Insurance distribution commission** (often 20–40% of premium) [prior, approximate] plus **parametric delay cover**. Natural fit because the planner holds itinerary and flight data.
5. **Claims share**, as a fallback for litigated claims only. Keep simple claims free to differentiate from AirHelp-type fees.
6. **B2B2C**: sell the "accountable planner" to card issuers and banks, which already fund 24/7 travel service and want to push agent liability onto someone (the Citi stance) [inferred].

### 9.4 Legal risks of standing behind the itinerary (lawyer needed on each)
- **Package organiser status (EU/UK).** Bundled booking flows plus data passing within 24h is likely a package under the 2026 PTD revision. That means strict liability for all components, an insolvency-protection requirement and a duty to assist.
- **ATOL (UK)** for flight-inclusive packages/Flight-Plus.
- **US seller-of-travel registration/bonding/trust accounts** (CA, FL, WA, HI) once taking money or arranging travel for compensation.
- **Insurance regulation.** An "accuracy guarantee" or "disruption guarantee" may be characterised as **insurance**, requiring an insurer partner (the planner as distributor/agent) rather than self-underwriting. Insurance distribution requires licensing (EU IDD, US state producer licences, UK FCA).
- **Advertising/deception (FTC §5, UK DMCC/CPRs, EU UCPD).** "Guaranteed," "verified," "AI travel agent" claims must match capability. FTC Operation AI Comply precedent. Display all-in prices (FTC fees rule for lodging).
- **Negligent misrepresentation (*Moffatt*).** Raising the reliance users place on you increases exposure. The guarantee should be the **exclusive remedy up to a cap** where law permits, with consumer-law floors preserved.
- **Unfair contract terms.** Blanket AI disclaimers are partly unenforceable for EU/UK consumers.
- **Product Liability Directive (from Dec 2026).** Personal-injury harms from AI software (dangerous routes, wrong safety info) fall under strict liability. Pure financial loss does not.
- **EU AI Act Art 50** disclosure (from Aug 2026); high-risk only if doing AI pricing/underwriting for health/life insurance.
- **Data protection.** Monitoring trips and passing traveller data to suppliers is a GDPR processing chain, and the same data passing helps create package status.
- **Chargeback / payment-network rules for agent-initiated transactions.** Visa/Mastercard agentic frameworks are evolving. Issuers signal the agent operator should bear liability.

---

## 10. Items to re-verify (search budget exhausted)
1. Official Journal reference and transposition and application dates for the revised PTD (claimed Directive (EU) 2026/1024).
2. EU261 reform status in 2026 (Council's 4h/6h thresholds vs Parliament).
3. US DOT 2025–26 actions: compensation rulemaking withdrawal; any changes to the automatic refund rule; ancillary-fee rule litigation.
4. CMA March 2026 AI-agents statement (primary text).
5. AI Act Article 50 application date after the Digital Omnibus.
6. Full ToS text: Mindtrip (consumer cap), Layla (post-Expedia), Wonderplan, Trip Planner AI, Kayak AI Mode, Booking.com AI Trip Planner, OpenAI apps and travel, Google AI Mode booking terms.
7. Current Hopper Disruption Guarantee terms and the Canada Competition Bureau penalty; Google Flights price guarantee current status.
8. Navan/TravelPerk published response-time SLAs; Faye/XCover claim-speed stats.
9. Complaint data: ECC-Net, DOT Air Travel Consumer Report, FTC Consumer Sentinel for AI-travel complaints.
10. Any AI-specific insurance or "accuracy guarantee" products launched in 2026 (Armilla, Munich Re aiSure, Lloyd's syndicates).

---

## Sources

Verified/reported this session (via search excerpts; full pages could not be fetched):
- Moffatt commentary: https://www.canlii.org/en/commentary/doc/2025CanLIIDocs1963 ; https://commons.allard.ubc.ca/cgi/viewcontent.cgi?article=1376&context=ubclawreview ; https://journalsonline.academypublishing.org.sg/Journals/SAL-Practitioner/Technology/ctl/eFirstSALPDFJournalView/mid/595/ArticleId/2065/Citation/JournalsOnlinePDF ; https://www.litigate.com/whose-responsibility-is-it-anyway-chatbots-and-legal-issues-in-moffatt-v-air-canada/pdf
- PTD revision: https://www.consilium.europa.eu/en/press/press-releases/2025/12/02/consumer-protection-council-and-parliament-strike-a-deal-on-revising-rules-on-package-travel/ ; https://www.europarl.europa.eu/legislative-train/theme-a-new-push-for-european-democracy/file-revision-of-the-package-travel-directive ; https://agenceurope.eu/en/bulletin/article/13827/21/european-parliament-approves-agreement-with-eu-council-on-revision-of-package-travel-directive ; https://www.hfw.com/insights/revision-of-the-package-holidays-directive-whats-changing/ ; https://www.travelextra.ie/provisional-agreement-reached-on-package-travel-directive-revision/ ; https://eulawlive.com/council-and-parliament-provisionally-agree-on-revision-of-package-travel-directive/
- Mindtrip ToS: https://mindtrip.ai/terms-of-service ; https://mindtrip.ai/creator-terms
- Layla: https://layla.ai/terms ; https://ir.expediagroup.com/news-and-events/news/news-details/2026/Expedia-Group-acquires-Layla-accelerating-its-AI-powered-trip-planning-and-booking-strategy/default.aspx ; https://www.hospitalitynet.org/news/4133792/expedia-group-acquires-layla-accelerating-its-ai-powered-trip-planning-and-booking-strategy ; https://skift.com/2026/07/31/expedia-acquired-ai-trip-planner-layla-exclusive/
- GuideGeek: https://brands.guidegeek.com/terms-of-service ; https://www.travelweekly.com/Travel-News/Travel-Technology/Travel-tackles-Artificial-Intelligence-hallucinations
- Wanderlog (tosdr): https://edit.tosdr.org/points/34467 ; https://edit.tosdr.org/points/34432 ; https://edit.tosdr.org/points/34430
- Expedia AI terms: https://www.expedia.com/legal/ai-terms ; https://www.expedia.co.in/legal/ai-terms ; https://www.expedia.com/lp/b/terms-of-service
- Pestronk / Travel Weekly: https://www.travelweekly.com/Mark-Pestronk/Using-agentic-AI-sites-comes-with-risks ; https://www.travelweekly.com/Mark-Pestronk/Advice-from-ChatGPT-is-advice-from-you
- Morgan Lewis: https://www.morganlewis.com/blogs/sourcingatmorganlewis/2026/08/ai-concierge-services-who-is-liable-when-a-bot-books-the-wrong-vacation ; https://www.lexology.com/library/detail.aspx?g=8744504f-1233-4ca6-a7fe-3ca99c09ab63 ; https://www.morganlewis.com/news/2026/10/rise-of-the-rogue-ai-bots-a-horror-show-for-retail-banking-and-travel-financial-review
- Skift / industry: https://skift.com/2026/11/11/citi-says-ai-companies-should-pay-when-their-agents-book-the-wrong-travel/ ; https://skift.com/2026/03/03/travel-brands-are-building-ai-agents-for-a-consumer-that-doesnt-exist ; https://skift.com/2026/09/25/whos-in-charge-when-a-trip-goes-wrong/ ; https://www.cioreview.com/leadership-perspectives/your-ai-agent-will-book-the-wrong-hotel-who-pays-nid-42992-cid-175.html ; https://www.pymnts.com/transportation/travel-payments/2026/ai-travel-agents-pack-a-threat-for-travel-aggregators/
- ChatGPT checkout: https://www.phocuswire.com/news/technology/openai-chatgpt-instant-checkout-travel-intermediaries ; https://www.modernretail.co/technology/what-went-wrong-with-chatgpts-instant-checkout/ ; https://www.checkout.com/blog/openai-agentic-commerce-shift ; https://www.conduit.ai/blog/how-ai-agents-book-hotels
- Google AI Mode: https://techcrunch.com/2026/08/27/googles-ai-mode-can-now-track-flight-prices-help-book-hotels-and-more/ ; https://www.phocuswire.com/news/technology/google-ai-mode-hotel-booking-agentic-flights-loyalty
- Airbnb AI support: https://www.customerexperiencedive.com/news/airbnb-reaches-another-service-milestone-with-its-ai-assistant/827358/ ; https://www.customerexperiencedive.com/news/airbnb-ai-assistant-resolves-customer-inquiries/819734/ ; https://www.pymnts.com/news/artificial-intelligence/2026/airbnb-is-weaving-ai-into-every-step-of-a-trip/ ; https://aifounders.cz/en/airbnbs-ai-now-solves-nearly-half-its-support-issues-read-the-denominator-first/
- Booking.com: https://www.bookingholdings.com/press-releases/booking-com-launches-new-ai-trip-planner-to-enhance-travel-planning-experience/ ; https://www.nerdwallet.com/article/travel/how-booking-coms-best-price-match-works ; https://conductatlas.com/platform/bookingcom/bookingcom-terms-and-conditions/provision/CA-P-076663/we-price-match-promise-to-refund-price-difference/
- Kayak: https://techcrunch.com/2025/10/16/kayak-launches-an-ai-mode-for-travel-questions-search-and-bookings/ ; https://www.kayak.com/news/ai-mode
- Harm cases: https://oecd.ai/en/incidents/2025-09-29-8b4f ; https://www.slate.fr/societe/lieux-imaginaires-tour-eiffel-pekin-pas-preparer-vacances-chatgpt-hallucinations-intelligence-artificielle-ia ; https://fialka.substack.com/p/ai-didnt-ruin-your-trip-you-did ; https://www.travelpulse.com/news/impacting-travel/influencer-goes-viral-for-trusting-chatgpt-s-visa-advice ; https://yourmileagemayvary.com/2025/08/18/influencer-used-chatgpt-for-travel-advice-wound-up-missing-her-flight/ ; https://krdo.com/stacker-travel/2026/10/02/bad-travel-advice-from-ai-from-bogus-bars-to-visa-fails/
- Rebooking gap: https://slicktrip.com/travel-talk/why-ai-can-book-your-flight-but-not-rebook-it-the-state-of-agentic-travel ; https://www.travelerstoday.com/articles/61028/20260923/ai-agents-can-now-book-your-flights-sabre-reaches-80-travel-customers.htm ; https://dailygenius.com/travel/ai-trip-planners-2026-bookings-refunds-rebooking-questions/

[prior] items (not fetched this session; primary sources to check): BCCRT decision 2024 BCCRT 149 (canlii.org); Directive (EU) 2015/2302 (eur-lex.europa.eu); Regulation (EC) 261/2004; US DOT 14 CFR Part 260 refund rule (transportation.gov); FTC Rule on Unfair or Deceptive Fees (ftc.gov); FTC Operation AI Comply (ftc.gov, Sep 2024); EU AI Act Regulation (EU) 2024/1689 Art 50; Product Liability Directive (EU) 2024/2853; CA Bus. & Prof. Code §17550; Fla. Stat. ch. 559 Part XI; RCW 19.138; HRS ch. 468L; UK CAA ATOL regulations; Hopper, Airbnb AirCover, TravelPerk FlexiPerk, Navan, Chase/Amex benefit guides; Cover Genius, Faye, Battleface, Allianz product pages.
