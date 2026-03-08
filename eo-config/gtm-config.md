# GTM — Fitness Scoring Configuration
# Version: 2.1
# 14 questions (7 business profile + 7 capability profile)
# 13 motions scored on Fit x Readiness x MENA Viability
# Composite = Fit*0.4 + Readiness*0.3 + MENA*0.3
# v2.1 Changes: Light engagement polish (pattern breaks after B, C, D; acknowledgments)

---

## ASSESSMENT METADATA

```yaml
id: gtm-fitness
name: GTM Fitness Scoring
short_name: GTM
version: "2.1"
total_points: 100
questions_count: 14
motions_count: 13
readiness_weight: 0.30
webhook_path: /webhook/eo-gtm-score
```

---

## ENGAGEMENT PROTOCOL (NEW in v2.1)

```yaml
engagement:
  pattern_breaks:
    - after: "Section B (Capability Profile)"
      type: "Insight Unlock"
      content: "Capability Profile Complete — shows strength summary"
    - after: "Section C (Motion Deep Dive)"
      type: "Variable Reward"
      content: "Shows top 5 motions with tier labels (PRIMARY/SECONDARY/etc.)"
    - after: "Section D (MENA Context)"
      type: "Pattern Break"
      content: "MENA Context Locked In — shows MENA viability adjustment"
  acknowledgment_protocol:
    - "Between all questions"
    - "Section-specific feedback based on fit/readiness scores"
  investment_signaling:
    - at: "results_screen"
      content: "Completion card showing time invested and strategy value"
```

---

## MOTIONS

```yaml
motions:
  - id: waitlist
    index: 0
    name: "Waitlist Heat-to-Webinar Close"
    short_name: "Waitlist"
    mena_base_viability: 3

  - id: build_in_public
    index: 1
    name: "Build-in-Public Trust Flywheel"
    short_name: "Build-in-Public"
    mena_base_viability: 2

  - id: authority_education
    index: 2
    name: "Authority Education Engine"
    short_name: "Authority Education"
    mena_base_viability: 5

  - id: wave_riding
    index: 3
    name: "Wave Riding Distribution"
    short_name: "Wave Riding"
    mena_base_viability: 2

  - id: ltd_cash
    index: 4
    name: "LTD Cash-to-MRR Ladder"
    short_name: "LTD Cash"
    mena_base_viability: 2

  - id: signal_sniper
    index: 5
    name: "Signal Sniper Outbound"
    short_name: "Signal Sniper"
    mena_base_viability: 4

  - id: outcome_demo
    index: 6
    name: "Outcome Demo First"
    short_name: "Outcome Demo"
    mena_base_viability: 5

  - id: hammering_launches
    index: 7
    name: "Hammering-Feature-First Launches"
    short_name: "Hammering Launches"
    mena_base_viability: 3

  - id: bofu_seo
    index: 8
    name: "MicroSaaS BOFU SEO Strike"
    short_name: "BOFU SEO"
    mena_base_viability: 4

  - id: dream100
    index: 9
    name: "Dream 100 Strategy"
    short_name: "Dream 100"
    mena_base_viability: 5

  - id: seven_four_eleven
    index: 10
    name: "7x4x11 Strategy"
    short_name: "7x4x11"
    mena_base_viability: 4

  - id: value_trust
    index: 11
    name: "Value Trust Engine"
    short_name: "Value Trust"
    mena_base_viability: 5

  - id: paid_vsl
    index: 12
    name: "Paid VSL Value Ladder"
    short_name: "Paid VSL"
    mena_base_viability: 4
```

---

## QUESTIONS

### Phase 1: Business Profile (7 Questions — determines FIT)

