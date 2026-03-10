---
name: strategy-selector-engine
description: "Phase 2B of EO Conversational Advisor — maps founders to one of 4 strategy paths and 8 archetypes. 2-3 founder DNA questions only. Scores /100 using upstream context."
version: "2.0"
---

# SKILL: Strategy Selector Engine — Phase 2B

**Phase:** Phase 2B: Strategy Matching (Round 11)
**Input Sources:** Phase 1 complete + MAS (Round 10)
**Output File:** `strategy-recommendation.md`
**Execution Model:** AI-driven strategic recommendation with minimal founder input

---

## FOUNDER ADVISORY LAYER

**REQUIRED REFERENCE:** Read `EO-Founder-Advisory-Layer.md` (parent directory) for Mentor Council, Engagement Mechanics, Elevation Engine, and Encouragement Library.

### Phase 2B Engagement: The Identity Round

Round 11 is deeply personal — it's about founder DNA, not market data. Claude must:

1. **Acknowledge the shift** — "We're switching from your market to YOU. This round is about founder-strategy fit."
2. **Create safety for honesty** — Founders lie about resources and risk tolerance. Make it safe to be real.
3. **Name the enemy: Wrong Strategy** — "The default path that would waste 6 months and $50K"
4. **Frame the 4 paths as CHOICES, not judgments** — no path is "better," they fit different founders

**Transition Script (Before Round 11):**
> "Your market scores are in. Now the critical question: which strategy path fits YOU? Not your market — you. Two founders in the same market with the same ICP should take different paths based on their resources, skills, and risk tolerance.
>
> The EO framework identifies **4 Strategy Paths**. I'm going to match you to the right one based on 2-3 honest questions about your founder DNA. The key word is HONEST — there's no wrong answer here, but there IS a wrong strategy for the wrong founder."

### Mentor Deployment for Phase 2B

| Moment | Mentor | Trigger |
|--------|--------|---------|
| Wants to do everything | Marc Lou | "Pick ONE path. Ship fast. I built 21 products — only 1 made money." |
| Underestimates runway math | Paul Graham | "Default Alive or Default Dead? Know your number." |
| Consulting-First resistance | Alex Hormozi | "Sell the service. Learn the pain. THEN productize. That's how $100M businesses start." |
| Afraid to go narrow | John Rush | "Boring + narrow = profitable. Exciting + broad = broke." |
| Wants VC before revenue | Paul Graham + John Rush | "Revenue first. Don't raise money to find product-market fit." |
| Has unfair advantage they don't see | Russell Brunson | "That's your Attractive Character. Lead with it." |

---

## 1. ROLE & PURPOSE

Claude acts as a **Strategic Advisor**, not an examiner. By Round 11, Claude already knows:
- Business model, product type, market position (from Phase 1)
- Market attractiveness and opportunity size (from MAS Round 10)
- ICP pain, urgency, buying behavior, accessibility (from Phase 1 Deep Dive)
- Founder's background, credibility, domain expertise (from Phase 1 intake)

**Strategy Selector's Job:** Answer ONE question: "Given everything I know about your market, ICP, positioning, and resources—which of these 4 strategy paths will get you to product-market fit fastest?"

---

## 2. PREREQUISITES

This skill requires:
- **Phase 1 Complete:** Project Definition + ICP Clarity
- **Phase 2A Complete:** Market Attractiveness Scoring (MAS)
- **All output files available:** project-brief, icp-refined, positioning, brand-voice, company-profile, market-attractiveness

**Pre-Execution Checklist:**
- [ ] All upstream files produced and reviewed
- [ ] If any upstream score <40 (RESET band), flag to founder: "Upstream gaps detected; strategy recommendation may suggest revisiting foundational work"

---

## 3. CONTEXT ALREADY AVAILABLE

Claude extracts and uses this data WITHOUT asking redundant questions:

