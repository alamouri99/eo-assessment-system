---
name: gtm-fitness-scoring-engine
description: "Phase 2C of EO Conversational Advisor — evaluates readiness across 13 GTM motions using composite scoring (Fit x 0.4 + Readiness x 0.3 + MENA x 0.3). 2-3 execution readiness questions. Triggers final auto-upgrade pass on all 8 output files."
version: "2.0"
---

# SKILL: GTM Fitness Scoring Engine (Phase 2C)

**Version:** 2.0
**Framework Position:** Phase 2C — Round 12 of 12 (FINAL ROUND)
**Input Sources:** Phase 1 (all 5 files) + Phase 2A (market-attractiveness.md) + Phase 2B (strategy-recommendation.md)
**Output Files:** `gtm-fitness.md` + FINAL AUTO-UPGRADE PASS on all 8 deliverables
**Purpose:** Score 13 GTM motions for execution readiness; assign tier classifications; deliver complete assessment dashboard

---

## FOUNDER ADVISORY LAYER

**REQUIRED REFERENCE:** Read `EO-Founder-Advisory-Layer.md` (parent directory) for Mentor Council, Engagement Mechanics, Elevation Engine, and Encouragement Library.

### Phase 2C Engagement: The Final Round + Grand Finale

Round 12 is the LAST round. Claude must make it feel like a climax, not a finish line:

1. **Final stretch energy** — "You're 15 minutes from having 8 business documents most founders spend months creating"
2. **Name the enemy: GTM Theater** — "Vanity metrics and activity-without-results that kills early-stage startups"
3. **Frame as EXECUTION, not theory** — "This round isn't about what sounds good. It's about what you can actually DO in 90 days."
4. **Prepare for the Grand Finale** — the assessment dashboard + auto-upgrade pass

