# MAS — Market Attractiveness Scoring Configuration
# Version: 1.0
# Total Points: 100 (4 sections x 25 points)
# Each question: 0-5 scale

---

## ASSESSMENT METADATA

```yaml
id: market-attractiveness
name: Market Attractiveness Scoring
short_name: MAS
version: "1.0"
total_points: 100
questions_count: 20
readiness_weight: 0.35
webhook_path: /webhook/eo-mas-score
```

---

## SECTIONS

```yaml
sections:
  - id: A
    key: pain_reality
    name: "Pain Reality"
    subtitle: "Understanding Your Buyer's Problem"
    max_score: 25
    questions_count: 5

  - id: B
    key: purchasing_power
    name: "Purchasing Power"
    subtitle: "Can They Actually Buy?"
    max_score: 25
    questions_count: 5

  - id: C
    key: market_momentum
    name: "Market Momentum"
    subtitle: "Is Your Market Growing?"
    max_score: 25
    questions_count: 5

  - id: D
    key: competitive_advantage
    name: "Competitive Advantage"
    subtitle: "Why Should Buyers Choose You?"
    max_score: 25
    questions_count: 5
```

---

## QUESTIONS

### Section A: Pain Reality (25 points)

```yaml
questions:
  - id: a1
    section: A
    text: "Can you describe the exact moment your buyer feels this pain?"
    options:
      - label: "Yes — I can describe the specific moment, time, and trigger"
        score: 5
      - label: "I know the general pain but not the exact moment"
        score: 3
      - label: "I think they have this pain based on my research"
        score: 1
      - label: "I'm not sure how they experience it"
        score: 0

  - id: a2
    section: A
    text: "How often does your buyer experience this pain?"
    options:
      - label: "Daily — it disrupts their workflow every day"
        score: 5
      - label: "Weekly — it's a recurring frustration"
        score: 4
      - label: "Monthly — it surfaces periodically"
        score: 3
      - label: "Quarterly or less — it's occasional"
        score: 1

  - id: a3
    section: A
    text: "Can your buyer put a dollar/AED amount on this pain?"
    options:
      - label: "Yes — they can quote the exact cost"
        score: 5
      - label: "They can estimate the cost range"
        score: 3
      - label: "They acknowledge it costs money but can't quantify"
        score: 1
      - label: "No — they haven't connected it to money"
        score: 0

  - id: a4
    section: A
    text: "What are they currently doing to solve this problem?"
    options:
      - label: "Paying for an inferior solution they hate"
        score: 5
      - label: "Using a painful manual process"
        score: 4
      - label: "Using free tools or spreadsheets"
        score: 2
      - label: "Nothing — they've accepted the pain"
        score: 0

  - id: a5
    section: A
    text: "If you solved this tomorrow, how fast would they buy?"
    options:
      - label: "Same day — they'd sign immediately"
        score: 5
      - label: "Within a week — minimal decision process"
        score: 4
      - label: "Within a month — some evaluation needed"
        score: 3
      - label: "Eventually — no urgency to switch"
        score: 1
```

### Section B: Purchasing Power (25 points)

```yaml
questions:
  - id: b1
    section: B
    text: "Does your buyer control the purchase budget?"
    options:
      - label: "Sole decision maker — signs and pays"
        score: 5
      - label: "Needs one approval above them"
        score: 4
      - label: "Committee decision — multiple approvers"
        score: 2
      - label: "No budget authority — needs to request"
        score: 0

  - id: b2
    section: B
    text: "How does your price compare to the pain cost?"
    options:
      - label: "10x+ ROI — price is a no-brainer"
        score: 5
      - label: "5x ROI — clearly worth it"
        score: 4
      - label: "2-3x ROI — reasonable but needs justification"
        score: 3
      - label: "Break-even or unclear ROI"
        score: 1

  - id: b3
    section: B
    text: "Can your buyer actually pay you easily?"
    options:
      - label: "Credit card or instant payment — frictionless"
        score: 5
      - label: "Bank transfer — some process but doable"
        score: 4
      - label: "Invoice/PO required — procurement process"
        score: 3
      - label: "Significant payment friction (cash market, no digital)"
        score: 1

  - id: b4
    section: B
    text: "Are they already paying for solutions in this category?"
    options:
      - label: "Yes — spending $1,000+/month on similar tools"
        score: 5
      - label: "Yes — spending $100-1,000/month"
        score: 4
      - label: "Yes — but under $100/month"
        score: 3
      - label: "Only using free tools"
        score: 1

  - id: b5
    section: B
    text: "Have buyers expressed willingness to pay?"
    options:
      - label: "Sent deposit, PO, or signed LOI"
        score: 5
      - label: "Verbal commitment with specific budget"
        score: 4
      - label: "Said 'sounds interesting, send pricing'"
        score: 2
      - label: "No buying signal yet"
        score: 0
```

### Section C: Market Momentum (25 points)

