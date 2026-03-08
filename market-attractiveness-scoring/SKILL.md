---
name: market-attractiveness-scoring-engine
description: Scorecard 3 of 5 — Evidence-based market attractiveness in 6 questions / 25 minutes. Evaluates Pain Reality, Purchasing Power, Market Sizing, and Growth signals. Scores /100.
version: "3.0"
---

# SKILL: Market Attractiveness Scoring Engine (SC3)

**Version:** 3.0
**Created:** 2026-03-08
**Framework:** Alex Hormozi ($100M Leads), Hormozi's Grand Slam (Dream × Likelihood) / (Delay × Effort)
**Input Sources:** SC1 (Project Definition) + SC2 (ICP Clarity)
**Output File:** `MarketAttractiveness.md`
**Execution Model:** 4-section flow (A: AI auto-load | B: 3 FT/MC questions | C: 3 FT/MC questions | D: AI synthesis) = ~25 minutes

---

## 1. STRATEGIC PURPOSE

Market Attractiveness Scoring (MAS v3.0) determines whether a market is worth entering in 25 minutes through 6 evidence-based questions instead of 25. The system strips away assumption-based ratings and requires concrete evidence: customer conversations, pricing benchmarks, TAM/SAM/SOM calculations, and growth signals.

**V3.0 Philosophy:**
- Shorter: 6 questions instead of 25 (15 min of questions + 10 min of input/output)
- Focused: Pain Reality → Purchasing Power → Market Sizing → Growth
- Evidence-first: No rating scales; only "cite your evidence"
- Synthesis-ready: AI auto-scores using Hormozi framework

**Core Shift:**
- Old (v2): "Rate pain 1-5 on frequency, cost, urgency." (5 questions, high subjectivity)
- New (v3): "Show evidence that: (1) pain is real, (2) ICP can pay, (3) market is sizeable, (4) market is growing" (6 focused questions)

---

## 2. PREREQUISITES

This scorecard builds on upstream data. Do not administer until student has completed:

| Prerequisite | Provides | Used In |
|--------------|----------|---------|
| **SC1: Project Definition** | Niche, sub-market, positioning, geography, product scope | Sections B, C, D |
| **SC2: ICP Clarity** | Pain statements, congregation points, budget range, buying behavior | Sections A, B, C |

**Pre-Admin Checklist:**
- Display SC1 outputs (niche, positioning, geography, ICP)
- Display SC2 outputs (pain statements, congregation points, budget range)
- Ask student: "Are these still accurate? Any updates?"
- Note any updates; flag for cross-scorecard consistency review

---

## 3. SECTION ARCHITECTURE

| Section | Points | Questions | Duration | Focus |
|---------|--------|-----------|----------|-------|
| **A. Upstream Confirmation** | 0 | 0 (AI auto) | 3 min | Load + display SC1/SC2 data; confirm or update |
| **B. Evidence Validation** | 40 | 3 (2 FT, 1 MC) | 10 min | Real evidence that pain is real and budget exists |
| **C. Market Sizing & Growth** | 40 | 3 (2 FT, 1 MC) | 10 min | TAM/SAM/SOM + growth signals + competitive gap |
| **D. AI Synthesis** | 20 | 0 (AI auto) | 2 min | AI scores overall MAS from upstream + new data |
| **TOTAL** | **100** | **6 user-facing** | **~25 min** | |

### Score Bands

| Range | Band | Meaning | Risk | Action |
|-------|------|---------|------|--------|
| **85-100** | LAUNCH READY | Strong evidence across all dimensions | Low | Execute GTM; move to SC5 |
| **70-84** | ALMOST THERE | Solid core appeal; 1-2 sections need validation | Low-Med | Fix weakest section; re-score; confirm |
| **55-69** | NEEDS WORK | Right direction but significant gaps | Medium | 30-day validation plan required |
| **40-54** | EARLY STAGE | Fundamental validation needed | Med-High | 10+ buyer interviews before GTM |
| **0-39** | RESET | Core assumptions likely wrong | High | Revisit SC1/SC2; consider pivot |

---

## 4. SECTION A: UPSTREAM CONFIRMATION (0 POINTS, 0 USER QUESTIONS)

**Goal:** Load upstream data from SC1 + SC2; confirm accuracy; flag updates for consistency review.

### Process

**Step 1: Load SC1 Outputs**
Display to student:
- Niche & Sub-market: [from SC1]
- Positioning: [from SC1]
- Target geography: [from SC1]
- Product scope: [from SC1]

