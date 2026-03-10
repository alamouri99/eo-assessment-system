---
name: market-attractiveness-scoring-engine
description: "Phase 2A of EO Conversational Advisor — scores market attractiveness /100 across Pain Reality, Purchasing Power, ICP Accessibility, and Market Growth. 80%+ scored autonomously from Phase 1 context. Only 3-5 strategic gap-filler questions."
version: "2.0"
---

# SKILL: Market Attractiveness Scoring Engine — Phase 2A

**Framework:** Alex Hormozi ($100M Leads), Chet Holmes (7x4x11)
**Input Sources:** Phase 1 deliverables (project-brief, icp-refined, positioning) + Round 10 gap-fillers
**Output File:** `market-attractiveness.md`
**Model:** Conversational advisor with autonomous scoring + strategic questioning
**Round:** 10 of 12

---

## FOUNDER ADVISORY LAYER

**REQUIRED REFERENCE:** Read `EO-Founder-Advisory-Layer.md` (parent directory) for Mentor Council, Engagement Mechanics, Elevation Engine, and Encouragement Library.

### Phase 2A Engagement: The Transition Moment

Phase 2A is where the conversation shifts from INTAKE to SCORING. The founder has just invested 20-30 minutes. Claude must:

1. **Celebrate the Phase 1 completion** before asking Round 10 questions
2. **Show what Claude already knows** — summarize the market picture from Phase 1 data
3. **Name the Phase 2 enemy: Market Myths** — "The assumptions about this market that keep incumbents complacent"
4. **Frame the gap-fillers as strategic, not tedious** — "I only need 3-4 data points to complete your market picture"

**Transition Script (Before Round 10):**
> "Phase 1 is complete. You've given me a clearer picture of your business than most founders have after 6 months of building. Let me show you what I see:
>
> From your answers, I can already score about 80% of your market attractiveness. Your pain architecture is [assessment]. Your ICP's purchasing power signals [assessment]. Your access channels point to [assessment].
>
> I just need a few strategic data points to complete the picture — things that require market-level knowledge, not just customer knowledge. These are the questions that separate 'I think this market works' from 'I KNOW this market works.'"

### Mentor Deployment for Phase 2A

| Moment | Mentor | Trigger |
|--------|--------|---------|
| Market size unknown | John Rush | "Validate via search volume. 1,000+ monthly searches = market exists." |
| No competitive awareness | Paul Graham | "If there are no competitors, ask yourself: is this a real market or a sitcom idea?" |
| Overestimating TAM | Alex Hormozi | "Starving crowd > big market. How DESPERATE are they?" |
| Market momentum unclear | Marc Lou | "Is this boring and growing? Boring + growing = money." |

---

## 1. STRATEGIC PURPOSE

Market Attractiveness Scoring (MAS) determines whether a market is worth entering by shifting from subjective ratings to evidence-based validation. This is **Phase 2A** of the new EO Conversational Advisor Framework.

**The Transformation:**
- **OLD:** Claude asks 25 questions → Student answers all → Claude scores
- **NEW:** Claude has gathered 80%+ of needed context in Phase 1 → Claude scores autonomously using Phase 1 data → Claude asks only 3-5 strategic gap-fillers → Claude produces market-attractiveness.md with transparent scoring

**Key Insight:** Pain reality, willingness to pay, accessibility, and market growth were mostly validated in Phase 1 through structured conversation (Pain chunks, WHO+Access, 3-Level Niche definition). MAS Round 10 fills only strategic gaps that Phase 1 conversation couldn't surface.

---

## 2. PREREQUISITES

This skill executes ONLY after Phase 1 is complete. Do not administer until:

| Prerequisite | What Claude Now Knows |
|--------------|----------------------|
| **Round 1-3 (Project Intake)** | 3-Level Niche, PSP, geography, revenue model → Input for Section D (Market Growth) |
| **Round 4 (Hero Journey)** | Customer narrative, transformation specifics → Input for Section A (Pain Reality depth) |
| **Rounds 5-8 (Pain & Pleasure)** | 5 primary pains + costs, 5 secondary pains, 5 pleasures, 5 away-froms → Section A fully informed |
| **Round 9 (WHO + Access)** | Full ICP profile, budget range, channels, congregation points → Sections B & C fully informed |

**Pre-Admin Checklist:**
- [ ] All 5 Phase 1 output files exist and are reviewed by student
- [ ] Student confirms: "No major changes to market, ICP, or business model since Phase 1?"
- [ ] Display Phase 1 summary: niche, pain statements, budget range, key channels

---

## 3. SECTION ARCHITECTURE

MAS evaluates market attractiveness across **4 sections (25 pts each = 100 total)**

