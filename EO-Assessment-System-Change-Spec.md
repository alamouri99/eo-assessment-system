# EO Assessment System — Complete Change Specification

**Version:** 1.1 (Auth + Retrieval)
**Date:** 2026-03-09
**Author:** SMOrchestra / Mamoun
**Repo:** `eo-assessment-system` (GitHub)
**Live:** `https://score.entrepreneursoasis.me/`

---

## OVERVIEW

This document is the single source of truth for all changes to the EO Founder Assessment System. It covers 6 HTML files (1 dashboard + 5 scorecards) across 7 change categories:

1. **Design Changes** — headline, layout, Flow Guide positioning
2. **Results Format** — what shows on-page vs what goes in MD export
3. **PDF Button Removal** — remove all non-functional PDF exports
4. **Question Revamp** — reduce from 93 total questions to 39
5. **Results Philosophy Revamp** — different output goals per scorecard type
6. **Authentication Revamp** — email + venture name (replaces email-only)
7. **Score Retrieval** — return users can load previous scores and resume

---

## FILES IN SCOPE

| File | Scorecard | Current Qs | New Qs | Status |
|------|-----------|-----------|--------|--------|
| `EO-Assessment-Dashboard.html` | Dashboard | — | — | Design changes only |
| `EO-Project-Definition-Scoring.html` | SC1 | 23 | 7 | Full revamp |
| `EO-ICP-Clarity-Scoring.html` | SC2 | 22 | 6 | Full revamp |
| `EO-Market-Attractiveness-Scoring.html` | SC3 | 6 | 6 | Results revamp only |
| `EO-Strategy-Selector.html` | SC4 | 20 | 10 | Question + results revamp |
| `EO-GTM-Fitness-Scoring.html` | SC5 | 22 | 10 | Question + results revamp |

---

## 1. DESIGN CHANGES (All Files)

### 1A. Dashboard Headline

**Current:**
```
EO Founder Assessment Suite
Five tools. One system. Know exactly where you stand.
```

**New:**
```
MENA MicroSaaS Founders OS — Clarity Suite
First Step to Launch Your MicroSaaS with AI.
Five tools. One system.
```

### 1B. Flow Guide Position

**Current:** Flow Guide section appears BELOW the 5 tool cards.

**New:** Flow Guide section moves ABOVE the 5 tool cards. It acts as the primary navigation and orientation element — the first thing the user sees after the headline.

### 1C. Flow Guide Metadata

**Current:** Flow Guide shows step names only (arrows between steps).

**New:** Each step in the Flow Guide shows:
- Step name
- Number of questions (e.g., "7 questions")
- Time estimate (e.g., "~15 min")
- Completion status indicator (checkmark if done, number if not)

| Step | Questions | Time |
|------|-----------|------|
| 1. Project Definition | 7 questions | ~15 min |
| 2. ICP Clarity | 6 questions | ~12 min |
| 3. Market Attractiveness | 6 questions | ~25 min |
| 4. Strategy Selector | 10 questions | ~20 min |
| 5. GTM Fitness | 10 questions | ~25 min |

### 1D. Card Design Preservation

**Keep the current card design language across all scorecard pages:**
- Dark theme (`#1A1A2E` background)
- Beige question cards (`#FAF5EF`)
- Orange accent (`#E94D1B`) for selected states, CTAs, progress
- `12px` border radius on primary cards, `8px` on options
- `max-width: 640px` centered question cards
- Shadow: `0 4px 20px rgba(0,0,0,0.3)`
- RTL toggle support preserved
- Mobile responsive at `680px` breakpoint
- Progress bar at top showing current question position

**Do NOT change:** fonts, colors, card structure, layout patterns, or visual language. All changes are content/question level, not visual.

### 1E. Engagement Breaks

**Add between sections** (not between every question):
- Short contextual message acknowledging progress
- Example after SC1 Section 1: "Good — your venture context is clear. Now let's sharpen the niche."
- Keep under 2 sentences. No fluff. Advisor tone.

---

## 2. RESULTS FORMAT — ON-PAGE vs MD FILE

### 2A. Universal Rule: No Answer Repetition On-Page

