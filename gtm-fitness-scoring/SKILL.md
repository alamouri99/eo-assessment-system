---
name: gtm-fitness-scoring-engine
description: Scorecard 5 of 5 — Evaluates readiness across 13 GTM motions using composite scoring (Fit x 0.4 + Readiness x 0.3 + MENA x 0.3). Assigns PRIMARY/SECONDARY/CONDITIONAL/SKIP tiers.
version: "2.0"
---

# SKILL: GTM Fitness Scoring Engine

**Version:** 2.0
**Created:** 2026-03-06
**Input Sources:** SC1-SC4 (all upstream scorecards)
**Output File:** `gtm-fitness.md`
**Execution Model:** Pre-scored upstream + Readiness-focused deep dive

---

## 1. STRATEGIC PURPOSE

GTM Fitness Scoring identifies which of the 13 go-to-market motions are realistic and highest-ROI given founder resources, market conditions, ICP, and strategy path. It answers: "Of all possible GTM motions, which 2-3 should I activate first?"

**Philosophy:** Not every motion works for every founder. Fitness depends on upstream context (MAS, ICP clarity, strategy path). Pre-populate Fit and MENA Viability; focus depth on Readiness (what founder can execute).

---

## 2. PREREQUISITES

**Completion Required:**
- SC1 (Project Definition): Niche, positioning, geography, ACV, product scope
- SC2 (ICP Clarity): ICP profile, congregation points, buying behavior, payment method
- SC3 (Market Attractiveness): Market conditions, growth, competitive landscape
- SC4 (Strategy Selector): Recommended strategy path (Replicate/Consulting/Micro/Hammering)

**Pre-Admin Checklist:**
- Load all upstream data
- Pre-populate Fit scores (from ICP + MAS data)
- Pre-populate MENA Viability (from geography + language strategy)
- Display these pre-scores to student for confirmation/update
- Flag if any upstream scorecard is <40 (RESET band)

---

## 3. SECTION ARCHITECTURE

| Section | Points | Focus | Duration |
|---------|--------|-------|----------|
| **A. Business Context Confirmation** | 10 | Validate upstream data; confirm ACV, buyer type, sales cycle | 5 min |
| **B. Capability Assessment** | 30 | Content library, outbound infra, audience, budget, network, proof | 10 min |
| **C. Motion-Specific Deep Dive (Top 5)** | 40 | 5 most relevant motions, 2 questions each, 4 pts each | 20 min |
| **D. MENA Execution Context** | 10 | Regional channel adaptations, competitive positioning | 5 min |
| **E. Motion Sequencing** | 10 | Activation order, dependencies, 90-day sequence | 5 min |
| **TOTAL** | **100** | | **45 min** |

---

## 4. SECTION A: BUSINESS CONTEXT CONFIRMATION (10 POINTS)

**Goal:** Validate upstream context; confirm key GTM parameters.

**System Behavior:** Pre-populate from SC1 and SC4; ask for confirmation or updates.

**Questions (MC, Deterministic):**

**A1. ACV Confirmation (5 pts)**
"Your projected Annual Contract Value (ACV) is $[X] per year. Is this accurate?"
- Yes, correct (5 pts)
- Within 20% (3 pts)
- Needs update to $[X] (5 pts if update provided and reasonable)
- Unknown (0 pts)

**A2. Sales Cycle Length (5 pts)**
"How long is your typical sales cycle?"
- <1 month (self-serve, quick) (5 pts) → Favors: Micro-SaaS, Waitlist, Build-in-Public
- 1-3 months (consultative) (4 pts) → Favors: Consulting-First, Authority Education, Dream 100
- 3-6 months (complex, relationship) (3 pts) → Favors: Consulting-First, 7x4x11, Value Trust Engine
- 6+ months (enterprise) (2 pts) → Favors: Dream 100, Strategic Partnerships, Consulting-First
- Unknown (0 pts)

**Section A Total:** A1+A2 = 0-10 pts (deterministic)

---

## 5. SECTION B: CAPABILITY ASSESSMENT (30 POINTS)