| Section | Title | Phase 1 Source | Autonomy Level |
|---------|-------|---|---|
| **A** | Pain Reality & Intensity (25 pts) | Rounds 5-8 (pain chunks) + Round 4 (narrative) | 85% autonomous; may need cost clarification |
| **B** | Purchasing Power & Willingness (25 pts) | Round 9 (WHO + budget range + current spend) | 80% autonomous; may need price/willingness confirmation |
| **C** | ICP Accessibility (25 pts) | Round 9 (congregation points + channels) + Rounds 1-2 (geography) | 75% autonomous; may need reach validation |
| **D** | Market Growth & Momentum (25 pts) | Round 2 (niche size signals) + competitive context | 60% autonomous; needs market data + tailwinds |

**Total Score Bands:**

| Range | Band | Meaning |
|-------|------|---------|
| **85-100** | LAUNCH READY | Market clearly attractive; strong validation across all sections |
| **70-84** | ALMOST THERE | Solid core appeal; 1-2 sections need deeper validation |
| **55-69** | NEEDS WORK | Right direction but material gaps in validation |
| **40-54** | EARLY STAGE | Core market assumptions unvalidated |
| **0-39** | RESET | Market fundamentals questionable |

---

## 4. CONTEXT MAPPING: PHASE 1 → MAS SECTIONS

### Section A: Pain Reality (from Rounds 5-8 + Round 4)

**What Claude Already Knows:**
- Primary pains (5): specific, frequency, stated cost
- Secondary pains (5): root causes beneath surface
- Pain statement evidence: customer quotes, patterns, behaviors
- Narrative arc: customer frustration depth
- Quantified cost implications: already discussed

**Autonomy:** Claude scores pain reality using Phase 1 pain statements directly. No new questions needed unless confidence is LOW (e.g., pain costs were vague or hypothetical).

**Scoring Approach:**
- A1 (Pain Evidence): Validate against Round 5-8 pain statements; score as evidence already gathered
- A2 (Pain Frequency): Extract from Round 5 responses; score directly
- A3 (Pain Cost): May need brief clarification if cost estimates were rough
- A4 (Workaround Assessment): Extract from Rounds 5-8 analysis of current state
- A5 (Pain Urgency): Extract from Round 8 (away-froms = urgency signals)

**Confidence Flag Trigger:** If Phase 1 showed strong pain signals → score 4-5. If vague or hypothetical → flag and ask clarifying question.

### Section B: Purchasing Power (from Round 9)

**What Claude Already Knows:**
- Budget range: direct question in Round 9 (WHO + Access)
- Current spend: tools/vendors/platforms customer uses for related problems
- Decision-maker and approval process: explicitly asked in Round 9
- Payment methods: MENA context from Round 9 congregation discussion
- Willingness signals: may need brief test

**Autonomy:** Claude scores B1-B4 directly from Round 9 data. Only may need:
- B3 (Price Point Validation): If student's price hasn't been stated clearly, ask directly
- B5 (Willingness Signal): If no pilot/LOI exists, brief gap-filler question

**Scoring Approach:**
- B1 (Existing Spend): Reconstruct from Round 9 tool/vendor discussion
- B2 (Budget Authority): Extract from Round 9 decision-maker conversation
- B3 (Price Validation): May need: "Given pain cost + alternative spend + your proposed price, does this pass the no-brainer test?" (2 min question)
- B4 (Payment Infrastructure): Extract from Round 9 MENA context
- B5 (Willingness Signal): If lacking: "What's your strongest indicator someone would pay?" (1 min question)

### Section C: ICP Accessibility (from Round 9 + Rounds 1-2)

**What Claude Already Knows:**
- Congregation density: specific points where ICP congregates (LinkedIn groups, associations, platforms, events, communities)
- Reach capability: Round 9 asked "What's the fastest way to get 15 minutes of their attention?" = reach method
- Channel viability: Round 9 asked "Where do they hang out online? Offline?"
- MENA context: geography from Round 1; MENA channel knowledge from Round 9
- Competitor gaps: may need brief research question if not discussed

**Autonomy:** Claude scores C1-C4 directly from Round 9. May need:
- C4 (Competitor Access Pattern): If student hasn't researched competitors, ask: "How are competitors reaching these buyers?" (3 min question)

**Scoring Approach:**
- C1 (Congregation Density): Extract Round 9 congregation points; calculate density estimate
- C2 (Reach Capability): Map Round 9 "fastest 15 min" answer to reach plan
- C3 (Channel Viability): Extract Round 9 online/offline hangouts; assess realism
- C4 (Competitor Pattern): May need direct question if not discussed
- C5 (MENA Access Reality): Extract Round 9 MENA context; apply channel penetration table

### Section D: Market Growth & Momentum (from Round 2 + implied context)

**What Claude Already Knows:**
- Market size signals: niche definition (Round 2: industry → sub-niche → micro-niche) provides size clues
- Geographic signals: Round 1-2 geography + growth trends in that region
- Revenue model: Round 1 implies demand/willingness

