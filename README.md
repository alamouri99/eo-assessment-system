# Entrepreneurs Oasis MENA Assessment System

A comprehensive, client-side assessment framework designed for MENA-region founders evaluating their MicroSaaS readiness. The system guides users through five sequential scorecards, culminating in a consolidated Project Brief that can be fed into Claude Projects, Cowork, or Claude Code to begin building.

## Assessment Flow

```
ICP Clarity --> Market Attractiveness --> Strategy Selector --> GTM Fitness --> Project Files
     |                  |                      |                    |               |
     v                  v                      v                    v               v
  Score saved       Score saved           Score saved          Score saved      Score saved
     \                  |                      |                    |               /
      \                 |                      |                    |              /
       +-----------+----+----------+-----------+----------+---------+------------+
                                   |
                            Assessment Dashboard
                                   |
                         Generate Project Brief (MD)
```

## File Structure

```
05-Tools-Templates/
|-- EO-Assessment-Dashboard.html     # Hub / aggregator dashboard
|-- EO-ICP-Clarity-Scoring.html      # Scorecard 1: Ideal Customer Profile
|-- EO-Market-Attractiveness-Scoring.html  # Scorecard 2: Market Attractiveness
|-- EO-Strategy-Selector.html        # Scorecard 3: Strategy (with live scoreboard)
|-- EO-GTM-Fitness-Scoring.html      # Scorecard 4: Go-To-Market Fitness
|-- EO-Project-Files-Scoring.html    # Scorecard 5: Project Files Readiness
|-- EO-Strategy-Selector-Lite.html   # Standalone lead magnet (not in main flow)
|-- EO-Assessment-n8n-Architecture.md  # Backend webhook architecture docs
|
|-- eo-config/
|   |-- icp-config.md                # ICP question bank + scoring config
|   |-- mas-config.md                # Market Attractiveness config
|   |-- strategy-selector-config.md  # Strategy Selector config
|   |-- gtm-config.md                # GTM Fitness config
|   |-- project-files-config.md      # Project Files config
|   |-- consolidated-config.md       # Cross-scorecard config
|   +-- EO-ADMIN-GUIDE.md            # Admin setup and operations guide
|
|-- icp-clarity-scoring/SKILL.md     # Claude analysis prompt for ICP results
|-- market-attractiveness-scoring/SKILL.md  # Claude analysis prompt for MAS results
|-- gtm-fitness-scoring/SKILL.md     # Claude analysis prompt for GTM results
|-- strategy-selector/SKILL.md       # Claude analysis prompt for Strategy results
|-- project-files-scoring/SKILL.md   # Claude analysis prompt for PF results
```

## Scorecards

### 1. ICP Clarity Scoring
- **Questions:** 15 (across 5 sections)
- **Max Score:** 75
- **Bands:** Crystal Clear (85%+), Good Foundation (70%+), Fuzzy ICP (50%+), No Clarity (25%+), Critical (<25%)
- **Webhook:** `eo-icp-score`

### 2. Market Attractiveness Scoring
- **Questions:** 20 (across 4 sections)
- **Max Score:** 100
- **Bands:** Strong Market (80%+), Viable Market (65%+), Weak Market (50%+), High Risk (35%+), No Market (<35%)
- **Webhook:** `eo-mas-score`

### 3. Strategy Selector
- **Questions:** 7
- **Paths:** Product-Led, Service-Led, Community-Led, Content-Led
- **Features:** Live path scoreboard showing real-time scoring during assessment
- **No email screen** (enters directly into stepper; email captured at contact form)
- **Webhook:** `eo-strategy-selector`

### 4. GTM Fitness Scoring
- **Questions:** 25 (across 5 sections using motion-based assessment)
- **Max Score:** 100
- **Bands:** ELITE (80%+), STRONG (60%+), EMERGING (40%+), WEAK (<40%)
- **Geography options:** Gulf, Levant, North Africa, MENA Broadly, Global
- **Webhook:** `eo-gtm-score`

### 5. Project Files Scoring
- **Questions:** 20 (5 sections x 4 questions, scored 0-5 each)
- **Max Score:** 100
- **Bands:** Ready (80%+), Partial (60%+), Gaps (40%+), Start Over (<40%)
- **Gate rule:** If PF < 60, flags "NOT READY for Claude Desktop"
- **Webhook:** `eo-project-files`

