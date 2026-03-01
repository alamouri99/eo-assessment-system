# EO Strategy Selector: Consolidated Founder Strategy Engine

## PURPOSE

This skill is the **decision brain** of the EO Assessment System. It takes the completed results from all three deep assessments (MAS /100, ICP /100, GTM /100) and produces a unified strategic recommendation: what to do, in what order, with what resources, and why.

The three assessments answer separate questions:
- **MAS:** Is this market worth entering?
- **ICP:** Do you know who you're selling to, and can you reach them?
- **GTM:** Which distribution channels fit your situation?

This skill answers the question none of them can answer alone: **Given everything we now know about your market, your customer, and your distribution fitness, what is the optimal strategy for the next 90 days?**

---

## WHEN TO INVOKE THIS SKILL

Trigger this skill when:
- A founder has completed all 3 deep assessments (MAS, ICP, GTM)
- The n8n consolidated workflow fires (all 3 records exist in Supabase for same email)
- A founder asks "what should I do now?" after running assessments
- A founder shares their 3 scores and wants strategic direction
- The EO Assessment Dashboard triggers the consolidated view

**Do NOT invoke** if fewer than 3 assessments are completed. Instead, direct the founder to complete the missing assessment(s) first. Partial strategy is worse than no strategy because it creates false confidence.

---

## INPUTS REQUIRED

### Primary Inputs (Mandatory)

```
1. MAS Score: [XX/100]
   - Section A (Pain Reality): [XX/25]
   - Section B (Purchasing Power): [XX/25]
   - Section C (Market Momentum): [XX/25]
   - Section D (Competitive Advantage): [XX/25]
   - MAS Band: [STRONG | VIABLE | WEAK | HIGH RISK | NO MARKET]

2. ICP Score: [XX/100]
   - Section A (WHO - Dream Customer): [XX/25]
   - Section B (WHERE - Congregation): [XX/20]
   - Section C (WHAT CAPTURE - Attraction): [XX/20]
   - Section D (RESULT - Transformation): [XX/15]
   - Section E (Epiphany Bridge): [XX/10]
   - Section F (Attractive Character): [XX/10]
   - ICP Band: [CRYSTAL CLEAR | GOOD FOUNDATION | FUZZY | NO CLARITY | CRITICAL]

3. GTM Score: [XX/100]
   - Top 3 Primary Motions (score 4.0-5.0): [List with scores]
   - Secondary Motions (score 3.0-3.9): [List with scores]
   - Overall GTM Band: [ELITE | STRONG | EMERGING | WEAK | NO READINESS]
```

### Secondary Inputs (If Available)

```
4. Strategy Selector Lite Path: [Replicate & Localize | Consulting-First | Boring Micro-SaaS | Hammering Deep]
5. Founder Context:
   - Business stage (pre-revenue, early revenue, scaling)
   - Target geography (UAE, KSA, Egypt, pan-MENA, global)
   - Available capital ($0-$5K, $5K-$25K, $25K-$100K, $100K+)
   - Team size (solo, 2-3, 4-10, 10+)
```

---

## STEP 1: CALCULATE FOUNDER READINESS SCORE

**Formula:** `Founder Readiness = (MAS × 0.35) + (ICP × 0.35) + (GTM × 0.30)`

### Readiness Bands

| Range | Band | Strategic Meaning |
|-------|------|-------------------|
| 80-100 | **LAUNCH READY** | All three pillars are strong. Execute aggressively. The market is real, you know who to sell to, and you have viable channels. Speed is your competitive advantage now. |
| 60-79 | **ALMOST THERE** | Two pillars are solid, one is dragging. Fix the weakest pillar before scaling spend. You're 30-60 days from being dangerous. |
| 40-59 | **NEEDS WORK** | Multiple gaps across pillars. Scaling now will burn cash. Focus the next 60 days on your two weakest sections (not just weakest pillar). |
| 20-39 | **EARLY STAGE** | Fundamental gaps in market validation, customer understanding, or distribution. Go back to buyer conversations before building. |
| 0-19 | **RESET** | The current idea-market-customer combo isn't working. Consider pivoting the market (MAS), the customer (ICP), or both. |

---

## STEP 2: IDENTIFY THE SCORE PATTERN ARCHETYPE

The consolidated score tells you HOW READY you are. The score PATTERN tells you WHAT TO DO. Two founders with a 62 readiness score can need completely different strategies depending on which pillar is strong and which is weak.

### The 8 Score Pattern Archetypes

#### Archetype 1: THE LAUNCHER
**Pattern:** MAS >= 70, ICP >= 70, GTM >= 60
**Meaning:** Market is real, customer is clear, channels exist. You're over-researching.
**Strategy:** Stop planning. Start selling. Ship this week.