**Autonomy:** Claude scores D1-D5 with MOST need for gap-fillers:
- D1 (Market Direction): May need: "Any market size data?" (1 min)
- D2 (Tailwind Events): May need: "What regulatory/tech/economic shifts push your market?" (2 min)
- D3 (Competitive Funding): May need: "Any funded competitors in this space?" (1 min)
- D4 (Search Demand): May need: "Checked Google Trends or keyword data?" (1 min)
- D5 (MENA Readiness): Can infer partly from geography; may need: "Is this market already buying in [country]?" (1 min)

---

## 5. THE 3-5 GAP-FILLER QUESTIONS (Round 10)

Claude asks these ONLY if previous answers are missing or unclear. Lead with explanation: "I can score most of your market attractiveness from what you've told me in Phase 1. I just need to fill a few strategic gaps..."

### Gap-Filler 1: Market Size Evidence (D1 + D3)

**When to Ask:** If niche definition from Round 2 was vague (e.g., "mid-market SaaS companies") OR if no data mentioned on market size

**Question:**
> "Let's nail market size. From your **3-Level Niche**, I have [niche definition]. Do you have ANY data on how many [micro-niche] exist in [geography]? Even a rough estimate — 'I think there are about 2,000 [micro-niche] in [geography]' is helpful. If you don't know, just say so and I'll work with what we have."

**What Claude Extracts:**
- Explicit market size estimate
- Whether student has researched this
- Confidence level in estimate

**Scoring Use:** D1 (Market Direction) + D3 (Competitive Landscape) context

**Time:** 2 min

---

### Gap-Filler 2: Competitive Density & Validation (D3 + C4)

**When to Ask:** If no competitors mentioned OR if unclear how many direct competitors exist

**Question:**
> "Market validation: How many competitors are directly solving [your specific problem] for [your micro-niche]? Name them if you can. Are they well-funded, bootstrapped, or scrappy? This tells me how validated the market is."

**What Claude Extracts:**
- Named competitors
- Approximate count
- Funding status (proxy for market validation)
- Competitive intensity

**Scoring Use:** D3 (Competitive Landscape) + C4 (Competitor Access Pattern)

**Time:** 2-3 min

---

### Gap-Filler 3: Market Momentum & Tailwinds (D2)

**When to Ask:** Always, unless student spontaneously mentioned regulatory/tech/economic shifts in Phase 1

**Question:**
> "Market momentum: In the next 12-24 months, what's pushing [your micro-niche] toward solutions like yours? Examples: regulatory mandate (like ZATCA), technology shift (AI, cloud adoption), cost pressure (labor inflation), or competitive threat. Or is the market stable?"

**What Claude Extracts:**
- Regulatory tailwinds (highest signal)
- Technology/economic shifts
- Competitive pressure
- Market stability assessment

**Scoring Use:** D2 (Tailwind Events) directly

**Time:** 2-3 min

---

### Gap-Filler 4: Price Sensitivity Test (B3 + B5)

**When to Ask:** If pricing strategy hasn't been tested with real buyers OR if price feels misaligned with pain cost

**Question:**
> "Price sense-check: Based on what you've told me about pain costs and your ICP's budget, what price are you charging monthly? And gut-check: at that price, would they flinch, negotiate hard, or say 'where do I sign'? What's your real confidence that they'd pay?"

**What Claude Extracts:**
- Stated price
- Buyer reaction prediction
- Founder confidence in price
- Willingness signals

**Scoring Use:** B3 (Price Point Validation) + B5 (Willingness Signal)

**Time:** 2 min

---

### Gap-Filler 5: Demand Signal / Search Validation (D4)

**When to Ask:** ONLY if helpful for confidence; often skippable

**Question (optional):**
> "One final check: Have you looked at Google Trends or search volume for keywords like '[your solution type]' or '[your micro-niche] + [pain keyword]'? Is search volume up, flat, or down over the last 12 months? This just confirms demand direction."

**What Claude Extracts:**
- Demand validation signal
- Search trend data
- Keyword specificity student has researched

**Scoring Use:** D4 (Search Demand Signal)

**Time:** 1-2 min (optional; skip if time is tight or other gaps filled)

---

**Total Gap-Filler Time:** 8-15 minutes (3-5 questions × 2-3 min each)

---

## 6. AUTONOMOUS SCORING RUBRICS (ALL 25 Questions Internalized)

Claude uses these rubrics to score against Phase 1 data, NOT by asking questions.

### SECTION A: PAIN REALITY & INTENSITY (25 POINTS)

#### A1. Pain Evidence Strength (0-5 pts)
**Source:** Rounds 5-8 pain statements + Round 4 narrative

**Rubric:**
| Score | Criteria | What This Means |
|-------|----------|---|
| 0-1 | Vague/unvalidated pains | Student speculated; no customer evidence in Phase 1 |
| 2 | Generic evidence | Named pain types but customer quotes/specifics thin |
| 3 | Partial evidence | Some customer conversations or market research mentioned |
| 4 | Strong evidence | Multiple pains grounded in customer conversations + observable behaviors |
| 5 | Expert evidence | Deep pain statements with rich customer quotes; specific frequencies/impacts |

