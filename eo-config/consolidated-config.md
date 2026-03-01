# Consolidated Assessment Configuration
# Version: 1.0
# Combines MAS + ICP + GTM into Founder Readiness Score
# Uses strategy-selector/SKILL.md for AI analysis

---

## ASSESSMENT METADATA

```yaml
id: consolidated
name: Founder Readiness Assessment
short_name: Consolidated
version: "1.0"
requires:
  - market-attractiveness
  - icp-clarity
  - gtm-fitness
skill_file: "strategy-selector/SKILL.md"
webhook_path: /webhook/eo-consolidated
```

---

## READINESS FORMULA

```yaml
readiness:
  formula: "(mas_score * mas_weight) + (icp_score * icp_weight) + (gtm_score * gtm_weight)"
  weights:
    mas_weight: 0.35
    icp_weight: 0.35
    gtm_weight: 0.30
  max_score: 100
```

---

## READINESS BANDS

```yaml
bands:
  - id: LAUNCH_READY
    name: "Launch Ready"
    min_score: 80
    max_score: 100
    color: "#22C55E"
    tag: "eo-readiness-strong"
    action: "Full speed ahead. Execute primary GTM motions. Scale."
    description: "All three pillars are strong. Market validated, ICP crystal clear, GTM channels ready."

  - id: ALMOST_THERE
    name: "Almost There"
    min_score: 60
    max_score: 79
    color: "#3B82F6"
    tag: "eo-readiness-viable"
    action: "Fix the bottleneck pillar. Then scale."
    description: "Strong foundation but one pillar is holding you back. Focus there for 30 days."

  - id: NEEDS_WORK
    name: "Needs Work"
    min_score: 40
    max_score: 59
    color: "#F59E0B"
    tag: "eo-readiness-weak"
    action: "Significant gaps. Fix lowest 2 pillars before scaling."
    description: "Multiple areas need attention. Don't scale yet — validate and strengthen first."

  - id: EARLY_STAGE
    name: "Early Stage"
    min_score: 20
    max_score: 39
    color: "#EF4444"
    tag: "eo-readiness-risk"
    action: "Fundamental gaps. Focus on buyer research and market validation."
    description: "Core assumptions need testing. Invest in discovery, not distribution."

  - id: RESET
    name: "Reset Required"
    min_score: 0
    max_score: 19
    color: "#991B1B"
    tag: "eo-readiness-risk"
    action: "Start over with customer discovery. Talk to 10+ buyers before building."
    description: "All pillars are critically weak. Return to fundamentals."
```

---

## BOTTLENECK ANALYSIS

```yaml
bottleneck:
  # Bottleneck = pillar with lowest score
  calculation: "min(mas_score, icp_score, gtm_score)"

  # Which pillar is the bottleneck
  rules:
    - condition: "mas_score is lowest"
      bottleneck: "market"
      tag: "eo-bottleneck-market"
      action: "Market attractiveness is your weakest link. Focus on validating pain + purchasing power."

    - condition: "icp_score is lowest"
      bottleneck: "icp"
      tag: "eo-bottleneck-icp"
      action: "ICP clarity is your weakest link. You can't sell to a customer you can't describe."

    - condition: "gtm_score is lowest"
      bottleneck: "gtm"
      tag: "eo-bottleneck-gtm"
      action: "GTM fitness is your weakest link. You have the market and the customer — now build distribution."
```

---

## SCORE PATTERN ARCHETYPES

From strategy-selector/SKILL.md — 8 patterns based on score combinations:

```yaml
archetypes:
  - id: launcher
    name: "The Launcher"
    condition: "MAS >= 70 AND ICP >= 70 AND GTM >= 70"
    description: "All systems go. Market is real, ICP is clear, distribution is ready."
    action: "Execute immediately. Your bottleneck is speed, not strategy."

  - id: market_hunter
    name: "The Market Hunter"
    condition: "MAS >= 70 AND ICP < 60 AND GTM < 60"
    description: "You found a hot market but can't describe your buyer or reach them."
    action: "Lock ICP first. Then build GTM channels to that specific buyer."

  - id: channel_seeker
    name: "The Channel Seeker"
    condition: "MAS >= 70 AND ICP >= 70 AND GTM < 60"
    description: "Market and buyer are clear. You just can't reach them yet."
    action: "Focus 100% on GTM. You have permission to sell — now build the pipes."

  - id: solution_seeker
    name: "The Solution Seeker"
    condition: "MAS < 60 AND ICP >= 70 AND GTM >= 70"
    description: "You know who to sell to and how to reach them, but the market pull is weak."
    action: "Validate pain deeper. Are they paying for alternatives? What's the urgency trigger?"

  - id: expert_without_stage
    name: "Expert Without Stage"
    condition: "MAS < 60 AND ICP >= 70 AND GTM < 60"
    description: "You know your buyer intimately but have no market pull or distribution."
    action: "Test market demand with your existing network. If demand exists, build GTM."

  - id: ghost
    name: "The Ghost"
    condition: "MAS >= 70 AND ICP < 60 AND GTM >= 60"
    description: "You have market and channels but talking to the wrong person."
    action: "Sharpen ICP. Your marketing is reaching people — but not the right people."

  - id: operator
    name: "The Operator"
    condition: "MAS < 60 AND ICP < 60 AND GTM >= 70"
    description: "Strong execution capability but no market or customer clarity."
    action: "Stop executing. Start discovering. Talk to 20 potential buyers before building."

  - id: scrambler
    name: "The Scrambler"
    condition: "MAS < 60 AND ICP < 60 AND GTM < 60"
    description: "Everything needs work. This is a reset moment."
    action: "Pick ONE customer who loves you. Study them. Build everything from that single insight."
```

---

## DEMAND-FIRST MATRIX