**Goal:** Assess founder's capability across 6 GTM dimensions.

**System Behavior:** 6 MC questions; 5 pts each; deterministic scoring.

**Questions:**

**B1. Content Library (5 pts)**
"Do you have a content library (blog posts, videos, case studies, frameworks)?"
- Yes, 50+ pieces (5 pts) → Enables: Authority Education, Build-in-Public, Wave Riding
- Yes, 10-49 pieces (4 pts)
- Some, <10 pieces (2 pts)
- No, need to build (1 pt)
- Not applicable to my model (5 pts) → Enables: Consulting-First, Dream 100 (relationship-based)

**B2. Outbound Infrastructure (5 pts)**
"Do you have lists and tools for outbound (email lists, LinkedIn access, cold email tool)?"
- Yes, fully set up (email, LinkedIn, tracking) (5 pts) → Enables: Signal Sniper, Dream 100, Cold email campaigns
- Partial (one tool; one list) (3 pts)
- No, starting from scratch (1 pt)
- N/A to my strategy (5 pts) → Inbound-focused strategies only

**B3. Audience Size (5 pts)**
"How large is your audience (email, social, network)?"
- 10K+ followers/connections (5 pts) → Enables: Waitlist Heat, Build-in-Public, Wave Riding
- 1K-10K (4 pts)
- 100-1K (2 pts)
- <100 (1 pt) → Must build audience; favor long-tail strategies
- Building/growing (3 pts)

**B4. Marketing Budget (5 pts)**
"What's your GTM marketing budget for the next 90 days?"
- $5K+ (5 pts) → Enables: Paid ads, Paid VSL, Wave Riding, Webinars (ads)
- $1K-5K (4 pts) → Limited paid; must focus on organic/free
- <$1K (2 pts) → Organic only; favor low-cost motions
- $0 (1 pt) → Bootstrap; favor built-in-public, referrals, content
- Unknown/TBD (1 pt)

**B5. Network Strength (5 pts)**
"Can you leverage your network (advisors, mentors, investors, friends) for introductions?"
- Yes, strong network (50+ warm relationships) (5 pts) → Enables: Dream 100, Referrals, Wave Riding
- Moderate (10-50 warm relationships) (4 pts)
- Weak (<10 warm relationships) (2 pts)
- No network; cold outreach only (1 pt)
- N/A; focusing on inbound (3 pts)

**B6. Proof Assets (5 pts)**
"Do you have proof assets (case studies, testimonials, early wins, metrics)?"
- Yes, documented (3+ case studies, testimonials) (5 pts) → Enables: Authority Education, Value Trust Engine, Outcome Demo
- Some (1-2 case studies or early wins) (3 pts)
- Minimal (1 win, some metrics) (2 pts)
- None yet (1 pt) → Must build proof; favor early-stage motions (Waitlist, Build-in-Public)
- Will have proof in 30 days (3 pts)

**Section B Total:** B1+B2+B3+B4+B5+B6 = 0-30 pts (deterministic)

---

## 6. SECTION C: MOTION-SPECIFIC DEEP DIVE (40 POINTS)

**Goal:** Score founder's readiness for each of the 13 GTM motions; identify top 5 for focus.

**System Behavior:**
1. Pre-score all 13 motions using formula: (Fit × 0.4) + (Readiness × 0.3) + (MENA × 0.3)
   - Fit: Pre-populated from ICP + MAS data (0-10)
   - MENA: Pre-populated from geography (0-10)
   - Readiness: To be assessed in this section (0-10 per motion)
2. Rank all 13 motions by score
3. Ask deep-dive questions on TOP 5 ONLY (to save time)
4. For each top 5 motion: 2 questions × 2 pts each = 4 pts per motion
5. Top 5 × 4 pts = 40 pts total

**13 GTM Motions (Reference & Pre-Scores):**

