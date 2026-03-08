# EO Assessment Implementation Spec
**For:** Claude Code session — EO-Build repo revamp
**Date:** 2026-03-08
**Copy this file to:** `EO-Build/References/ASSESSMENT-IMPLEMENTATION-SPEC.md`

---

## PURPOSE

This document tells Claude Code exactly what to build for the self-serve assessment engine (Sprint 5+). It consolidates all 5 scorecard specs into implementation requirements.

---

## 1. SCORECARD SUMMARY (Post-Redesign)

| SC | Name | Version | User Qs | Duration | Points | Key Change |
|----|------|---------|---------|----------|--------|------------|
| SC1 | Project Definition | 1.1 | 23 (2 warm-up + 21 scored) | ~60 min | 100 | Added Section 0 (venture intro + naming), engagement layer, elevation instructions |
| SC2 | ICP Clarity | 1.1 | 14 interactions (B reduced 10→5, C reduced 10→5) + AI follow-ups | ~55 min | 100 | Reduced B/C pain/pleasure statements, added engagement, added elevation |
| SC3 | Market Attractiveness | 3.0 | 6 | ~25 min | 100 | **FULL REWRITE**: 25→6 questions, upstream inheritance from SC1+SC2 |
| SC4 | Strategy Selector | 2.1 | ~10 user-facing + AI auto | ~40 min | 100 | Light engagement polish |
| SC5 | GTM Fitness | 2.1 | 22 (18 MC + 4 FT) | ~50 min | 100 | Light engagement polish |

**Total assessment time:** ~230 minutes (~3.8 hours) across all 5 scorecards
**Total user-facing questions:** ~75 (down from ~110 pre-redesign)

---

## 2. SCORING ARCHITECTURE

### Overall Score Formula
```
Overall = (MAS × 0.35) + (ICP × 0.35) + (GTM × 0.30)
```
SC1 and SC2 are prerequisites — they feed SC3-SC5 but don't factor into the composite score directly.

### Score Bands (Universal)
| Range | Band | Color |
|-------|------|-------|
| 80-100 | LAUNCH READY | #00C853 (green) |
| 60-79 | ALMOST THERE | #FF6600 (orange) |
| 40-59 | NEEDS WORK | #FFD600 (yellow) |
| 20-39 | EARLY STAGE | #FF5722 (red-orange) |
| 0-19 | RESET | #D50000 (red) |

### Per-Scorecard Scoring
- **SC1:** 100 pts across Sections A-F (Section 0 is unscored warm-up)
- **SC2:** 100 pts across Sections A-E
- **SC3:** 100 pts = B (40) + C (40) + D-auto (20). Sections A and D are AI-auto.
- **SC4:** 100 pts with composite scoring. 4 strategy paths, 8 archetypes.
- **SC5:** 100 pts. 13 GTM motions scored: (Fit × 0.4) + (Readiness × 0.3) + (MENA × 0.3). Motions tiered: PRIMARY / SECONDARY / CONDITIONAL / SKIP.

---

## 3. CASCADE / DATA FLOW

```
SC1 (Project Definition)
├── Outputs: project-brief.md, niche-validation.md, positioning.md, product-spec.md
├── Provides to SC2: niche, positioning, geography, product angle
├── Provides to SC3: niche, positioning, geography, product scope
├── Provides to SC4: all SC1 outputs
└── Provides to SC5: all SC1 outputs

SC2 (ICP Clarity)
├── Output: icp-refined.md
├── Provides to SC3: pain statements, congregation points, budget range, buying behavior
├── Provides to SC4: ICP data
└── Provides to SC5: ICP data

SC3 (Market Attractiveness)  ← REDESIGNED: inherits 80% from upstream
├── Output: MarketAttractiveness.md
├── Section A: AUTO-LOADS SC1+SC2 data (no user questions)
├── Section D: AI SYNTHESIS (no user questions)
└── Provides to SC4+SC5: MAS score + evidence summary

SC4 (Strategy Selector)
├── Output: strategy-recommendation.md
├── AI auto-generates several inputs from SC1-SC3
└── Provides to SC5: strategy path, archetype

SC5 (GTM Fitness)
├── Output: gtm-fitness-report.md
├── Pre-populates Fit + MENA from upstream
└── Final assessment output
```

---

## 4. VENTURE IDENTITY

SC1 Section 0 introduces venture naming:
- **Question 0.1:** Free-flow "tell me about your idea" (unscored)
- **Question 0.2:** "Name your venture" (unscored)
- If founder can't name it, AI suggests 2-3 names with rationale