**90-Day Plan:**
- Week 1-2: Activate your top 2 GTM motions simultaneously
- Week 3-4: Close first 3-5 paying customers
- Week 5-8: Iterate based on buyer feedback, not theory
- Week 9-12: Double down on the motion that's converting best

**Biggest Risk:** Perfectionism. The data says go. Trust the data.

---

#### Archetype 2: THE MARKET HUNTER
**Pattern:** MAS >= 70, ICP < 60, GTM any
**Meaning:** The market is attractive, but you don't know who specifically to sell to. You're chasing a market without a face.
**Strategy:** ICP Discovery Sprint. The market will wait for you if it's real. But selling to "everyone" means selling to no one.

**90-Day Plan:**
- Week 1-2: 15 discovery conversations with different buyer personas within the market
- Week 3-4: Identify the 1-2 buyer segments with strongest pain + purchasing power combo
- Week 5-6: Build ICP profile (Section A of ICP assessment should move to 20+/25)
- Week 7-8: Map congregation points for this specific buyer (Section B)
- Week 9-10: Build one lead magnet + test one hook (Section C)
- Week 11-12: Re-run ICP assessment. If >= 65, activate GTM.

**Biggest Risk:** Impatience. You'll want to start selling before the ICP is clear. Resist.

---

#### Archetype 3: THE CHANNEL SEEKER
**Pattern:** MAS >= 60, ICP >= 60, GTM < 50
**Meaning:** You know your market and your customer, but you haven't figured out how to reach them at scale. You can sell in a room. You can't sell to the internet yet.
**Strategy:** GTM Motion Testing. You need to find 2-3 repeatable channels.

**90-Day Plan:**
- Week 1-2: Review your GTM assessment. Which 3 motions scored highest? Activate the top 2.
- Week 3-4: Run 2 parallel GTM experiments (e.g., Dream 100 + Authority Education, or Signal Sniper + BOFU SEO)
- Week 5-8: Measure: Which motion generated more qualified leads per hour invested?
- Week 9-10: Kill the losing motion. Double down on the winner.
- Week 11-12: Add one secondary motion to complement primary.

**Biggest Risk:** Spreading across too many channels. Pick 2. Test. Kill 1. Add 1.

---

#### Archetype 4: THE SOLUTION SEEKER
**Pattern:** MAS < 50, ICP >= 60, GTM >= 60
**Meaning:** You know your customer and have channels to reach them, but the MARKET isn't validating. Pain isn't strong enough, purchasing power is low, or timing is off.
**Strategy:** Market Pivot or Reframe. Keep the customer, find a better problem.

**90-Day Plan:**
- Week 1-2: Interview 10 of your ICP. Ask: "What's the most expensive problem you're dealing with right now?" (Not what you THINK their problem is. What THEY say.)
- Week 3-4: Identify the top 3 pain points they mentioned. Score each on MAS dimensions (Pain Reality, Purchasing Power, Momentum, Competitive Advantage).
- Week 5-6: Pick the highest-scoring problem. Reframe your solution around it.
- Week 7-8: Test new positioning with 5 buyers. "Would you pay $X/month to solve [new framing]?"
- Week 9-12: If validated, re-run MAS with the new framing. If MAS >= 60, proceed.

**Biggest Risk:** Emotional attachment to the original problem. The customer is right. The market is right. You might be wrong about what they need.

---

#### Archetype 5: THE EXPERT WITHOUT A STAGE
**Pattern:** MAS >= 60, ICP < 50, GTM < 50
**Meaning:** The market exists, but you don't know your buyer AND you don't know how to reach them. You're an expert sitting in a room alone.
**Strategy:** Customer Development First. Everything else follows from knowing your buyer.

**90-Day Plan:**
- Week 1-4: ICP Discovery Sprint (same as Archetype 2, but more aggressive). 20+ conversations.
- Week 5-6: Build ICP profile. Map congregation points.
- Week 7-8: Based on WHERE your ICP congregates, identify which GTM motions are natural fits.
- Week 9-10: Activate 1 GTM motion. Just 1.
- Week 11-12: Measure. Adjust. Re-assess ICP + GTM.

**Biggest Risk:** Building product instead of talking to people. You don't have permission to build yet.

---

#### Archetype 6: THE GHOST
**Pattern:** MAS < 50, ICP < 50, GTM any
**Meaning:** No validated market, no clear customer. The GTM score is irrelevant because you're distributing something nobody wants to someone you can't identify.
**Strategy:** Full Reset. Go back to problem discovery.