**Scoring Logic:**
- Extract the 5 primary pains from Round 5 output
- Check Round 5-8 narrative: Were these grounded in conversations or research?
- Check Round 4 Hero Journey: Did student demonstrate deep customer empathy?
- Award based on depth of evidence in Phase 1 record

**Confidence Flag:** If pains felt speculative → "I scored your Pain Evidence at 3/5, but I'm less confident here. Do you have customer conversations validating your top 3 pains? If yes, share and I'll re-score."

---

#### A2. Pain Frequency (0-5 pts)
**Source:** Round 5 primary pain statements (which included frequency)

**Rubric:**
| Score | Frequency |
|-------|-----------|
| 5 pts | Multiple times daily |
| 4 pts | Daily |
| 3 pts | Weekly |
| 2 pts | Monthly |
| 1 pt | Quarterly or less |

**Scoring Logic:**
- Extract frequency estimates from Round 5 pain statements
- Average across top 3 pains
- Score directly

**Consistency Check:** If average frequency is low (e.g., quarterly) but pain cost (A3) is high → Flag: "Your pain is high-cost but infrequent. This can work IF you show compound cost (quarterly × 4 = annual). Let me re-score if you clarify."

---

#### A3. Pain Cost (0-5 pts)
**Source:** Round 5-8 pain statements (students often discussed costs)

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | No quantification |
| 2 | Rough estimate (math okay but arbitrary) |
| 3 | Reasonable math (realistic rates; missing 1 cost type) |
| 4 | Sharp calculation (labor + error + opportunity costs) |
| 5 | Expert model (comprehensive; sensitivity analysis) |

**Scoring Logic:**
- Extract any cost language from Round 5-8
- If quantified (e.g., "15 hours/week × $50/hour = $750/month"), score 4-5
- If stated but not calculated (e.g., "costs them a lot"), ask Gap-Filler clarification or score 2-3
- MENA adjustment: Verify hourly rates match geography (Egypt $20-40/hr; Saudi $40-60/hr)

**Confidence Flag:** If costs weren't quantified in Phase 1 → "Pain Cost scored 2/5 — rough estimate. If you have real numbers from customer research, share and I'll re-score."

---

#### A4. Workaround Assessment (0-5 pts)
**Source:** Round 5-8 discussion of current state + Round 6 secondary pains (often discuss workarounds)

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | No awareness of workarounds |
| 2 | Generic ("they use spreadsheets") |
| 3 | Named tools with basic failures |
| 4 | Tools + specific failure points |
| 5 | Comprehensive failure map; clear frustration |

**Scoring Logic:**
- Extract workaround mentions from Round 5-8
- Check Round 6 secondary pains (which often explain why current workarounds fail)
- Award for specificity + failure understanding

**Example:** If Round 5 mentions "they use Zapier and manual emails" and Round 6 explains "Zapier workflows break if format changes," → Score 4

---

#### A5. Pain Urgency Signal (0-5 pts)
**Source:** Round 8 away-from motivations (fear-based drivers = urgency proxies)

**Rubric:**
| Score | Signal Type | Criteria |
|-------|---|---|
| 0-1 | Wishful | "They want it ASAP"; no evidence |
| 2 | Assumption | Logical guess; unvalidated |
| 3 | Some signals | 1-2 urgency drivers (budget allocated, timeline mentioned) |
| 4 | Strong signals | 2-3 drivers (regulatory + budget + competitive) |
| 5 | Validated | 3+ signals; external deadlines; direct buyer statement |

**Scoring Logic:**
- Extract away-from motivations from Round 8
- Map to urgency signals: "They fear being replaced by competitor X" = competitive urgency
- Check for external pressures: Regulatory deadline? Budget period? Crisis?
- Award based on signal count + strength

**Example:** If Round 8 included "terrified of competitor automation forcing manual brokers obsolete within 18 months + budget allocated this quarter" → Score 4-5

**Confidence Flag:** If urgency was implied but not explicit → "Urgency scored 3/5 based on inferred timeline. Have you asked the buyer directly when they'd need this?"

---

**SECTION A TOTAL:** A1+A2+A3+A4+A5 = 0-25 pts

---

### SECTION B: PURCHASING POWER & WILLINGNESS (25 POINTS)

#### B1. Existing Spend (0-5 pts)
**Source:** Round 9 WHO + Access (asked current solution, tools, vendors)

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | Blank or "don't know" |
| 2 | Generic tools; no prices |
| 3 | Specific tools with vague pricing |
| 4 | Named tools + actual prices; includes labor |
| 5 | Complete spend map; hidden costs; purchasing precedent clear |

**Scoring Logic:**
- Extract named tools from Round 9
- Extract pricing if mentioned
- Calculate total: Tools + Services + Internal Labor
- Benchmark against pain cost (A3): Should be in same ballpark

**Confidence:** If Round 9 was vague on spend → Score 2-3 and flag

