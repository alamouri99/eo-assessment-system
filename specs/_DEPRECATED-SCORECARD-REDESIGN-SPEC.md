# EO Scorecard Redesign Spec
**Date:** 2026-03-08
**Purpose:** Before/after spec for all 5 scorecards. NO files will be touched until you approve this.

---

## DESIGN PHILOSOPHY (What We're Actually Doing)

This is NOT about "cutting questions." This is about three things:

1. **ENGAGEMENT** — SC1 and SC2 should feel like talking to a battle-tested advisor, not filling out a government form. Acknowledge good answers, encourage dreams, throw stones at the enemy, use interesting quotes, deliver variable rewards along the way.

2. **ELEVATION** — The founder gives scrappy, rough input. The AI takes that raw material and produces polished strategy documents (project-brief.md, icp-refined.md). The output docs ARE the value. Scoring is secondary.

3. **CASCADE** — SC3 should NOT re-ask what SC1+SC2 already covered. SC4 already does this right (AI auto-generates from upstream). SC5 already does this right (pre-populates Fit/MENA). SC3 needs the same treatment.

---

## SC1: PROJECT DEFINITION (project-files-scoring/SKILL.md)

### CURRENT STATE (v1.0)
- 21 questions total (16 free-text, 5 MC)
- No time estimate in file
- No engagement layer
- No elevation instructions — AI scores but doesn't transform input
- Philosophy section exists but execution flow is clinical/bureaucratic
- Produces: project-brief.md, niche-validation.md, positioning.md, product-spec.md

### WHAT CHANGES
**Questions:** Keep all 21. The questions themselves are good — they force clarity. The problem is HOW they're delivered, not WHAT is asked.

**Add: Engagement Layer to Execution Flow**
- After every 3 questions (~10 min), insert a **Pattern Break** using Brendan Kane's Hook Point formulas:
  - After A3 (Niche complete): Deliver **"Insight Unlock"** — "Your niche hierarchy [Market → Sub → Niche] is sharper than 80% of the founders I've worked with. Here's why that matters..."
  - After B5 (Problem-Solution complete): Deliver **"Enemy Reveal"** — "The enemy behind [their problem] is [named enemy]. Most founders fight symptoms. You're naming the cause."
  - After D4 (Product Scope complete): Deliver **"Offer Preview"** — show a draft positioning statement built from their answers so far
  - After F3 (Final): Deliver full **Variable Reward** — all 4 polished output documents

- **Acknowledgment Protocol** (added to execution flow):
  - When answer is strong: "That's specific. Most founders stay vague here — you gave me something I can actually work with."
  - When answer is weak: "I need more from you here. [Specific follow-up]. The difference between a $10K idea and a $100K idea often hides in this answer."
  - Encourage dreams: "If this niche plays out the way you're describing, you're looking at..."
  - Throw stones at enemy: "The competitors in this space are still doing [old way]. Your angle attacks that directly."

- **Investment Signaling:**
  - After Section B (30 min): "You've invested 30 minutes. Your problem-solution statement is uniquely yours — no generic strategy template could produce this."
  - After Section D (50 min): "50 minutes in. Your product scope document is more specific than what most agencies deliver for $5K."
  - After Section F (final): "Your project definition package is complete. These 4 documents could anchor a $50K go-to-market strategy."

**Add: Elevation Instructions**
- In the Claude Execution Flow section, add explicit instructions that AI must:
  1. Take the raw answers and UPGRADE the language in output docs
  2. Add strategic context the founder didn't mention but is implied
  3. Flag contradictions between answers (e.g., "you said budget market but premium positioning")
  4. Produce output docs that feel like they were written by a strategist, not transcribed from a survey

**No changes to:** Question text, scoring rubrics, section architecture, output file structure, MENA scoring

### ESTIMATED EDIT SIZE
~150 lines added to Execution Flow section + ~50 lines added as new "Engagement Protocol" section = ~200 lines of new content. No deletions.

---

## SC2: ICP CLARITY (icp-clarity-scoring/SKILL.md)

### CURRENT STATE (v1.0)
- 14 interaction points (Interview Gate + A1-A5 + B1(10 pains) + C1(10 pleasures) + D1-D4 + E1-E3)
- B section asks for 10 pain statements in one compound question
- C section asks for 10 pleasure statements in one compound question
- Heavy free-text with large word limits
- No engagement layer
- No elevation mechanics
- Produces: icp-refined.md

### WHAT CHANGES

**Questions: Reduce B and C compound questions**
- B section: Change from "list 10 pain statements" → "list your TOP 5 pains" (still compound but less overwhelming). AI then probes the top 2 with follow-up questions to deepen them.
- C section: Change from "list 10 pleasure statements" → "list your TOP 5 dream outcomes." AI probes top 2.
- This makes the Hard Middle (Rounds 5-8 equivalent) less of a wall. Total interaction time drops ~15 min.