**90-Day Plan:**
- Week 1-2: STOP all product work. STOP all marketing.
- Week 3-4: Pick 3 different problem-customer combos. Interview 5 people for each (15 total conversations).
- Week 5-6: Run MAS Lite on each combo. Pick the one scoring highest.
- Week 7-8: Run ICP Lite on the winning combo. If ICP Lite >= 14/20, proceed.
- Week 9-10: Build MVP or pilot for ONE use case.
- Week 11-12: Get 3 paying customers (even at discount). If you can't, restart.

**Biggest Risk:** Denial. "My idea is good, the market just doesn't understand it yet." If MAS < 50, the market has spoken.

---

#### Archetype 7: THE OPERATOR
**Pattern:** MAS < 50, ICP >= 60, GTM < 50
**Meaning:** You know your customer well (probably from consulting or services), but the market for a PRODUCT isn't validated and you don't have scalable channels. You're a service business trying to become a product business.
**Strategy:** Consulting-First SaaS. Lean into what's working (customer relationships) and extract the product from the service.

**90-Day Plan:**
- Week 1-2: List the top 5 repetitive tasks you do for clients. Which one could be automated?
- Week 3-4: Build a rough prototype (even a spreadsheet or Supabase table) that automates one task.
- Week 5-6: Give it to your 3 best clients for free. "Test this. Tell me if it saves you time."
- Week 7-8: Iterate based on feedback. Can this become self-serve?
- Week 9-10: Price it. Offer existing clients a subscription for the tool.
- Week 11-12: If 3+ clients pay, you have product-market fit signal. Now run MAS on this specific product.

**Biggest Risk:** Never shipping. The consulting revenue is comfortable. The product is scary. Ship anyway.

---

#### Archetype 8: THE SCRAMBLER
**Pattern:** All three scores < 50
**Meaning:** Nothing is validated yet. This is not a failure. This is starting from scratch. Most founders start here but don't know it.
**Strategy:** Demand-First Discovery. Do NOT build anything. Go find demand.

**90-Day Plan:**
- Week 1-4: 30 conversations with 3 different potential buyer segments (10 each).
- Week 5-6: Score each segment on MAS Lite. Pick the winner.
- Week 7-8: Build ICP profile for the winning segment. 5 more deep conversations.
- Week 9-10: Test one GTM motion (the simplest available: Dream 100, manual outbound, or speaking).
- Week 11-12: If you have 2+ interested buyers willing to pay, you've found something. Run full MAS + ICP.

**Biggest Risk:** Staying in this phase too long. Set a 90-day deadline. If nothing validates by Day 90, try a completely different problem space.

---

## STEP 3: CROSS-PILLAR BOTTLENECK ANALYSIS

Beyond the archetype, identify the specific SECTIONS across all 3 assessments that are dragging the score. This reveals the surgical interventions that move the needle fastest.

### Bottleneck Priority Matrix

Rank all sections by their weighted impact on the consolidated score. Lower-scoring sections with higher weight = bigger bottleneck.

**Calculation:**
```
Section Impact = (Section Max Points / Assessment Max Points) × Assessment Weight × (1 - Section Score / Section Max Points)
```

**Example:**
- MAS Pain Reality: (25/100) × 0.35 × (1 - 15/25) = 0.035 impact
- ICP WHO: (25/100) × 0.35 × (1 - 10/25) = 0.053 impact ← bigger bottleneck

### Claude Should:
1. Calculate impact score for every section across all 3 assessments
2. Rank them by impact (highest = biggest bottleneck)
3. Present the top 5 bottleneck sections
4. For each: name the section, current score, what a 5-point improvement would do to the consolidated score, and the specific recommendation from that assessment's skill

### Cross-Pillar Interaction Effects

Some bottlenecks compound across pillars. Flag these:

| If This Is Low... | And This Is Low... | Compound Effect |
|---|---|---|
| MAS Pain Reality | ICP Dream Customer | You're guessing about pain AND who feels it. Interview buyers immediately. |
| MAS Purchasing Power | ICP Guarantee Structure | You can't prove value AND they can't pay. Rethink pricing or buyer. |
| MAS Competitive Advantage | GTM (all motions low) | No defensibility AND no distribution. Dangerous combination. Consider niche harder. |
| ICP Congregation Points | GTM (channel motions) | You don't know where buyers are AND you can't reach them. Map 5 congregation points this week. |
| ICP Hook Strength | GTM Authority Education | Your messaging doesn't land AND you're trying to teach. Fix the message before producing content. |
| MAS Market Momentum | GTM Wave Riding | No tailwinds AND you're trying to ride them. Switch to Dream 100 or Signal Sniper instead. |
| ICP Attractive Character | GTM Build-in-Public | No personal brand AND you're trying to build in public. Build the character identity first. |
| MAS MENA Readiness | GTM MENA Viability (across motions) | The region isn't ready AND your channels don't work there. Consider starting with UAE/KSA only or going global-first. |

