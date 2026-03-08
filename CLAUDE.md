# EO Assessment System — Claude Code Project Context

## What This Repo Is

A standalone, client-side assessment system for MENA founders evaluating MicroSaaS readiness. 5 sequential scorecards, each a single-file HTML scorecard + a SKILL.md (Claude conversation skill definition). No frameworks, no build tools — vanilla JS/HTML/CSS served statically.

## Repo Structure

```
├── CLAUDE.md                              ← YOU ARE HERE
├── specs/
│   ├── SCORECARD-REDESIGN-SPEC.md         ← BEFORE/AFTER spec for all 5 scorecards
│   └── ASSESSMENT-IMPLEMENTATION-SPEC.md  ← Implementation requirements (scoring, data flow, schema)
│
├── project-files-scoring/SKILL.md         ← SC1: Project Definition v1.1  ✅ UPDATED
├── icp-clarity-scoring/SKILL.md           ← SC2: ICP Clarity v1.1         ✅ UPDATED
├── market-attractiveness-scoring/SKILL.md ← SC3: Market Attractiveness v3.0 ✅ UPDATED (FULL REWRITE)
├── strategy-selector/SKILL.md             ← SC4: Strategy Selector v2.1   ✅ UPDATED
├── gtm-fitness-scoring/SKILL.md           ← SC5: GTM Fitness v2.1         ✅ UPDATED
│
├── EO-Project-Definition-Scoring.html     ← SC1 HTML scorecard ❌ NEEDS UPDATE
├── EO-ICP-Clarity-Scoring.html            ← SC2 HTML scorecard ❌ NEEDS UPDATE
├── EO-Market-Attractiveness-Scoring.html  ← SC3 HTML scorecard ❌ NEEDS FULL REWRITE
├── EO-Strategy-Selector.html              ← SC4 HTML scorecard ❌ NEEDS UPDATE
├── EO-GTM-Fitness-Scoring.html            ← SC5 HTML scorecard ❌ NEEDS UPDATE
├── EO-Assessment-Dashboard.html           ← Hub dashboard ❌ NEEDS UPDATE
│
├── eo-config/                             ← Config files per scorecard (question banks, scoring)
│   ├── project-files-config.md
│   ├── icp-config.md
│   ├── mas-config.md
│   ├── strategy-selector-config.md
│   ├── gtm-config.md
│   ├── consolidated-config.md
│   └── EO-ADMIN-GUIDE.md
│
├── EO-Assessment-n8n-Architecture.md      ← Webhook/backend architecture
├── _DEPRECATED-EO-Project-Files-Scoring.html
└── _DEPRECATED-EO-Strategy-Selector-Lite.html
```

## Current State

The SKILL.md files have been updated to their latest versions (v1.1, v1.1, v3.0, v2.1, v2.1). The HTML scorecards are BEHIND — they still reflect the old SKILL.md versions. The HTML files need to be updated to match the new SKILL.md specs.

## YOUR JOB: Update HTML Scorecards to Match Updated SKILL.md Files

### Read Order (MANDATORY)
1. `specs/SCORECARD-REDESIGN-SPEC.md` — understand what changed and why
2. `specs/ASSESSMENT-IMPLEMENTATION-SPEC.md` — understand scoring, data flow, engagement protocol
3. Each SKILL.md before touching its corresponding HTML

### Execution Order (follow this exactly)

**STEP 1: SC3 — Market Attractiveness (FULL REWRITE)**
- Read `market-attractiveness-scoring/SKILL.md` (v3.0)
- Read `specs/SCORECARD-REDESIGN-SPEC.md` → SC3 section
- REWRITE `EO-Market-Attractiveness-Scoring.html` from 25 questions → 6 questions
- New structure:
  - Section A: Upstream Confirmation (auto-load SC1+SC2 data from localStorage, display summary, no user questions)
  - Section B: Evidence Validation (3 questions, 40 pts)
  - Section C: Market Sizing & Growth (3 questions, 40 pts)
  - Section D: AI Synthesis (auto, 20 pts)