**Add: Engagement Layer (The Hard Middle Fix)**
This is where the engagement-engine's "Hard Middle Problem" framework gets applied:

- After A5 (WHO complete): **Pattern Break — "Insight Unlock"** — "Your ICP is already more specific than 90% of the pitches I see. Here's what's interesting about who you chose..."
- After B section (Pains complete): **Pattern Break — "Competitor Reveal"** — "Companies charging $[X]/month are solving pain #2 and #3. Nobody is touching pain #1. That's your wedge."
- After C section (Pleasures complete): **Variable Reward** — Auto-generate Pain-Pleasure Matrix visualization (text-based). Show them their pains mapped against pleasures.
- After D section (Hero Journey): **Pattern Break — "Offer Preview"** — Draft the transformation statement: "You take [WHO] from [PAIN STATE] to [PLEASURE STATE] in [TIMEFRAME]"
- After E section (Final): **Ultimate Variable Reward** — Full polished icp-refined.md delivered

- **Investment Signaling:**
  - After B (pain complete): "Your pain matrix has more depth than most consultants charge $5K for."
  - After D (hero journey): "You've just mapped the complete hero journey. This is the foundation of every piece of content, every sales conversation, every ad you'll ever run."
  - After E (final): "90 minutes invested. Your ICP document could anchor a $50K GTM strategy."

**Add: Elevation Instructions**
- AI must take scrappy pain statements and rewrite them as professional pain narratives in the output doc
- AI must take raw pleasure statements and craft them into outcome promises
- AI must synthesize the Hero Journey (D section) into a transformation arc suitable for landing pages, pitch decks, and sales scripts
- Output icp-refined.md should read like a professional strategy document, not a transcript

**Add: Acknowledgment Protocol** (same framework as SC1)

### ESTIMATED EDIT SIZE
~30 lines modified (B/C compound questions reduced) + ~180 lines added (engagement layer + elevation instructions) = ~210 lines net new. Minor deletions in B/C sections.

---

## SC3: MARKET ATTRACTIVENESS (market-attractiveness-scoring/SKILL.md)

### CURRENT STATE (v2.0 — but only philosophy changed)
- **25 questions, 60 minutes** (explicitly stated in architecture table)
- 4 sections × 5 questions each + scoring + output
- Re-asks pain evidence that SC2 already covered
- Re-asks competitive landscape that SC1 already covered
- Re-asks budget/pricing that SC2 already covered
- v2.0 label only changed from "rate 1-5" to "show evidence" — good philosophy but didn't reduce scope

### WHAT CHANGES

**This is the biggest redesign. SC3 goes from 25 questions to ~6 NEW questions.**

**Principle:** SC1 gave us niche, positioning, geography, product scope. SC2 gave us pain statements, congregation points, budget range, buying behavior. SC3 should ONLY ask what SC1+SC2 didn't cover — and that's primarily evidence validation and market sizing.

**New Section Architecture:**

| Section | Questions | Points | Focus | Duration |
|---------|-----------|--------|-------|----------|
| **A. Upstream Confirmation** | 0 (AI auto) | 0 | Load + display SC1/SC2 data; confirm or update | 3 min |
| **B. Evidence Validation** | 3 (2 FT, 1 MC) | 40 | Real evidence that pain is real and budget exists | 10 min |
| **C. Market Sizing & Growth** | 3 (2 FT, 1 MC) | 40 | TAM/SAM/SOM + growth signals + competitive gap | 10 min |
| **D. AI Synthesis** | 0 (AI auto) | 20 | AI scores overall MAS from upstream + new data | 2 min |
| **TOTAL** | **6 user-facing** | **100** | | **~25 min** |

**Section A: Upstream Confirmation (0 questions, auto)**
- AI loads SC1 (niche, positioning, geography) and SC2 (pain statements, congregation, budget, buying behavior)
- Displays summary to student: "Based on your previous work, here's what I know about your market..."
- Student confirms or flags updates
- No scoring — this is context loading

**Section B: Evidence Validation (3 questions, 40 pts)**
- B1 (FT, 15 pts): "What EVIDENCE do you have that this pain is real? Cite: customer conversations, competitor reviews, market data, personal experience, regulatory signals." — AI scores quality of evidence (0-15 scale)
- B2 (FT, 15 pts): "What EVIDENCE do you have that your ICP can and will pay? Cite: competitor pricing, customer interviews about budget, industry benchmark data, payment method availability." — AI scores evidence quality
- B3 (MC, 10 pts): "Which best describes your evidence base?" — Options: Primary research (interviewed 5+ ICPs), Secondary research (analyzed competitor data), Mixed (some interviews + some data), Assumption-based (no evidence yet)