```yaml
phase1_questions:
  - id: bp1
    phase: 1
    text: "What is your product's annual contract value (ACV) or price point?"
    fit_mapping: "ACV determines transactional vs relationship motions"
    options:
      - label: "Under $500/year"
        desc: "Micro-SaaS pricing. Volume play."
        fit_impact:
          high: [waitlist, build_in_public, wave_riding, ltd_cash, outcome_demo, hammering_launches]
          medium: [authority_education, bofu_seo, paid_vsl]
          low: [dream100, seven_four_eleven, value_trust, signal_sniper]
      - label: "$500 - $5,000/year"
        desc: "SMB SaaS. Hybrid motions work."
        fit_impact:
          high: [authority_education, signal_sniper, bofu_seo, outcome_demo, paid_vsl]
          medium: [waitlist, build_in_public, hammering_launches, dream100]
          low: [ltd_cash, wave_riding, seven_four_eleven, value_trust]
      - label: "$5,000 - $50,000/year"
        desc: "Mid-market. Relationship motions."
        fit_impact:
          high: [dream100, seven_four_eleven, signal_sniper, value_trust]
          medium: [authority_education, outcome_demo]
          low: [waitlist, build_in_public, wave_riding, ltd_cash, hammering_launches, bofu_seo, paid_vsl]
      - label: "Over $50,000/year"
        desc: "Enterprise. Long-cycle motions."
        fit_impact:
          high: [dream100, seven_four_eleven, value_trust]
          medium: [signal_sniper, authority_education]
          low: [waitlist, build_in_public, wave_riding, ltd_cash, outcome_demo, hammering_launches, bofu_seo, paid_vsl]

  - id: bp2
    phase: 1
    text: "Is your buyer a searcher or a scroller?"
    fit_mapping: "Determines inbound vs outbound motions"
    options:
      - label: "Searcher — has a specific problem, actively looking"
        desc: "High intent. SEO and signal-based motions."
        fit_impact:
          high: [bofu_seo, signal_sniper, outcome_demo]
          medium: [authority_education, dream100, seven_four_eleven]
          low: [waitlist, build_in_public, wave_riding, ltd_cash, hammering_launches, value_trust, paid_vsl]
      - label: "Scroller — discovering problems, open to solutions"
        desc: "Awareness play. Content and attention motions."
        fit_impact:
          high: [waitlist, build_in_public, wave_riding, paid_vsl]
          medium: [authority_education, outcome_demo, hammering_launches]
          low: [bofu_seo, signal_sniper, dream100, seven_four_eleven, ltd_cash, value_trust]
      - label: "Both — some search, some discover"
        desc: "Hybrid. Multiple motions can work."
        fit_impact:
          high: [authority_education, outcome_demo]
          medium: [bofu_seo, signal_sniper, waitlist, build_in_public, paid_vsl, dream100]
          low: [wave_riding, ltd_cash, hammering_launches, seven_four_eleven, value_trust]
      - label: "Not sure yet"
        desc: "Need more buyer research."
        fit_impact:
          high: []
          medium: [authority_education, outcome_demo, build_in_public]
          low: [waitlist, wave_riding, ltd_cash, signal_sniper, hammering_launches, bofu_seo, dream100, seven_four_eleven, value_trust, paid_vsl]

  - id: bp3
    phase: 1
    text: "What is your typical sales cycle?"
    fit_mapping: "Maps to fast vs long-cycle motions"
    options:
      - label: "Under 7 days — fast impulse"
        fit_impact:
          high: [waitlist, wave_riding, outcome_demo, ltd_cash, paid_vsl]
          medium: [hammering_launches, build_in_public]
          low: [authority_education, signal_sniper, bofu_seo, dream100, seven_four_eleven, value_trust]
      - label: "7-30 days — moderate consideration"
        fit_impact:
          high: [authority_education, signal_sniper, hammering_launches]
          medium: [waitlist, outcome_demo, bofu_seo, paid_vsl, build_in_public]
          low: [wave_riding, ltd_cash, dream100, seven_four_eleven, value_trust]
      - label: "30-90 days — consultative"
        fit_impact:
          high: [dream100, seven_four_eleven, bofu_seo]
          medium: [signal_sniper, authority_education, value_trust]
          low: [waitlist, build_in_public, wave_riding, ltd_cash, outcome_demo, hammering_launches, paid_vsl]
      - label: "90+ days — enterprise"
        fit_impact:
          high: [dream100, seven_four_eleven, value_trust]
          medium: [signal_sniper]
          low: [waitlist, build_in_public, wave_riding, ltd_cash, outcome_demo, hammering_launches, bofu_seo, authority_education, paid_vsl]

  - id: bp4
    phase: 1
    text: "Does your product have a visual before/after?"
    fit_mapping: "Demo-first vs education-first motions"
    options:
      - label: "Yes — dramatic visual transformation"
        fit_impact:
          high: [outcome_demo, wave_riding, paid_vsl]
          medium: [waitlist, hammering_launches, build_in_public]
          low: [authority_education, signal_sniper, bofu_seo, dream100, seven_four_eleven, value_trust, ltd_cash]
      - label: "Somewhat — takes explanation"
        fit_impact:
          high: [authority_education, outcome_demo]
          medium: [waitlist, bofu_seo, paid_vsl, hammering_launches]
          low: [build_in_public, wave_riding, ltd_cash, signal_sniper, dream100, seven_four_eleven, value_trust]
      - label: "No — value is in data/process, not visual"
        fit_impact:
          high: [authority_education, bofu_seo, build_in_public]
          medium: [signal_sniper, dream100, seven_four_eleven, value_trust]
          low: [waitlist, wave_riding, ltd_cash, outcome_demo, hammering_launches, paid_vsl]

  - id: bp5
    phase: 1
    text: "Are you selling to individuals or committees?"
    fit_mapping: "Individual = all transactional; Committee = relationship motions"
    options:
      - label: "Individual decision maker"
        fit_impact:
          high: [waitlist, build_in_public, wave_riding, ltd_cash, outcome_demo, hammering_launches, bofu_seo, paid_vsl, authority_education]
          medium: [signal_sniper, dream100]
          low: [seven_four_eleven, value_trust]
      - label: "Small team (2-3 approvers)"
        fit_impact:
          high: [authority_education, signal_sniper, outcome_demo, dream100]
          medium: [waitlist, bofu_seo, hammering_launches, seven_four_eleven, paid_vsl]
          low: [build_in_public, wave_riding, ltd_cash, value_trust]
      - label: "Committee (4+ stakeholders)"
        fit_impact:
          high: [dream100, seven_four_eleven, signal_sniper]
          medium: [authority_education, value_trust]
          low: [waitlist, build_in_public, wave_riding, ltd_cash, outcome_demo, hammering_launches, bofu_seo, paid_vsl]

  - id: bp6
    phase: 1
    text: "What's your founder background?"
    fit_mapping: "Technical = build-first motions; Sales = relationship motions"
    options:
      - label: "Technical (developer, engineer)"
        fit_impact:
          high: [build_in_public, hammering_launches, wave_riding, bofu_seo]
          medium: [waitlist, ltd_cash, outcome_demo, authority_education]
          low: [signal_sniper, dream100, seven_four_eleven, value_trust, paid_vsl]
      - label: "Sales / Business Development"
        fit_impact:
          high: [dream100, seven_four_eleven, signal_sniper, paid_vsl]
          medium: [authority_education, outcome_demo, value_trust, waitlist]
          low: [build_in_public, hammering_launches, wave_riding, ltd_cash, bofu_seo]
      - label: "Marketing / Content"
        fit_impact:
          high: [authority_education, build_in_public, bofu_seo, paid_vsl]
          medium: [waitlist, wave_riding, outcome_demo, value_trust]
          low: [signal_sniper, dream100, seven_four_eleven, ltd_cash, hammering_launches]
      - label: "Domain expert (industry veteran)"
        fit_impact:
          high: [authority_education, value_trust, dream100]
          medium: [signal_sniper, seven_four_eleven, outcome_demo]
          low: [waitlist, build_in_public, wave_riding, ltd_cash, hammering_launches, bofu_seo, paid_vsl]

  - id: bp7
    phase: 1
    text: "Is your primary market MENA?"
    fit_mapping: "Adjusts MENA viability weighting"
    options:
      - label: "Yes — MENA first"
        mena_multiplier: 1.0
      - label: "MENA is one of several markets"
        mena_multiplier: 0.7
      - label: "Global first, MENA later"
        mena_multiplier: 0.4
      - label: "No — Western markets only"
        mena_multiplier: 0.1
```

