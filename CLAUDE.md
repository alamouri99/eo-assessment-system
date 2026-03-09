# EO Assessment System — Claude Code Execution Guide

**Version:** 2.0 — COMPLETE REWRITE (replaces all previous CLAUDE.md, specs, and instructions)
**Date:** 2026-03-09
**Author:** SMOrchestra / Mamoun

---

## ⚠️ CRITICAL: SOURCE OF TRUTH HIERARCHY

```
1. EO-Assessment-System-Change-Spec.md  ← THE SPEC (what to build)
2. THIS FILE (CLAUDE.md)                ← HOW to build it
3. SHARED-PATTERNS.md                   ← EXACT code patterns to use
4. The live HTML files in this repo      ← Current state (read before changing)
```

**IGNORE these files — they are OUTDATED and SUPERSEDED:**
- `specs/_DEPRECATED-SCORECARD-REDESIGN-SPEC.md` — OLD, wrong question counts
- `specs/_DEPRECATED-ASSESSMENT-IMPLEMENTATION-SPEC.md` — OLD, wrong data flow
- `SC1-SKILL.md` through `SC5-SKILL.md` — These are CONVERSATION SKILL definitions, NOT HTML build specs
- `eo-config/*.md` — Will be regenerated AFTER HTML is done
- Any CLAUDE.md version that mentions "SC3 first" or "23 questions for SC1"

---

## WHAT THIS REPO IS

A standalone, client-side assessment system for MENA MicroSaaS founders. 5 sequential scorecards + 1 dashboard, each a SINGLE-FILE HTML app (vanilla JS/CSS, no frameworks, no build tools, no external JS except font imports).

**Live:** `https://score.entrepreneursoasis.me/`
**Repo:** `eo-assessment-system` (GitHub)

---

## REPO STRUCTURE

```
├── CLAUDE.md                              ← YOU ARE HERE
├── EO-Assessment-System-Change-Spec.md    ← THE SPEC (read first!)
├── SHARED-PATTERNS.md                     ← Auth, slugify, localStorage code (copy exactly)
│
├── EO-Assessment-Dashboard.html           ← Dashboard ❌ REBUILD
├── EO-Project-Definition-Scoring.html     ← SC1: Project Definition ❌ REBUILD (7 questions)
├── EO-ICP-Clarity-Scoring.html            ← SC2: ICP Clarity ❌ REBUILD (6 questions)
├── EO-Market-Attractiveness-Scoring.html  ← SC3: Market Attractiveness ❌ RESULTS REVAMP ONLY (6 questions, same)
├── EO-Strategy-Selector.html              ← SC4: Strategy Selector ❌ REBUILD (20→10 questions)
├── EO-GTM-Fitness-Scoring.html            ← SC5: GTM Fitness ❌ REBUILD (22→10 questions)
```

---

## DESIGN SYSTEM (FROM THE LIVE HTML — USE THESE EXACT VALUES)

The live deployed SC1 is the design reference. Extract CSS variables from it.

```css
:root {
  --bg: #050A12;
  --surface: #0C1220;
  --card: #111827;
  --card-hover: #161F33;
  --border: rgba(255,255,255,0.06);
  --border-active: rgba(255,102,0,0.4);
  --accent: #FF6600;
  --accent-dim: rgba(255,102,0,0.15);
  --accent-glow: rgba(255,102,0,0.3);
  --teal: #0D9488;
  --teal-dim: rgba(13,148,136,0.15);
  --gold: #D97706;
  --red: #EF4444;
  --green: #22C55E;
  --text: #F1F5F9;
  --text-2: #94A3B8;
  --text-3: #64748B;
  --radius: 14px;
  --radius-sm: 8px;
}
```

**Font:** `'DM Sans', system-ui, sans-serif` (body) + `'DM Serif Display', serif` (headings)
**Import:** `https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&family=DM+Serif+Display&display=swap`

**⚠️ WARNING:** The Change Spec mentions `#1A1A2E`, `#FAF5EF`, `#E94D1B`, and Inter font. Those are WRONG — they came from an earlier design iteration. The LIVE HTML uses the values above. **USE THE LIVE VALUES.**

**Layout constants:**
- `max-width: 760px` centered container
- `14px` border radius on primary cards, `8px` on options/small elements
- Sticky nav with blur backdrop
- Progress bar at top (3px height, gradient fill)
- Questions use `<textarea>` for free-text (min-height: 160px)
- MC options are stacked cards with hover/selected states

---

## EXECUTION ORDER (FOLLOW EXACTLY)