**Section C: Market Sizing & Growth (3 questions, 40 pts)**
- C1 (FT, 15 pts): "Estimate your TAM → SAM → SOM. Show your math." — AI validates logic and assigns score
- C2 (FT, 15 pts): "What growth signals exist in this market? (New entrants, funding rounds, regulatory changes, technology shifts, hiring trends)" — AI scores signal strength
- C3 (MC, 10 pts): "How defensible is your competitive gap?" — Options: Unique mechanism (hard to copy), First-mover in sub-niche, Better execution (same approach), No clear gap

**Section D: AI Synthesis (0 questions, auto, 20 pts)**
- AI synthesizes all data from SC1 + SC2 + new SC3 answers
- Auto-generates MAS score using the Hormozi framework (Pain × Purchasing Power × Accessibility × Growth)
- Produces MarketAttractiveness.md

**Add: Engagement Layer (lighter than SC1/SC2 since this is shorter)**
- After B section: "Your evidence base is [strong/moderate/weak]. Here's what that means for your confidence level..."
- After C section: Variable Reward — draft market sizing paragraph for their output doc
- Investment Signaling: "25 minutes. Your market assessment is now evidence-based, not assumption-based. That alone puts you ahead of 90% of founders."

### ESTIMATED EDIT SIZE
This is essentially a **full rewrite** of the question set, execution flow, and scoring architecture. ~500 lines deleted, ~300 lines added. Net reduction of ~200 lines. The philosophy section, prerequisites, output format, and MENA scoring stay.

---

## SC4: STRATEGY SELECTOR (strategy-selector/SKILL.md)

### CURRENT STATE (v2.0 — already well-designed)
- ~10 user-facing questions (rest AI-auto from upstream)
- Pattern of Inaction gate built in
- 4 strategy paths, 8 archetypes
- Upstream inheritance working correctly
- Expert frameworks integrated (Attractive Character, Content-to-Paid Pipeline, etc.)

### WHAT CHANGES
**Minimal. SC4 is the model for how SC3 should work.**

**Add: Light Engagement Layer**
- After Section A (Founder DNA): "Your founder profile maps to the [Archetype] pattern. Here's what that means for your next 90 days..."
- After Section C (Strategy-Market Fit): Variable Reward — show draft strategy recommendation before final scoring
- After Section E (Final): Full strategy-recommendation.md delivered with "Your 90-day strategic recommendation is ready. This maps your specific strengths to the highest-probability path."
- Investment Signaling: "Your strategy recommendation accounts for your market data, ICP clarity, and personal resources. This is custom, not template."

**Add: Acknowledgment Protocol** (same framework)

### ESTIMATED EDIT SIZE
~80 lines added (engagement layer in execution flow). No structural changes.

---

## SC5: GTM FITNESS (gtm-fitness-scoring/SKILL.md)

### CURRENT STATE (v2.0 — already well-designed)
- 22 questions (18 MC + 4 FT), 45-65 min
- Pre-populates Fit and MENA from upstream
- Top 5 motion deep dive
- Expert frameworks: Pattern of Inaction, Content Systems Check, Solo Founder Bandwidth Calculator, Pattern Interrupt Readiness, Engagement Audit Gate
- 72-Hour Launch Commitment gate

### WHAT CHANGES
**Minimal. SC5 is solid.**

**Add: Light Engagement Layer**
- After Section B (Capability): "Your capability profile: [strong/moderate/building]. Here's what that unlocks..."
- After Section C (Motion Deep Dive): Variable Reward — show ranked motion table with tier assignments BEFORE asking sequencing questions
- After Section F (72-Hour Commitment): "Your GTM fitness assessment is complete. You have a ranked motion list, a 90-day sequence, and a 72-hour launch commitment. Most founders spend months figuring out what you just mapped in an hour."
- Investment Signaling after each major section

**Add: Acknowledgment Protocol** (same framework)

### ESTIMATED EDIT SIZE
~80 lines added (engagement layer in execution flow). No structural changes.

---

## SUMMARY TABLE

| Scorecard | Current State | What Changes | Edit Size |
|-----------|--------------|--------------|-----------|
| **SC1** (Project Definition) | v1.0, 21 Qs, no engagement | ADD engagement layer + elevation instructions. Keep all questions. | +200 lines |
| **SC2** (ICP Clarity) | v1.0, 14 interactions, heavy FT | REDUCE B/C from 10→5 statements. ADD engagement layer + elevation. | +180 lines, -30 lines |
| **SC3** (Market Attractiveness) | v2.0 label but 25 Qs/60 min | **REWRITE** from 25→6 questions. Inherit 80% from upstream. | -500 lines, +300 lines |
| **SC4** (Strategy Selector) | v2.0, well-designed | ADD light engagement layer. No structural changes. | +80 lines |
| **SC5** (GTM Fitness) | v2.0, well-designed | ADD light engagement layer. No structural changes. | +80 lines |