### Phase 2: Capability Profile (7 Questions — determines READINESS)

```yaml
phase2_questions:
  - id: cp1
    phase: 2
    text: "Do you have any existing content? (blog, videos, courses)"
    readiness_mapping: "Content library → Authority, Build-in-Public, Value Trust"
    options:
      - label: "20+ pieces of content"
        readiness_impact:
          authority_education: 5
          build_in_public: 5
          value_trust: 5
          bofu_seo: 4
          default: 3
      - label: "10-19 pieces"
        readiness_impact:
          authority_education: 4
          build_in_public: 4
          value_trust: 4
          bofu_seo: 3
          default: 3
      - label: "3-9 pieces"
        readiness_impact:
          authority_education: 3
          build_in_public: 3
          value_trust: 3
          bofu_seo: 2
          default: 2
      - label: "None or 1-2 pieces"
        readiness_impact:
          authority_education: 1
          build_in_public: 1
          value_trust: 1
          bofu_seo: 1
          default: 2

  - id: cp2
    phase: 2
    text: "Do you have an email list or social following?"
    readiness_mapping: "Audience → Waitlist, Authority, Build-in-Public"
    options:
      - label: "5K+ engaged subscribers/followers"
        readiness_impact:
          waitlist: 5
          authority_education: 5
          build_in_public: 5
          paid_vsl: 4
          default: 3
      - label: "1K-5K subscribers/followers"
        readiness_impact:
          waitlist: 4
          authority_education: 4
          build_in_public: 4
          paid_vsl: 3
          default: 3
      - label: "100-1K subscribers/followers"
        readiness_impact:
          waitlist: 3
          authority_education: 3
          build_in_public: 3
          default: 2
      - label: "Under 100 or none"
        readiness_impact:
          waitlist: 1
          authority_education: 1
          build_in_public: 1
          default: 2

  - id: cp3
    phase: 2
    text: "Do you have outbound infrastructure? (CRM, lists, tools)"
    readiness_mapping: "Outbound tools → Signal Sniper, Dream 100, 7x4x11"
    options:
      - label: "CRM + email tool + signal tools (HeyReach/Clay)"
        readiness_impact:
          signal_sniper: 5
          dream100: 5
          seven_four_eleven: 5
          default: 3
      - label: "CRM + email tool"
        readiness_impact:
          signal_sniper: 4
          dream100: 4
          seven_four_eleven: 4
          default: 3
      - label: "Email tool only"
        readiness_impact:
          signal_sniper: 3
          dream100: 3
          seven_four_eleven: 3
          default: 2
      - label: "No system — manual outreach"
        readiness_impact:
          signal_sniper: 1
          dream100: 2
          seven_four_eleven: 1
          default: 2

  - id: cp4
    phase: 2
    text: "What's your advertising budget (monthly)?"
    readiness_mapping: "Ad budget → Paid VSL, Wave Riding, Waitlist"
    options:
      - label: "$5K+ available"
        readiness_impact:
          paid_vsl: 5
          wave_riding: 4
          waitlist: 4
          default: 3
      - label: "$2-5K available"
        readiness_impact:
          paid_vsl: 4
          wave_riding: 3
          waitlist: 3
          default: 3
      - label: "$500-2K available"
        readiness_impact:
          paid_vsl: 3
          wave_riding: 2
          waitlist: 2
          default: 2
      - label: "$0 — organic only"
        readiness_impact:
          paid_vsl: 1
          wave_riding: 1
          waitlist: 1
          default: 2

  - id: cp5
    phase: 2
    text: "Do you have a network of 20+ industry contacts?"
    readiness_mapping: "Network → Dream 100, Value Trust Engine"
    options:
      - label: "50+ warm contacts"
        readiness_impact:
          dream100: 5
          value_trust: 5
          seven_four_eleven: 4
          default: 3
      - label: "20-49 contacts"
        readiness_impact:
          dream100: 4
          value_trust: 4
          seven_four_eleven: 3
          default: 3
      - label: "10-19 contacts"
        readiness_impact:
          dream100: 3
          value_trust: 3
          seven_four_eleven: 2
          default: 2
      - label: "Under 10 contacts"
        readiness_impact:
          dream100: 1
          value_trust: 2
          seven_four_eleven: 1
          default: 2

  - id: cp6
    phase: 2
    text: "Do you have customer case studies or testimonials?"
    readiness_mapping: "Proof → Authority, Outcome Demo, Value Trust"
    options:
      - label: "5+ case studies or testimonials"
        readiness_impact:
          authority_education: 5
          outcome_demo: 5
          value_trust: 5
          default: 4
      - label: "3-4 case studies/testimonials"
        readiness_impact:
          authority_education: 4
          outcome_demo: 4
          value_trust: 4
          default: 3
      - label: "1-2 case studies/testimonials"
        readiness_impact:
          authority_education: 3
          outcome_demo: 3
          value_trust: 3
          default: 2
      - label: "None — no case studies but have demo"
        readiness_impact:
          authority_education: 1
          outcome_demo: 2
          value_trust: 1
          default: 2

  - id: cp7
    phase: 2
    text: "What's your #1 constraint right now?"
    readiness_mapping: "Constraint affects motion feasibility"
    options:
      - label: "Time — too busy to execute"
        readiness_impact:
          build_in_public: 2
          bofu_seo: 2
          authority_education: 2
          default: 2
      - label: "Money — limited budget"
        readiness_impact:
          paid_vsl: 1
          value_trust: 1
          wave_riding: 2
          default: 3
      - label: "Skill — need to learn GTM"
        readiness_impact:
          signal_sniper: 1
          seven_four_eleven: 1
          dream100: 2
          default: 2
      - label: "Team — need help to execute"
        readiness_impact:
          hammering_launches: 2
          value_trust: 1
          seven_four_eleven: 2
          default: 3
```

