# MAS — Market Attractiveness Scoring Configuration
# Version: 3.0
# FULL REWRITE: 20→6 user questions + upstream inheritance + AI synthesis
# Total Points: 100 (B:40 + C:40 + D-auto:20)
# Section A: Auto-loaded from SC1+SC2 (no user questions)

---

## ASSESSMENT METADATA

```yaml
id: market-attractiveness
name: Market Attractiveness Scoring
short_name: MAS
version: "3.0"
total_points: 100
user_questions_count: 6
auto_sections: 2  # A (upstream) and D (AI synthesis)
readiness_weight: 0.35
webhook_path: /webhook/eo-mas-score
```

---

## UPSTREAM INHERITANCE (NEW in v3.0)

```yaml
upstream:
  description: "SC3 inherits ~80% of its context from SC1 (Project Definition) and SC2 (ICP Clarity)"
  sources:
    SC1:
      - niche_definition
      - positioning_statement
      - geography
      - product_scope
    SC2:
      - pain_statements (top 5)
      - congregation_points
      - budget_range
      - buying_behavior
  storage_keys:
    SC1: "eo_project-files_answers"
    SC2: "eo_icp-clarity_answers"
  auto_load: "Section A displays upstream data for founder confirmation"
```

---

## ENGAGEMENT PROTOCOL (NEW in v3.0)

```yaml
engagement:
  pattern_breaks:
    - after: "Section A confirmation"
      type: "Insight Unlock"
      content: "AI insight on upstream data quality"
    - after: "Section B (Evidence Validation)"
      type: "Investment Signal"
      content: "Your evidence base is stronger than most Series A pitch decks."
    - after: "Section C (Market Sizing)"
      type: "Variable Reward"
      content: "Market sizing snapshot: TAM/SAM/SOM visual"
  acknowledgment_protocol:
    - "Between all scored questions in B and C"
    - "Strong answers: positive reinforcement"
    - "Weak answers: constructive push"
  elevation_instructions:
    - "Upgrade language: scrappy input → polished strategic prose"
    - "Add strategic context: implications not stated but logically implied"
    - "Flag contradictions: cross-section misalignments with ⚠️ warnings"
```

---

## SECTIONS

```yaml
sections:
  - id: A
    key: upstream_confirmation
    name: "Upstream Confirmation"
    subtitle: "Auto-loaded from SC1 + SC2"
    max_score: 0
    questions_count: 0
    type: auto
    notes: "Displays SC1/SC2 data for founder review. No user input required."

  - id: B
    key: evidence_validation
    name: "Evidence Validation"
    subtitle: "Do buyers actually pay for this?"
    max_score: 40
    questions_count: 3
    notes: "b1 (FT, 15pts), b2 (FT, 15pts), b3 (MC, 10pts)"

  - id: C
    key: market_sizing
    name: "Market Sizing & Growth"
    subtitle: "How big is this and where is it going?"
    max_score: 40
    questions_count: 3
    notes: "c1 (FT, 15pts), c2 (FT, 15pts), c3 (MC, 10pts)"

  - id: D
    key: ai_synthesis
    name: "AI Synthesis"
    subtitle: "AI-generated market verdict"
    max_score: 20
    questions_count: 0
    type: auto
    notes: "AI synthesizes all data (A+B+C) into market verdict. Scored automatically."
```

---

## QUESTIONS

### Section A: Upstream Confirmation (0 points — auto-loaded)

No user questions. System auto-loads from localStorage:
- `eo_project-files_answers`: niche, positioning, geography, product scope
- `eo_icp-clarity_answers`: pain statements, congregation points, budget range

Founder reviews and confirms. If data is missing, founder is directed to complete SC1/SC2 first.

### Section B: Evidence Validation (40 points)