## Assessment Dashboard

The hub page (`EO-Assessment-Dashboard.html`) provides:

- **Completion tracking:** Visual flow showing which scorecards are done, available, or locked
- **Score display:** Reads from `eo_completion_status` in localStorage
- **Demand-First Matrix:** 2x2 quadrant (Market Pull vs Execution Readiness)
- **Generate Project Brief:** Downloads a consolidated `project-brief.md` when all 5 assessments are complete
- **Email lookup:** Fetches scores from backend via consolidated webhook, with localStorage fallback

## Technical Architecture

### Client-Side (No Build Tools)
- Single-file HTML scorecards with embedded CSS and JavaScript
- No frameworks or dependencies (vanilla JS, ES5-compatible)
- Stepper UX pattern: Email -> Stepper -> Contact Form -> Results

### Data Persistence
| Key | Purpose |
|-----|---------|
| `eo_user_email` | Shared email across all scorecards |
| `eo_icp-clarity_answers` | ICP answer persistence |
| `eo_market-attractiveness_answers` | MAS answer persistence |
| `eo_strategy-selector_answers` | Strategy answer persistence |
| `eo_gtm-fitness_answers` | GTM answer persistence |
| `eo_project-files_answers` | Project Files answer persistence |
| `eo_completion_status` | Cross-scorecard completion tracking (scores + bands) |

### Email Auth Flow
1. **First scorecard (ICP):** Captures email, saves to `eo_user_email` in localStorage
2. **Subsequent scorecards:** Auto-skip email screen if `eo_user_email` exists
3. **Contact form:** Pre-fills email from captured value; updates localStorage on submit
4. **Dashboard:** Auto-fills lookup field from `eo_user_email`

### Flow Enforcement
Each scorecard checks prerequisites on page load:
- **MAS** requires ICP completion
- **Strategy** requires MAS completion
- **GTM** requires Strategy completion
- **Project Files** requires GTM completion

If prerequisites are not met, user is prompted to redirect.

### Webhooks (n8n Backend)
All scorecards POST results to n8n webhooks at:
```
https://ai.mamounalamouri.smorchestra.com/webhook/eo-{scorecard}
```

Payload structure:
```json
{
  "assessment": "scorecard-name",
  "answers": { "q1": 4, "q2": 3 },
  "section_scores": { "sectionA": 18 },
  "total_score": 78,
  "band": "Strong",
  "contact": { "name": "...", "email": "...", "company": "..." }
}
```

### MD Export
Each scorecard has a "Download Results (MD)" button on the results screen that generates a client-side markdown file containing:
- Score and band with description
- Section breakdown with percentage and strength indicators
- All questions with selected answers and scores
- Improvement recommendations

### Project Brief (Consolidated MD)
Generated from the Dashboard when all 5 assessments are complete. Combines:
- Overall readiness score and band
- All pillar scores in a summary table
- Demand-First Matrix position
- Bottleneck analysis
- Individual assessment scores
- Recommended next steps
- Claude prompt for the build phase

## Design System

| Color | Role |
|-------|------|
| `#1A1A2E` (dark navy) | Page background, navbar, heading text on light surfaces |
| `#E94D1B` (orange) | CTAs, buttons, progress bar, selected answers |
| `#FAF5EF` (warm beige) | Question card backgrounds, results containers |
| `#FFFFFF` (white) | Text on dark backgrounds, answer card defaults |
| `#6B7280` / `#9CA3AF` (gray) | Section labels, question counters |

## Strategy Selector Lite

`EO-Strategy-Selector-Lite.html` is a standalone lead magnet version of the Strategy Selector. It is:
- NOT part of the main 5-scorecard assessment flow
- NOT linked from the Dashboard
- Accessible via separate URL (e.g., `https://score.entrepreneursoasis.me/strategy-lite`)
- No email capture, no contact form, no webhook, no MD export
- Links to Telegram community as CTA

## Deployment

Static HTML files served via any web server or CDN. No server-side rendering required.

Recommended: Serve all files from the same origin domain for localStorage sharing.

Example: `https://score.entrepreneursoasis.me/`

## Communication Channels

- **Community:** Telegram (https://t.me/entrepreneursoasis)
- **Website:** entrepreneursoasis.me