```yaml
matrix:
  x_axis:
    name: "Execution Readiness"
    calculation: "(icp_score + gtm_score) / 2"
    threshold: 60

  y_axis:
    name: "Market Pull"
    calculation: "mas_score"
    threshold: 60

  quadrants:
    - id: SCALE
      position: "high_y_high_x"
      name: "SCALE"
      description: "Strong market pull + strong execution. Go fast."
      action: "Double down. Scale what works. Add team."

    - id: VALIDATE
      position: "high_y_low_x"
      name: "VALIDATE"
      description: "Market wants it, but you can't execute yet."
      action: "Fix ICP and GTM. Market is waiting."

    - id: OPTIMIZE
      position: "low_y_high_x"
      name: "OPTIMIZE"
      description: "You can execute, but market pull is weak."
      action: "Validate demand. Pivot offer if needed."

    - id: BUILD
      position: "low_y_low_x"
      name: "BUILD"
      description: "Both market pull and execution are weak."
      action: "Go back to customer discovery. Don't scale."
```

---

## COMPOUND INTERACTION EFFECTS

When multiple pillars are weak, they compound each other:

```yaml
compound_effects:
  - condition: "MAS < 50 AND ICP < 50"
    effect: "No market pull + no buyer clarity = burning money on marketing"
    priority: "Stop all marketing. Return to buyer research."

  - condition: "ICP < 50 AND GTM < 50"
    effect: "No buyer clarity + no channels = can't reach anyone effectively"
    priority: "Fix ICP first. Then GTM naturally follows."

  - condition: "MAS < 50 AND GTM < 50"
    effect: "Weak market + no channels = execution without direction"
    priority: "Validate market first. Channels are useless without demand."

  - condition: "ALL < 50"
    effect: "Triple failure — nothing works at scale"
    priority: "Full reset. Pick ONE customer. Build from there."
```

---

## SECTION-LEVEL BOTTLENECK FORMULA

For deep analysis, identify the weakest SECTION across all assessments:

```yaml
section_bottleneck:
  formula: "Section Impact = (Section Max / Assessment Max) * Assessment Weight * (1 - Section Score / Section Max)"

  # Higher impact = bigger bottleneck
  # Example: MAS Pain Reality scores 8/25
  # Impact = (25/100) * 0.35 * (1 - 8/25) = 0.25 * 0.35 * 0.68 = 0.0595

  # Sort all sections by impact descending
  # Top 3 = priority bottlenecks
```

---

## GHL TAGS (Complete List)

```yaml
tags:
  # Completion
  strategy_assessed: "eo-strategy-assessed"
  mas_assessed: "eo-mas-assessed"
  icp_assessed: "eo-icp-assessed"
  gtm_assessed: "eo-gtm-assessed"
  full_assessed: "eo-full-assessed"

  # Strategy Paths
  path_replicate: "eo-path-replicate"
  path_consulting: "eo-path-consulting"
  path_boring: "eo-path-boring"
  path_hammering: "eo-path-hammering"

  # MAS Bands
  mas_strong: "eo-mas-strong"
  mas_viable: "eo-mas-viable"
  mas_weak: "eo-mas-weak"
  mas_risk: "eo-mas-risk"

  # ICP Bands
  icp_clear: "eo-icp-clear"
  icp_decent: "eo-icp-decent"
  icp_fuzzy: "eo-icp-fuzzy"
  icp_none: "eo-icp-none"

  # GTM Bands
  gtm_elite: "eo-gtm-elite"
  gtm_strong: "eo-gtm-strong"
  gtm_emerging: "eo-gtm-emerging"
  gtm_weak: "eo-gtm-weak"

  # Readiness Bands
  readiness_strong: "eo-readiness-strong"
  readiness_viable: "eo-readiness-viable"
  readiness_weak: "eo-readiness-weak"
  readiness_risk: "eo-readiness-risk"

  # Bottleneck
  bottleneck_market: "eo-bottleneck-market"
  bottleneck_icp: "eo-bottleneck-icp"
  bottleneck_gtm: "eo-bottleneck-gtm"
```

---

## GHL CUSTOM FIELDS

```yaml
custom_fields:
  - key: eo_strategy_path
    type: TEXT
    description: "Primary strategy path result (replicate/consulting/boring/hammering)"

  - key: eo_strategy_path_score
    type: NUMBER
    description: "Strategy path fit percentage"

  - key: eo_mas_score
    type: NUMBER
    description: "MAS total score (0-100)"

  - key: eo_mas_band
    type: TEXT
    description: "MAS band (STRONG/VIABLE/WEAK/RISK)"

  - key: eo_icp_score
    type: NUMBER
    description: "ICP total score (0-100)"

  - key: eo_icp_band
    type: TEXT
    description: "ICP band (CRYSTAL_CLEAR/GOOD_FOUNDATION/FUZZY/NO_CLARITY/CRITICAL)"

  - key: eo_gtm_score
    type: NUMBER
    description: "GTM total score (0-100)"

  - key: eo_gtm_band
    type: TEXT
    description: "GTM band (ELITE/STRONG/EMERGING/WEAK)"

  - key: eo_readiness_score
    type: NUMBER
    description: "Founder Readiness Score (0-100)"

  - key: eo_readiness_band
    type: TEXT
    description: "Readiness band (LAUNCH_READY/ALMOST_THERE/NEEDS_WORK/EARLY_STAGE/RESET)"

  - key: eo_assessment_date
    type: TEXT
    description: "Last assessment date (ISO format)"

  - key: eo_bottleneck
    type: TEXT
    description: "Lowest scoring pillar (market/icp/gtm)"

  - key: eo_matrix_position
    type: TEXT
    description: "Demand-First Matrix quadrant (SCALE/VALIDATE/OPTIMIZE/BUILD)"
```