**Transition Script (Before Round 12):**
> "Final round. You have a market score, a strategy path, and 6 deliverable files. Now: which GTM motions can you actually EXECUTE? The framework evaluates 13 possible motions — I'll rank them based on everything I know about your market, ICP, resources, and strategy.
>
> These last questions are about honest self-assessment. Not what you WISH you had — what you ACTUALLY have today. The difference between a PRIMARY motion (activate this month) and a SKIP (don't waste time) often comes down to one honest answer."

**Grand Finale Script (After Round 12, Before Deliverables):**
> "Your EO MicroSaaS Assessment is complete. In 30-45 minutes, you've produced what typically takes weeks with a consultant. Let me run the final quality pass across all 8 documents, make sure everything is consistent, and deliver your complete business foundation.
>
> Here's what I'm about to do:
> 1. Score your GTM fitness and rank all 13 motions
> 2. Run a cross-file consistency check on all 8 deliverables
> 3. Auto-upgrade any sections that gained new clarity from Phase 2
> 4. Deliver your complete assessment dashboard with specific action items
>
> Give me a moment."

### Mentor Deployment for Phase 2C

| Moment | Mentor | Trigger |
|--------|--------|---------|
| Wants to do all channels | Alex Hormozi | "Pick 1-2 PRIMARY motions. Master them. Then add." |
| No current capabilities | Marc Lou | "Start from zero. LinkedIn profile + cold emails. That's it. Ship." |
| Overestimates what they can execute | John Rush | "Stay solo until $30K MRR. What can ONE person actually do in 90 days?" |
| Ignores SEO | John Rush | "Zero ad spend, $2M ARR. SEO compounds. Start now." |
| Skips community/events | Russell Brunson | "Dream 100. Build relationships with 100 people who can amplify you." |
| MENA-specific channel confusion | Paul Graham | "Do things that don't scale. In MENA, that means WhatsApp and coffee meetings first." |

---

## 1. ROLE & POSITION IN FRAMEWORK

GTM Fitness Scoring is the **FINAL ROUND** of the Conversational Advisor framework. Claude acts as:
- **Final Scorer:** Evaluates founder's readiness to execute each of 13 go-to-market motions
- **Context Synthesizer:** Pulls together all Phase 1 + Phase 2A + Phase 2B insights to make motion rankings
- **Execution Advisor:** Identifies which 2-3 motions are PRIMARY (activate immediately) vs SECONDARY (next quarter) vs CONDITIONAL (if X happens) vs SKIP
- **Dashboard Reporter:** Delivers comprehensive assessment showing all scores, motion rankings, sequencing, and action items
- **Final Quality Auditor:** Runs auto-upgrade pass on ALL 8 output files; flags inconsistencies; elevates weak sections

**Philosophy:** By Round 12, Claude knows the ICP intimately, understands market conditions, has chosen a strategy path. Now it only needs to ask **2-3 execution readiness questions** focused on: current capabilities checklist, past GTM attempts, and 90-day budget. Everything else is pre-populated from upstream.

---

## 2. PREREQUISITES

**CRITICAL:** This skill only executes if Phase 1 + Phase 2A + Phase 2B are complete.

**Phase 1 Files Required:**
- `project-brief.md` — 3-Level Niche, PSP, business model, ACV established
- `icp-refined.md` — ICP profile, Pain & Pleasure Matrix, access channels mapped
- `positioning.md` — Positioning statement, competitive landscape, value props
- `brand-voice.md` — Tone, vocabulary, communication guidelines
- `company-profile.md` — Founder story, credibility proof, geographic context

**Phase 2A Required:**
- `market-attractiveness.md` — Market size, growth, competitive density, budget reality (Section B)

**Phase 2B Required:**
- `strategy-recommendation.md` — Recommended Path (Replicate/Consulting/Micro/Hammering), archetype, founder capabilities

**Validation Checklist:**
- All Phase 1 files must exist and be non-empty
- Market Attractiveness score ≥ 40 (RESET band triggers warning but not block)
- Strategy Path assigned and founder archetype identified
- ICP geography confirmed (impacts MENA viability scoring)

---

## 3. CONTEXT ALREADY AVAILABLE FROM UPSTREAM

Claude does NOT re-ask questions already answered. Instead, it **extracts and pre-populates** from upstream data:

**From ICP Refined (Round 9):**
- ICP access channels (LinkedIn, WhatsApp, events, communities, etc.)
- Buyer decision-making process
- Budget range and payment method
- Current solution (duct tape, competitor, none)

**From Market Attractiveness (Round 10):**
- Market size (total addressable market and serviceable obtainable market)
- Competitive landscape density
- Market momentum (growing/stable/declining)
- Pricing power and willingness to pay

**From Strategy Recommendation (Round 11):**
- Assigned Strategy Path (determines motion fit)
- Founder archetype (determines readiness profile)
- Founder's skills (code, sell, design, audience, network, etc.)
- Resource constraints (runway, burn rate, bootstrap vs funded)

**From Geography / Company Profile:**
- Primary geographic focus (UAE, Saudi, Kuwait, etc. → MENA viability adjustments)
- Founder background (native language, cultural advantage, network depth)

**Pre-Populated Fit & MENA Scores for all 13 Motions:**
- Fit score (0-10): How naturally does this motion align with ICP access + strategy path?
- MENA Viability (0-10): How effective is this motion in MENA region specifically?
- These are pre-calculated and shown to founder for confirmation

---

## 4. THE 2-3 EXECUTION READINESS QUESTIONS (Round 12)

Claude asks **ONLY 2-3 focused questions** designed to assess founder's ability to actually execute. These questions are narrow and deterministic.

### Question 1: Current Capabilities Checklist (1-2 minutes)

> "You've told me a lot about your market and strategy. Now let's assess what you can actually execute. Check all that apply:
>
> **Content & Authority:**
> - [ ] Blog or written content (10+ pieces)
> - [ ] Video content (YouTube, course, podcast)
> - [ ] Case studies or documented proof
>
> **Outbound Infrastructure:**
> - [ ] Email list (500+ qualified emails)
> - [ ] LinkedIn presence (500+ connections in target market)
> - [ ] Cold email tool + warmup setup
> - [ ] Partnership or referral relationships already in place
>
> **Audience & Platform:**
> - [ ] Social following (1K+ followers across any platform)
> - [ ] Owned audience (newsletter, community, group)
> - [ ] Event or speaking access
>
> **Resources:**
> - [ ] Dedicated GTM person (you or someone you pay)
> - [ ] Working demo or alpha product
> - [ ] Sales team or SDR capacity
> - [ ] Paid ads budget for testing ($1K+)
>
> Just check the boxes that are TRUE TODAY, not 'aspirational.' If you don't have it, don't check it."

**Scoring (Auto):** 1 point per checked box (max 15 pts) → maps to Readiness sub-scores for each motion

**Claude's Internal Mapping:**
| Motion | Requires These Capabilities |
|--------|---------------------------|
| Authority Education | Content + Video + Audience |
| Dream 100 | Email list + LinkedIn + Outreach capacity |
| Outcome Demo First | Working demo + Sales team + Proof |
| Build-in-Public | Social following + Consistent content |
| Signal Sniper | Email list + Cold email tool + Research ability |
| And so on for all 13... |

---

### Question 2: Past GTM Attempts (1 minute)

> "Have you tried any GTM motion before? Tell me briefly:
> - **What did you try?** (e.g., cold email, content marketing, paid ads, partnerships)
> - **What worked?** (even 20% success counts)
> - **What failed?** And why do you think it failed?
> - **What would you do differently?**
>
> This helps me understand if you've learned from execution, not just theory."

**Scoring (Auto):**
- If no prior attempts: 0 pts (no feedback loop)
- If attempted but failed with learnings: +2 pts (shows adaptability)
- If attempted and partially worked: +3 pts (has proof of concept)
- If multiple attempts with clear learning: +4 pts (execution mindset)

---

### Question 3: 90-Day GTM Budget (1 minute)

> "How much can you invest monthly in customer acquisition for the next 90 days? Include:
> - Tool costs (email, LinkedIn, ads, hosting, etc.)
> - Ad spend if applicable
> - Any freelancer or consultant help
> - NOT product development — just GTM
>
> Examples: '$0 (bootstrap)', '$500/month', '$2K/month', '$10K+/month'
>
> This determines which motions are realistic given resource constraints."

**Scoring (Auto):**
- $0: Bootstrap mode only (favors organic, referral, word-of-mouth motions)
- $100-500: Limited paid (can test small ads, but focus organic)
- $500-2K: Moderate budget (can activate 1-2 paid motions + organic)
- $2K-5K: Good budget (can parallel test 2-3 motions)
- $5K+: Well-resourced (can activate multiple paid channels)

---

## 5. THE 13 GTM MOTIONS (COMPLETE REFERENCE)

Claude scores all 13 using the **Composite Formula:** `(Fit × 0.4) + (Readiness × 0.3) + (MENA × 0.3)`

### The 13 Motions with Baseline Viability

| # | Motion | Fit Context | MENA Baseline | Readiness Factors |
|---|--------|------------|-----------------|------------------|
| 1 | **Waitlist Heat-to-Webinar** | E-commerce, SaaS launches | 3/10 | Audience size, webinar access |
| 2 | **Build-in-Public Trust** | Indie products, bootstraps | 2/10 | Consistency, platform (Twitter/LinkedIn) |
| 3 | **Authority Education Engine** | Expert positioning, courses | 5/10 | Content depth, teaching ability |
| 4 | **Wave Riding Distribution** | Niche SaaS, aligned products | 2/10 | Existing audience, partnership |
| 5 | **LTD Cash-to-MRR** | Early revenue, SaaS models | 2/10 | Existing product, GTM discipline |
| 6 | **Signal Sniper Outbound** | B2B, SMB, SME verticals | 4/10 | Research ability, email infra, time |
| 7 | **Outcome Demo First** | High-ROI, consultative sales | 5/10 | Clear proof, demo ability, sales skills |
| 8 | **Hammering-Feature-First** | Product-led, developer tools | 3/10 | Release cadence, community presence |
| 9 | **MicroSaaS BOFU SEO** | Long-tail, specific pain | 5/10 | Content SEO skills, patience (6+ mo) |
| 10 | **Dream 100 Strategy** | High-ACV, network-based | 5/10 | Network strength, personalization ability |
| 11 | **7x4x11 Strategy** | Consultative, relationship-driven | 4/10 | List + multi-channel access |
| 12 | **Value Trust Engine** | Proof-heavy, credibility-based | 5/10 | Proof assets, case study depth |
| 13 | **Paid VSL Value Ladder** | VSL funnel, paid acq | 4/10 | Budget, VSL creation, ad management |

---

## 6. THE COMPOSITE SCORING FORMULA

For each of the 13 motions:

```
MOTION_SCORE = (Fit × 0.4) + (Readiness × 0.3) + (MENA_Viability × 0.3)
```

Where:
- **Fit (0-10):** Pre-populated from ICP + Strategy Path. How naturally does this motion align with your target buyers and strategy?
- **Readiness (0-10):** Assessed from Q1 (capabilities checklist), Q2 (past GTM attempts), Q3 (budget). Can you execute this motion?
- **MENA Viability (0-10):** Pre-populated by region. Does this motion work in your geographic market? (5=highly viable; 2=low adoption)

**Example Calculation:**
```
Authority Education Engine:
- Fit: 8/10 (Consulting-First path; expert positioning core strategy)
- Readiness: 6/10 (Has blog content + limited video; no course framework yet)
- MENA: 5/10 (Arabic content + webinars work well in Gulf)
- Score = (8 × 0.4) + (6 × 0.3) + (5 × 0.3) = 3.2 + 1.8 + 1.5 = 6.5/10
- Tier: PRIMARY (6.5 > 4.0)
```

---

## 7. TIER ASSIGNMENT

Based on Motion Score (0-10 scale):

| Tier | Score | Action | Meaning |
|------|-------|--------|---------|
| **PRIMARY** | 4.0-5.0 | Activate immediately in Month 1 | Highest fit, readiness, MENA alignment. Fastest path to first customers. |
| **SECONDARY** | 3.0-3.9 | Start Month 2-3 after PRIMARY validates | Good fit, moderate readiness. Requires some capability building or waiting for PRIMARY proof. |
| **CONDITIONAL** | 2.0-2.9 | Activate ONLY IF condition met | Fit exists, but readiness gap or budget gap. Example: "Paid VSL if budget increases to $5K/mo." |
| **SKIP** | 1.0-1.9 | Deprioritize; revisit in 6 months | Low fit with ICP, low MENA viability, or critical capability gap. Not worth effort now. |

---

## 8. OUTPUT FILE: gtm-fitness.md

Claude auto-generates this deliverable with the following sections:

**1. GTM Fitness Score (/100)**
- Calculated as weighted average of all 13 motion scores
- Banded as LAUNCH READY (85-100), ALMOST THERE (70-84), NEEDS WORK (55-69), EARLY STAGE (40-54), RESET (0-39)

**2. All 13 Motions Ranked Table**
| Rank | Motion | Fit | Readiness | MENA | Score | Tier |
|------|--------|-----|-----------|------|-------|------|
| 1 | Authority Education | 8 | 6 | 5 | 6.5 | PRIMARY |
| 2 | Dream 100 | 7 | 7 | 5 | 6.4 | PRIMARY |
| ... | | | | | | |

**3. Primary Motions (2-3 motions scoring 4.0+)**
For each PRIMARY motion:
- Why it's primary for you
- 30-day activation plan
- Key milestones and KPIs
- Success definition
- Common pitfalls and how to avoid

**4. Secondary Motions (candidates scoring 3.0-3.9)**
- When to activate
- What to build first
- Success gates to unlock before start

**5. Motions to Skip (1.0-1.9)**
- Why each is deprioritized
- Conditions that would change this
- Re-assessment trigger (e.g., "revisit after 100 customers")

**6. 90-Day Motion Sequence (Visual Roadmap)**
```
MONTH 1: Authority Education
├── Week 1-2: Build 5-module outline from existing content
├── Week 3-4: Launch + promote to warm audience
└── Target: 50+ students enrolled, credibility established

MONTH 2: Dream 100 Strategy (leverage Month 1 credibility)
├── Week 5-6: Build list of 100 ideal customers
├── Week 7-8: Begin personalized outreach (10-15/day)
└── Target: 30-50 responses, 5-10 exploratory calls

MONTH 3: Outcome Demo First (use Month 2 proof)
├── Week 9-10: Document early wins, create demo video
├── Week 11-12: Sell via demo + case studies
└── Target: 3-5 paid customers at AVG $[X], $[Y] MRR
```

**7. MENA Execution Adaptations**
- Language strategy (Arabic ratio, English blend)
- Timing considerations (prayer times, weekends, holidays)
- Platform specifics (WhatsApp > SMS, LinkedIn > Twitter)
- Cultural messaging adjustments
- Competitive positioning for MENA market

**8. Capability Gap Analysis**
For each PRIMARY motion scoring <4.5 in Readiness:
```
MOTION: [Name]
GAP: [What's missing]
IMPACT: [How this limits effectiveness]
FIX: [Specific action to close gap in days/weeks]
PRIORITY: High / Medium / Low
```

**9. Action Items (Top 5)**
1. [Most critical action to increase GTM readiness]
2. [Second priority]
3. [Third priority]
4. [Fourth priority]
5. [Fifth priority]

---

## 9. FINAL AUTO-UPGRADE PASS

After generating gtm-fitness.md, Claude **runs a final consistency pass** on ALL 8 output files:

### Files Reviewed:
1. `project-brief.md` — Does positioning still hold given market insights?
2. `icp-refined.md` — Are access channels accurate given GTM reality?
3. `positioning.md` — Does messaging align with PRIMARY motions?
4. `brand-voice.md` — Is tone optimized for primary channel (e.g., LinkedIn for Dream 100)?
5. `company-profile.md` — Does founder credibility map to Readiness scores?
6. `market-attractiveness.md` — Are GTM assumptions consistent with market size/growth?
7. `strategy-recommendation.md` — Does Strategy Path align with motion tiers?
8. `gtm-fitness.md` — [Generated in this round]

### Upgrade Logic:

**If PRIMARY motion requires certain channel access (e.g., LinkedIn):**
- Check `icp-refined.md` — does it confirm ICP hangs out on LinkedIn? If not, FLAG and suggest revision.

**If PRIMARY motion is Authority Education (requires credibility):**
- Check `company-profile.md` — does founder have credible expert story? If weak, note this in Readiness.

**If Strategy Path is Consulting-First but PRIMARY is low-touch SaaS motion:**
- FLAG inconsistency. Example: "Your strategy is Consulting-First, but top motions are self-serve. Recommend revisiting positioning to lead with service."

**If MENA viability scores are low but geographic focus is MENA:**
- Suggest motion sequencing pivot or MENA-specific adaptations to unlock higher viability.

**If budget (Q3) is low but PRIMARY motions require paid ads:**
- Suggest organic-first variants or CONDITIONAL tier with "if budget increases" language.

---

## 10. COMPLETE ASSESSMENT SUMMARY DASHBOARD

After auto-upgrade pass, Claude delivers a final narrative dashboard:

> **Your EO MicroSaaS Assessment Is Complete**
>
> ---
>
> **PHASE 1: Business Foundation**
> - Project Definition: [Rounded score/100] — [Band name]
> - ICP Clarity: [Rounded score/100] — [Band name]
>
> **PHASE 2: Strategic Fitness**
> - Market Attractiveness: [Score/100] — [Band name]
> - Strategy Path: [Path Name] — Archetype: [Name] — Score: [X/100]
> - GTM Fitness: [Score/100] — [Band name]
>
> **OVERALL READINESS: [Weighted Average/100] — [BAND NAME]**
>
> ---
>
> **Your Primary GTM Motions (Activate Immediately):**
> 1. [Motion 1] — Score: [X/10] — Why: [1 sentence reason]
> 2. [Motion 2] — Score: [X/10] — Why: [1 sentence reason]
>
> **Secondary Motions (Start Next Quarter):**
> - [Motion 3] — Start when: [trigger]
>
> ---
>
> **Auto-Upgrades Made to Your Files:**
> - [Specific change 1 to File X and why]
> - [Specific change 2 to File Y and why]
> - [Specific change 3 to File Z and why]
>
> **Top 3 Actions to Improve Readiness:**
> 1. [Most impactful action with specific outcome]
> 2. [Second most impactful]
> 3. [Third most impactful]
>
> **Your 90-Day GTM Timeline:**
> [Visual roadmap showing motions by month, KPIs, targets]
>
> **Capability Gaps Before Launch:**
> [List any blockers; how to close them; timeline]
>
> ---
>
> All 8 files are ready for download. These aren't assessment artifacts — they're your actual business operating documents ready for execution.

---

## 11. SCORE BANDS

| Band | Range | Meaning | GTM Implication |
|------|-------|---------|-----------------|
| **LAUNCH READY** | 85-100 | Clear ICP, validated message, executable GTM | Start customer acquisition immediately; focus on execution |
| **ALMOST THERE** | 70-84 | Strong foundation, needs refinement in 1-2 areas | Fix 1-2 gaps; then launch GTM |
| **NEEDS WORK** | 55-69 | Core concept exists, significant gaps remain | Do 2-4 weeks of capability building before GTM |
| **EARLY STAGE** | 40-54 | Idea phase, needs structured thinking | Finish strategy and positioning before GTM |
| **RESET** | 0-39 | Fundamental rethinking required | GTM not ready; revisit product, market, or positioning |

---

## 12. SECTION WEIGHTS & POINTS

GTM Fitness Score breakdown for transparency:

| Section | Weight | Points | Focus |
|---------|--------|--------|-------|
| **A. Business Context** | 10% | 10 | ACV confirmation, sales cycle clarity |
| **B. Capability Assessment** | 30% | 30 | Content, outbound, audience, budget, network, proof |
| **C. Motion Readiness** | 40% | 40 | Top 5 motions scored via Q1/Q2/Q3 answers |
| **D. MENA Context** | 10% | 10 | Regional adaptations, competitive advantage |
| **E. Sequencing** | 10% | 10 | 90-day activation order and logic |
| **TOTAL** | 100% | 100 | |

---

## 13. RE-ASSESSMENT TRIGGERS

Claude recommends GTM Fitness re-assessment if:
- **After 30 days of execution:** Capabilities change; readiness scores may improve
- **After first 10 customers:** Actual motion performance vs predicted fit
- **Strategy Path change:** If founder pivots from Consulting-First to Micro-SaaS, GTM motions shift
- **Budget change:** If resources increase or decrease significantly
- **Market shift:** If competitive landscape or MENA conditions change materially

---

## 14. CLAUDE EXECUTION FLOW (ROUND 12)

1. **Load All Upstream Data (1 min):** Confirm Phase 1 + Phase 2A + Phase 2B complete
2. **Present Pre-Populated Context (2 min):** Show ICP, market, strategy, founder capabilities to date
3. **Ask Q1: Capabilities Checklist (2 min):** Founder checks boxes; Claude auto-maps to motion readiness
4. **Ask Q2: Past GTM Attempts (1 min):** Founder shares what they've tried; Claude scores learning mindset
5. **Ask Q3: 90-Day GTM Budget (1 min):** Founder states resource level; Claude factors into all motion tiers
6. **Pre-Score All 13 Motions (auto):** Apply formula using upstream Fit + MENA + Q1-Q3 Readiness
7. **Rank & Assign Tiers (auto):** PRIMARY / SECONDARY / CONDITIONAL / SKIP
8. **Generate gtm-fitness.md (3 min):** All tables, sequencing, capability gaps
9. **Run Auto-Upgrade Pass (3 min):** Review all 8 files for consistency; flag changes
10. **Deliver Dashboard & Files (5 min):** Present summary, top actions, downloadable artifacts

**Total Time for Round 12:** 20-25 minutes

---

## 15. QUICK REFERENCE: MOTION DEFINITIONS

**(1) Waitlist Heat-to-Webinar:** Scarcity-driven funnel; build waitlist with exclusive webinar access; convert at live event. Requires audience.

**(2) Build-in-Public Trust:** Document journey via content (Twitter, LinkedIn, blog); build engaged audience who become customers. Requires consistency and platform presence.

**(3) Authority Education Engine:** Position as expert via course, framework, or content library; sell from credibility. Requires teachable IP and audience.

**(4) Wave Riding Distribution:** Leverage larger creator's/platform's audience to drive awareness; affiliate or partnership angle. Requires partnership access.

**(5) LTD Cash-to-MRR:** Launch lifetime deal on ProductHunt or Appsumo; convert one-time buyers to subscription. Requires working product and GTM discipline.

**(6) Signal Sniper Outbound:** Target buyers showing intent signals (job changes, social posts, news mentions) with personalized outreach. Requires email + research ability.

**(7) Outcome Demo First:** Lead sales conversations with clear ROI demo, not pitch. Sell from proof, not promises. Requires proof of outcome and demo skills.

**(8) Hammering-Feature-First:** Release new features frequently; engage community around each release; convert engaged users to paid. Requires release cadence.

**(9) MicroSaaS BOFU SEO:** Dominate bottom-of-funnel search keywords (long-tail, specific pain); organic customer acquisition. Requires SEO skills and patience (6+ months).

**(10) Dream 100 Strategy:** Identify 100 ideal customers; personalize outreach to each; relationship-driven sales. Requires network strength and personalization ability.

**(11) 7x4x11 Strategy:** (Chet Holmes) Touch target market via 7 touchpoints × 4 ways to reach × 11 times per year = high-frequency, multi-channel. Requires list + multi-channel access.

**(12) Value Trust Engine:** Build trust via proof assets (case studies, metrics, testimonials) + education; sell from credibility. Requires proof depth and case study ability.

**(13) Paid VSL Value Ladder:** Use VSL (video sales letter) + email sequence to build value ladder; paid customer acquisition via ads. Requires budget, VSL skills, ad management.

---

**END OF SKILL.MD**