---

## EXECUTION ORDER

1. **SC3 first** — biggest change, most risk, needs full rewrite
2. **SC1 second** — add engagement + elevation to existing structure
3. **SC2 third** — reduce B/C + add engagement + elevation
4. **SC4 fourth** — light engagement polish
5. **SC5 fifth** — light engagement polish

After each file edit: verify question count, confirm engagement layer present, confirm upstream inheritance.

---

## WHAT I WILL NOT CHANGE

- Question scoring rubrics (unless the question itself changes, like SC3)
- Output file formats (project-brief.md, icp-refined.md, etc.)
- MENA-specific scoring logic
- Expert framework additions (Pattern of Inaction, Content Systems, etc.)
- Frontmatter/description fields
- Prerequisites/upstream dependency logic

---

## ADDENDUM A: SC1 SECTION 0 — VENTURE INTRODUCTION (Implemented 2026-03-08)

**What:** Added a new Section 0 before the existing Section A in SC1 (project-files-scoring/SKILL.md).

**Why:** The first interaction with the system should feel like sitting across from a sharp advisor who says "tell me what you're building." No forms, no scoring. Just talk.

**Two new questions (both unscored):**

1. **0.1 The Idea (Free-Flow):** "Before we get into the structured assessment, just tell me — what are you building? Who is it for? What problem does it solve? Talk to me like you're explaining it to a friend over coffee."
   - AI uses the raw answer to pre-populate context for later sections
   - Acknowledgment: "Got it. I can already see the shape of something here. Let's sharpen it."

2. **0.2 Name Your Venture:** "What would you call this venture? Give me your best shot — even if it's rough or temporary."
   - If founder provides a name → AI confirms and uses it across all output doc headers
   - If founder can't name it → AI generates 2-3 name suggestions with rationale, founder picks one
   - Selected venture name propagates to ALL output files across SC1-SC5

**Cross-scorecard impact:** Venture name appears in headers of project-brief.md, icp-refined.md, MarketAttractiveness.md, strategy-recommendation.md, gtm-fitness-report.md, and both downloadable documents.

**Status:** ✅ IMPLEMENTED in SC1 SKILL.md

---

## ADDENDUM B: DOCUMENT DOWNLOADS — ALL ANSWERS + STRATEGIC SUMMARY (Implemented 2026-03-08)

**What:** Two new download buttons under the "My Scorecard" section in EO-Assessment-Dashboard.html.

**Why:** Founders need two things after completing all 5 scorecards: (1) a complete record of everything they said (for reference, sharing with cofounders, or revisiting later), and (2) a polished executive brief that summarizes their venture strategy (the kind of document you'd hand to an investor or advisor).

**Button 1: "Download All Answers" (📋)**
- Generates a self-contained styled HTML document
- Contains: venture name header, per-scorecard sections with score badges, all Q&A pairs formatted professionally
- Dark theme styling consistent with SMO brand
- Downloads as `{VentureName}-All-Answers.html`
- Opens in any browser, prints cleanly to PDF

**Button 2: "Download Strategic Summary" (📄)**
- Generates a polished executive brief HTML
- Contains: score hero section (large score number + band label), three-pillar breakdown (MAS × 0.35 + ICP × 0.35 + GTM × 0.30), strategy path from SC4, key insights (strongest/weakest pillar), MENA context, top 3 GTM motion recommendations, next steps section
- Designed to feel like a $5K strategy deliverable
- Downloads as `{VentureName}-Strategic-Summary.html`

**Technical implementation:**
- Both use JavaScript `Blob` + `URL.createObjectURL` for client-side HTML generation
- Data pulled from localStorage (`eo-answers-{key}`, `eo-assessment-status`)
- No server-side dependency — works fully offline from the standalone HTML dashboard
- Format chosen: HTML (not DOCX/PDF) for maximum reliability in a standalone HTML dashboard context

**Status:** ✅ IMPLEMENTED in EO-Assessment-Dashboard.html

---

## EXECUTION STATUS (2026-03-08)

| Scorecard | Change | Status | Version |
|-----------|--------|--------|---------|
| SC1 | Section 0 + Engagement + Elevation | ✅ DONE | 1.1 |
| SC2 | B/C reduction (10→5) + Engagement + Elevation | ✅ DONE | 1.1 |
| SC3 | Full rewrite (25→6 questions) | ✅ DONE | 3.0 |
| SC4 | Light engagement polish | ✅ DONE | 2.1 |
| SC5 | Light engagement polish | ✅ DONE | 2.1 |
| Dashboard | Document downloads (All Answers + Strategic Summary) | ✅ DONE | — |
| Spec | ASSESSMENT-IMPLEMENTATION-SPEC.md created for Claude Code | ✅ DONE | — |

**All scorecard redesign work complete.** Ready for Claude Code implementation session.