---

#### B2. Budget Authority (0-5 pts)
**Source:** Round 9 WHO + Access (decision-maker process)

**Rubric:**
| Score | Decision Complexity |
|-------|---|
| 5 pts | User/manager decides alone (fast) |
| 4 pts | User + 1 approver (faster) |
| 2.5 pts | Department head (medium) |
| 1.5 pts | C-suite (slow) |
| 1 pt | Committee (slowest) |

**Scoring Logic:**
- Extract decision-maker and approval chain from Round 9
- Check timeline: "Director approves within 1 week if <$500" → Factor into sales cycle
- Validate: Does student's ACV fit within threshold?

**Flag:** If ACV exceeds threshold → "Budget Authority low because your $2K price exceeds their $500 threshold."

---

#### B3. Price Point Validation (0-5 pts)
**Source:** Round 1 (ACV mentioned?) + Gap-Filler Q4 if needed

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | No price; or price > pain cost |
| 2 | Price set but not validated (no benchmarks) |
| 3 | Two comparisons (price vs. pain OR price vs. alternatives) |
| 4 | Three comparisons clear; ROI >3x validated |
| 5 | Expert model; all 3 comparisons + sensitivity tested |

**Scoring Logic:**
- Extract price from student's statements
- Benchmark vs. pain cost: Price should be 20-50% of monthly pain cost
- Benchmark vs. alternatives: Price should be <25% of current spend (B1)
- Calculate ROI: (Annual savings) ÷ (Annual cost) — aim for 3x+
- Award based on clarity + realism

**Confidence:** If price unclear or not validated → Ask Gap-Filler Q4

---

#### B4. Payment Infrastructure (0-5 pts)
**Source:** Round 9 MENA context or implied by geography

**Rubric:**
| Payment Method | Base Score | MENA Adjustment |
|---|---|---|
| Credit card online | 5 pts | -1 if Egypt/Jordan/Lebanon only |
| Bank transfer | 5 pts | +1 if offered (preferred in some MENA) |
| Mobile wallets | 5 pts | +1 MENA-specific edge |
| BNPL (Tabby, Tamara) | 4 pts | Strategic in UAE/Saudi |
| Cash/check | 2 pts | Outdated; avoid |
| Unknown | 0 pts | Research required |

**Scoring Logic:**
- Infer from student's geography and niche
- Award based on payment method diversity
- Apply MENA adjustments if relevant

**Example:** Saudi Arabia + multiple payment methods (credit card + bank transfer + mobile) = 5 pts

---

#### B5. Willingness Signal (0-5 pts)
**Source:** Phase 1 (any pilot mention?) or Gap-Filler Q4

**Rubric (Hierarchy):**
| Score | Signal Type | Criteria |
|-------|---|---|
| 0-1 | Aspirational | "I think people would pay"; no evidence |
| 2 | Behavioral | Waitlist, signups (intent; no commitment) |
| 3 | Verbal | Buyer said they'd pay (unnamed or unconfirmed) |
| 4 | Signed | Signed LOI, pre-order, pilot agreement |
| 5 | Executed | Paid pilot, pre-orders collected, revenue |

**Scoring Logic:**
- Check Phase 1 for any mentions of pilots, pre-orders, or early customers
- If none, ask Gap-Filler Q4 or score 2-3
- Award based on commitment strength

**Confidence:** If none, flag: "No willingness signal yet. Before full launch, get a signed LOI or paid pilot commitment."

---

**SECTION B TOTAL:** B1+B2+B3+B4+B5 = 0-25 pts

---

### SECTION C: ICP ACCESSIBILITY (25 POINTS)

#### C1. Congregation Density (0-5 pts)
**Source:** Round 9 congregation points

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | Vague ("online somewhere") |
| 2 | Generic point; no estimate |
| 3 | Specific point + rough estimate |
| 4 | Layered calculation (total → filters → ICP fit) |
| 5 | Multiple points ranked; specific counts; actionable reach |

**Scoring Logic:**
- Extract congregation points from Round 9 (LinkedIn groups, associations, events, communities)
- Check for density estimates: Did student calculate "Of 5K group members, 20% by role × 40% by size = 400 ICP fit"?
- Award for calculation quality + specificity

**Example:** "Top point: Finance Manager LinkedIn group, 5K members, 20% right role × 40% right size = 400 exact fit" = 4 pts

---

#### C2. Reach Capability (0-5 pts)
**Source:** Round 9 fastest way to reach + implied capacity

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | No reach plan |
| 2 | Generic plan; unrealistic numbers |
| 3 | Specific channels + weekly targets; realistic |
| 4 | Channels + daily cadence + response rates + time |
| 5 | Multiple channels + contingency + validated rates |

**Scoring Logic:**
- Extract "fastest way to reach 15 min" answer from Round 9
- Map to 100-in-30 days calculation: 100 ÷ 30 = 3.3/day minimum
- Check realism: LinkedIn 4 msgs/day is realistic; 100+ is not
- Award based on specificity + achievability