| # | Motion | Fit | MENA Viability | Readiness (To be scored) |
|---|--------|-----|---|---|
| 1 | Waitlist Heat-to-Webinar | Varies | 3/10 | ? |
| 2 | Build-in-Public Trust | Varies | 2/10 | ? |
| 3 | Authority Education Engine | High if expert | 5/10 | ? |
| 4 | Wave Riding Distribution | Varies | 2/10 | ? |
| 5 | LTD Cash-to-MRR | Low | 2/10 | ? |
| 6 | Signal Sniper Outbound | Varies | 4/10 | ? |
| 7 | Outcome Demo First | High if clear ROI | 5/10 | ? |
| 8 | Hammering-Feature-First | High if niche | 3/10 | ? |
| 9 | MicroSaaS BOFU SEO | High if long-tail | 5/10 | ? |
| 10 | Dream 100 Strategy | High if network | 5/10 | ? |
| 11 | 7x4x11 Strategy (Chet Holmes) | Varies | 4/10 | ? |
| 12 | Value Trust Engine | High if proof | 5/10 | ? |
| 13 | Paid VSL Value Ladder | Medium | 4/10 | ? |

**MENA Viability Legend:**
- 5/10: Highly viable in MENA (proven, culturally aligned, high adoption potential)
- 4/10: Good viability (emerging, reasonable friction)
- 3/10: Moderate viability (works but requires localization)
- 2/10: Low viability (Western-centric, low adoption in MENA)

**Example: Top 5 Motions Selection**

Assume student's ICP = Finance managers at mid-market Saudi companies; Strategy = Consulting-First SaaS; Budget = $2K

Pre-scoring example:
| Motion | Fit | MENA | Readiness | Score | Rank |
|--------|-----|------|-----------|-------|------|
| Authority Education | 8 | 5 | ? | ? | 1 |
| Dream 100 Strategy | 7 | 5 | ? | ? | 2 |
| Outcome Demo First | 7 | 5 | ? | ? | 3 |
| 7x4x11 Strategy | 6 | 4 | ? | ? | 4 |
| Signal Sniper Outbound | 6 | 4 | ? | ? | 5 |

→ Top 5 selected for deep dive

**Deep-Dive Questions for Each Top Motion (2 questions × 2 pts = 4 pts per motion):**

### Motion 1: Authority Education Engine (4 pts)

**C1.1. Content Readiness (2 pts)**
"What core framework or methodology would you teach to position as an expert?"
- Options:
  - Already defined, tested with customers (2 pts)
  - Rough framework, needs refinement (1 pt)
  - Undefined (0 pts)

**C1.2. Implementation Timeline (2 pts)**
"Can you create and launch a 5-module course (or equivalent) within 30 days?"
- Options:
  - Yes, have content ready (2 pts)
  - Yes, with 2-week build time (1.5 pts)
  - Need 4-6 weeks (1 pt)
  - Can't do this (0 pts)

---

### Motion 2: Dream 100 Strategy (4 pts)

**C2.1. Target List Quality (2 pts)**
"Can you identify and list 100 named companies/individuals who are ideal customers?"
- Options:
  - Yes, list already built (100+) (2 pts)
  - Yes, can build in 1 week (1.5 pts)
  - Rough idea, need to research (1 pt)
  - Can't do this (0 pts)

**C2.2. Outreach Capability (2 pts)**
"Can you personally send customized outreach to 10-15 people per week?"
- Options:
  - Yes, have time and infrastructure (2 pts)
  - Yes, with effort (1.5 pts)
  - Not sure (1 pt)
  - No (0 pts)

---

### Motion 3: Outcome Demo First (4 pts)

**C3.1. Outcome Clarity (2 pts)**
"Can you demonstrate a clear, quantified outcome (e.g., 'saves $1K/month' or 'improves [metric] by X%')?"
- Options:
  - Yes, tested and proven (2 pts)
  - Yes, based on customer feedback (1.5 pts)
  - Yes, theoretical calculation (1 pt)
  - Not clear (0 pts)

**C3.2. Demo Readiness (2 pts)**
"Can you deliver a compelling 15-minute outcome demo (live or video)?"
- Options:
  - Yes, already have recording (2 pts)
  - Yes, can film this week (1.5 pts)
  - Yes, with prep time (1 week) (1 pt)
  - Not ready (0 pts)