**Step 2: Load SC2 Outputs**
Display to student:
- Pain statements: [from SC2, list all]
- Congregation points: [from SC2, list all]
- Budget range: [from SC2]
- Buying behavior: [from SC2]

**Step 3: Confirmation**
Ask student: "Are these still accurate, or do you want to update anything?"

**Action if Updates:**
- Record updates
- Flag for cross-scorecard consistency review at end
- Note: "I'll check if these updates affect your SC1 or SC2 data"

**No Scoring:** Section A is context-loading only. Zero points assigned.

---

## 5. SECTION B: EVIDENCE VALIDATION (40 POINTS, 3 QUESTIONS)

**Goal:** Validate that pain is real (not assumption) and ICP can & will pay (not aspirational).

### B1. Pain Evidence Strength (15 pts)
**Type:** Free-text, 200 words
**Question:**
> What EVIDENCE do you have that this pain is real? Cite: customer conversations, competitor reviews, market data, personal experience, regulatory signals. Don't tell me pain exists — SHOW me proof.

**Display:** Show SC2 pain statements as reference. Provide example of strong answer.

**AI Scoring Rubric:**

| Score | Criteria |
|-------|----------|
| 0 | Blank or off-topic |
| 1 | Assertion only ("I think people have this pain") |
| 2 | Generic evidence ("Asked people" or "did research") |
| 3 | Partial evidence (1-2 evidence types, some vagueness) |
| 6 | Decent evidence (2 distinct types + some specificity) |
| 9 | Strong evidence (2+ types across multiple pains; named sources; specific numbers) |
| 12 | Very strong evidence (3+ types; all named/specific; consistent across pains) |
| 15 | Expert evidence (3+ types; pitch-deck ready; could present to investor today) |

**Evaluation Process:**
1. Extract evidence types cited (conversations, competitor data, market research, regulatory, personal)
2. Count distinct types; assess diversity
3. Verify specificity: Named sources + numbers (high) vs. generic (low)
4. Check consistency with SC2 pain statements
5. Assess pitch-readiness: Could founder include this in investor deck?

**Improvement (if <9):**
- Score 0-3: "Schedule 3 buyer conversations: 'How does this pain show up for you?' Document names + quotes."
- Score 3-6: "Add one more evidence type: competitor data (G2, Capterra), market data (Google Trends), or regulatory signal."
- Score 6-9: "Expand one evidence type. If you have interviews, add 2-3 more quotes. If you have competitor data, quantify it."

---

### B2. Purchasing Power Evidence (15 pts)
**Type:** Free-text, 200 words
**Question:**
> What EVIDENCE do you have that your ICP can and will PAY? Cite: competitor pricing, customer interviews about budget, industry benchmark data, payment method availability. Show me their willingness + ability to pay.

**AI Scoring Rubric:**

| Score | Criteria |
|-------|----------|
| 0 | Blank |
| 1 | Assertion only ("I think they can pay") |
| 2 | Generic evidence ("People have budgets for this") |
| 3 | Partial evidence (1-2 types, some specificity) |
| 6 | Decent evidence (2 distinct types; some numbers) |
| 9 | Strong evidence (2+ types; named competitors; budget benchmarks + interview quotes) |
| 12 | Very strong evidence (3+ types; specific prices; payment methods validated) |
| 15 | Expert evidence (All 4 components: interviews + competitor pricing + budget benchmarks + payment infrastructure) |

**Evaluation Process:**
1. Extract evidence types: customer interviews (intent), competitor pricing (ability), industry benchmarks (standard), payment methods (infrastructure)
2. Assess specificity: Named competitor + actual price (high) vs. "market rates" (low)
3. Verify consistency with SC2 budget range
4. Check willingness signals: Would ICP choose your product?

**Improvement (if <9):**
- Score 0-3: "Ask 5 ICPs: 'Would you pay $[your price] to solve this pain?' Get 3+ explicit yes answers."
- Score 3-6: "Research 3 competitors' pricing. Also get 2-3 customer willingness quotes."
- Score 6-9: "Add one more: industry benchmarks OR validate payment methods work in your geography."

---

### B3. Purchasing Evidence Type (10 pts)
**Type:** Multiple Choice
**Question:** Which best describes your evidence base for purchasing power?