**Confidence:** If vague → "Reach scored 2/5. Can you actually reach 100 in 30 days with your current resources? What's the realistic plan?"

---

#### C3. Channel Viability (0-5 pts)
**Source:** Round 9 online/offline hangouts + implied experience

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0 | No channels fit ICP |
| 1 | 1-2 channels with weak fit |
| 3 | 3 viable channels, lower fit |
| 5 | 3+ channels with strong ICP fit + founder experience |

**Scoring Logic:**
- Extract channel mentions from Round 9 (LinkedIn, WhatsApp, cold email, content, events, etc.)
- Check ICP-channel alignment: Does ICP actually use these channels?
- Check founder capability: Has student tried this before? Success signals?
- Award based on fit + proof

**Example:** "ICP congregates on LinkedIn + WhatsApp; founder has 5K LinkedIn connections with 15% response history + WhatsApp experience" = 4-5 pts

---

#### C4. Competitor Access Pattern (0-5 pts)
**Source:** Phase 1 positioning discussion or Gap-Filler Q2

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | No competitor awareness |
| 2 | Names competitors; knows 1 channel |
| 3 | 2-3 competitors; 1-2 channels each; 1 weakness |
| 4 | Sharp map (channels + metrics; 2+ weaknesses) |
| 5 | Detailed channels + metrics; clear positioning gap |

**Scoring Logic:**
- Check Phase 1 for competitive context (from positioning discussion)
- If vague, ask Gap-Filler Q2
- Assess: Do competitors dominate LinkedIn? Are they weak on WhatsApp? → Strategic gap?
- Award for competitive insight quality

**Confidence:** If not researched → "Competitor pattern scored 1/5. Before launch, map where your 2-3 key competitors are strongest and where they're weak."

---

#### C5. MENA Access Reality (0-5 pts)
**Source:** Round 9 geography context + MENA channel knowledge

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | Western assumptions (email/LinkedIn only; no MENA adaptation) |
| 2 | Surface awareness (WhatsApp more; vague) |
| 3 | Some context (2-3 MENA factors; partial channel mix) |
| 4 | Sharp strategy (3+ factors; channel % provided; language clear) |
| 5 | Expert (detailed mix by geography; language strategy; local advantage) |

**MENA Channel Reference Table:**
| Country | LinkedIn | WhatsApp | Email | Events | Language |
|---------|----------|----------|-------|--------|----------|
| Saudi | 65-70% | 90%+ | 40-50% | Medium | Arabic growing |
| UAE | 75%+ | 95%+ | 60% | High | Mixed |
| Egypt | 35-45% | 95%+ | 15-25% | Low | Arabic primary |
| Jordan | 45-50% | 95%+ | 20-30% | Low | Arabic primary |

**Scoring Logic:**
- Extract geography from Round 1-2
- Check Round 9 for MENA-specific channel mix
- Compare student's strategy to baseline table (misalignment = flag)
- Award for local market knowledge + language strategy

**Example:** "Egypt: Strategy 50% WhatsApp + 35% LinkedIn + 10% email + 5% in-person. All content Arabic." = 4-5 pts

---

**SECTION C TOTAL:** C1+C2+C3+C4+C5 = 0-25 pts

---

### SECTION D: MARKET GROWTH & MOMENTUM (25 POINTS)

#### D1. Market Direction (0-5 pts)
**Source:** Round 2 niche definition + Gap-Filler Q1 if needed

**Rubric:**
| Score | Direction |
|-------|---|
| 2 pts | Rapidly growing (>30% YoY) |
| 2 pts | Growing (10-30% YoY) |
| 1.5 pts | Stable (0-10% YoY) |
| 0.5 pts | Declining (<0% YoY) |
| 0 pts | Don't know |

**Scoring Logic:**
- Infer from Round 2 niche definition (if narrowly defined micro-niche, likely growing)
- If vague, ask Gap-Filler Q1: "Market size data?"
- Award based on growth direction

**Confidence:** If unknown → "Market Direction scored 0/5. Research required: Google '[market] market size 2024 2025 2026.' Find specific growth rate."

---

#### D2. Tailwind Events (0-5 pts)
**Source:** Geography context (Round 1-2) or Gap-Filler Q3

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | No tailwinds or generic |
| 2 | 1 tailwind; vague |
| 3 | 2 specific tailwinds (regulatory, economic) |
| 4 | 2-3 specific + dated tailwinds; buyer urgency clear |
| 5 | 3+ specific tailwinds; dates; magnitude; strategic impact |

**Scoring Logic:**
- Check Phase 1 for any tailwind mentions (Vision 2030, ZATCA, labor cost inflation, AI, etc.)
- If missing, ask Gap-Filler Q3: "What shifts push buyers toward your solution?"
- Award for specificity + strategic relevance

**Tailwind Hierarchy:** Regulatory > Economic > Technology > Competitive > Seasonal