**Current behavior (all scorecards):** Results page shows a "Full Answers Summary" section that repeats every question and the user's answer. This is the majority of the results page.

**New behavior:** Results page shows ONLY:
1. Visual score (gauge ring or number)
2. Section breakdown (progress bars per section)
3. Strategic feedback cards (advice on how to improve)
4. One CTA: "Download Full Analysis (MD)" for the complete breakdown

**The MD file** contains everything:
- All questions and answers
- Detailed scoring rubrics applied
- Section-by-section analysis
- AI synthesis (if webhook returned data)
- Recommendations with specifics
- Cross-scorecard references

### 2B. Scorecard-Specific Results Philosophy

The 5 scorecards serve 3 different purposes. Results must reflect this:

#### TYPE 1: CLARITY TOOLS (SC1 + SC2)

**Purpose:** Take the founder's scrappy, unstructured input and transform it into polished, professional strategic documents. These are NOT scoring tools — they are clarity engines.

**On-Page Results Show:**
- **Polished Output Card:** The system takes the founder's raw answers and generates a clean, structured summary. For SC1: a one-paragraph venture description, a crisp niche definition, a positioning statement, and an MVP scope. For SC2: a complete ICP profile card (who, pain, dream outcome, where to find them).
- **Clarity Score:** Visual gauge (0-100) indicating how clear/specific the founder's inputs were
- **"Sharpen These" Cards:** 2-3 cards highlighting the weakest areas with specific advice on how to make them crisper. Example: "Your niche is too broad. You said 'SMEs in MENA' — try: 'Real estate brokerages in Dubai with 5-20 agents using manual lead tracking.'"
- **No answer repetition.** The polished output IS the result.

**MD File Contains:**
- Complete polished project brief / ICP document (ready to use as context file)
- All raw answers (for reference)
- Scoring breakdown per dimension
- Detailed improvement recommendations
- Cross-references to how SC1 feeds SC2, SC2 feeds SC3

#### TYPE 2: SCORING TOOL (SC3 — Market Attractiveness)

**Purpose:** Cross-check the founder's market assumptions against evidence. Judge viability across 4 dimensions. Provide honest feedback.

**On-Page Results Show:**
- **Overall MAS Score:** Large gauge ring (0-100) with band label
- **4-Dimension Radar/Bar Chart:** Pain Reality, Purchasing Power, Market Sizing, Growth Signals — each scored visually
- **Viability Verdict Card:** One card with a clear statement: "Your market scores 72/100 — Almost There. Pain evidence is strong but purchasing power assumptions need validation."
- **"How to Raise Your Score" Cards:** One card per weak dimension with specific actions. Example: "Purchasing Power: You have zero pricing validation. Run 5 willingness-to-pay interviews this week. Ask: 'Would you pay $X/month for this?' Document exact responses."
- **No answer repetition on page.**

**MD File Contains:**
- Full 4-dimension analysis with evidence citations from founder's answers
- Hormozi framework application (Dream × Likelihood / Delay × Effort)
- TAM/SAM/SOM validation
- Competitive gap analysis
- 30-day validation plan for weak dimensions
- All raw answers

#### TYPE 3: RECOMMENDATION TOOLS (SC4 + SC5)

**Purpose:** SC4 recommends the right strategy path. SC5 recommends the right GTM motions. Both are about giving the founder a clear "do THIS" output.

**SC4 On-Page Results Show:**
- **Recommended Strategy Path:** Large card with the primary path name, one-line description, and "Why This Path" reasoning (3 bullets derived from upstream data)
- **Secondary Path:** Smaller card with "activate if [condition]"
- **Founder Archetype Badge:** Visual badge (e.g., "Expert Without a Stage") with one-line description
- **90-Day Roadmap Preview:** 3-column visual (Month 1 / Month 2 / Month 3) with key milestones
- **"Strengthen Your Strategy" Cards:** 2-3 cards highlighting execution gaps with specific fixes
- **No answer repetition.**

**SC4 MD File Contains:**
- Complete strategy recommendation with full reasoning
- All 4 paths compared (why chosen path wins, why others were deprioritized)
- Archetype classification with implications
- Attractive Character mapping
- Content-to-Paid Pipeline per path (12-month view)
- 30-day validation experiment design
- Movement Brief
- All raw answers