---

### Motion 4: 7x4x11 Strategy (Chet Holmes) (4 pts)

**C4.1. Target Market Definition (2 pts)**
"Have you defined your target market precisely enough for 7x4x11? (List of 7 touchpoints × 4 ways to reach × 11 time frequency)"
- Options:
  - Yes, detailed map (2 pts)
  - Partial, need refinement (1 pt)
  - No, too abstract (0 pts)

**C4.2. List + Infrastructure (2 pts)**
"Do you have: (1) A list of buyers, (2) Multiple ways to reach them (email, LinkedIn, phone, events, content, etc.)?"
- Options:
  - Yes, both (2 pts)
  - Partial (1 pt)
  - No (0 pts)

---

### Motion 5: Signal Sniper Outbound (4 pts)

**C5.1. Signal Definition (2 pts)**
"What 'signal' are you targeting? (E.g., 'Just hired a new Finance Director' or 'Posted about invoice automation')"
- Options:
  - Clear, actionable signal (2 pts)
  - Rough signal (1 pt)
  - Undefined (0 pts)

**C5.2. Signal Source (2 pts)**
"Where will you find these signals? (E.g., LinkedIn, job boards, news, manual research)"
- Options:
  - Automated or easy source (2 pts)
  - Manual research, doable (1 pt)
  - Unclear source (0 pts)

---

[Repeat similar deep-dive structures for all top 5 motions]

**Section C Total:** Top 5 Motions × 4 pts each = 0-40 pts

---

## 7. SECTION D: MENA EXECUTION CONTEXT (10 POINTS)

**Goal:** Address regional execution considerations.

**Questions (Free-text, 5 pts each):**

**D1. MENA Channel Adaptation (5 pts)**
"For your top 3 recommended motions, what specific MENA adaptations will you make? (Language, timing, tool choices, messaging)"

**Display Example:** "For Authority Education Engine: (1) Arabic-first content (50% Arabic, 50% English mix); (2) Evening timing (7-9pm Gulf time) for live webinars; (3) WhatsApp follow-up (SMS is lower adoption; WhatsApp is 95%+). For Dream 100: (1) Build list from Arabic LinkedIn profiles; (2) Initial outreach in Arabic; (3) Follow-up in English if no response."

**AI Scoring (0-5):**
| Score | Criteria |
|-------|----------|
| 0 | No MENA adaptation mentioned (generic Western approach) |
| 1 | Surface adaptation (mentioned Arabic or WhatsApp; vague) |
| 2 | Some specificity (2 adaptations with partial detail) |
| 3 | Specific adaptations (3+ adaptations with clear reasoning) |
| 4 | Sharp strategy (detailed for all top 3 motions) |
| 5 | Expert (detailed adaptations + cultural reasoning + competitive positioning) |

---

**D2. Competitive Advantage in MENA (5 pts)**
"What's your GTM advantage in MENA that competitors may not have?"

**Display Example:** "My advantage: (1) Arabic native (can create content and communicate in Arabic; competitors are English-only); (2) Deep Saudi network (can leverage relationships for Dream 100); (3) Cultural understanding (know that WhatsApp is primary, Friday timing is off, email is low priority)."

**AI Scoring (0-5):**
| Score | Criteria |
|-------|----------|
| 0 | No MENA advantage identified |
| 1 | Generic advantage (e.g., "I'll be first") |
| 2 | Some advantage (1-2 points; weak reasoning) |
| 3 | Specific advantages (2-3 points; clear reasoning) |
| 4 | Strong moat (defensible advantages; hard to replicate) |
| 5 | Expert positioning (sustainable competitive advantage in MENA context) |

**Section D Total:** D1+D2 = 0-10 pts

---

## 8. SECTION E: MOTION SEQUENCING (10 POINTS)

**Goal:** Determine activation order and dependencies.

**Questions (Free-text, 5 pts each):**

**E1. Activation Sequence (5 pts)**
"In what order will you activate your top 3 motions in the next 90 days? Why this order?"