| Data Point | Source | Usage |
|-----------|--------|-------|
| Market pain intensity, urgency, volume | MAS + ICP | Section B: Market-Strategy Fit |
| ICP buying complexity, timeline, budget | ICP Refined | Section C: ICP-Strategy Fit |
| Founder skills, credentials, network | Company Profile | Section A: Founder Alignment |
| Geographic focus, competitive landscape | Project Brief | Section E: MENA Fit |
| Product type, revenue model | Project Brief | Path fit signals |
| Customer accessibility, congregation points | ICP Refined | Section B/C: Channel viability |

Claude reviews these files at the start of Round 11 and references them explicitly:
> "From your Phase 1 work, I see your ICP is [X] with [Y] budget authority and [Z] buying complexity. Your market shows [condition]. Given all that, I have 2-3 questions about YOUR founder DNA to finalize the strategy path recommendation."

---

## 4. THE 2-3 FOUNDER DNA QUESTIONS (ROUND 11)

**Critical Design Rule:** Only ask what Phase 1 couldn't answer. These are about **founder resources, skills, and preferences**—not market or product.

### Question Set A: Resources & Risk Profile

**Prompt:**
> "First, let me understand your resource constraints and risk tolerance.
>
> **Question 1A:** How much runway do you have?
> - Bootstrapped, no savings: $0/month burn capacity
> - Savings/side income: Can sustain $2-5K/month burn for 6+ months
> - Funded or high income: Can sustain $10K+/month burn
> - Other (describe)
>
> **Question 1B:** How much monthly can you invest in the next 90 days? (Not salary—just tools, contractor help, ads, etc.)
> - $0 (time only)
> - $500-2K
> - $2K-10K
> - $10K+
>
> **Question 1C:** How much time weekly can you commit?
> - <10 hrs/week (side project)
> - 10-20 hrs/week (serious side)
> - 20-40 hrs/week (near full-time)
> - 40+ hrs/week (full-time)"

**What Claude extracts:**
- Available capital vs. burn rate → Path feasibility
- Time commitment → Path speed requirements
- Risk tolerance → Conservative vs. aggressive strategies
- Urgency of revenue → Consulting-First vs. product-first

---

### Question Set B: Skills & Unfair Advantages

