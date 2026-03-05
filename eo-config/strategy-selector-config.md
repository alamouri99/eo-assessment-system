# Strategy Selector Configuration
# Version: 1.0
# 7 questions, 4 strategy paths
# Each option scores against all 4 paths simultaneously

---

## ASSESSMENT METADATA

```yaml
id: strategy-selector
name: MicroSaaS Strategy Selector
short_name: Strategy Selector
version: "1.0"
questions_count: 7
paths_count: 4
webhook_path: /webhook/eo-strategy-selector
```

---

## PATHS

```yaml
paths:
  - index: 0
    id: replicate
    name: "Replicate & Localize"
    subtitle: "Language & geo arbitrage. Find what works globally, build the Arabic/MENA version."
    description: "You spotted a proven SaaS product that has no Arabic-native version. Your advantage is speed of localization and deep understanding of MENA market dynamics. The model is validated — you just need to execute the adaptation faster than the incumbent can localize."
    risk: "Incumbents may localize before you scale. Speed is your moat."
    proofs:
      - name: "Teachizy (Arabic LMS)"
        desc: "Localized course platform for Arabic-speaking creators"
        metric: "Growing MRR"
      - name: "SaaSFast"
        desc: "MENA-native SaaS toolkit modeled on global patterns"
        metric: "Active users"
      - name: "EO Platform"
        desc: "AppSumo model for MENA solopreneurs"
        metric: "In development"

  - index: 1
    id: consulting
    name: "Consulting-First SaaS"
    subtitle: "Start with services. Productize what repeats. SaaS emerges from your expertise."
    description: "You have deep domain expertise and existing client relationships. Instead of guessing what to build, you start with consulting — solving the problem manually. When you find the repeatable part, you productize it. This is the lowest-risk path because you generate revenue from day 1."
    risk: "Getting stuck in service mode and never shipping the product."
    proofs:
      - name: "EO MicroSaaS"
        desc: "Mamoun's journey: Avaya/Cisco consulting to signal engine product"
        metric: "$3,500/mo engine"
      - name: "SparkLine"
        desc: "Service-to-product in content marketing space"
        metric: "Profitable SaaS"
      - name: "CXMfast AI"
        desc: "Contact center consulting to AI-native platform"
        metric: "Enterprise clients"

  - index: 2
    id: boring
    name: "Boring Micro-SaaS"
    subtitle: "One unsexy problem. $20-200/month. Patient compounding through volume."
    description: "You don't need to build the next big thing. Find one painful, unsexy problem that people will pay $20-200/month to solve. Stack revenue through volume and patience. This path works best when you're comfortable with niche markets and have the discipline to resist feature creep."
    risk: "Market may be too small if not properly scoped."
    proofs:
      - name: "Curator.io"
        desc: "Social media aggregation tool. Boring, profitable, growing."
        metric: "$50K+ MRR"
      - name: "Frill.co"
        desc: "Feature request tracking. Solves one problem perfectly."
        metric: "Steady growth"
      - name: "Mike Hill Portfolio"
        desc: "Multiple boring tools stacked together."
        metric: "$200K MRR"

  - index: 3
    id: hammering
    name: "Hammering Deep"
    subtitle: "One feature. One persona. Relentless depth. Undisputed best at one thing."
    description: "You resist the temptation to add features. You pick one persona with one burning problem and you become the undisputed best solution. This path requires obsessive focus and the courage to say no to adjacent opportunities. When it works, it creates a defensible moat through depth, not breadth."
    risk: "Market may not be deep enough for one-feature dominance."
    proofs:
      - name: "Tibo"
        desc: "LinkedIn posting tool. One feature, obsessively polished."
        metric: "~$700K MRR"
      - name: "Revit.ai"
        desc: "Deep focus on one vertical with one killer feature."
        metric: "$400K MRR"
      - name: "ShipFast (Marc Lou)"
        desc: "One thing: ship Next.js SaaS fast."
        metric: "$250K+ MRR"
```

---

## QUESTIONS

Each option has a `scores` array: `[replicate, consulting, boring, hammering]`