---

## STEP 4: STRATEGY PATH ALIGNMENT

### Mapping Consolidated Profile to the 4 Strategy Paths

The Strategy Selector Lite recommends one of 4 paths based on a short questionnaire. The deep assessments either CONFIRM or CHALLENGE that recommendation.

#### Path 1: Replicate & Localize
**Confirmed when:** MAS Market Momentum >= 4 (section C average), MAS Competitive Advantage D4 (Arabic/MENA Moat) >= 3, ICP >= 60, GTM has Authority Education or BOFU SEO as primary.
**Challenged when:** MAS < 50 (the market may not exist in MENA), GTM shows no viable Arabic-content motions, ICP Congregation shows no MENA-specific gathering points.
**If challenged:** Consider global-first approach, or pick a different market to replicate into.

#### Path 2: Consulting-First SaaS
**Confirmed when:** ICP >= 60 (you know your customer from consulting), MAS < 60 (product-market fit is unproven), GTM has Dream 100 or 7x4x11 as primary.
**Challenged when:** MAS >= 75 (market is ready for product, consulting is a speed tax), GTM shows Paid VSL or Waitlist as primary (these need a product, not a service).
**If challenged:** Skip consulting phase. Go straight to product with your ICP knowledge.

#### Path 3: Boring Micro-SaaS
**Confirmed when:** MAS Pain Reality >= 20/25 (specific, quantifiable pain), MAS Competitive Advantage D5 (Speed to Value) >= 4 (same-day results), ICP has narrow WHO (specific buyer, not broad), GTM has BOFU SEO or Signal Sniper as primary.
**Challenged when:** ICP is broad (trying to serve everyone), MAS shows the market requires education (Market Momentum < 3 average), GTM relies on content-heavy motions.
**If challenged:** Niche harder. Boring Micro-SaaS only works when the problem is specific and the buyer is narrow.

#### Path 4: Hammering Deep
**Confirmed when:** MAS Competitive Advantage D1 (Differentiation) >= 4 (crystal clear one-sentence differentiator), ICP WHO >= 20/25 (vivid buyer), GTM has Outcome Demo or Hammering Launches as primary.
**Challenged when:** MAS Competitive Advantage D3 (Unfair Advantage) < 2 (no moat), ICP shows multiple buyer segments (not one focused persona), GTM fitness is weak across all motions.
**If challenged:** You need a moat before you can hammer. Build the unfair advantage first.

### Strategy Path Output

```
RECOMMENDED PATH: [Path name]
CONFIDENCE LEVEL: [CONFIRMED | CONFIRMED WITH CAVEATS | CHALLENGED — REVIEW NEEDED]

RATIONALE:
- [2-3 sentences explaining why the assessments confirm or challenge this path]

IF CONFIRMED:
- Proceed with [specific next actions]

IF CHALLENGED:
- Consider [alternative path] because [specific data point from assessments]
- Or fix [specific bottleneck] before committing to this path
```

---

## STEP 5: GTM MOTION PRESCRIPTION

Based on the combined MAS + ICP profile, refine the GTM motion recommendations. The GTM skill scores motions in isolation. This skill adjusts those recommendations based on market and customer context.

### Motion Adjustment Rules