**Options:**
- **(10 pts)** Primary research: I've interviewed 5+ ICPs with documented responses about budget + willingness
- **(7 pts)** Mixed research: Interviews (3-4) + competitor pricing analysis + some market data
- **(5 pts)** Secondary research only: Analyzed competitor pricing, reviews, market reports (no direct customer conversations)
- **(2 pts)** Assumption-based: Logical reasoning but no direct customer/market evidence

---

**ENGAGEMENT AFTER B SECTION:**

> "Your evidence base is [strong/moderate/weak]. Here's what that means: [AI-generated 2-3 sentence insight]"
>
> "You've validated your pain with real evidence, not assumptions. That alone puts you ahead of 80% of founders."

---

**Section B Total:** B1 (0-15) + B2 (0-15) + B3 (0-10) = **0-40 pts**

---

## 6. SECTION C: MARKET SIZING & GROWTH (40 POINTS, 3 QUESTIONS)

**Goal:** Validate that market is sizeable AND growing AND you have defensible positioning.

### C1. Market Sizing (TAM/SAM/SOM) (15 pts)
**Type:** Free-text, 250 words
**Question:**
> Estimate your TAM → SAM → SOM. Show your math. Example: TAM = $50B global HR tech → SAM = $2B MENA mid-market → SOM = $50M UAE finance teams under 500 employees.

**AI Scoring Rubric:**

| Score | Criteria |
|-------|----------|
| 0 | Blank |
| 1 | No math ("Market is big") |
| 2 | Rough estimates (plausible but unsourced) |
| 3 | Some math (basic estimates, 1-2 layers, sources unclear) |
| 6 | Decent math (all 3 layers with some sources) |
| 9 | Strong math (all 3 layers with cited sources, logic is clear) |
| 12 | Very strong math (sources named, sensitivity analysis, MENA-specific adjustments) |
| 15 | Expert model (All above + bottom-up validation from customer count) |

**Evaluation Process:**
1. Extract TAM, SAM, SOM figures and formulas
2. Verify narrowing logic: Is each layer smaller than previous?
3. Check source quality: Named source vs. "online research"
4. Assess MENA-specificity: Did they use global numbers or localize?
5. Calculate bottoms-up: # of companies × ACV = SOM (verify it's realistic)

**Improvement (if <9):**
- Score 0-3: "Find ONE good source (Statista, Gartner, IBISWorld) for global market size. Build from there."
- Score 3-6: "You have estimates. Add sources. For each number, cite where it came from."
- Score 6-9: "Good math. Validate bottoms-up: 'I'm targeting [X] companies in [geography] at $[ACV]. X × ACV = [SOM].'"

---

### C2. Growth Signals (15 pts)
**Type:** Free-text, 200 words
**Question:**
> What growth signals exist in this market? (New entrants, funding rounds, regulatory changes, technology shifts, hiring trends, search volume trends) Show me this market is growing.

**AI Scoring Rubric:**

| Score | Criteria |
|-------|----------|
| 0 | Blank |
| 1 | Vague ("Market is growing") |
| 2 | Generic signals (1-2 signals with no dates/specificity) |
| 3 | Some specific (2-3 signals with partial dates/sources) |
| 6 | Decent signals (2-3 specific signals with dates; some sources) |
| 9 | Strong signals (4+ signals across categories with dates/sources) |
| 12 | Very strong (5+ signals, diversity across types, timeline clear) |
| 15 | Expert (Comprehensive signal map with implications for buyer urgency) |

**Evaluation Process:**
1. Extract distinct signal types (funding, regulatory, technology, hiring, search, competitor)
2. Verify recency: Are signals from last 12 months?
3. Count signals; assess diversity
4. Extract specificity: "12 companies funded" (high) vs. "companies are funded" (low)

**Improvement (if <9):**
- Score 0-3: "Find 3 specific growth signals: (1) Crunchbase for competing companies funded in last 18 months, (2) Google Trends for your keyword, (3) One regulatory/hiring/technology shift."
- Score 3-6: "You have some signals. Add dates and numbers. Instead of 'market growing,' say '15 companies funded in 2025, up from 4 in 2023.'"
- Score 6-9: "Add one more category (if funding + regulatory, add hiring or technology shift)."

---

### C3. Competitive Defensibility (10 pts)
**Type:** Multiple Choice
**Question:** How defensible is your competitive gap in this market?