### STEP 0: READ BEFORE ANYTHING
1. Read `EO-Assessment-System-Change-Spec.md` — ALL of it (Sections 1-10)
2. Read `SHARED-PATTERNS.md` — the auth, slugify, and localStorage code
3. Read EACH existing HTML file BEFORE modifying it

### STEP 1: DASHBOARD
**File:** `EO-Assessment-Dashboard.html`
**Scope:** Design changes + auth + resume assessment

Changes:
- [ ] New headline: "MENA MicroSaaS Founders OS — Clarity Suite / First Step to Launch Your MicroSaaS with AI. / Five tools. One system."
- [ ] Move Flow Guide section ABOVE tool cards
- [ ] Add metadata to Flow Guide steps (question count + time estimate per scorecard)
- [ ] Add completion indicators scoped to email+venture
- [ ] Add "Resume Assessment" section below Flow Guide (see Spec Section 7C)
- [ ] Auth flow: email entry → shows venture list from localStorage → select venture → populate scores
- [ ] Remove any PDF buttons
- [ ] localStorage migration logic (see SHARED-PATTERNS.md)

**Test:** Enter email with existing localStorage data → scores populate → Flow Guide shows completion

### STEP 2: SC1 — Project Definition (THE CRITICAL PATH)
**File:** `EO-Project-Definition-Scoring.html`
**Scope:** FULL REBUILD — 7 conversational questions + venture creation + clarity output

This is the MOST COMPLEX build. Every pattern created here is reused in SC2-SC5.

Changes:
- [ ] AUTH SCREEN: Email + Venture Name (this is the CREATION POINT)
  - User enters email
  - User enters venture name (free-text, required, min 3 chars)
  - System generates venture_slug (see SHARED-PATTERNS.md slugify function)
  - Stores to `eo_ventures_[email]` array in localStorage
  - If returning user: show retrieval banner (see Spec Section 7C)
- [ ] QUESTIONS: Replace ALL existing questions with these 7:
  1. `venture_intro` — "Tell me what you're building..." (free-text)
  2. `founder_fit` — "Why are YOU the person to build this?..." (free-text)
  3. `niche` — "Who exactly is this for?..." (free-text)
  4. `positioning` — "If your ideal buyer is comparing you..." (free-text)
  5. `product_vision` — "Walk me through the product..." (free-text)
  6. `founder_story` — "What's your founder story?..." (free-text)
  7. `mena_context` — "Where are you launching first..." (free-text)
  (Full question text in Spec Section 4, SC1 table)
- [ ] ENGAGEMENT BREAKS between sections (advisor-tone, <2 sentences)
- [ ] RESULTS PAGE (TYPE 1: CLARITY TOOL):
  - Polished Output Card (venture description, niche definition, positioning statement, MVP scope)
  - Clarity Score gauge (0-100)
  - "Sharpen These" cards (2-3 weakest areas with specific advice)
  - NO answer repetition
  - Single download button: "Download Full Analysis (MD)"
- [ ] SCORING: AI heuristic (specificity, evidence, MENA awareness, quantification)
- [ ] REMOVE: PDF buttons, html2pdf library, answer repetition in results
- [ ] localStorage keys: `eo_sc1_answers_[email]_[venture_slug]`, `eo_sc1_result_[email]_[venture_slug]`, `eo_scores_[email]_[venture_slug]`
- [ ] Webhook: POST to `https://smorchestra.app.n8n.cloud/webhook/eo-assessment` with venture_name + venture_slug in payload

**Test:** Complete all 7 questions → results show polished output (not raw answers) → MD download works → localStorage has correct composite keys → webhook fires with venture_slug

### STEP 3: SC2 — ICP Clarity
**File:** `EO-ICP-Clarity-Scoring.html`
**Scope:** FULL REBUILD — 6 conversational questions + venture selector + ICP profile output

Changes:
- [ ] AUTH SCREEN: Email + Venture SELECTOR (not creation)
  - User enters email
  - System looks up `eo_ventures_[email]` → auto-select if 1, dropdown if multiple, error if 0
  - Show retrieval banner if previous results exist
- [ ] QUESTIONS: 6 free-text questions (see Spec Section 4, SC2 table)
  1. `who` — Describe your ideal customer...
  2. `pain` — Top 3 pains...
  3. `dream` — Dream outcome...
  4. `journey` — Current state...
  5. `access` — Where do you find them...
  6. `validation` — How to reach 100 buyers in 30 days...
- [ ] RESULTS PAGE (TYPE 1: CLARITY TOOL):
  - Complete ICP Profile Card (who, pain, dream outcome, where to find them)
  - Clarity Score gauge (0-100)
  - "Sharpen These" cards
  - NO answer repetition
  - Single MD download
- [ ] All localStorage/webhook patterns from SC1