| Market Condition (MAS) | Customer Condition (ICP) | Motion Adjustments |
|---|---|---|
| Pain high, momentum high | WHO clear, attraction strong | Aggressive motions: Paid VSL, Signal Sniper, Hammering Launches. Speed wins. |
| Pain high, momentum low | WHO clear, attraction strong | Educational motions: Authority Education, Value Trust Engine. You need to create the category. |
| Pain high, momentum high | WHO fuzzy, attraction weak | Broad discovery motions: Build-in-Public, Wave Riding. Use content to find your buyer. |
| Pain low, momentum high | WHO clear, attraction strong | Reframe the pain. The market is moving but your angle doesn't land. Fix positioning before activating motions. |
| Pain high, purchasing power low | Any ICP | Free-tier or freemium strategy. Use LTD Cash-to-MRR. Avoid Paid VSL (economics won't work). |
| Any MAS | Congregation clear | Dream 100 + 7x4x11 targeting those exact congregation points. |
| Any MAS | Congregation unknown | Do NOT activate outbound motions. Map congregation first. |
| MENA Readiness high | Any ICP | Prioritize Arabic content motions: BOFU SEO (Arabic keywords are massively underserved), Authority Education (Arabic), Value Trust Engine (Arabic bootcamps). |
| MENA Readiness low | Any ICP | Go UAE/KSA first (most digital-ready). Or target English-first MENA buyers (multinationals, diaspora). |

### Output Format

```
YOUR GTM PRESCRIPTION (Based on Combined Profile)

PRIMARY MOTIONS (Execute now):
1. [Motion Name] — Score: [X/5] — WHY: [1-sentence based on MAS+ICP alignment]
2. [Motion Name] — Score: [X/5] — WHY: [1-sentence]

SECONDARY MOTIONS (Build capacity, activate in 60 days):
3. [Motion Name] — Score: [X/5] — WHY: [1-sentence]

MOTIONS TO AVOID (Despite decent GTM scores):
- [Motion Name] — WHY: [Specific MAS or ICP conflict]

MOTION SEQUENCING:
Week 1-4: [Primary Motion 1] — Measure: [KPI]
Week 5-8: [Primary Motion 1 + Primary Motion 2] — Measure: [KPIs]
Week 9-12: [Winner + Secondary Motion] — Measure: [KPIs]
```

---

## STEP 6: DEMAND-FIRST MATRIX POSITIONING

Map the founder into the Demand-First Matrix using the assessment data:

### Matrix Quadrants

```
                    HIGH MAS (Market Pull)
                           |
         VALIDATE          |          SCALE
    (Strong market,        |    (Strong market,
     weak execution)       |     strong execution)
                           |
   ————————————————————————+————————————————————————
                           |
         BUILD             |         OPTIMIZE
    (Weak market,          |    (Weak market but
     weak execution)       |     strong execution)
                           |
                    LOW MAS (Market Push)
```

**X-Axis:** Execution Readiness = (ICP × 0.5) + (GTM × 0.5)
**Y-Axis:** Market Pull = MAS score

| Quadrant | MAS | Execution (ICP+GTM avg) | Strategic Mode |
|----------|-----|------------------------|----------------|
| **SCALE** | >= 65 | >= 65 | Accelerate. Spend on growth. Hire. Automate. |
| **VALIDATE** | >= 65 | < 65 | Market is ready. You're not. Fix ICP and/or GTM. Don't slow-walk this, the market window has an expiration date. |
| **OPTIMIZE** | < 65 | >= 65 | You can execute but the market isn't pulling. Reposition, reframe the pain, or pivot the market. |
| **BUILD** | < 65 | < 65 | Foundation work. Buyer conversations, ICP clarity, basic GTM testing. No paid spend yet. |

### Quadrant-Specific Playbook

**SCALE Quadrant:**
- Activate 3+ GTM motions simultaneously
- Budget: Allocate 15-25% of revenue to growth
- Hire: First hire should be in your primary GTM motion (SDR for outbound, content person for education, etc.)
- Automation: Build n8n workflows to scale what's working manually
- Timeline: 90-day sprint to 2-3x current revenue
- MENA: If in UAE/KSA, expand to Egypt/Jordan. If single-country, go pan-Gulf.

**VALIDATE Quadrant:**
- DO NOT increase spending until ICP + GTM improve
- Spend 80% of time on buyer conversations and channel testing
- Run 2 GTM experiments per month. Kill losers fast.
- Budget: Minimal. Under $2K/month on marketing. Rest goes to learning.
- Timeline: 60 days to get ICP >= 65 and GTM >= 55. Then move to SCALE.
- MENA: Focus on one country. Don't expand until validated.

**OPTIMIZE Quadrant:**
- Your execution is strong but the market isn't responding. Something is wrong with positioning.
- Re-run MAS with 3 different problem framings. Find the one that scores highest.
- Consider: Are you solving a real pain or a "nice to have"?
- Budget: Pause paid spend. Invest in repositioning research.
- Timeline: 45 days of repositioning. If MAS doesn't improve, pivot the market entirely.
- MENA: Consider whether the product is too early for MENA. Maybe start in a more digital-ready market (UK, global English) and circle back.

**BUILD Quadrant:**
- You're at the beginning. That's fine. Most honest founders are here.
- Priority order: MAS first (find a real market), then ICP (find real buyers), then GTM (find real channels).
- Budget: $0 on marketing. Spend on conversations only.
- Timeline: 90 days of pure research and customer development. No product building allowed.
- MENA: Pick ONE city. Dubai, Riyadh, or Cairo. Talk to 30 people. That's your first quarter.

---

## STEP 7: 90-DAY STRATEGIC ROADMAP

Synthesize everything into a single executable plan.

### Roadmap Template

```
════════════════════════════════════════════════════════════════
           FOUNDER STRATEGY ROADMAP
════════════════════════════════════════════════════════════════

FOUNDER: [Name]
DATE: [Assessment Date]
FOUNDER READINESS SCORE: [XX/100]
READINESS BAND: [Band]
SCORE PATTERN: [Archetype Name]
DEMAND-FIRST QUADRANT: [SCALE | VALIDATE | OPTIMIZE | BUILD]
STRATEGY PATH: [Path Name] — [CONFIRMED | CHALLENGED]

════════════════════════════════════════════════════════════════
PILLAR SCORES
════════════════════════════════════════════════════════════════

MAS: [XX/100] — [Band]
  Strongest: [Section name + score]
  Weakest:   [Section name + score]

ICP: [XX/100] — [Band]
  Strongest: [Section name + score]
  Weakest:   [Section name + score]

GTM: [XX/100] — [Band]
  Primary Motions: [Top 2-3 with scores]
  Skip Motions:    [Bottom 2-3 with scores]

════════════════════════════════════════════════════════════════
TOP 5 BOTTLENECKS (Biggest Impact Actions)
════════════════════════════════════════════════════════════════

1. [Section] — Current: [X/Max] — If fixed: +[X] to Readiness
   ACTION: [Specific action from assessment recommendation engine]

2. [Section] — Current: [X/Max] — If fixed: +[X] to Readiness
   ACTION: [Specific action]

3. [Section] — Current: [X/Max] — If fixed: +[X] to Readiness
   ACTION: [Specific action]

4. [Section] — Current: [X/Max] — If fixed: +[X] to Readiness
   ACTION: [Specific action]

5. [Section] — Current: [X/Max] — If fixed: +[X] to Readiness
   ACTION: [Specific action]

════════════════════════════════════════════════════════════════
GTM PRESCRIPTION
════════════════════════════════════════════════════════════════

PRIMARY: [Motion 1], [Motion 2]
SECONDARY: [Motion 3]
AVOID: [Motion X] because [reason from MAS/ICP conflict]

════════════════════════════════════════════════════════════════
90-DAY PLAN
════════════════════════════════════════════════════════════════

MONTH 1: [Theme — e.g., "ICP Discovery Sprint"]
  Week 1: [Actions]
  Week 2: [Actions]
  Week 3: [Actions]
  Week 4: [Actions]
  Month 1 KPIs: [Measurable outcomes]

MONTH 2: [Theme — e.g., "GTM Motion Testing"]
  Week 5: [Actions]
  Week 6: [Actions]
  Week 7: [Actions]
  Week 8: [Actions]
  Month 2 KPIs: [Measurable outcomes]

MONTH 3: [Theme — e.g., "Scale What Works"]
  Week 9: [Actions]
  Week 10: [Actions]
  Week 11: [Actions]
  Week 12: [Actions]
  Month 3 KPIs: [Measurable outcomes]

════════════════════════════════════════════════════════════════
RE-ASSESSMENT TRIGGERS
════════════════════════════════════════════════════════════════

Re-run assessments when:
- [ ] 90 days elapsed
- [ ] First 5 paying customers acquired
- [ ] Primary GTM motion generating consistent leads
- [ ] Major pivot in problem, ICP, or market
- [ ] Entering a new geography

TARGET SCORES FOR NEXT ASSESSMENT:
- MAS: [Current] → [Target]
- ICP: [Current] → [Target]
- GTM: [Current] → [Target]
- Readiness: [Current] → [Target]

════════════════════════════════════════════════════════════════
```

---

## MENA-SPECIFIC STRATEGIC ADJUSTMENTS

### Geography-Based Strategy Modifiers

**UAE/KSA (Tier 1 Markets):**
- Higher purchasing power = more aggressive pricing acceptable
- English + Arabic content strategy works
- LinkedIn is the primary B2B channel
- Events: GITEX, STEP, Seamless are high-value congregation points
- Sales cycle: 30-60 days for SME, 60-120 days for enterprise
- Recommendation: If MENA Readiness is high, target UAE/KSA first. Always.

**Egypt/Jordan/Lebanon (Tier 2 Markets):**
- Lower purchasing power = freemium or tiered pricing required
- Facebook/WhatsApp dominate over LinkedIn for SMEs
- Arabic-first content is mandatory (English doesn't penetrate SME)
- Sales cycle: 45-90 days, relationship-heavy
- Recommendation: Only expand here AFTER validating in Tier 1 OR if your ICP is specifically in these markets.

**Pan-MENA Strategy:**
- DO NOT launch pan-MENA from day 1. Pick one country. Validate. Expand.
- Payment infrastructure varies dramatically (UAE = cards + Tabby; Egypt = bank transfers + Fawry)
- Legal entities differ. Each country has separate requirements.
- Recommendation: Start with one city (Dubai, Riyadh, or Cairo). Go pan-MENA only after 10+ paying customers in one market.

### Cultural Strategy Modifiers

**If ICP Section F (Attractive Character) is low AND target is MENA:**
- Personal brand matters more in MENA than in Western markets
- Founders who build authority through Arabic content + events convert 3-5x better
- Action: Invest in 90 days of Arabic content (LinkedIn posts, YouTube shorts, event speaking) BEFORE scaling outbound

**If MAS Section D4 (Arabic/MENA Moat) is high (>= 4):**
- You have a defensible advantage. Protect and market it aggressively.
- Position as "built for MENA" not "translated to Arabic"
- Use this moat as the primary message in all GTM motions

**If GTM shows Dream 100 as primary AND target is MENA:**
- This is the most natural MENA motion. Relationships ARE distribution in the Gulf.
- Build the list from GITEX attendees, LinkedIn connections, and referral mapping.
- Personalization > automation. In MENA, a personal note beats a sequenced campaign.

---

## CLAUDE EXECUTION FLOW

When this skill is invoked, follow these steps exactly:

### Phase 1: Data Collection (2 min)
If scores are not already provided:
> "I need your results from all three EO assessments to build your strategy. Can you share:
> 1. Your MAS score and section breakdown
> 2. Your ICP score and section breakdown
> 3. Your GTM score, including your top primary and secondary motions
>
> If you have your Strategy Selector Lite result too, share that as well."

### Phase 2: Readiness Calculation (30 sec)
Calculate the Founder Readiness Score. State it clearly.

### Phase 3: Pattern Recognition (1 min)
Identify which of the 8 archetypes matches their score pattern. If it's between two archetypes, pick the one where the dominant weakness is clearest.

### Phase 4: Bottleneck Analysis (2 min)
Calculate the top 5 cross-pillar bottlenecks. Check for compound interaction effects.

### Phase 5: Strategy Path Alignment (1 min)
If Strategy Selector Lite result is available, confirm or challenge it.
If not available, recommend the path based on assessment data alone.

### Phase 6: GTM Prescription (2 min)
Adjust GTM motion recommendations based on MAS + ICP context. Sequence them.

### Phase 7: Quadrant Mapping (1 min)
Map to Demand-First Matrix. Apply quadrant-specific playbook.

### Phase 8: Roadmap Assembly (3 min)
Build the full 90-day roadmap using the template. Be specific. No vague actions.

### Phase 9: Delivery
Present the complete Founder Strategy Roadmap. End with:

> "This roadmap is based on where you are today. The scores will change as you execute. Re-run all three assessments at the 90-day mark. The founders who improve fastest are the ones who do the hard thing first: fix their biggest bottleneck, not polish their strengths.
>
> Your biggest bottleneck right now is [Section Name]. Fix that, and your readiness score moves from [current] to approximately [projected]. That's the highest-leverage move you can make this month."

---

## SCORING PHILOSOPHY

### Why Weights Are 35/35/30

MAS and ICP carry equal weight (35% each) because a great market with no customer clarity is equally dangerous as perfect customer knowledge in a dead market. Neither can compensate for the other.

GTM carries slightly less weight (30%) because distribution is the most fixable of the three pillars. A founder can learn new channels in 60 days. But validating a market or understanding a buyer takes longer and has less room for error.

### Why Patterns Matter More Than Totals

A founder scoring 55/100 with MAS=80, ICP=45, GTM=40 is in a fundamentally different position than a founder scoring 55/100 with MAS=45, ICP=60, GTM=60. The first has a real market but can't execute. The second can execute but is in the wrong market. The strategic advice is opposite.

This is why this skill exists. The individual assessments tell you what's strong and what's weak. This skill tells you what to DO about the combination.

### Why 90 Days, Not 30

Each individual assessment gives a 30-day action plan for improving THAT pillar. But when you're optimizing across 3 pillars simultaneously, you need 90 days because:
- Month 1: Fix the biggest bottleneck
- Month 2: Activate GTM motions with improved foundation
- Month 3: Measure, iterate, prepare for re-assessment

Trying to fix everything in 30 days leads to surface-level improvements that don't stick.

---

## INTEGRATION WITH N8N CONSOLIDATED WORKFLOW

This skill is the logic that the n8n consolidated workflow (webhook: `eo-consolidated`) calls via Claude API. The workflow:

1. Triggers when a founder's email has all 3 assessment records in Supabase
2. Fetches scores from the `eo_founder_readiness` view
3. Calls Claude with this skill's logic and all 3 score sets
4. Receives the full strategy roadmap
5. Stores the result in Supabase (add `strategy_recommendation JSONB` column to `eo_assessments` or create new `eo_strategy` table)
6. Updates GHL with tag `eo-full-assessed` + strategy band
7. Sends founder the consolidated email with their roadmap

### Claude API Prompt Template (for n8n)

```
You are the EO Strategy Selector. You have the Strategy Selector skill loaded.

Here are the founder's three assessment results:

MAS: {{MAS_SCORE}}/100
  Pain Reality: {{mas_pain_reality}}/25
  Purchasing Power: {{mas_purchasing_power}}/25
  Market Momentum: {{mas_market_momentum}}/25
  Competitive Advantage: {{mas_competitive_advantage}}/25
  Band: {{MAS_BAND}}

ICP: {{ICP_SCORE}}/100
  WHO (Dream Customer): {{icp_who}}/25
  WHERE (Congregation): {{icp_where}}/20
  WHAT CAPTURE (Attraction): {{icp_capture}}/20
  RESULT (Transformation): {{icp_result}}/15
  Epiphany Bridge: {{icp_epiphany}}/10
  Attractive Character: {{icp_character}}/10
  Band: {{ICP_BAND}}

GTM: {{GTM_SCORE}}/100
  Primary Motions: {{gtm_primary_motions}}
  Secondary Motions: {{gtm_secondary_motions}}
  Band: {{GTM_BAND}}

Strategy Selector Lite Path: {{lite_path}}
Target Geography: {{geography}}
Business Stage: {{stage}}

Execute the full Strategy Selector flow:
1. Calculate Founder Readiness Score
2. Identify Score Pattern Archetype
3. Run Cross-Pillar Bottleneck Analysis
4. Confirm/Challenge Strategy Path
5. Prescribe GTM Motions
6. Map to Demand-First Matrix Quadrant
7. Build 90-Day Strategic Roadmap

Output the complete Founder Strategy Roadmap.
```

---

## EDGE CASES

### When Two Archetypes Fit Equally

If the score pattern matches two archetypes, default to the one that prioritizes ICP. Reason: customer clarity compounds faster than market research or GTM testing. A founder who deeply understands their buyer can adapt to any market or channel shift. A founder who doesn't understand their buyer will fail at every motion.

### When Strategy Selector Lite Conflicts With Deep Assessments

Trust the deep assessments. The Lite version uses 8-12 questions. The deep assessments use 20 questions each (60 total). More data wins. When presenting the conflict, frame it as: "Your initial instinct was [Lite Path], but the deeper analysis suggests [Alternative]. Here's why..."

### When Founder Is Pre-Revenue

Adjust the 90-day plan to focus on validation, not scale:
- Replace "revenue KPIs" with "buyer conversations completed" and "willingness signals collected"
- Replace "activate GTM motions" with "test one motion with manual execution"
- Replace "hire" with "do it yourself first, then systematize"

### When Founder Has Existing Revenue (> $10K MRR)

Adjust the strategy to protect existing revenue while improving weak pillars:
- Don't stop what's currently generating revenue, even if the assessment says the motion scores low
- Layer improvements on top of existing channels
- Use revenue to fund GTM experiments (allocate 15-20% to testing new motions)

### When Founder Is Pan-MENA vs. Single Country

Pan-MENA founders should be advised to focus on one country until ICP >= 70 in that market. Spreading across countries prematurely dilutes every pillar score. The exception: if they're already generating revenue in 2+ countries, treat each as a separate ICP assessment.

---

## VERSION HISTORY

- **v1.0** (Feb 2026): Initial framework. 8 archetypes, cross-pillar bottleneck analysis, GTM motion prescription, Demand-First Matrix mapping, 90-day roadmap template, MENA strategic adjustments, n8n integration spec.

---

## DEPENDENCY MAP

```
Strategy Selector Skill
├── REQUIRES: Market Attractiveness Scoring (/skills/market-attractiveness-scoring/SKILL.md)
├── REQUIRES: ICP Clarity Scoring (/skills/icp-clarity-scoring/SKILL.md)
├── REQUIRES: GTM Fitness Scoring (/skills/gtm-fitness-scoring/SKILL.md)
├── REFERENCES: Strategy Selector Lite (EO-Strategy-Selector.html)
├── REFERENCES: Demand-First Matrix (frameworks.md Section 2)
├── INTEGRATES: n8n Consolidated Workflow (EO-Assessment-n8n-Architecture.md Section 4)
└── STORES: Supabase eo_founder_readiness view
```

---

**This skill is the capstone of the EO Assessment System. Without it, founders get three separate diagnoses but no treatment plan. With it, they get a unified strategy that accounts for how markets, customers, and channels interact. The individual assessments are the blood tests. This skill is the doctor.**
