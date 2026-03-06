# MicroSaaS Project Files Readiness Scorecard

## Purpose
Assesses whether a founder has the core business files needed to effectively
use Claude Desktop / Claude Code for building their MicroSaaS product.

## Scoring
- 20 questions across 5 sections (4 questions each)
- Each question: 0-5 scale
  - 0 = Nothing exists
  - 1 = Vague idea in my head
  - 2 = Rough draft / scattered notes
  - 3 = Decent document that covers the basics
  - 4 = Polished, detailed, reviewed document
  - 5 = Battle-tested, updated based on real market feedback
- Section score: /20
- Total score: /100

## Sections
| Section | Name | Questions | Max |
|---------|------|-----------|-----|
| A | Brand Foundation Files | Q1-Q4 | 20 |
| B | Pricing & Offer Files | Q5-Q8 | 20 |
| C | ICP & Market Files | Q9-Q12 | 20 |
| D | Product & Tech Files | Q13-Q16 | 20 |
| E | GTM & Content Files | Q17-Q20 | 20 |

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