**Options:**
- **(10 pts)** Unique mechanism: Proprietary tech, data moat, network effect, or regulatory barrier hard to replicate
- **(7 pts)** First-mover advantage: First in specific sub-niche with execution head start
- **(5 pts)** Better execution: Speed, price, UX, localization, or service better than competitors
- **(2 pts)** No clear gap: Competing on effort and hustle; no structural advantage

---

**ENGAGEMENT AFTER C SECTION:**

> "Auto-generating your market positioning paragraph..."
>
> "Here's your market story for investor conversations: [AI-generated 3-4 sentences]"
>
> "Your market assessment is now evidence-based, not assumption-based. That alone puts you ahead of 90% of founders."

---

**Section C Total:** C1 (0-15) + C2 (0-15) + C3 (0-10) = **0-40 pts**

---

## 7. SECTION D: AI SYNTHESIS (20 POINTS, 0 USER QUESTIONS)

**Goal:** AI synthesizes ALL data (SC1 + SC2 + B + C answers) and scores using Hormozi framework.

### Process

**Step 1: Compile Data**
- SC1: Niche, positioning, geography, product scope
- SC2: Pain, congregation, budget, buying behavior
- B answers: Pain evidence + purchasing evidence
- C answers: Market sizing + growth signals + defensibility

**Step 2: Score Using Hormozi Grand Slam Framework**

Calculate four dimensions:

**Pain Reality (0-5):**
- Extracted from: B1 + B2 evidence strength
- Scoring: 5 = expert evidence (3+ types, pitch-ready) | 3 = strong evidence (2+ types) | 1 = weak evidence

**Purchasing Power (0-5):**
- Extracted from: B2 + B3 evidence
- Scoring: 5 = primary interviews + competitor pricing + budget benchmarks | 3 = mixed evidence | 1 = assumption-based

**Market Accessibility (0-5):**
- Extracted from: C1 (market size) + SC2 (congregation points)
- Scoring: 5 = large SOM + dense congregation | 3 = moderate SOM + some congregation | 1 = small SOM or scattered audience

**Growth Momentum (0-5):**
- Extracted from: C2 (growth signals) + C3 (defensibility)
- Scoring: 5 = 4+ strong signals + defensible gap | 3 = 2-3 signals + moderate gap | 1 = weak signals or no gap

**Step 3: Calculate Overall MAS Score**

```
MAS (0-20) = [Pain Reality × 0.3 + Purchasing Power × 0.25 + Accessibility × 0.25 + Growth × 0.2] × 4
```

Then add Section B + C scores:

```
Total MAS (0-100) = B Score (0-40) + C Score (0-40) + D Score (0-20)
```

**Step 4: Determine Band**

Map to Score Bands table (Section 3).

**Step 5: Generate Output**

Create `MarketAttractiveness.md` file with complete assessment.

---

**FINAL ENGAGEMENT:**

> "**Your Market Attractiveness Score: [X]/100**
>
> **Band: [BAND NAME]**
>
> **What This Means:** [1-2 sentence interpretation tailored to their score]
>
> **Next Step:** [Band-specific guidance]"

---

**Section D Total:** AI-scored = **0-20 pts**

---

## 8. ENGAGEMENT PROTOCOL

### Acknowledgment Rules

**Strong answer (≥80% of max):**
> "That's specific. Most founders stay vague here — you gave me something I can work with."

**Weak answer (<40% of max):**
> "I need more from you here. The difference between a funded startup and a side project hides in this answer."

**Evidence-rich answer:**
> "This is the kind of evidence that makes investors lean forward. You're proving, not guessing."

### Pattern Breaks

**After Section A:**
> "I've loaded your SC1 and SC2 data. Now we validate it against market reality."

**After Section B:**
> **Insight Unlock** — "[AI-generated insight about evidence strength and GTM implications]"

**After Section C:**
> **Variable Reward** — "Here's your market positioning paragraph for the next investor conversation: [3-4 sentences]"

### Investment Signaling

**After B:** "Your evidence base is real. No hand-waving."

**After C:** "Your market assessment has more rigor than most pitch decks I review."

**After D:** "Market assessment complete. This document could anchor your funding deck's market section."

---

## 9. CROSS-SCORECARD CONSISTENCY CHECKS

**Claude automatically checks:**

1. **SC1 ↔ SC3 Alignment:**
   - ICP from SC1 matches pain evidence in B1?
   - Geography from SC1 matches market sizing in C1?
   - Positioning aligns with competitive defensibility (C3)?