**Storage:**
- localStorage key: `eo-assessment-status.ventureName`
- Supabase column: `assessments.venture_name`
- Propagates to ALL output document headers across SC1-SC5
- Used in both downloadable documents (All Answers + Strategic Summary)

---

## 5. DOCUMENT GENERATION

Two downloadable documents under the "My Scorecard" dashboard section:

### 5A. Download All Answers
- **Filename:** `{VentureName}-All-Answers.html`
- **Content:** Complete record of every response across all 5 scorecards
- **Structure:** Venture name header → per-scorecard sections → score badge per SC → formatted Q&A pairs
- **Data source:** localStorage `eo-answers-{scorecard}` or Supabase `assessment_responses`
- **Styling:** SMO dark theme (#000000 bg, #FF6600 accent, Inter font)

### 5B. Download Strategic Summary
- **Filename:** `{VentureName}-Strategic-Summary.html`
- **Content:** Polished executive brief
- **Structure:**
  - Score hero section (large score number + band label)
  - Three-pillar breakdown: MAS (×0.35) + ICP (×0.35) + GTM (×0.30)
  - Strategy path from SC4 (path name + archetype)
  - Key insights: strongest pillar, weakest pillar, critical gap
  - MENA context paragraph
  - Top 3 GTM motion recommendations with tier labels
  - Next steps section
- **Design intent:** Should feel like a $5K strategy deliverable

### Implementation
- Both use JavaScript `Blob` + `URL.createObjectURL` for client-side generation
- Both produce self-contained HTML (no external dependencies)
- Both print cleanly to PDF via browser print dialog
- Already implemented in standalone dashboard (EO-Assessment-Dashboard.html)
- Need reimplementation in Next.js for the web platform

---

## 6. ENGAGEMENT PROTOCOL (All Scorecards)

Every scorecard now includes engagement mechanics. Claude Code should implement UI support for:

### Pattern Breaks
Appear between question groups (~every 10 minutes). Types:
- **Insight Unlock:** AI-generated insight about answer quality
- **Enemy Reveal:** AI identifies the systemic enemy from answers
- **Offer Preview:** Draft positioning/strategy shown mid-assessment
- **Variable Reward:** Polished artifact delivered (matrix, paragraph, table)
- **Competitor Reveal:** Gap analysis vs. market

### Acknowledgment Protocol
Before scoring each answer, AI acknowledges:
- Strong answers: positive reinforcement with specificity praise
- Weak answers: constructive push with specific follow-up
- Dream encouragement: validate ambition
- Enemy acknowledgment: reinforce competitive awareness

### Investment Signaling
At time milestones (~every 15-20 min), deliver value statements:
- "Your [X] has more depth than most consultants charge $5K for."
- "[X] minutes invested. Your [document] could anchor a $50K strategy."

### UI Requirements
- Pattern breaks should render as distinct UI cards (not inline text)
- Variable rewards (matrices, tables, draft paragraphs) should be visually distinct
- Investment signals can be subtle (toast notifications or inline callouts)
- Acknowledgments should appear before the next question loads

---

## 7. ELEVATION INSTRUCTIONS

All scored scorecards (SC1-SC5) now include elevation instructions. When generating output documents:

1. **Upgrade language:** Scrappy input → polished strategic prose
2. **Add strategic context:** Implications the founder didn't state but are logically implied
3. **Flag contradictions:** Mark cross-section misalignments with ⚠️ warnings
4. **Strategy-grade output:** Documents should read like professional deliverables

This affects the AI processing layer, not the UI directly. But the output documents should be renderable in the dashboard.

---

## 8. DATABASE SCHEMA ADDITIONS

```sql
-- Sprint 5 migration: 005_assessments.sql

-- Venture identity
ALTER TABLE assessments ADD COLUMN venture_name TEXT;

-- Answer storage (per question, per scorecard)
CREATE TABLE assessment_responses (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  assessment_id UUID REFERENCES assessments(id),
  scorecard TEXT NOT NULL CHECK (scorecard IN ('SC1','SC2','SC3','SC4','SC5')),
  question_id TEXT NOT NULL,       -- e.g., 'A1', 'B3', '0.1'
  question_text TEXT NOT NULL,
  answer_text TEXT,
  answer_mc TEXT,                   -- for MC answers
  score NUMERIC(5,2),
  max_score NUMERIC(5,2),
  ai_feedback TEXT,                 -- acknowledgment text
  created_at TIMESTAMPTZ DEFAULT now()
);

-- Per-scorecard scores
CREATE TABLE assessment_scores (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  assessment_id UUID REFERENCES assessments(id),
  scorecard TEXT NOT NULL,
  total_score NUMERIC(5,2),
  max_score NUMERIC(5,2) DEFAULT 100,
  band TEXT,                        -- LAUNCH READY, ALMOST THERE, etc.
  section_scores JSONB,             -- {A: 15, B: 22, C: 18, ...}
  created_at TIMESTAMPTZ DEFAULT now()
);

-- Overall composite score
-- Calculated: (MAS × 0.35) + (ICP × 0.35) + (GTM × 0.30)
-- Store in assessments.overall_score
ALTER TABLE assessments ADD COLUMN overall_score NUMERIC(5,2);
ALTER TABLE assessments ADD COLUMN overall_band TEXT;

-- Document generation tracking
ALTER TABLE assessments ADD COLUMN documents_generated JSONB DEFAULT '{}';
-- Example: {"all_answers": "2026-03-08T...", "strategic_summary": "2026-03-08T..."}
```

---

## 9. WEBHOOK INTEGRATION

Assessment data syncs to GHL via webhook:
- **Endpoint:** `https://ai.mamounalamouri.smorchestra.com/webhook/eo-consolidated`
- **Payload:** assessment_id, venture_name, per-scorecard scores, overall_score, band, strategy_path, top_3_motions
- **Trigger:** After each scorecard completion + after overall score calculation

---

## 10. SCORECARD SOURCE FILES

The full SKILL.md files with all question definitions, scoring rubrics, and engagement protocols live in:

```
EO_Claude_Training/skills/
├── project-files-scoring/SKILL.md      (SC1 v1.1)
├── icp-clarity-scoring/SKILL.md        (SC2 v1.1)
├── market-attractiveness-scoring/SKILL.md  (SC3 v3.0)
├── strategy-selector/SKILL.md          (SC4 v2.1)
└── gtm-fitness-scoring/SKILL.md        (SC5 v2.1)
```

Copy these to `EO-Build/References/scorecards/` before starting Claude Code. They are the source of truth for question text, scoring logic, and engagement mechanics.

---

## 11. DESIGN SYSTEM

- **Background:** #000000 (pure black) or #0F0F1A (near-black)
- **Cards:** #1A1A2E with #2D2D4A borders
- **Primary accent:** #FF6600 (orange)
- **Text:** #FFFFFF (primary), #A0A0A0 (secondary)
- **Font:** Inter (all text)
- **Score colors:** Green (#00C853) for high, Orange (#FF6600) for mid, Red (#D50000) for low
- **Pattern break cards:** Gradient background (#1a1a1a → #0f0f0f), orange left border
- **Variable reward cards:** Orange gradient background, white text

---

## 12. SPRINT 5 PROMPT FOR CLAUDE CODE

```
Read CLAUDE.md first, then References/ASSESSMENT-IMPLEMENTATION-SPEC.md.

This is Sprint 5: Self-Serve Assessment + Scoring Engine + Document Generation.

Requirements:
1. Assessment flow UI: 5 scorecards administered sequentially (SC1→SC2→SC3→SC4→SC5)
2. Question rendering: free-text fields, multiple choice, compound questions — all defined in scorecard SKILL.md files (in References/scorecards/)
3. SC1 Section 0: Free-flow opener + venture naming (unscored)
4. SC3 Section A: Auto-load SC1+SC2 data, display for confirmation
5. Real-time scoring with AI evaluation (use Claude API for free-text scoring)
6. Engagement layer: pattern breaks as distinct UI cards between question groups, acknowledgments before next question, investment signals as callouts
7. Per-scorecard results pages with score breakdown
8. Overall score calculation: (MAS × 0.35) + (ICP × 0.35) + (GTM × 0.30)
9. "My Scorecard" dashboard section with progress tracking
10. Two document downloads: "Download All Answers" and "Download Strategic Summary" (HTML generation)
11. Venture name storage and propagation across all documents
12. Webhook to GHL after each scorecard completion
13. Supabase tables: assessment_responses, assessment_scores (see schema in spec)

Database migration: Create 005_assessments.sql with schema from spec.

QA Gate:
- All questions from all 5 scorecards render correctly
- Scoring math verified against manual calculation
- Both document downloads generate valid HTML with correct data
- Venture name propagates to all document headers
- Webhook fires with correct payload
- Responsive at 375/768/1440 widths
- Dark theme compliance
```