**Example:** "ZATCA e-invoicing mandate June 2026 + Saudi labor inflation 12% YoY + cloud adoption 40% CAGR = 3 strong tailwinds" = 5 pts

---

#### D3. Competitive Landscape (0-5 pts)
**Source:** Positioning discussion (Round 3) or Gap-Filler Q2

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0-1 | No competitor awareness |
| 2 | Names competitors; no funding data |
| 3 | 2 competitors with partial funding |
| 4 | 2-3 competitors with amounts + stages; viability clear |
| 5 | 3+ funded competitors + amounts + dates + acquisitions; market validated |

**Scoring Logic:**
- Check Phase 1 for competitive positioning mentions
- If vague, ask Gap-Filler Q2: "Funded competitors in this space?"
- Assess: Multiple VC-funded competitors = market validated + high competition
- Award for competitive intelligence + market validation signal

**Confidence:** If no funding data → "Competitive Landscape scored 1/5. Research Crunchbase: Find 2-3 direct competitors and their funding."

---

#### D4. Search Demand Signal (0-5 pts)
**Source:** Implied (rarely asked in Phase 1) or Gap-Filler Q5 (optional)

**Rubric:**
| Score | Criteria |
|-------|----------|
| 0 | Blank |
| 1 | "Don't know" (no research) |
| 2 | "I think search is up" (no data) |
| 3 | Checked Google Trends; direction unclear |
| 4 | Specific keywords + 1-year trend + volume data |
| 5 | Multiple keywords + trend data + confirmed via 2+ tools |

**Scoring Logic:**
- Rarely covered in Phase 1 → Often skip this question
- If time allows, ask Gap-Filler Q5: "Google Trends data?"
- Award for data quality

**Confidence:** If not researched → "Demand scored 0/5. Optional but helpful: Google Trends '[keyword]' March 2025-2026. Check direction."

---

#### D5. MENA Market Readiness (0-5 pts)
**Source:** Round 2 geography + Round 9 MENA context

**Rubric:**
| Score | Readiness Level | Signal |
|-------|---|---|
| 2 pts | Already buying | Category exists; competitors operate; buyers compare |
| 1.5 pts | Aware not buying | Know category; barriers (price/regulatory) |
| 1 pt | Unaware | Don't know category exists |
| 0 pts | Resistant | Legacy systems entrenched; blockers |

**Readiness Implications:**
| Level | Sales Cycle | GTM |
|---|---|---|
| Already buying | 4-8 weeks | Price competitive |
| Aware not buying | 8-16 weeks | Education + ROI |
| Unaware | 16-26 weeks | Authority building |
| Resistant | 26+ weeks | Long-term; niche focus |

**Scoring Logic:**
- Infer from geography (Saudi/UAE = higher readiness; Egypt/Jordan = lower)
- Check Round 9 for MENA-specific competitor mentions
- If uncertain, ask Gap-Filler Q3 or Q5: "Is market already buying in [country]?"
- Award based on adoption signals

**Example:** "Saudi Arabia: Already buying. Evidence: ZATCA vendors list 50+ e-invoicing solutions; major firms implementing" = 5 pts

---

**SECTION D TOTAL:** D1+D2+D3+D4+D5 = 0-25 pts

---

## 7. SCORING PROCESS & CONFIDENCE FLAGGING

### Scoring Order

1. **Section A (Pain Reality):** Fully autonomous from Phase 1 (5 min internal scoring)
2. **Section B (Purchasing Power):** 80% autonomous + may ask B3/B5 gap-fillers (3 min)
3. **Section C (ICP Accessibility):** 75% autonomous + likely ask C4 gap-filler (5 min)
4. **Section D (Market Growth):** 60% autonomous + likely ask D1/D2/D3 gap-fillers (5 min)

### Confidence Flagging Rules

After scoring each section, Claude flags LOW confidence:

**Low Confidence Trigger:** Score < 4 AND evidence in Phase 1 was thin or speculative

**Flag Format:**
> "**Section [X] Confidence Note:** I scored you [score]/25 on [dimension], but I'm less confident here. [Reason]. If you have more data on [specific topic], I can re-score and potentially move this higher."

**Example:**
> "**Section B Confidence Note:** I scored your Price Point Validation at 2/4 because pricing wasn't validated against pain cost in Phase 1. If you've done pricing research or customer willingness testing, share it and I'll re-score."

### Cross-Scorecard Consistency Checks

Claude automatically flags contradictions:

- **Contradiction:** High pain cost (A3 = 5) but quarterly frequency (A2 = 1) → Flag: "Your pain is expensive but infrequent. Is the compound annual cost still high enough to justify urgency?"
- **Contradiction:** Large market size (D1 = 5) but no funded competitors (D3 = 1) → Flag: "Market seems attractive but unvalidated. Have you researched competitor landscape?"
- **Contradiction:** High congregation density (C1 = 5) but weak reach capability (C2 = 1) → Flag: "ICP congregates in accessible places but your reach plan is unclear. Let's refine Channel Viability."