- Keep: design system, localStorage patterns, webhook integration, RTL support, email capture flow
- Add: engagement layer (pattern breaks between sections, investment signaling)
- Verify: total still scores /100, localStorage keys unchanged, webhook payload updated

**STEP 2: SC1 — Project Definition (AMEND)**
- Read `project-files-scoring/SKILL.md` (v1.1)
- Read `specs/SCORECARD-REDESIGN-SPEC.md` → SC1 section
- AMEND `EO-Project-Definition-Scoring.html`:
  - ADD Section 0 before existing Section A (2 unscored warm-up questions: free-flow idea + venture naming)
  - ADD engagement layer: Pattern Breaks after A3, B5, D4, F3
  - ADD acknowledgment protocol: dynamic response cards between questions
  - ADD investment signaling: callout cards at 30min, 50min, final
  - ADD venture name capture → store in `eo-assessment-status.ventureName` in localStorage
- Keep: all 21 scored questions, scoring rubrics, section architecture, output structure
- Verify: scoring still /100, Section 0 is unscored, venture name propagates

**STEP 3: SC2 — ICP Clarity (AMEND)**
- Read `icp-clarity-scoring/SKILL.md` (v1.1)
- Read `specs/SCORECARD-REDESIGN-SPEC.md` → SC2 section
- AMEND `EO-ICP-Clarity-Scoring.html`:
  - REDUCE B section: "list 10 pains" → "list TOP 5 pains" + AI probes top 2
  - REDUCE C section: "list 10 pleasures" → "list TOP 5 dream outcomes" + AI probes top 2
  - ADD engagement layer: Pattern Breaks after A5, B, C, D, E
  - ADD acknowledgment protocol
  - ADD investment signaling
  - ADD elevation instructions for output doc generation
- Keep: Section structure A-E, scoring rubrics (except B/C adjustment)
- Verify: scoring still /100, B/C questions reduced, engagement renders

**STEP 4: SC4 — Strategy Selector (LIGHT POLISH)**
- Read `strategy-selector/SKILL.md` (v2.1)
- Read `specs/SCORECARD-REDESIGN-SPEC.md` → SC4 section
- AMEND `EO-Strategy-Selector.html`:
  - ADD light engagement layer: feedback after Section A (Founder DNA), C (Strategy-Market Fit), E (Final)
  - ADD acknowledgment protocol
- Keep: everything else — SC4 is already well-designed
- Verify: no scoring changes, engagement renders, upstream data still loads

**STEP 5: SC5 — GTM Fitness (LIGHT POLISH)**
- Read `gtm-fitness-scoring/SKILL.md` (v2.1)
- Read `specs/SCORECARD-REDESIGN-SPEC.md` → SC5 section
- AMEND `EO-GTM-Fitness-Scoring.html`:
  - ADD light engagement layer: feedback after Section B (Capability), C (Motion Deep Dive), F (72-Hour Commitment)
  - ADD acknowledgment protocol
- Keep: everything else — SC5 is already solid
- Verify: no scoring changes, engagement renders, upstream data still loads

**STEP 6: Dashboard — Document Downloads**
- Read `specs/ASSESSMENT-IMPLEMENTATION-SPEC.md` → Section 5 (Document Generation)
- AMEND `EO-Assessment-Dashboard.html`:
  - ADD "Download All Answers" button → generates `{VentureName}-All-Answers.html`
  - ADD "Download Strategic Summary" button → generates `{VentureName}-Strategic-Summary.html`
  - Both use JS Blob + URL.createObjectURL for client-side HTML generation
  - Data from localStorage (`eo-answers-{key}`, `eo-assessment-status`)
  - ADD venture name display in dashboard header
  - UPDATE score formula display: Overall = (MAS × 0.35) + (ICP × 0.35) + (GTM × 0.30)
- Verify: both downloads produce valid HTML, venture name appears in headers, prints cleanly