**Display Example:** "Order: (1) Month 1: Authority Education Engine (build credibility and content; takes 2-3 weeks to launch). (2) Month 2: Dream 100 (use education content as hook in outreach; reference in emails). (3) Month 3: Outcome Demo First (use early pilot customers from Dream 100 as proof for demos). Dependencies: Education content → Dream 100 outreach → Outcome demo with proof."

**AI Scoring (0-5):**
| Score | Criteria |
|-------|----------|
| 0 | No sequence (random order) |
| 1 | Sequence mentioned; no logic |
| 2 | Sequence with weak logic |
| 3 | Logical sequence; some dependencies noted |
| 4 | Strong sequence with clear dependencies |
| 5 | Expert sequencing (identifies leverage points, compound effects) |

---

**E2. 90-Day Execution Plan (5 pts)**
"Summarize your 90-day GTM plan: Week 1-4, Week 5-8, Week 9-12. Key milestones and targets?"

**Display Example:**
"Weeks 1-4 (Authority Education): Launch Arabic course on [platform]; 50 students enrolled; build community. Weeks 5-8 (Dream 100): Send 300 personalized emails (10-15/day); aim for 30-50 responses (10-15% response rate); convert 3-5 to consulting clients. Weeks 9-12 (Outcome Demo): Document 2 case studies from consulting clients; create 2-minute demo videos; use in sales conversations. Target: 5-10 consulting clients at $3K/month = $15-30K MRR."

**AI Scoring (0-5):**
| Score | Criteria |
|-------|----------|
| 0 | No plan |
| 1 | Vague plan (no timeline, targets, or milestones) |
| 2 | Rough plan (timeline + some targets; lacking detail) |
| 3 | Specific plan (clear milestones, targets, activities for each phase) |
| 4 | Sharp plan (includes metrics, response rates, conversion targets) |
| 5 | Expert plan (realistic targets with built-in contingencies and pivot points) |

**Section E Total:** E1+E2 = 0-10 pts

---

## 9. OVERALL GTM FITNESS SCORE

**Formula:**
- Section A (Context): 0-10 pts
- Section B (Capability): 0-30 pts
- Section C (Motion Readiness): 0-40 pts
- Section D (MENA Context): 0-10 pts
- Section E (Sequencing): 0-10 pts
- **TOTAL: 0-100 pts**

**Motion Composite Score (for each motion):**
```
Motion Score = (Fit × 0.4) + (Readiness × 0.3) + (MENA Viability × 0.3)
```

**Motion Tiers (Classification):**
| Tier | Score | Action | Meaning |
|------|-------|--------|---------|
| **PRIMARY** | 4.0-5.0 | Activate immediately | High fit, high readiness, high MENA viability → Fastest ROI |
| **SECONDARY** | 3.0-3.9 | Start after PRIMARY | Good fit, moderate readiness → Do next quarter |
| **CONDITIONAL** | 2.0-2.9 | Activate only if [X] | Fit exists but gaps → Fix gaps first, then activate |
| **SKIP** | 1.0-1.9 | Deprioritize | Low fit or low readiness → Not worth effort |

---

## 10. OUTPUT FILE: gtm-fitness.md

**Automatically generated with all sections populated:**
- GTM Fitness Score (/100)
- All 13 Motions Ranked Table (Fit | Readiness | MENA | Score | Tier)
- Primary Motions Detail (top 2-3 with 30-day activation plans)
- Secondary Motions (next-wave candidates)
- Motions to Skip (with reasons)
- 90-Day Motion Sequence (visual roadmap)
- MENA Execution Adaptations
- Capability Gap Analysis (what to fix before activation)
- Re-Assessment Triggers

---

## 11. CLAUDE EXECUTION FLOW