**Test:** Venture selector works → 6 questions render → results show ICP profile card → upstream SC1 data accessible

### STEP 4: SC3 — Market Attractiveness
**File:** `EO-Market-Attractiveness-Scoring.html`
**Scope:** RESULTS REVAMP ONLY (questions stay at 6)

Changes:
- [ ] AUTH SCREEN: Same venture selector pattern as SC2
- [ ] QUESTIONS: Keep existing 6 questions unchanged
- [ ] RESULTS PAGE (TYPE 2: SCORING TOOL):
  - Overall MAS Score: Large gauge ring (0-100)
  - 4-Dimension visual (Pain Reality, Purchasing Power, Market Sizing, Growth Signals)
  - Viability Verdict Card (one clear statement)
  - "How to Raise Your Score" cards (one per weak dimension)
  - NO answer repetition
  - Single MD download
- [ ] Remove PDF buttons
- [ ] Update localStorage keys to composite format
- [ ] Add retrieval banner

**Test:** Venture selector → questions → 4-dimension visual renders → verdict card clear → weak dimensions get actionable cards

### STEP 5: SC4 — Strategy Selector
**File:** `EO-Strategy-Selector.html`
**Scope:** Question revamp (20→10) + strategy recommendation output

Changes:
- [ ] AUTH SCREEN: Venture selector
- [ ] QUESTIONS: 10 questions (see Spec Section 4, SC4 table)
  - Q1-Q4: MC (skill, capital, time, risk)
  - Q5: Free-text strategy hypothesis
  - Q6-Q9: Path-specific MC (dynamic based on Q5 answer)
  - Q10: Free-text MENA fit
- [ ] RESULTS PAGE (TYPE 3: RECOMMENDATION TOOL):
  - Recommended Strategy Path card (primary path + "Why This Path" reasoning)
  - Secondary Path card (smaller, with activation condition)
  - Founder Archetype Badge
  - 90-Day Roadmap Preview (3 columns: Month 1/2/3)
  - "Strengthen Your Strategy" cards
  - NO answer repetition
  - Single MD download
- [ ] Remove PDF buttons, update localStorage, add retrieval

**Test:** MC questions render → Q5 triggers dynamic Q6-Q9 → results show strategy card → archetype badge renders

### STEP 6: SC5 — GTM Fitness
**File:** `EO-GTM-Fitness-Scoring.html`
**Scope:** Question revamp (22→10) + GTM motion cards

Changes:
- [ ] AUTH SCREEN: Venture selector
- [ ] QUESTIONS: 10 questions (see Spec Section 4, SC5 table)
  - Q1: MC/Confirm (ACV + sales cycle)
  - Q2: Free-text capability overview
  - Q3-Q7: Free-text per motion (DYNAMIC — motion names from pre-ranking)
  - Q8: Free-text MENA adaptations
  - Q9: Free-text activation sequence
  - Q10: Free-text 90-day plan
- [ ] Q3-Q7 DYNAMIC RENDERING: Pre-rank 13 motions using `(Fit × 0.4) + (Readiness × 0.3) + (MENA × 0.3)` where Fit and MENA are pre-populated from upstream data. Select top 5. Render motion name in question text.
  - **FALLBACK if no upstream data:** Show all 13 motions as a checklist, let user select top 5, then deep-dive on those.
- [ ] RESULTS PAGE (TYPE 3: RECOMMENDATION TOOL):
  - Top 3 GTM Motion Cards (name, tier, score breakdown, "How to Start" 3 steps, weekly hours)
  - 72-Hour Launch Commitment card (tied to PRIMARY motion)
  - Motion Ranking Table (all 13, compact)
  - NO answer repetition
  - Single MD download
- [ ] Remove PDF buttons, update localStorage, add retrieval

**Test:** Motion pre-ranking works → Q3-Q7 show motion names → results show 3 motion cards → ranking table renders all 13

---

## localStorage KEY SCHEMA (NEW — ALL FILES MUST USE THIS)

```javascript
// Venture registry (per email)
`eo_ventures_${email}` → [{ venture_name, venture_slug, created_at, last_active }]

// Cross-scorecard scores (per email+venture)
`eo_scores_${email}_${venture_slug}` → { sc1: 72, sc2: 65, sc3: null, sc4: null, sc5: null }

// Per-scorecard answers
`eo_sc${N}_answers_${email}_${venture_slug}` → { question_id: "answer", ... }

// Per-scorecard results
`eo_sc${N}_result_${email}_${venture_slug}` → { score, band, sections, polished_output/recommendations }
```