**No penalties for contradictions** — just surface them and offer clarification conversation.

---

## 8. OUTPUT FILE SPECIFICATION

### market-attractiveness.md (Auto-Generated)

```markdown
# Market Attractiveness Score (MAS)

**Total Score: [X]/100**
**Band: [LAUNCH READY | ALMOST THERE | NEEDS WORK | EARLY STAGE | RESET]**
**Confidence Level: [HIGH | MEDIUM | LOW]**

---

## Score Breakdown

| Section | Points | Status | Confidence |
|---------|--------|--------|---|
| A. Pain Reality | [X]/25 | [Notes] | [HIGH/MED/LOW] |
| B. Purchasing Power | [X]/25 | [Notes] | [HIGH/MED/LOW] |
| C. ICP Accessibility | [X]/25 | [Notes] | [HIGH/MED/LOW] |
| D. Market Growth | [X]/25 | [Notes] | [HIGH/MED/LOW] |
| **TOTAL** | **[X]/100** | | |

---

## Section A: Pain Reality & Intensity ([X]/25)

**A1. Pain Evidence (0-5):** [Score + explanation]
**A2. Pain Frequency (0-5):** [Score + explanation]
**A3. Pain Cost (0-5):** [Score + explanation]
**A4. Workaround Assessment (0-5):** [Score + explanation]
**A5. Pain Urgency (0-5):** [Score + explanation]

**Confidence Note (if <4):** [Flag if applicable]

---

## Section B: Purchasing Power & Willingness ([X]/25)

[Same structure as A]

---

## Section C: ICP Accessibility ([X]/25)

[Same structure as A]

---

## Section D: Market Growth & Momentum ([X]/25)

[Same structure as A]

---

## Consistency Checks

[Flags any contradictions found; offers clarification]

---

## Top Improvement Actions (Prioritized by Impact)

1. **[Action 1]** — Current score: [X/5]. Gap: [gap]. Potential lift: [Y pts]. Time: [Z hours]
2. **[Action 2]** — [Same format]
3. **[Action 3]** — [Same format]

---

## Band Interpretation

**[BAND NAME]:** [What this means for next steps]

- If <70: "30-Day Validation Action Plan" section
- If 70-84: "Strengthen X to Move to Launch Ready" section
- If 85+: "You're ready; move to Phase 2B (Strategy Matching)"

---

## Next Steps

[Band-specific guidance]
```

---

## 9. HANDOFF TO PHASE 2B

After MAS scoring is complete and market-attractiveness.md is generated:

> "Your Market Attractiveness Score is [X]/100 ([BAND]). This tells me [interpretation].
>
> If you'd like to improve before moving forward, here are your top 3 actions: [list].
>
> Otherwise, you're ready for **Round 11: Strategy Matching**. In that round, I'll understand your founder DNA — your resources, skills, and preferences — and recommend the best strategy path for your business.
>
> Ready to continue?"

---

## 10. MENA-SPECIFIC ADJUSTMENTS (Throughout)

Applied across all sections:
- **B4 Payment:** Adjust for WhatsApp/bank transfer/BNPL adoption by country
- **C3/C5 Channels:** Apply geographic penetration rates from channel table
- **D2 Tailwinds:** Recognize MENA-specific drivers (Vision 2030, ZATCA, data laws, regulatory timelines)
- **D5 Readiness:** Expect longer sales cycles in emerging markets; government adoption slower than commercial

---

## 11. CLAUDE EXECUTION FLOW (Round 10)

1. **Setup (2 min):** Display Phase 1 summary; confirm context accuracy
2. **Autonomous Scoring (15 min):** Score all 4 sections internally using Phase 1 data
3. **Gap-Filling (8-15 min):** Ask 3-5 strategic gap-filler questions based on confidence
4. **Cross-Consistency (3 min):** Surface and resolve contradictions
5. **Output Generation (3 min):** Create market-attractiveness.md
6. **Presentation (5 min):** Show score, band, confidence levels, top 3 improvements
7. **Handoff (2 min):** Explain next round (Phase 2B Strategy Matching)

**Total Round 10 Time:** 40-50 minutes

---

## 12. COMPARISON TO OLD MODEL

| Dimension | OLD (SC3) | NEW (Phase 2A) |
|-----------|-----------|---|
| **When Administered** | After SC2 complete | After Phase 1 complete |
| **Questions Asked** | 25 direct questions | 3-5 strategic gap-fillers |
| **Scoring Source** | Student answers to questions | Phase 1 context + gap-filler answers |
| **Autonomy** | 0% (scores only what student says) | 80%+ (scores from gathered context) |
| **Time** | 60-90 minutes | 40-50 minutes |
| **Output** | Scored answers + rubric report | market-attractiveness.md + confidence flags |
| **Tone** | Examiner asking questions | Advisor explaining what I'm seeing |

---

**END OF SKILL.MD**