```yaml
questions:
  - id: b1
    section: B
    type: free_text
    text: "What evidence do you have that real people experience this pain? (conversations, forums, reviews, support tickets)"
    maxScore: 15
    rubric_summary: "15=Multiple sources of direct evidence. 10=Some direct evidence. 5=Indirect evidence. 0=Assumption only."

  - id: b2
    section: B
    type: free_text
    text: "What evidence do you have that they're willing to PAY for a solution? (existing spend, price conversations, competitor revenue)"
    maxScore: 15
    rubric_summary: "15=Direct payment evidence. 10=Strong willingness signals. 5=Indirect signals. 0=No evidence."

  - id: b3
    section: B
    type: multiple_choice
    text: "How would you rate the strength of your evidence base overall?"
    maxScore: 10
    options:
      - label: "Direct buyer conversations + payment proof + competitor validation"
        score: 10
      - label: "Buyer conversations + some payment signals"
        score: 7
      - label: "Market research + forum/review mining"
        score: 4
      - label: "Assumptions + general industry knowledge"
        score: 1
```

### Section C: Market Sizing & Growth (40 points)

```yaml
questions:
  - id: c1
    section: C
    type: free_text
    text: "What is your TAM → SAM → SOM? Walk through the funnel with specific numbers."
    maxScore: 15
    rubric_summary: "15=All three tiers with credible numbers and sources. 10=Two tiers clear. 5=One tier only. 0=No sizing."

  - id: c2
    section: C
    type: free_text
    text: "What growth signals exist in your market? (new entrants, funding rounds, regulatory changes, search trends)"
    maxScore: 15
    rubric_summary: "15=Multiple growth signals with data. 10=Some signals identified. 5=Generic growth claim. 0=No signals."

  - id: c3
    section: C
    type: multiple_choice
    text: "How defensible is your position in this market?"
    maxScore: 10
    options:
      - label: "Arabic-first + domain expertise + data moat"
        score: 10
      - label: "Two defensibility factors (e.g., localization + expertise)"
        score: 7
      - label: "One defensibility factor (e.g., first-mover only)"
        score: 4
      - label: "No clear defensibility — anyone could replicate"
        score: 1
```

### Section D: AI Synthesis (20 points — auto-scored)

No user questions. AI synthesizes all upstream data (Section A) + user evidence (B+C) into a market verdict.

```yaml
ai_synthesis:
  inputs:
    - "SC1 niche and positioning data"
    - "SC2 ICP and pain data"
    - "Section B evidence validation answers"
    - "Section C market sizing answers"
  output: "Market verdict with confidence level"
  scoring:
    - "20 = High confidence: strong market with clear evidence"
    - "15 = Moderate confidence: viable market with some gaps"
    - "10 = Low confidence: market potential but weak evidence"
    - "5 = Very low confidence: significant concerns"
    - "0 = No confidence: evidence contradicts market viability"
```

---

## SCORING BANDS

```yaml
bands:
  - id: STRONG
    name: "Strong Market"
    min_score: 80
    max_score: 100
    color: "#22C55E"
    tag: "eo-mas-strong"
    action: "Scale aggressively. Your market is validated."

  - id: VIABLE
    name: "Viable Market"
    min_score: 60
    max_score: 79
    color: "#3B82F6"
    tag: "eo-mas-viable"
    action: "Good foundation. Strengthen evidence in weak areas."

  - id: WEAK
    name: "Weak Market"
    min_score: 40
    max_score: 59
    color: "#F59E0B"
    tag: "eo-mas-weak"
    action: "Significant gaps. Needs deeper validation."

  - id: RISK
    name: "High Risk"
    min_score: 0
    max_score: 39
    color: "#EF4444"
    tag: "eo-mas-risk"
    action: "Reconsider market or pivot approach."
```

---

## SCORING FORMULA

```yaml
scoring:
  section_scores:
    A: 0  # Auto-loaded, no score
    B: 40  # Evidence Validation (b1:15 + b2:15 + b3:10)
    C: 40  # Market Sizing (c1:15 + c2:15 + c3:10)
    D: 20  # AI Synthesis (auto-scored)
  total_score: "B + C + D = 100"
  band_assignment: "Match total_score to bands"
  readiness_contribution: "total_score * 0.35"
```