**SC5 On-Page Results Show:**
- **Top 3 GTM Motions:** Three recommendation cards, each showing:
  - Motion name and tier (PRIMARY / SECONDARY / CONDITIONAL)
  - Composite score breakdown: Fit × 0.4 + Readiness × 0.3 + MENA × 0.3
  - "How to Start" — 3 concrete first steps for this motion
  - Estimated weekly hours required
- **72-Hour Launch Commitment:** Highlighted action card with the specific commitment tied to the PRIMARY motion
- **Motion Ranking Table:** All 13 motions ranked with tier labels (compact, not verbose)
- **No answer repetition.**

**SC5 MD File Contains:**
- Full 13-motion ranking table with Fit/Readiness/MENA/Score/Tier
- Detailed analysis of top 5 motions
- Capability gap analysis
- MENA execution adaptations
- 90-day motion sequence (week-by-week)
- Bandwidth calculation (hours/week vs. motion load)
- Pattern of Inaction diagnosis (if triggered)
- 72-hour commitment details
- All raw answers

---

## 3. PDF BUTTON REMOVAL

### Current State
Every scorecard has two download buttons:
- "Download Results (MD)" — **KEEP**
- "Download Results (PDF)" — **REMOVE**

Some also have:
- "Download Scorecard (PDF)" — **REMOVE**
- "Download Strategic Summary (HTML)" — **KEEP** (rename to "Download Full Analysis (MD)" if it's HTML-based, or keep as-is)

### Action
- Remove ALL PDF download buttons and their associated `html2pdf` library code
- Remove the `html2pdf` script import
- Keep only MD download functionality
- Single download button label: **"Download Full Analysis (MD)"**

---

## 4. QUESTION REVAMP

### SC1: Project Definition (23 → 7 questions)

**Philosophy shift:** Stop quizzing the founder with 23 granular questions. Instead, ask 7 broad conversational questions that let the founder explain their venture naturally. AI extracts all scoring signals from the answers.

| # | ID | Question | Replaces | Type |
|---|-----|----------|----------|------|
| 1 | `venture_intro` | "Tell me what you're building — the problem, who it's for, and why it matters. Talk to me like you're explaining it to a sharp friend over coffee." | s0_1, s0_2, a1 (3→1) | Free-text |
| 2 | `founder_fit` | "Why are YOU the person to build this? What's your unfair advantage — experience, access, obsession?" | a2, a3 (2→1) | Free-text |
| 3 | `niche` | "Who exactly is this for? Give me the specific niche — not 'SMEs' but the exact type of business, their size, their geography, and what makes them YOUR buyer." | b1, b2, b3, b4, b5 (5→1) | Free-text |
| 4 | `positioning` | "If your ideal buyer is comparing you to alternatives right now, what do they use today and why would they switch to you? Complete this: '[Product] is a _____ for _____ that _____ unlike _____.'" | c1, c2, c3, c4 (4→1) | Free-text |
| 5 | `product_vision` | "Walk me through the product: what does the MVP look like, what are the 3-5 core features, and how fast does a new user get their first win?" | d1, d2, d3, d4 (4→1) | Free-text |
| 6 | `founder_story` | "What's your founder story? Which archetype fits you — Leader, Reluctant Hero, Reporter, or Adventurer? Tell me the 3-sentence version of why you started this." | e1, e2 (2→1) | Free-text |
| 7 | `mena_context` | "Where are you launching first, what languages will you support, and how does your product account for MENA business culture?" | f1, f2, f3 (3→1) | Free-text |

**Scoring:** AI heuristic scoring based on answer specificity (names, numbers, examples, MENA mentions, competitive awareness). Each question maps to scoring dimensions from the original SKILL.md rubrics.

---

### SC2: ICP Clarity (22 → 6 questions)

**Philosophy shift:** Same as SC1. One conversational question per dimension. AI scores depth and specificity.

| # | ID | Question | Replaces | Type |
|---|-----|----------|----------|------|
| 1 | `who` | "Describe your ideal customer as a real person — their role, company size, industry, daily frustrations, and how they currently solve the problem you're targeting." | a1, a2, a3, a4, a5 (5→1) | Free-text |
| 2 | `pain` | "What are the top 3 pains your ICP feels? For each: how urgent is it, how often does it happen, and what does it cost them (time, money, reputation)?" | b1-b5 (5→1) | Free-text |
| 3 | `dream` | "What does 'success' look like for your ICP after using your product? Describe their dream outcome — both the business result and how it makes them feel." | c1-c5 (5→1) | Free-text |
| 4 | `journey` | "Where is your ICP right now in their journey? What's their current state, what obstacles block them, and how does your product bridge the gap to their dream outcome?" | d1, d2, d3, d4 (4→1) | Free-text |
| 5 | `access` | "Where do you find these people? List their online congregation points (LinkedIn groups, forums, communities) and offline gathering spots (events, associations, coworking)." | e1, e2 (2→1) | Free-text |
| 6 | `validation` | "How will you reach 100 potential buyers in the next 30 days? Be specific: which channels, what message, what offer." | e3 (1→1) | Free-text |

---

### SC3: Market Attractiveness (6 → 6 questions — NO CHANGE)

SC3 was already rewritten to v3.0 with 6 evidence-based questions. Questions stay the same.

**Changes needed:**
- Results format revamp (see Section 2B above — 4-dimension visual + viability verdict)
- Remove PDF button
- Add "How to Raise Your Score" cards
- Remove answer repetition from results page

---

### SC4: Strategy Selector (20 → 10 questions)

| # | ID | Question | Replaces | Type |
|---|-----|----------|----------|------|
| 1 | `core_skill` | "What's your strongest skill set?" (Technical/Sales/Content/Operations/Relationships) | A1 | MC |
| 2 | `capital` | "How much can you invest in the next 90 days?" ($0 / $500-2K / $2K-10K / $10K-50K / $50K+) | A2 | MC |
| 3 | `time` | "How many hours per week can you dedicate?" (<10 / 10-20 / 20-40 / 40+) | A3 | MC |
| 4 | `risk` | "What's your risk profile?" (Revenue in 30d / 90d / 6mo runway / Have other income) | A4 | MC |
| 5 | `strategy_hypothesis` | "Based on everything you know about your market and ICP, which of these 4 strategy paths feels right and why? (1) Replicate & Localize, (2) Consulting-First SaaS, (3) Boring Micro-SaaS, (4) Hammering Deep." | B1-B5 + C1-C5 (10→1) | Free-text |
| 6 | `exec_d1` | Path-specific D1 (changes based on Q5 answer) | D1 | MC |
| 7 | `exec_d2` | Path-specific D2 | D2 | MC |
| 8 | `exec_d3` | Path-specific D3 | D3 | MC |
| 9 | `exec_d4` | Path-specific D4 | D4 | MC |
| 10 | `mena_fit` | "What's your MENA execution advantage, and what's the biggest challenge you'll face in your target geography?" | E1+E2 (2→1) | Free-text |

**Key change:** B1-B4 and C1-C4 (8 AI-auto confirmation questions) are eliminated. The AI now silently cross-checks the founder's strategy hypothesis (Q5) against SC2 and SC3 upstream data during scoring. No need to quiz the founder on their own scores.

**What moves to output (not questions):**
- 90-day roadmap → AI-generated in results
- Archetype classification → AI-generated from Q1-Q5 signals
- Movement Brief → AI-generated in MD file
- 30-day validation experiment → AI-generated in MD file

---

### SC5: GTM Fitness (22 → 10 questions)

| # | ID | Question | Replaces | Type |
|---|-----|----------|----------|------|
| 1 | `business_context` | "Confirm your pricing: ACV is $[X]/year and sales cycle is [Y] months. Still accurate? (Update if needed)" | A1+A2 (2→1) | MC/Confirm |
| 2 | `capability_overview` | "Describe your current GTM capability across these dimensions: content library, outbound tools/infrastructure, audience size, marketing budget (next 90 days), network strength, and proof assets (case studies, testimonials, wins)." | B1-B6 (6→1) | Free-text |
| 3 | `motion_1_readiness` | "For [Top Motion #1 name]: what do you already have in place to execute this, and what's missing?" | C1.1+C1.2 (2→1) | Free-text |
| 4 | `motion_2_readiness` | "For [Top Motion #2 name]: what do you already have in place, and what's missing?" | C2.1+C2.2 (2→1) | Free-text |
| 5 | `motion_3_readiness` | "For [Top Motion #3 name]: what do you already have in place, and what's missing?" | C3.1+C3.2 (2→1) | Free-text |
| 6 | `motion_4_readiness` | "For [Top Motion #4 name]: what do you already have in place, and what's missing?" | C4.1+C4.2 (2→1) | Free-text |
| 7 | `motion_5_readiness` | "For [Top Motion #5 name]: what do you already have in place, and what's missing?" | C5.1+C5.2 (2→1) | Free-text |
| 8 | `mena_adaptations` | "For your top 3 motions, what specific MENA adaptations will you make? (language, timing, channels, messaging, cultural considerations)" | D1+D2 (2→1) | Free-text |
| 9 | `activation_sequence` | "In what order will you activate your top 3 motions over the next 90 days? Why this sequence?" | E1 | Free-text |
| 10 | `ninety_day_plan` | "Summarize your 90-day GTM execution plan: Weeks 1-4, 5-8, 9-12. Key milestones and targets for each phase." | E2 | Free-text |

**Key changes:**
- Section B collapses from 6 MC to 1 conversational free-text. AI extracts scores per dimension.
- Section C: 1 question per motion instead of 2. AI scores readiness from the answer.
- Fit and MENA Viability remain pre-populated from upstream data (not asked again).
- 72-Hour Launch Commitment becomes AI-generated output, not a question.

**Note on Q3-Q7 (motion readiness):** These questions are dynamic — the system pre-ranks all 13 motions using the formula `(Fit × 0.4) + (Readiness × 0.3) + (MENA × 0.3)` where Fit and MENA are pre-populated. It selects the top 5 for deep-dive. The question text includes the motion name dynamically.

---

## 5. SCORING APPROACH CHANGES

### Free-Text AI Scoring (SC1, SC2, SC4 Q5, SC4 Q10, SC5 Q2-Q10)

**Current:** MC questions with deterministic point values.

**New (for free-text questions):** Heuristic scoring based on answer quality signals:

| Signal | Weight | Examples |
|--------|--------|---------|
| **Specificity** | High | Named companies, specific roles, dollar amounts, percentages |
| **Evidence** | High | "I interviewed 10 people," "Our pilot showed 3x improvement" |
| **MENA awareness** | Medium | Mentions of regional specifics (WhatsApp, Arabic, Gulf timing, Ramadan) |
| **Competitive awareness** | Medium | Names competitors, explains differentiation |
| **Quantification** | Medium | Numbers, timelines, TAM calculations, pricing |
| **Depth** | Medium | Answer length >100 words with substance (not filler) |
| **Framework application** | Low | References to positioning frameworks, Hormozi, niche strategy |

**Scoring bands remain the same across all scorecards:**
- 85-100: Launch Ready
- 70-84: Almost There
- 55-69: Needs Work
- 40-54: Early Stage
- 0-39: Reset

**For the standalone HTML (no webhook):** Use client-side heuristic scoring (keyword detection, length analysis, specificity signals). This provides a reasonable estimate. When webhook is available, AI scoring overrides with more accurate assessment.

---

## 6. AUTHENTICATION REVAMP — Email + Venture Name

### 6A. Problem with Current Approach

**Current:** Users authenticate with email address only. This creates collisions — a founder with multiple ventures stores/overwrites data under one key. It also means SC2-SC5 can't distinguish between ventures when pulling upstream data.

**New:** Composite authentication key = `email + venture_name`. The venture name is created in SC1 (the first scorecard) and becomes a required field for SC2-SC5.

### 6B. Authentication Flow Per File

#### Dashboard (`EO-Assessment-Dashboard.html`)
- **New UI Element:** "Start New Assessment" requires both email and venture name
- **New UI Element:** "Resume Assessment" dropdown — after entering email, shows list of venture names associated with that email from localStorage
- Stores `eo_ventures_[email]` → array of `{ venture_name, venture_slug, created_at, last_active }`
- Flow Guide completion indicators now scoped to `email + venture_slug`

#### SC1 (`EO-Project-Definition-Scoring.html`) — THE CREATION POINT
- **Step 1:** User enters email
- **Step 2:** User enters venture name (free-text, required, min 3 chars)
- System generates `venture_slug` from venture name: lowercase, spaces→hyphens, strip special chars (e.g., "Dubai Real Estate CRM" → `dubai-real-estate-crm`)
- Stores venture registration: adds to `eo_ventures_[email]` array
- All SC1 data keyed to `eo_sc1_answers_[email]_[venture_slug]`
- Venture name + slug passed to webhook payload

#### SC2-SC5 (All Subsequent Scorecards) — CONSUMPTION POINTS
- **Step 1:** User enters email
- **Step 2:** System looks up `eo_ventures_[email]` from localStorage
  - If 1 venture → auto-select, show confirmation: "Continuing assessment for: [venture_name]"
  - If multiple ventures → show dropdown to select which venture
  - If 0 ventures → show error: "No assessment found for this email. Please complete SC1 first." + link to SC1
- **Step 3:** Load upstream data using composite key `[email]_[venture_slug]`
- All data storage keyed to `eo_sc[N]_answers_[email]_[venture_slug]`

### 6C. localStorage Key Schema Change

**Old keys (email-only):**
```
eo-scores                           → { email: "x@y.com", sc1: 72, sc2: 65 ... }
eo_sc1_answers_x@y.com             → { venture_intro: "...", ... }
eo_sc1_result                       → { score: 72, band: "Almost There", ... }
```

**New keys (email + venture):**
```
eo_ventures_x@y.com                → [{ venture_name: "Dubai RE CRM", venture_slug: "dubai-re-crm", created_at: "2026-03-09", last_active: "2026-03-09" }]
eo_scores_x@y.com_dubai-re-crm    → { sc1: 72, sc2: 65, sc3: null, sc4: null, sc5: null }
eo_sc1_answers_x@y.com_dubai-re-crm → { venture_intro: "...", ... }
eo_sc1_result_x@y.com_dubai-re-crm  → { score: 72, band: "Almost There", sections: {...}, polished: {...} }
eo_sc2_answers_x@y.com_dubai-re-crm → { ... }
eo_sc2_result_x@y.com_dubai-re-crm  → { ... }
... (same pattern for sc3-sc5)
```

**Migration note:** On first load, if old-format keys exist, the system should attempt to migrate them. If `eo_sc1_answers_x@y.com` exists but no venture registry, prompt the user to assign a venture name and migrate.

### 6D. Webhook Payload Change

**Add to all webhook payloads:**
```json
{
  "email": "x@y.com",
  "venture_name": "Dubai Real Estate CRM",
  "venture_slug": "dubai-re-crm",
  "scorecard": "SC1",
  "answers": { ... },
  "scores": { ... },
  "upstream_data": { ... }
}
```

The `venture_slug` becomes the primary identifier in n8n workflows for grouping all 5 scorecards into one assessment session.

### 6E. UI Spec — Auth Screen

**Visual design (same dark theme):**
- Centered card (same `max-width: 640px`, beige `#FAF5EF` background)
- Header: "Start Your Assessment" (SC1) or "Continue Your Assessment" (SC2-SC5)
- Field 1: Email (input, type=email, required)
- Field 2 (SC1 only): Venture Name (input, type=text, required, min 3 chars, placeholder: "e.g., Dubai Real Estate CRM")
- Field 2 (SC2-SC5): Venture selector (dropdown, populated from localStorage after email entry)
- Orange CTA button: "Begin" / "Continue"
- Below CTA: "Already completed this? [Retrieve Previous Results]" link (see Section 7)

---

## 7. SCORE RETRIEVAL — Return Users Load Previous Data

### 7A. Problem

Currently there is NO way for a user to come back and see their previous scores or download their files again. If they close the browser, they lose access to results (unless localStorage persists). Cross-device access is impossible.

### 7B. Retrieval Flow

#### Option A: localStorage-Based (MVP — Build First)

When a user enters their email + selects a venture on any scorecard page:
1. System checks localStorage for `eo_sc[N]_result_[email]_[venture_slug]`
2. If result exists → show a banner: "You've already completed this scorecard (Score: X/100). [View Results] or [Retake Assessment]"
3. "View Results" loads the stored results and renders them (same results page as first-time)
4. "Retake Assessment" clears stored answers for this scorecard+venture and starts fresh
5. MD file re-download available from the results view

#### Option B: Webhook-Backed (Phase 2 — Cross-Device)

The n8n webhook already receives all data. For cross-device retrieval:
1. User enters email + venture name on Dashboard "Resume Assessment" screen
2. Dashboard sends a GET request to a new webhook endpoint: `https://smorchestra.app.n8n.cloud/webhook/eo-retrieve`
3. Webhook returns all stored results for that email+venture pair
4. Dashboard populates localStorage from webhook response + updates Flow Guide completion indicators
5. User can then navigate to any completed scorecard to view results

**Phase 2 webhook endpoint spec:**
```
GET /webhook/eo-retrieve?email={email}&venture={venture_slug}
Response: {
  "found": true,
  "scores": { "sc1": 72, "sc2": 65, "sc3": 80, "sc4": null, "sc5": null },
  "results": {
    "sc1": { score, band, sections, polished_output, md_content },
    "sc2": { ... },
    "sc3": { ... }
  }
}
```

### 7C. Per-File Retrieval UI

#### Dashboard
- **New section:** "Resume Assessment" area (below Flow Guide, above tool cards)
- Fields: Email + Venture Name (or dropdown of ventures if email matches localStorage)
- On submit: loads all scores, updates Flow Guide indicators, enables "View Results" buttons on completed scorecards

#### Each Scorecard (SC1-SC5)
- **Auth screen addition:** After email + venture are entered, if previous results exist:
  - Show inline banner: `"You completed [Scorecard Name] on [date] — Score: [X]/100"`
  - Two buttons: `[View Previous Results]` `[Start Fresh]`
- **View Previous Results:** Jumps directly to results page with stored data
- **Start Fresh:** Clears this scorecard's data for this venture, begins question flow

### 7D. Visual Design for Retrieval Elements

**Resume Banner (on auth screen):**
- Card style: same beige card, but with a green-ish left border (`#2D8F4E`) to signal "completed"
- Score badge: orange circle with score number
- Date completed: light gray text
- Two action buttons side by side: orange outline "View Results" + dark fill "Start Fresh"

**Dashboard Resume Section:**
- Same card grid as tool cards but single wide card
- Heading: "Resume Your Assessment"
- Email + venture input
- After match: show progress summary — 5 circles (SC1-SC5) with scores filled in for completed ones, empty for incomplete
- CTA: "Continue to [Next Incomplete Scorecard]"

---

## 8. TECHNICAL IMPLEMENTATION NOTES

### localStorage Keys (CHANGED — See Section 6C)

**New key structure:**
- `eo_ventures_[email]` → venture registry array
- `eo_scores_[email]_[venture_slug]` → cross-scorecard score object
- `eo_sc[N]_answers_[email]_[venture_slug]` → per-scorecard answers
- `eo_sc[N]_result_[email]_[venture_slug]` → per-scorecard results (score, band, sections, outputs)

### Webhook Integration (UPDATED)
- **Score submission:** `POST https://smorchestra.app.n8n.cloud/webhook/eo-assessment` — all answers + scores + venture_slug
- **Score retrieval (Phase 2):** `GET https://smorchestra.app.n8n.cloud/webhook/eo-retrieve?email={email}&venture={venture_slug}`
- Payload now includes `venture_name` and `venture_slug` fields

### RTL Support (No Change)
- `dir` attribute toggle on `<html>`
- CSS flexbox `row-reverse` for RTL
- Arabic placeholder text where applicable

### What Gets Removed
- `html2pdf` library import (`<script src="...html2pdf.bundle.min.js">`)
- All PDF generation functions
- All PDF download button elements
- Answer repetition sections in results display
- MC option sets for collapsed questions (replaced by free-text textareas)
- Old email-only auth flow (replaced by email + venture)

### What Gets Added
- Free-text `<textarea>` elements (min 3 rows, expandable)
- Engagement break messages between sections
- Visual gauge ring component for scores (if not already present)
- "How to Raise Your Score" / "Sharpen These" card components
- Polished output generation logic (SC1, SC2)
- Strategy recommendation card component (SC4)
- GTM motion recommendation cards (SC5)
- Dynamic question rendering for SC5 Q3-Q7 (motion names from pre-ranking)
- **Email + venture name auth screen** (all 6 files)
- **Venture registration logic** (SC1)
- **Venture selector dropdown** (SC2-SC5, Dashboard)
- **Score retrieval banner** (SC1-SC5 auth screens)
- **Resume Assessment section** (Dashboard)
- **localStorage migration logic** (old email-only → new email+venture keys)

---

## 9. EXECUTION ORDER

Recommended build sequence. **Authentication is a cross-cutting concern** — it must be built into every file from the start, not bolted on later.

| Priority | File | Scope | Depends On |
|----------|------|-------|------------|
| 1 | Dashboard | Design changes + headline + Flow Guide reposition + Resume Assessment section + auth (email+venture) | Nothing |
| 2 | SC1 | Full revamp: 7 questions + clarity output + no PDF + **venture creation** (auth origin point) + retrieval banner | Dashboard done |
| 3 | SC2 | Full revamp: 6 questions + ICP profile output + no PDF + venture selector auth + retrieval banner | SC1 pattern (venture exists) |
| 4 | SC3 | Results revamp only + venture selector auth + retrieval banner | SC1/SC2 pattern |
| 5 | SC4 | Question revamp (20→10) + strategy recommendations + venture selector auth + retrieval banner | SC3 done |
| 6 | SC5 | Question revamp (22→10) + GTM motion cards + 72hr commitment + venture selector auth + retrieval banner | SC4 done |
| 7 | Phase 2: Retrieval webhook | Build `eo-retrieve` endpoint in n8n for cross-device data loading | All scorecards done |

**Critical path note:** SC1 is the most complex build because it introduces (a) the new question format, (b) the clarity output pattern, (c) the venture creation flow, and (d) the retrieval banner. Every subsequent scorecard inherits these patterns. Get SC1 right and the rest flows.

---

## 10. SUMMARY TABLE

| Change | Dashboard | SC1 | SC2 | SC3 | SC4 | SC5 |
|--------|-----------|-----|-----|-----|-----|-----|
| New headline | ✅ | — | — | — | — | — |
| Flow Guide above cards | ✅ | — | — | — | — | — |
| Flow Guide metadata | ✅ | — | — | — | — | — |
| Remove PDF buttons | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Remove answer repetition | — | ✅ | ✅ | ✅ | ✅ | ✅ |
| Question reduction | — | 23→7 | 22→6 | 6→6 | 20→10 | 22→10 |
| Free-text conversion | — | ✅ (all 7) | ✅ (all 6) | — | ✅ (2 of 10) | ✅ (8 of 10) |
| Clarity output (polished docs) | — | ✅ | ✅ | — | — | — |
| Scoring visual (4-dim) | — | — | — | ✅ | — | — |
| Strategy recommendation cards | — | — | — | — | ✅ | — |
| GTM motion cards | — | — | — | — | — | ✅ |
| Engagement breaks | — | ✅ | ✅ | ✅ | ✅ | ✅ |
| Keep card design | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Auth: email + venture** | ✅ | ✅ (creates) | ✅ (selects) | ✅ (selects) | ✅ (selects) | ✅ (selects) |
| **Venture registry** | ✅ (resume UI) | ✅ (writes) | ✅ (reads) | ✅ (reads) | ✅ (reads) | ✅ (reads) |
| **Score retrieval banner** | ✅ (resume section) | ✅ | ✅ | ✅ | ✅ | ✅ |
| **localStorage migration** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

---

**END OF SPEC — v1.1 (Auth + Retrieval added)**