```yaml
questions:
  - index: 0
    dimension: "Existing Expertise"
    text: "How deep is your domain expertise in your target market?"
    context: "This isn't about general tech skills. It's about knowing the buyer's pain, the purchase journey, and the industry dynamics in your specific niche."
    options:
      - label: "I have 5+ years in this exact industry"
        desc: "You know the buyers by name. You've seen the pain firsthand."
        scores: [2, 5, 3, 4]
      - label: "I have adjacent experience"
        desc: "You know the space but haven't sold to this specific buyer."
        scores: [4, 3, 3, 3]
      - label: "I've done research but no direct experience"
        desc: "You've validated through interviews and data, not lived experience."
        scores: [3, 1, 4, 2]
      - label: "Starting fresh — this is a new market for me"
        desc: "Pure opportunity play. No domain baggage, no domain advantage."
        scores: [5, 1, 3, 2]

  - index: 1
    dimension: "Available Capital"
    text: "How much runway can you commit to building this?"
    context: "Be honest. This determines whether you need revenue on day 1 or can afford to build first. There's no wrong answer — each path has a different capital requirement."
    options:
      - label: "I can self-fund 6-12 months of development"
        desc: "Enough runway to build without immediate revenue pressure."
        scores: [4, 2, 3, 5]
      - label: "I have 3-6 months of savings to commit"
        desc: "Moderate runway. Need to see traction signals within 90 days."
        scores: [3, 3, 4, 3]
      - label: "I need revenue within 30-60 days"
        desc: "Cash-constrained. Must monetize skills immediately."
        scores: [2, 5, 2, 1]
      - label: "I have a job — this is a side project"
        desc: "Limited time but no financial pressure. Evenings and weekends."
        scores: [3, 2, 5, 4]

  - index: 2
    dimension: "Risk Tolerance"
    text: "How do you handle uncertainty in business?"
    context: "Every path has risk. This question reveals which type of risk you can stomach — market risk, execution risk, or competition risk."
    options:
      - label: "I'll ship fast and iterate — speed over perfection"
        desc: "Comfortable with public failure. Learn by shipping."
        scores: [4, 2, 3, 5]
      - label: "I prefer validating before building"
        desc: "Methodical. You need signal before investing time."
        scores: [3, 4, 4, 2]
      - label: "I follow proven models and adapt them"
        desc: "Lower risk preference. Why reinvent when you can localize?"
        scores: [5, 3, 3, 1]
      - label: "I invest deeply in one bet and go all-in"
        desc: "High conviction player. When you commit, you commit fully."
        scores: [2, 4, 2, 5]

  - index: 3
    dimension: "Market Familiarity"
    text: "How well do you understand MENA buyer behavior?"
    context: "MENA B2B is not Silicon Valley. Trust mechanics, payment friction, and decision timelines are fundamentally different. This matters more than most founders think."
    options:
      - label: "I've sold B2B in MENA for years"
        desc: "You know the coffee meetings, the trust timeline, the payment workarounds."
        scores: [3, 5, 3, 4]
      - label: "I live in MENA but haven't sold B2B here"
        desc: "Cultural context yes, commercial context no."
        scores: [4, 3, 4, 3]
      - label: "I'm targeting MENA from outside the region"
        desc: "Opportunity-driven. You see the gap but haven't lived the dynamics."
        scores: [5, 2, 3, 2]
      - label: "I'm focused on global markets, MENA is secondary"
        desc: "MENA is one geography in a multi-market strategy."
        scores: [3, 2, 4, 4]

  - index: 4
    dimension: "Competitive Landscape"
    text: "What does the competition look like in your space?"
    context: "Competition isn't always bad. Sometimes it proves the market. The question is: does an Arabic-native solution exist?"
    options:
      - label: "Global players exist but no Arabic/MENA version"
        desc: "Classic localization opportunity. The model is proven, the gap is clear."
        scores: [5, 1, 2, 2]
      - label: "Competitors exist but they're mediocre"
        desc: "They have the market but not the execution. Room to outperform."
        scores: [2, 3, 4, 5]
      - label: "It's a crowded space — many solutions available"
        desc: "Differentiation will be harder. Need a sharp angle."
        scores: [1, 2, 3, 5]
      - label: "Almost no competition — new category"
        desc: "Exciting but risky. You'll need to educate the market."
        scores: [3, 4, 4, 3]

  - index: 5
    dimension: "Building Style"
    text: "How do you prefer to build products?"
    context: "This reveals your natural motion as a builder. Some founders are code-first, others are customer-first. Neither is wrong — but each fits different paths."
    options:
      - label: "I build with AI tools (Claude, bolt.new, Cursor)"
        desc: "Modern builder. Ship fast using AI-assisted development."
        scores: [4, 2, 4, 5]
      - label: "I hire developers or use agencies"
        desc: "You manage, they build. Capital-for-speed trade."
        scores: [5, 3, 3, 3]
      - label: "I start with manual processes, then automate"
        desc: "Service-first mindset. Prove it works before coding it."
        scores: [2, 5, 3, 2]
      - label: "I use no-code / low-code platforms"
        desc: "GHL, Bubble, Webflow — platforms over custom code."
        scores: [4, 3, 5, 2]

  - index: 6
    dimension: "Revenue Goal"
    text: "What's your 12-month revenue target?"
    context: "This isn't about ambition — it's about which path has the ceiling height you need. A boring micro-SaaS can hit $20K MRR. Hammering deep can hit $200K MRR. Different games."
    options:
      - label: "$1K - $5K MRR"
        desc: "Side income. Replace a salary or fund your next project."
        scores: [3, 3, 5, 2]
      - label: "$5K - $20K MRR"
        desc: "Full-time founder income. Sustainable micro-SaaS."
        scores: [4, 3, 4, 4]
      - label: "$20K - $50K MRR"
        desc: "Serious business. Will need team and systems."
        scores: [4, 4, 3, 4]
      - label: "$50K+ MRR"
        desc: "Venture-scale ambition. Dominant market position."
        scores: [3, 3, 2, 5]
```

---

## SCORING FORMULA

```yaml
scoring:
  # Each answer adds its scores array to running path totals
  # pathScores[i] += selectedOption.scores[i] for each question

  max_score_per_path: 35  # 7 questions x max 5 per path

  # Rank all 4 paths by total score, descending
  primary_path: "Highest scoring path"
  secondary_path: "Second highest scoring path"

  # Path fit percentage
  path_percentage: "(pathScore / max_score_per_path) * 100"

  # 2x2 Matrix proxy (from path scores)
  mas_proxy: "pathScores[replicate] + pathScores[boring]"
  gtm_proxy: "pathScores[consulting] + pathScores[hammering]"
  mas_proxy_threshold: "questions_count * 5 * 0.5"
  gtm_proxy_threshold: "questions_count * 5 * 0.5"

  # Quadrants
  quadrant_high_high: "BUILD + SELL"
  quadrant_high_low: "BUILD + LEARN"
  quadrant_low_high: "SELL + VALIDATE"
  quadrant_low_low: "KILL or PIVOT"
```

---

## GHL TAGS

```yaml
tags:
  completion: "eo-strategy-assessed"
  paths:
    replicate: "eo-path-replicate"
    consulting: "eo-path-consulting"
    boring: "eo-path-boring"
    hammering: "eo-path-hammering"
```