**MIGRATION:** On page load, check for old-format keys (`eo_sc1_answers_x@y.com` without venture slug). If found, show migration prompt asking user to assign a venture name. See SHARED-PATTERNS.md for migration code.

---

## WEBHOOK

**Single endpoint for ALL scorecards:**
```
POST https://smorchestra.app.n8n.cloud/webhook/eo-assessment
```

**Payload structure:**
```json
{
  "email": "user@example.com",
  "venture_name": "Dubai Real Estate CRM",
  "venture_slug": "dubai-real-estate-crm",
  "scorecard": "SC1",
  "answers": { "venture_intro": "...", "founder_fit": "...", ... },
  "scores": { "total": 72, "sections": { ... } },
  "upstream_data": { "sc1_score": 72, "sc2_score": 65 },
  "timestamp": "2026-03-09T12:00:00Z"
}
```

---

## SCORING BANDS (ALL SCORECARDS)

| Range | Band | Color |
|-------|------|-------|
| 85-100 | Launch Ready | `var(--green)` |
| 70-84 | Almost There | `var(--accent)` |
| 55-69 | Needs Work | `var(--gold)` |
| 40-54 | Early Stage | `var(--red)` |
| 0-39 | Reset | `var(--red)` |

---

## CRITICAL RULES (VIOLATE ANY = START OVER)

1. **SINGLE-FILE HTML.** Each scorecard is ONE .html file. No external JS files, no build tools, no npm. Only external imports allowed: Google Fonts CDN.

2. **READ THE LIVE HTML FIRST.** Before changing any file, read it completely. Understand its structure, patterns, and existing code. Don't rewrite from scratch unless explicitly told to.

3. **DESIGN SYSTEM FROM LIVE HTML.** Use `#050A12`/`#FF6600`/`#111827`/DM Sans. NOT `#1A1A2E`/`#E94D1B`/`#FAF5EF`/Inter. See Design System section above.

4. **THE CHANGE SPEC IS LAW.** If this CLAUDE.md and the Change Spec disagree, the Change Spec wins.

5. **AUTH IS NOT OPTIONAL.** Every file must implement email + venture authentication. SC1 creates, SC2-SC5 select. No exceptions.

6. **NO ANSWER REPETITION IN RESULTS.** Results pages show strategic output (polished docs / scores / recommendations). Raw answers go in the MD file only.

7. **VENTURE SLUG FUNCTION MUST BE IDENTICAL.** Copy the exact `slugify()` function from SHARED-PATTERNS.md into every HTML file. Character-for-character identical. A slug mismatch between files = data loss.

8. **RTL SUPPORT PRESERVED.** Every file must keep the RTL toggle and `body.rtl` class. Test with Arabic text in venture name and free-text answers.

9. **MOBILE RESPONSIVE.** Test at 375px, 768px, 1440px widths. The container is 760px max-width.

10. **WEBHOOK FIRES ON EVERY COMPLETION.** Every scorecard sends results to the webhook on completion. Include venture_slug in every payload.

---

## QA CHECKLIST (RUN AFTER EACH FILE)

- [ ] Auth screen renders correctly (email + venture name/selector)
- [ ] Correct number of questions renders (7/6/6/10/10)
- [ ] All free-text textareas accept input and save
- [ ] MC options highlight on selection
- [ ] Progress bar advances correctly
- [ ] Engagement breaks appear between sections
- [ ] Results page shows strategic output (NOT raw answers)
- [ ] Score gauge renders with correct band/color
- [ ] MD download works and contains full analysis
- [ ] No PDF buttons anywhere
- [ ] localStorage keys use composite format `[email]_[venture_slug]`
- [ ] Returning user sees retrieval banner with correct score
- [ ] Webhook fires with venture_slug in payload
- [ ] RTL toggle works
- [ ] Mobile responsive at 375px
- [ ] No console errors

---

## FILE DEPENDENCIES (DO NOT SKIP)

```
Dashboard ← nothing (build first)
    ↓
SC1 ← Dashboard (venture creation pattern)
    ↓
SC2 ← SC1 (needs venture to exist, loads SC1 upstream data)
    ↓
SC3 ← SC2 (loads SC1+SC2 upstream data)
    ↓
SC4 ← SC3 (loads SC1-SC3 upstream data)
    ↓
SC5 ← SC4 (loads SC1-SC4 upstream data, pre-ranks motions)
```

Each scorecard checks that its prerequisites are complete. If not, show a blocking message with a link to the missing scorecard.

---

## WHAT DOES NOT NEED CHANGING (LEAVE ALONE)

- The cross-linking between scorecard pages (nav links)
- The RTL CSS implementation (just preserve it)
- The favicon / meta tags
- The nav bar structure (just update step labels if needed)