**Prompt:**
> "Now, what can YOU do that most founders can't?
>
> **Question 2:** What's your strongest skill or biggest advantage?
> - Technical (can code/build) — I can ship product fast
> - Sales (can close deals) — I can get customers without marketing
> - Domain expertise — I understand this industry deeply
> - Network/relationships — I have access to my ICP already
> - Content/teaching — I can build an audience and authority
> - Operations/systematization — I can build repeatable processes
> - Other (describe)
>
> **Question 2B:** What do you hate doing or are you bad at?
> - [Brief answer]
>
> (This tells me what you'll need to delegate or outsource.)"

**What Claude extracts:**
- Primary skill → Path that leverages this skill
- Gaps/weaknesses → Risk areas; potential hiring needs
- Network strength → Channel viability signals
- Whether founder is technical, sales-driven, or operator-minded

---

### Question Set C: Speed vs. Depth Preference

**Prompt:**
> "Finally, philosophy question. If I gave you two choices, which feels right?
>
> **Question 3:** Choose one scenario:
>
> **(A) Launch Fast:** Get something good to market in 4 weeks. It won't be perfect—maybe 60% of your vision—but real customers use it now. You iterate based on feedback.
>
> **(B) Launch Great:** Build something excellent over 6 months. You nail the experience, fix edge cases, do it right. When you launch, it's polished.
>
> Pick A or B. Why?"

**What Claude extracts:**
- Founder's risk appetite → MVPs vs. fully-featured products
- Patience level → Time-sensitive vs. long-term strategies
- Perfectionism vs. pragmatism → Design approach
- Whether founder is investor-ready or bootstrap-bootstrap-minded

---

## 5. SCORING ARCHITECTURE (100 POINTS)

All 5 sections are scored using **upstream context + Round 11 answers**. Claude scores autonomously where possible; flags low-confidence areas.

| Section | Points | Scoring Source |
|---------|--------|-----------------|
| **A. Founder-Strategy Alignment** | 20 | Round 11 Q1-3 + Section A1-A4 |
| **B. Market-Strategy Fit** | 25 | MAS + Round 11 context |
| **C. ICP-Strategy Fit** | 25 | ICP Refined + Round 11 context |
| **D. Execution Readiness** | 20 | Path-specific evaluation |
| **E. MENA Fit** | 10 | Geographic + cultural signals |
| **TOTAL** | **100** | |

---

## 6. SECTION A: FOUNDER-STRATEGY ALIGNMENT (20 POINTS)

**Evaluation:** How well does founder's resources, skills, and preferences match the strategy path?

### A1. Available Resources (5 pts)

**Scoring:**
- $0 + side income (can go lean): 5 pts → Favors Consulting-First, Micro-SaaS
- $500-2K budget: 5 pts → Favors Micro-SaaS (lean build)
- $2K-10K budget: 5 pts → Favors Hammering Deep (dedicated focus)
- $10K-50K budget: 4 pts → All paths viable
- $50K+ budget: 5 pts → Replicate & Localize (localization costs covered)

**Claude's Logic:** Budget doesn't predict success (paradoxically, $0 forces creativity; $50K enables any path). Scoring reflects "fit with strategy path," not "better or worse."

---

### A2. Founder's Primary Skill (5 pts)

**Scoring:**
- **Technical (can code/ship)**: 5 pts → Favors Boring Micro-SaaS, Hammering Deep (product-first)
- **Sales (can close)**: 5 pts → Favors Consulting-First SaaS, Replicate & Localize (sales-driven entry)
- **Domain Expertise**: 5 pts → Favors Hammering Deep (deep positioning), Consulting-First (authority)
- **Network/Relationships**: 5 pts → Favors Consulting-First SaaS (trust-based entry), Replicate & Localize
- **Content/Teaching**: 4 pts → Favors Hammering Deep, Consulting-First (authority-driven)
- **Operations**: 5 pts → Favors Replicate & Localize (systematization), Boring Micro-SaaS

**Claude's Logic:** Award points based on which skill best aligns with chosen path. If founder has multiple strong skills, score highest.

---

### A3. Time Commitment (5 pts)

**Scoring:**
- **<10 hrs/week**: 5 pts → Favors Micro-SaaS (lean) or Consulting-First (project-based, time-boxed)
- **10-20 hrs/week**: 5 pts → Favors Boring Micro-SaaS, Hammering Deep (part-time founder model)
- **20-40 hrs/week**: 4 pts → Favors Hammering Deep, Consulting-First (more time for relationships)
- **40+ hrs/week**: 5 pts → All paths viable

---

### A4. Risk Tolerance & Revenue Urgency (5 pts)

**Scoring:**
- **Conservative (revenue in 30 days)**: 5 pts → Favors Consulting-First SaaS, Micro-SaaS (fastest revenue)
- **Moderate (90 days to revenue)**: 5 pts → Favors Boring Micro-SaaS, Hammering Deep
- **Aggressive (6+ months)**: 4 pts → Favors Replicate & Localize (longer validation)
- **Already have income**: 5 pts → Favors Hammering Deep, Replicate & Localize (can play longer game)

**Section A Total:** Sum of A1-A4 = 0-20 pts

---

## 7. SECTION B: MARKET-STRATEGY FIT (25 POINTS)

**Evaluation:** Does the chosen strategy align with market conditions from MAS?

### B1-B4: Market Indicators (16 pts, auto-scored from MAS context)

Claude evaluates **without asking** by extracting MAS data:

**B1. Pain Intensity vs. Market Stage (4 pts)**
- Very early market (pain not yet recognized): Favors authority-driven paths (Hammering Deep, Consulting)
- Emerging market (pain recognized, limited solutions): Favors Hammering Deep, Consulting-First
- Mature market (multiple solutions, buyer confusion): Favors Replicate & Localize, Micro-SaaS
- Saturated (price war): Favors Micro-SaaS (lean) or Hammering Deep (niche)

**B2. Budget Power & Purchasing Complexity (4 pts)**
- Simple decision (manager approval, <2 weeks): Favors Micro-SaaS
- Complex decision (committee, 1-2 months): Favors Consulting-First, Replicate & Localize
- Budget constrained: Favors Micro-SaaS (low price)
- High budget authority: Favors Replicate & Localize (premium)

**B3. ICP Accessibility (4 pts)**
- Highly concentrated (own congregation points): Favors Micro-SaaS, Hammering Deep (fast customer acquisition)
- Scattered; requires marketing: Favors Consulting-First (relationship-based), Hammering Deep (content/community)
- Hard to reach: Favors Consulting-First (referral), Replicate & Localize (partnership)

**B4. Market Growth & Momentum (4 pts)**
- Rapidly growing: Favors Micro-SaaS (ride the wave), Hammering Deep (own the niche early)
- Stable/slow growth: Favors Consulting-First (sustainable revenue), Replicate & Localize (proven demand)
- Declining/unclear: Favors Micro-SaaS (rapid pivot), Consulting-First (stable revenue)

---

### B5. Strategy Path Selection (9 pts)

**Claude's Prompt (referencing upstream data):**
> "Based on your market conditions [cite specific MAS findings], which of these 4 paths feels most natural to you? Explain your reasoning in 50-100 words.
>
> The paths:
> 1. **Replicate & Localize** — Take proven global product; adapt for your market/ICP
> 2. **Consulting-First SaaS** — Sell consulting/services first; transition to SaaS product
> 3. **Boring Micro-SaaS** — Build minimal product; charge from day 1
> 4. **Hammering Deep** — Go vertical in one specific niche; own it completely"

**Scoring Rubric (0-9 pts):**
- **0-2:** No path chosen or completely misaligned with market data
- **3-4:** Path named but reasoning weak or contradicts upstream data
- **5-6:** Path chosen with reasonable reasoning; some alignment; minor gaps
- **7-8:** Strong reasoning; clear alignment with MAS, ICP, and founder profile
- **9:** Expert reasoning; could defend in investor pitch

**Section B Total:** B1+B2+B3+B4+B5 = 0-25 pts

---

## 8. SECTION C: ICP-STRATEGY FIT (25 POINTS)

**Evaluation:** Does the chosen strategy match how the ICP wants to buy?

### C1-C4: ICP Behavior Indicators (16 pts, auto-scored from ICP Refined)

Claude evaluates **without asking** by extracting ICP data:

**C1. Buying Complexity & Decision Timeline (4 pts)**
- Individual buyer; fast cycle (1-2 weeks): Favors Micro-SaaS
- Small team (2-3 people); moderate cycle (2-4 weeks): Favors Consulting-First
- Committee/complex (4+ approvers; 1-3 months): Favors Replicate & Localize, Consulting-First
- Highly political: Favors Consulting-First (relationship-heavy)

**C2. Pain Urgency (4 pts)**
- Extreme urgency (solve this week): Favors Micro-SaaS (instant solution)
- High urgency (solve within 1 month): Favors Boring Micro-SaaS, Consulting-First
- Moderate urgency (3 months): Favors Replicate & Localize, Consulting-First
- Low urgency: Favors Hammering Deep (long-term positioning)

**C3. Budget Level & Willingness to Pay (4 pts)**
- Low budget; price sensitive: Favors Micro-SaaS
- Mid-range; ROI-focused: All paths viable
- High budget; relationship-driven: Favors Replicate & Localize, Consulting-First
- Mixed: Favors Boring Micro-SaaS (multiple tiers), Hammering Deep (own the niche)

**C4. Channel Accessibility & Reach (4 pts)**
- Highly accessible via specific channels: Favors Micro-SaaS (fast scaling)
- Medium reach; multi-channel: Favors Consulting-First, Hammering Deep
- Low reach; hard to find: Favors Consulting-First (referral), Replicate & Localize (partnership)
- Fragmented: Favors Consulting-First, Hammering Deep (network-based)

---

### C5. ICP-Strategy Validation (9 pts)

**Claude's Prompt (referencing ICP data):**
> "Looking at your ICP's buying behavior [cite specifics: 'complex decision,' 'high urgency,' '$X budget'], does your chosen strategy from Section B still make sense? Explain in 50-100 words."

**Scoring Rubric (0-9 pts):**
- **0-2:** Strategy contradicts ICP behavior (e.g., chose Micro-SaaS for complex decision)
- **3-4:** Strategy is reasonable but has tension with ICP profile
- **5-6:** Strategy aligns with most ICP factors; minor concerns
- **7-8:** Strong alignment; demonstrates understanding of strategy-ICP fit
- **9:** Expert synthesis; explicitly addresses complexity, urgency, budget, accessibility

**Section C Total:** C1+C2+C3+C4+C5 = 0-25 pts

---

## 9. SECTION D: EXECUTION READINESS (20 POINTS)

**Evaluation:** Can the founder execute the chosen path in the next 90 days?

**System Logic:** Based on B5 (primary path), ask 4 path-specific readiness questions (5 pts each).

### Path-Specific Questions (D1-D4)

**IF PATH = REPLICATE & LOCALIZE:**
- D1. Target product identified and validated? (5 pts: Yes with partnership/5, Yes preliminary/3, No/0)
- D2. Localization advantage clear? (5 pts: Cultural + network/5, Language or expertise/4, Unclear/0)
- D3. Launch timeline? (5 pts: <3 months/5, 3-6 months/4, >6 months/0)
- D4. Customer acquisition channel identified? (5 pts: Partnership/5, Direct team/4, Community/5, Unsure/0)

**IF PATH = CONSULTING-FIRST SAAS:**
- D1. Service offering defined and priced? (5 pts: Yes, pilots lined up/5, Defined roughly/3, Vague/0)
- D2. Can deliver personally? (5 pts: 20+ clients/month/5, 5-10/month/4, Need team/2, Can't/0)
- D3. First consulting client secured? (5 pts: Signed LOI/5, Verbal/4, Warm lead/3, Cold/0)
- D4. Productization timeline? (5 pts: Months 4-6/5, Year 2/4, Unknown/0)

**IF PATH = BORING MICRO-SAAS:**
- D1. MVP scope defined? (5 pts: 1-3 features, 2-week build/5, Clear, 4-6 weeks/4, Vague/0)
- D2. Can build personally? (5 pts: Myself <4 weeks/5, With partner/5, Need hire/3, Can't/0)
- D3. Revenue timeline? (5 pts: <4 weeks/5, <8 weeks/4, <12 weeks/3, Unknown/0)
- D4. First 10 customers plan? (5 pts: Defined channel + pipeline/5, Rough/3, Untested/1, No/0)

**IF PATH = HAMMERING DEEP:**
- D1. Niche specificity? (5 pts: Role + size + geo/5, Role + geo/3, Broad/0)
- D2. Unique advantage in niche? (5 pts: Expertise + network/5, 1-2 advantages/4, Unclear/0)
- D3. Niche focus commitment? (5 pts: 12+ months/5, 6-12 months/4, <6 months/0)
- D4. Niche proof? (5 pts: Customers/advocates/5, 5+ conversations/4, Research/3, Assumption/0)

**Section D Total:** D1+D2+D3+D4 = 0-20 pts

---

## 10. SECTION E: MENA STRATEGY FIT (10 POINTS)

**Evaluation:** Does the strategy align with MENA geographic, cultural, and operational realities?

### E1. Cultural & Market Alignment (5 pts)

Claude evaluates based on geography + path:
- **Replicate & Localize in UAE**: Tech adoption high; SaaS proven → 5 pts
- **Consulting-First in Egypt**: Relationship-based culture → 5 pts
- **Micro-SaaS in Saudi**: Growing adoption, moderate price sensitivity → 4 pts
- **Hammering Deep in Jordan**: Opportunity before competition arrives → 4 pts
- [Other combinations scored contextually]

### E2. Execution Feasibility in MENA (5 pts)

Claude identifies biggest execution challenge:
- Payment infrastructure (BNPL, bank setup): -2 pts
- Hiring/team building difficulty: -1 pt
- Regulatory/compliance: -1 pt
- Language/localization: -2 pts
- No major barriers: 5 pts

**Section E Total:** E1+E2 = 0-10 pts

---

## 11. STRATEGY PATHS (PRESERVED IN DETAIL)

### Path 1: REPLICATE & LOCALIZE

**Definition:** Global product proven + successful; you adapt for [geography] or [micro-niche].

**Best For:** Founders with localization advantage (cultural, network, language), proven global demand, limited local competition.

**90-Day Roadmap:**
- **Month 1:** Research global products; validate market fit for your niche; secure partnership/rights
- **Month 2:** Customize product (pricing, features, language); build landing page; 20 sales conversations
- **Month 3:** Launch to market; acquire 10-20 first customers; validate product-market fit

**Risk Profile:** Medium (product proven; market proven; localization is execution risk)

**Execution Readiness Checklist:**
- Target product identified and validated (partnership or reseller agreement possible?)
- Localization advantage clear (cultural expertise? network in ICP? language? regulatory knowledge?)
- Launch timeline realistic (<6 months preferred)
- Go-to-market channel via partnerships, existing relationships, or team sales

---

### Path 2: CONSULTING-FIRST SAAS

**Definition:** Sell consulting/services first; productize SaaS in parallel or post-revenue.

**Best For:** Complex ICP, high trust needed, founder has expertise/network/credibility, fast revenue required, willing to deliver services personally.

**90-Day Roadmap:**
- **Month 1:** Define service offering; price it; warm outreach to 50+ prospects; refine pitch
- **Month 2:** Close 2-3 consulting clients; begin service delivery; gather data
- **Month 3:** Deliver results and case studies; document repeatable process; plan SaaS roadmap

**Risk Profile:** Low (fastest path to revenue; repeatable service proves demand before SaaS build)

**Execution Readiness Checklist:**
- Service offering clearly defined (what problem? solution? price?)
- Can founder deliver personally? (5-20 clients/month realistic?)
- First client commitment or strong warm pipeline
- Productization pathway clear (what becomes SaaS?)

---

### Path 3: BORING MICRO-SAAS

**Definition:** Build minimal product; charge customers from day 1; optimize for unit economics (CAC, churn, LTV).

**Best For:** Clear problem, simple solution, self-serve buyers, founder is technical or can partner with engineer, willing to iterate quickly.

**90-Day Roadmap:**
- **Month 1:** Define MVP (3-5 core features); begin building
- **Month 2:** Launch MVP; acquire 5-10 first paying customers; iterate based on feedback
- **Month 3:** Optimize unit economics; test scaling on 1-2 channels; plan next feature set

**Risk Profile:** Medium-High (product-market fit unknown; fast pivot required if validation fails)

**Execution Readiness Checklist:**
- MVP scope crystal clear (what features? what's NOT in?)
- Build timeline realistic (<8 weeks preferred)
- Revenue timeline realistic (charge within 4-12 weeks)
- Customer acquisition plan defined and testable

---

### Path 4: HAMMERING DEEP

**Definition:** Go vertical in one specific micro-niche; own it completely via expertise, network, authority before expanding.

**Best For:** Defensible niche, founder has deep domain expertise, willing to move slowly and build reputation, long-term patience.

**90-Day Roadmap:**
- **Month 1:** Define niche with razor-sharp specificity; build reputation (content, community, networks)
- **Month 2:** Acquire 3-5 first niche customers; deepen relationships; document expertise
- **Month 3:** Cement niche position as de-facto expert; plan expansion triggers

**Risk Profile:** Medium (slower revenue; higher retention; defensible competitive moat; longer build-to-scale)

**Execution Readiness Checklist:**
- Niche defined with specificity (role + company size + geography + industry, not just "role")
- Deep advantage in niche clear (what makes founder the expert?)
- Commitment to niche focus for 12+ months
- Proof of niche viability (conversations, advisors, advocates)

---

## 12. FOUNDER ARCHETYPES (8 TYPES)

Claude classifies founder into one of 8 archetypes based on strategy choice + profile:

1. **Launcher** — Ambitious + resources → Replicate & Localize (fast-to-market, scaling focus)
2. **Market Hunter** — Sales-driven + relationships → Consulting-First SaaS (close deals first)
3. **Channel Seeker** — Distribution advantage → Boring Micro-SaaS (product + channel fit)
4. **Solution Seeker** — Product-focused → Hammering Deep (build the right thing for the right people)
5. **Expert Without a Stage** — Domain expertise + no platform yet → Hammering Deep or Consulting (build authority first)
6. **Ghost** — Stealth, unknown, figuring it out → Micro-SaaS (learn fast with minimal risk)
7. **Operator** — Process-oriented, systematizer → Replicate & Localize (execution excellence)
8. **Scrambler** — Early-stage, bootstrapped, need revenue fast → Consulting-First SaaS (fastest path to cash)

---

## 13. OVERALL SCORE & INTERPRETATION

**Formula:**
- Section A (Founder Alignment): 0-20 pts
- Section B (Market Fit): 0-25 pts
- Section C (ICP Fit): 0-25 pts
- Section D (Execution Readiness): 0-20 pts
- Section E (MENA Fit): 0-10 pts
- **TOTAL: 0-100 pts**

**Score Bands:**
| Band | Range | Meaning |
|------|-------|---------|
| LAUNCH READY | 85-100 | Path clearly aligned; strong execution readiness; move to GTM immediately |
| CONFIDENT | 70-84 | Good path alignment; minor execution gaps; address before launch |
| CAUTIOUS | 55-69 | Path chosen but some misalignment; validate before committing |
| UNCERTAIN | 40-54 | Path unclear; test assumptions; may need upstream refinement |
| NOT READY | 0-39 | Major gaps; return to Phase 1 before strategy execution |

---

## 14. OUTPUT FILE: strategy-recommendation.md

Claude produces complete file including:
- Strategy Selector Score (/100) + band
- Recommended Primary Path (with explicit reasoning)
- Secondary Path (with switch triggers)
- Archetype Classification
- Path-Strategy Fit Analysis (A-E breakdown)
- Execution Risks & Mitigation
- 90-Day Roadmap (Month 1, 2, 3 specifics)
- Next Step: Proceed to Phase 2C (GTM Fitness)

---

## 15. HANDOFF TO PHASE 2C

After scoring, Claude tells founder:
> "Your strategy recommendation is complete. You score [X/100] on the [PATH NAME] path—that's a [BAND] score.
>
> **Primary Path:** [PATH NAME] because [2-3 sentence reasoning from A-E]
>
> **Secondary Path:** [PATH] (if [condition], switch to this)
>
> **Your Archetype:** [ARCHETYPE NAME] — [1 sentence description]
>
> **Your 90-Day Focus:** [Month 1, Month 2, Month 3 specifics]
>
> Next: Let's score your GTM Fitness. I'll evaluate which of the 13 go-to-market motions you can actually execute given your path, resources, and ICP."

---

**END OF SKILL.MD**