**STEP 7: Update eo-config files**
- Sync each config file with its corresponding updated SKILL.md
- `project-files-config.md` ← from SC1 v1.1 (add Section 0, engagement protocol)
- `icp-config.md` ← from SC2 v1.1 (reduced B/C, engagement)
- `mas-config.md` ← from SC3 v3.0 (full rewrite — 6 questions, upstream inheritance)
- `strategy-selector-config.md` ← from SC4 v2.1 (light engagement)
- `gtm-config.md` ← from SC5 v2.1 (light engagement)
- `consolidated-config.md` ← update cascade/data flow diagram, scoring formula

## Design System

| Token | Value | Usage |
|-------|-------|-------|
| `--eo-dark` | `#1A1A2E` | Page background, navbar |
| `--eo-orange` | `#E94D1B` | CTAs, buttons, progress, selected answers |
| `--eo-beige` | `#FAF5EF` | Question card backgrounds |
| `--eo-card-bg` | `#FFFFFF` | Answer card defaults |
| `--eo-gray-text` | `#6B7280` / `#9CA3AF` | Section labels, counters |
| Font | Inter | All text |

### Engagement UI Components (NEW — add to all scorecards)
- **Pattern Break cards:** gradient bg (#1a1a1a → #0f0f0f), orange left border 4px, 16px padding
- **Variable Reward cards:** orange gradient bg, white text, rounded corners
- **Investment Signal:** subtle callout, orange-tinted bg, small text
- **Acknowledgment:** appears between questions, italic, orange accent on strong answers

## localStorage Keys (DO NOT CHANGE)

| Key | Purpose |
|-----|---------|
| `eo_user_email` | Shared email across all scorecards |
| `eo_icp-clarity_answers` | SC2 answer persistence |
| `eo_market-attractiveness_answers` | SC3 answer persistence |
| `eo_strategy-selector_answers` | SC4 answer persistence |
| `eo_gtm-fitness_answers` | SC5 answer persistence |
| `eo_project-files_answers` | SC1 answer persistence |
| `eo_completion_status` | Cross-scorecard completion tracking |

### NEW localStorage Keys
| Key | Purpose |
|-----|---------|
| `eo-assessment-status.ventureName` | Venture name from SC1 Section 0 |

## Webhook Endpoints (DO NOT CHANGE)

All POST to: `https://ai.mamounalamouri.smorchestra.com/webhook/eo-{scorecard}`

## Scoring (Source of Truth: SKILL.md files)

| SC | Points | Key Rule |
|----|--------|----------|
| SC1 | /100 | Section 0 is UNSCORED. Sections A-F scored. |
| SC2 | /100 | B reduced to 5 pains, C reduced to 5 pleasures |
| SC3 | /100 | B(40) + C(40) + D-auto(20). Section A is auto-load. |
| SC4 | /100 | 4 paths, 8 archetypes. Composite scoring. |
| SC5 | /100 | 13 motions: (Fit×0.4)+(Readiness×0.3)+(MENA×0.3) |
| **Overall** | | **(MAS × 0.35) + (ICP × 0.35) + (GTM × 0.30)** |

## Critical Rules

1. **Single-file HTML** — each scorecard is ONE .html file. No external JS, no build tools, no frameworks.
2. **RTL support** — every scorecard has `body.rtl` class and RTL toggle. Preserve this.
3. **Email flow** — first scorecard captures email, subsequent ones auto-skip if `eo_user_email` exists.
4. **Flow enforcement** — each scorecard checks prerequisites on page load (SC2 needs SC1, etc.)
5. **Stepper UX** — Email → Stepper → Contact Form → Results. Keep this pattern.
6. **No breaking changes to localStorage keys** — downstream depends on exact key names.
7. **Webhook payloads** — keep structure, add new fields (venture_name, engagement_data) alongside existing.
8. **MD export** — each scorecard has "Download Results (MD)" button. Keep this, add engagement summary.
9. **SKILL.md is source of truth** — if HTML and SKILL.md conflict, SKILL.md wins.

## QA After Each Step

After EACH scorecard update:
- Open in browser, complete full flow
- Verify scoring totals to /100
- Verify localStorage saves correctly
- Verify prerequisite checks work
- Test RTL toggle
- Test at 375px, 768px, 1440px widths
- Verify MD export works
- Verify webhook fires (check Network tab)
- Verify engagement components render (pattern breaks, acknowledgments, signals)