1. **Load Upstream Data (2 min):** SC1-SC4 complete; pre-populate Fit and MENA
2. **Confirm Business Context (5 min):** Section A (ACV, sales cycle)
3. **Assess Capabilities (10 min):** Section B (6 MC questions)
4. **Pre-Score All 13 Motions (auto):** Rank by formula; identify top 5
5. **Deep-Dive Top 5 (20 min):** Section C (2 questions × 4 pts each)
6. **MENA Execution (5 min):** Section D (2 free-text questions)
7. **Motion Sequencing (5 min):** Section E (2 free-text questions)
8. **Generate Output (3 min):** gtm-fitness.md with rankings
9. **Present Results (5 min):** Show primary motions, 90-day plan, capability gaps

**Total Time:** 55-65 minutes

---

## 12. MOTION TIERS & TIER DEFINITIONS

**PRIMARY TIER (4.0-5.0):**
"Activate these first. They have high fit with your ICP, you have the capability to execute, and MENA context is favorable. These are your fastest paths to first customers."

**SECONDARY TIER (3.0-3.9):**
"Good candidates for waves 2-3 of your launch. They require some capability building or are slightly less natural fits, but are worth investing in once PRIMARY is validated."

**CONDITIONAL TIER (2.0-2.9):**
"These could work IF you build certain capabilities or conditions are met. Example: 'Paid VSL would work IF you had $5K budget, but you only have $2K. Either increase budget or skip.'"

**SKIP TIER (1.0-1.9):**
"Not recommended for your current situation. Either poor fit with ICP, low MENA viability, or you lack key capabilities. Revisit in 6 months."

---

## 13. CAPABILITY GAP ANALYSIS

**System Generates Automatically:**

For each PRIMARY motion scoring <4.0 in readiness, generate:
```
MOTION: [Name]
GAP: [What's missing]
IMPACT: [How this limits motion effectiveness]
FIX: [Specific action to close gap]
TIME: [Estimate to close gap]
PRIORITY: [High / Medium / Low]
```

Example:
```
MOTION: Authority Education Engine
GAP: Content library exists (blog) but no structured course framework
IMPACT: Can't launch course in month 1; limits credibility signaling
FIX: Spend 1 week creating 5-module outline; use existing blog posts as module content
TIME: 1 week
PRIORITY: High
```

---

## 14. 13 GTM MOTIONS (FULL REFERENCE)

[Full descriptions of each motion with Fit context, MENA viability, execution requirements]

1. **Waitlist Heat-to-Webinar** (3/10 MENA) - Scarcity-driven webinar conversion
2. **Build-in-Public Trust** (2/10 MENA) - Journey-driven audience building
3. **Authority Education Engine** (5/10 MENA) - Expert positioning via content/course
4. **Wave Riding Distribution** (2/10 MENA) - Leverage existing audience waves
5. **LTD Cash-to-MRR** (2/10 MENA) - Lifetime deal → subscription transition
6. **Signal Sniper Outbound** (4/10 MENA) - Targeted outreach to buyers showing intent signals
7. **Outcome Demo First** (5/10 MENA) - ROI-driven demo-first sales
8. **Hammering-Feature-First** (3/10 MENA) - Release-driven community engagement
9. **MicroSaaS BOFU SEO** (5/10 MENA) - Bottom-of-funnel search dominance
10. **Dream 100 Strategy** (5/10 MENA) - Relationship-driven outreach to ideal customers
11. **7x4x11 Strategy** (4/10 MENA) - Chet Holmes frequency-based touch strategy
12. **Value Trust Engine** (5/10 MENA) - Trust-building through proof and education
13. **Paid VSL Value Ladder** (4/10 MENA) - VSL-driven paid customer acquisition

---

## 15. NOTES FOR DEVELOPERS & ADMINISTRATORS

- **Pre-Populate Aggressively:** Fit and MENA Viability should come from upstream scores; don't make student re-enter
- **Top 5 Selection:** Automatic based on composite formula; reduces scope to manageable depth
- **Readiness is the Differentiator:** This scorecard's value is assessing founder capacity to execute specific motions
- **MENA Context Critical:** Every motion has MENA viability score; this is not afterthought
- **Re-Assessment Trigger:** System recommends re-scoring GTM Fitness after 30 days of execution (capabilities improve; readiness changes)

---

**END OF SKILL.MD**
