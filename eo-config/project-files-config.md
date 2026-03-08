# MicroSaaS Project Definition Scorecard
# Version: 1.1

## Purpose
Defines the founder's venture identity, niche, positioning, product vision, brand voice, and MENA context.
Section 0 (Venture Introduction) is unscored warm-up. Sections A-F are scored.

## Scoring
- 23 questions: 2 warm-up (Section 0) + 21 scored (Sections A-F)
- Section 0: UNSCORED (venture idea + naming)
- Sections A-F: Scored per rubric in SKILL.md
- Total score: /100

## Engagement Protocol (NEW in v1.1)
- Pattern Breaks: After A3 (Insight Unlock), B5 (Enemy Reveal), D4 (Offer Preview), F3 (Final)
- Acknowledgment Protocol: Between all scored questions
- Investment Signaling: At ~30min, ~50min, and final
- Venture name stored in localStorage: `eo-assessment-status.ventureName`

## Sections
| Section | Name | Questions | Max | Notes |
|---------|------|-----------|-----|-------|
| 0 | Venture Introduction | s0_1, s0_2 | 0 | UNSCORED warm-up |
| A | Founder Context & Problem Origin | a1-a3 | 15 | |
| B | 3-Level Niche Definition | b1-b5 | 25 | |
| C | Positioning & Differentiation | c1-c4 | 20 | |
| D | Product Vision & Spec | d1-d4 | 20 | |
| E | Brand Voice & Founder Story | e1-e2 | 10 | |
| F | MENA Context & Localization | f1-f3 | 10 | |

## Bands
- READY (80-100): Files are production-grade. Start building immediately.
- PARTIAL (60-79): Good foundation but gaps will slow you down.
- GAPS (40-59): Critical files missing. Build these before touching code.
- START OVER (0-39): You're not ready for Claude Desktop. Do the work first.

## Consolidated Readiness Weight
Project Files contributes to the overall readiness formula as a GATE:
- If Project Files < 60: flag as "NOT READY for Claude Desktop" regardless of other scores
- If Project Files >= 60: proceed to consolidated readiness calculation

## Webhook
`https://ai.mamounalamouri.smorchestra.com/webhook/eo-project-files`

## Storage Key
`eo_project-files_answers`