2. **SC2 ↔ SC3 Alignment:**
   - Pain statements from SC2 referenced in B1?
   - Congregation points from SC2 in TAM/SAM/SOM (C1)?
   - Budget range from SC2 consistent with C1 market size?

3. **Internal MAS Consistency:**
   - Purchasing evidence (B2) realistic given market size (C1)?
   - Growth signals (C2) support pain urgency?
   - Defensibility (C3) realistic given competitive landscape?

**Flag Contradictions:** Surface for clarification; offer chance to update; don't penalize if explained.

---

## 10. MENA-SPECIFIC SCORING ADJUSTMENTS

### Market Size Validation (C1)

When validating TAM/SAM/SOM, apply MENA country adjustments:

| Country | Business Density | Market Maturity | Adjustment |
|---------|---|---|---|
| **Saudi** | High | Mature | Use Gartner MENA data as baseline |
| **UAE** | Very High | Mature | Use global; apply 1.2x premium |
| **Egypt** | Medium | Emerging | Apply 0.3x to global |
| **Jordan** | Medium | Emerging | Apply 0.25x to global |
| **Morocco** | Low-Medium | Emerging | Apply 0.2x to global |

**Scoring Trigger:** If student uses global market size without MENA adjustment:
> "Your TAM is global. For [country], apply adjustment factor of [X]. Adjusted SAM: ~$[adjusted]B."

### Growth Signal Validation (C2)

**Strong MENA Signals:**
- Vision 2030 / national digitization initiatives
- Regulatory mandates (ZATCA, CMA rules, data protection laws)
- MENA fintech/SaaS funding (Crunchbase MENA filters)
- LinkedIn hiring trends for target role in MENA
- Payment infrastructure growth (BNPL, mobile wallet adoption)

**Weak Signals:**
- "Global market is growing" (too broad)
- "Companies are digitizing" (vague)
- US/Europe competitor funding (doesn't validate MENA)

---

## 11. RECOMMENDATION ENGINE

**For every question < max score:**

```
QUESTION: [Text]
YOUR SCORE: [X/max]

WHY: [What's missing]
TO IMPROVE: [Specific action]
TIME TO FIX: [Estimate]
```

**Priority Recommendations:**
Rank by Impact Score = (Points to gain) × (Ease of fix, 1-5)

---

## 12. OUTPUT FILE: MarketAttractiveness.md

**Automatically generated with:**
- Score breakdown (B, C, D + total + band)
- Executive Summary (2-3 sentences on viability)
- Evidence Assessment (pain + purchasing power + sizing + growth)
- Cross-Scorecard Consistency Notes
- Key Strengths from This Session
- Key Gaps for Next Validation
- Prioritized Recommendations
- 30-Day Validation Action Plan (if score < 70)
- Next Steps (band-specific guidance)
- Frameworks & References

---

## 13. CLAUDE EXECUTION FLOW

1. **Preparation (3 min):** Load SC1 + SC2; display for confirmation
2. **Evidence Validation (10 min):** Administer B1-B3; provide examples; score real-time
3. **Market Sizing & Growth (10 min):** Administer C1-C3; provide examples; score real-time
4. **Synthesis (2 min):** AI scores D dimension using Hormozi framework
5. **Output (3 min):** Generate MarketAttractiveness.md; display score + band
6. **Next Steps (2 min):** Offer re-scoring, 30-day plan, or move to SC5

**Total Time:** ~30 minutes

---

## 14. KEY FRAMEWORKS REFERENCED

### Alex Hormozi's Grand Slam Formula

**Viability Index = (Dream Outcome × Perceived Likelihood) / (Time Delay × Effort Required)**

- **Dream Outcome:** How transformative is value? (from pain cost in B1)
- **Perceived Likelihood:** How credible is delivery? (from evidence strength in B1-B2)
- **Time Delay:** How fast can value be delivered? (from SC2 buying behavior)
- **Effort Required:** How easy is adoption? (from competitive gap in C3)

### TAM/SAM/SOM Framework

- **TAM (Total Addressable Market):** Global market size for problem category
- **SAM (Serviceable Addressable Market):** Market size you can realistically reach
- **SOM (Serviceable Obtainable Market):** Market you can capture in 3-5 years

### Evidence Hierarchy

1. Assertion ("I think...")
2. Logical reasoning ("It makes sense that...")
3. Generic data ("Market is growing")
4. Specific data with sources ("Google Trends shows...")
5. Customer validation ("5 customers said...")
6. Paid validation ("Pre-orders collected")

---