---

## SCORING FORMULAS

```yaml
scoring:
  # Per-motion composite score
  composite_formula: "(fit * 0.4) + (readiness * 0.3) + (mena_viability * 0.3)"

  # Fit score: Derived from Phase 1 answers (0-5 per motion)
  # high_impact = 5, medium_impact = 3, low_impact = 1
  fit_calculation: "Average of all Phase 1 fit impacts for each motion"

  # Readiness score: Derived from Phase 2 answers (0-5 per motion)
  readiness_calculation: "Average of all Phase 2 readiness impacts for each motion"

  # MENA Viability: Base score from config, adjusted by bp7 mena_multiplier
  mena_calculation: "mena_base_viability * mena_multiplier"

  # Overall GTM Fitness Score
  overall_formula: "(Average of all 13 composite scores) * 20"
  overall_max: 100
```

---

## MOTION TIERS

```yaml
tiers:
  - id: PRIMARY
    name: "Primary"
    min_composite: 4.0
    max_composite: 5.0
    color: "#22C55E"
    action: "Activate immediately. This is your growth engine."
    timeline: "Next 30 days"

  - id: SECONDARY
    name: "Secondary"
    min_composite: 3.0
    max_composite: 3.9
    color: "#3B82F6"
    action: "Build capacity. Activate after primary generates leads."
    timeline: "60-90 days"

  - id: CONDITIONAL
    name: "Conditional"
    min_composite: 2.0
    max_composite: 2.9
    color: "#F59E0B"
    action: "Only if resources allow after primary motions running."
    timeline: "As secondary flows"

  - id: SKIP
    name: "Skip"
    min_composite: 0.0
    max_composite: 1.9
    color: "#EF4444"
    action: "Do not invest energy here now."
    timeline: "N/A"
```

---

## OVERALL BANDS

```yaml
bands:
  - id: ELITE
    name: "Elite GTM Fitness"
    min_score: 80
    max_score: 100
    color: "#22C55E"
    tag: "eo-gtm-elite"
    action: "Multiple strong channels. Scale aggressively."

  - id: STRONG
    name: "Strong Foundation"
    min_score: 60
    max_score: 79
    color: "#3B82F6"
    tag: "eo-gtm-strong"
    action: "2-3 primary motions clear. Focus and execute."

  - id: EMERGING
    name: "Emerging GTM"
    min_score: 40
    max_score: 59
    color: "#F59E0B"
    tag: "eo-gtm-emerging"
    action: "Some motions available but need development."

  - id: WEAK
    name: "Weak GTM"
    min_score: 0
    max_score: 39
    color: "#EF4444"
    tag: "eo-gtm-weak"
    action: "Limited distribution options. Focus on ONE motion."
```