```yaml
questions:
  - id: c1
    section: C
    text: "What direction is your target market heading?"
    options:
      - label: "Explosive growth — 30%+ YoY expansion"
        score: 5
      - label: "Strong growth — 15-30% YoY"
        score: 4
      - label: "Stable — maintaining current size"
        score: 3
      - label: "Plateauing or declining"
        score: 1

  - id: c2
    section: C
    text: "Are there macro forces pushing this market?"
    options:
      - label: "Regulation mandating adoption"
        score: 5
      - label: "Technology shift creating new demand (AI, automation)"
        score: 4
      - label: "Cultural or behavioral trend supporting it"
        score: 3
      - label: "No specific external forces"
        score: 1

  - id: c3
    section: C
    text: "What's the investment activity in your space?"
    options:
      - label: "Multiple competitors raised $10M+ rounds"
        score: 5
      - label: "Series A/B activity in the space"
        score: 4
      - label: "Seed-stage activity"
        score: 3
      - label: "No funding activity — all bootstrapped"
        score: 1

  - id: c4
    section: C
    text: "Are people actively searching for your type of solution?"
    options:
      - label: "Google Trends up 50%+ in 12 months"
        score: 5
      - label: "Growing search volume steadily"
        score: 4
      - label: "Stable search volume"
        score: 3
      - label: "Low or declining search interest"
        score: 1

  - id: c5
    section: C
    text: "Is the MENA market specifically ready for this?"
    options:
      - label: "Confirmed Arabic SaaS gap — no local solution exists"
        score: 5
      - label: "Regional regulation creating specific demand"
        score: 4
      - label: "Growing SME digitization wave supports it"
        score: 3
      - label: "MENA market is still cash-heavy / resistant"
        score: 1
```

### Section D: Competitive Advantage (25 points)

```yaml
questions:
  - id: d1
    section: D
    text: "Can you explain why you're different in one sentence?"
    options:
      - label: "Crystal clear — tested and validated with buyers"
        score: 5
      - label: "Clear to me but not yet tested"
        score: 3
      - label: "Still working on positioning"
        score: 1
      - label: "Not differentiated yet"
        score: 0

  - id: d2
    section: D
    text: "Can you reach 1,000 target prospects in 30 days?"
    options:
      - label: "Yes — have the list AND the channel"
        score: 5
      - label: "Have the channel, building the list"
        score: 4
      - label: "Know which channel but haven't built it"
        score: 3
      - label: "No clear path to reach them"
        score: 1

  - id: d3
    section: D
    text: "What do you have that competitors can't easily copy?"
    options:
      - label: "Deep domain expertise + relationships + data"
        score: 5
      - label: "Technical moat or proprietary technology"
        score: 4
      - label: "First-mover advantage only"
        score: 2
      - label: "Nothing defensible yet"
        score: 0

  - id: d4
    section: D
    text: "Does Arabic localization create defensibility?"
    options:
      - label: "Arabic-first with deep cultural integration"
        score: 5
      - label: "Arabic translation with regional adaptation"
        score: 3
      - label: "English-only for now"
        score: 1
      - label: "Arabic not relevant to my market"
        score: 0

  - id: d5
    section: D
    text: "How fast can a new customer see results?"
    options:
      - label: "Same day — instant value visible"
        score: 5
      - label: "Within a week — quick onboarding"
        score: 4
      - label: "Within 30 days — some setup required"
        score: 3
      - label: "90+ days before value is clear"
        score: 1
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
    action: "Good foundation. Sharpen 1-2 weak sections."

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

## SECTION RECOMMENDATIONS

```yaml
recommendations:
  A:
    title: "Pain Reality"
    below_threshold: 15
    tips:
      - "Interview 5 buyers this week. Ask: 'Walk me through the last time this problem cost you money.'"
      - "Build a pain quantification calculator to help buyers see the dollar impact"
      - "Look for trigger events that make the pain urgent"
  B:
    title: "Purchasing Power"
    below_threshold: 15
    tips:
      - "Find the economic buyer — in MENA that's usually the owner/GM"
      - "Add flexible payment options: Tabby/Tamara installments, annual prepaid discounts"
      - "Price against the pain cost, not competitor pricing"
  C:
    title: "Market Momentum"
    below_threshold: 15
    tips:
      - "Research market growth data from credible sources"
      - "Identify regulatory tailwinds specific to MENA"
      - "Track search trends for your solution category in Arabic and English"
  D:
    title: "Competitive Advantage"
    below_threshold: 15
    tips:
      - "Articulate your differentiator in one sentence and test with 5 prospects"
      - "Build a reachability plan: How to get to 1,000 prospects in 30 days"
      - "Develop at least one unfair advantage (data, relationships, or domain depth)"
```

---

## SCORING FORMULA

```yaml
scoring:
  section_score: "Sum of all question scores in section (max 25 per section)"
  total_score: "Sum of all 4 section scores (max 100)"
  band_assignment: "Match total_score to bands (STRONG >= 80, VIABLE >= 60, WEAK >= 40, RISK < 40)"
  readiness_contribution: "total_score * 0.35"
```
