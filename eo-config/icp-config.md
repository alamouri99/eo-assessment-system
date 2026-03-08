# ICP — Clarity Scoring Configuration
# Version: 1.1
# Framework: Russell Brunson + Chet Holmes
# Total Points: 100 (5 sections A-E, weighted differently)
# Each question: 0-5 scale (except B/C which use 0-4 scale)
# 22 questions across 5 sections
# v1.1 Changes: B reduced 10→5 pains, C reduced 10→5 pleasures, engagement layer added

---

## ASSESSMENT METADATA

```yaml
id: icp-clarity
name: ICP Clarity Scoring
short_name: ICP
version: "1.1"
total_points: 100
questions_count: 22
readiness_weight: 0.35
webhook_path: /webhook/eo-icp-score
```

---

## ENGAGEMENT PROTOCOL (NEW in v1.1)

```yaml
engagement:
  pattern_breaks:
    - after: "Section A → B transition"
      type: "Insight Unlock"
      content: "AI-generated insight about WHO clarity quality"
    - after: "Section B → C transition"
      type: "Investment Signal"
      content: "Your pain statements have more depth than most consultants charge $5K for."
    - after: "Section C → D transition"
      type: "Variable Reward"
      content: "Pain-Pleasure Matrix: visual grid of pains vs dream outcomes"
    - after: "Section D → E transition"
      type: "Offer Preview"
      content: "Draft ICP profile based on answers so far"
  acknowledgment_protocol:
    - "Between all scored questions"
    - "Strong answers: positive reinforcement with specificity praise"
    - "Weak answers: constructive push with specific follow-up"
  investment_signaling:
    - at: "~20min"
      message: "Your ICP clarity is sharper than most founders who've raised $500K."
    - at: "~40min"
      message: "This ICP document could anchor a $50K consulting engagement."
    - at: "final"
      message: "Complete ICP profile built. This is strategy-grade output."
  elevation_instructions:
    - "Upgrade language: scrappy input → polished strategic prose"
    - "Add strategic context: implications not stated but logically implied"
    - "Flag contradictions: cross-section misalignments with ⚠️ warnings"
    - "Strategy-grade output: documents read like professional deliverables"
```

---

## SECTIONS

```yaml
sections:
  - id: A
    key: who
    name: "WHO — Dream Customer Definition"
    max_score: 25
    questions_count: 5

  - id: B
    key: pain
    name: "PAIN — Top 5 Pain Statements"
    max_score: 20
    questions_count: 5
    notes: "v1.1: Reduced from 10→5 pains. Each scored 0-4. AI probes top 2."

  - id: C
    key: pleasure
    name: "PLEASURE — Top 5 Dream Outcomes"
    max_score: 20
    questions_count: 5
    notes: "v1.1: Reduced from 10→5 pleasures. Each scored 0-4. AI probes top 2."

  - id: D
    key: hero_journey
    name: "HERO JOURNEY — Current → Future State"
    max_score: 20
    questions_count: 4

  - id: E
    key: access
    name: "ACCESS & CONGREGATION — Where to Find Them"
    max_score: 15
    questions_count: 3
```

---

## QUESTIONS

### Section A: WHO — Dream Customer Definition (25 points)

```yaml
questions:
  - id: a1
    section: A
    text: "Can you name a specific person who represents your ideal customer?"
    rubric_summary: "5=Concrete example with name/age/location/context, 3=Specific role, 1=Vague segment, 0=Generic"
    options:
      - label: "Yes — specific person with name, role, location, and context"
        score: 5
      - label: "Specific role with multiple descriptors"
        score: 4
      - label: "Role without detail (e.g., 'Salon owners in UAE')"
        score: 3
      - label: "Vague segment (e.g., 'SME owners')"
        score: 1

  - id: a2
    section: A
    text: "Which state is your dream customer in RIGHT NOW?"
    rubric_summary: "Brunson's 4 States: Frustrated(5), Satisfied but Open(3), Diehard(1), Unaware(0)"
    options:
      - label: "Frustrated with current solution (searching for alternatives)"
        score: 5
      - label: "Satisfied but open (not looking, but will listen)"
        score: 3
      - label: "Loyal to a competitor (hard to flip)"
        score: 1
      - label: "Unaware of the problem"
        score: 0

  - id: a3
    section: A
    text: "Can you describe their ideal future in THEIR WORDS, not yours?"
    rubric_summary: "5=Direct quotes, 3=Paraphrased from conversations, 1=Your assumption, 0=Never asked"
    options:
      - label: "I can quote them directly from real conversations"
        score: 5
      - label: "Paraphrased from multiple conversations"
        score: 3
      - label: "My assumption about what they want"
        score: 1
      - label: "I've never asked them"
        score: 0

  - id: a4
    section: A
    text: "Are they running FROM pain or running TOWARD desire (or both)?"
    rubric_summary: "5=Both clear, 3=One clear, 2=One partial, 0=Neither clear"
    options:
      - label: "Both pain AND desire are clear and specific"
        score: 5
      - label: "Pain is clear, desire is vague (or vice versa)"
        score: 3
      - label: "One is barely articulated"
        score: 2
      - label: "Not clear on either"
        score: 0

  - id: a5
    section: A
    text: "Which Brunson archetype does your buyer embody?"
    rubric_summary: "5=Identified + message aligned, 3=Suspected, 2=Torn between two, 0=No idea"
    options:
      - label: "Identified archetype AND shaped message to match"
        score: 5
      - label: "Clear archetype fit, message partially aligned"
        score: 4
      - label: "Suspect an archetype but haven't tested"
        score: 3
      - label: "No idea — treating all buyers the same"
        score: 0
```

### Section B: PAIN — Top 5 Pain Statements (20 points)

v1.1: Reduced from 10 to 5 pain statements. Each scored 0-4. AI probes the top 2 for depth.

```yaml
questions:
  - id: b1
    section: B
    type: free_text
    text: "TOP Pain #1 — What is the single biggest pain your ICP faces?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Specific, quantified, emotionally resonant. 2=Generic but relevant. 0=Vague or missing."

  - id: b2
    section: B
    type: free_text
    text: "TOP Pain #2 — What is the second most urgent pain?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Specific, quantified, emotionally resonant. 2=Generic but relevant. 0=Vague or missing."

  - id: b3
    section: B
    type: free_text
    text: "TOP Pain #3 — What operational pain do they tolerate daily?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Specific, quantified, emotionally resonant. 2=Generic but relevant. 0=Vague or missing."

  - id: b4
    section: B
    type: free_text
    text: "TOP Pain #4 — What pain keeps them up at night?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Specific, quantified, emotionally resonant. 2=Generic but relevant. 0=Vague or missing."

  - id: b5
    section: B
    type: free_text
    text: "TOP Pain #5 — What pain would they pay to eliminate TODAY?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Specific, quantified, emotionally resonant. 2=Generic but relevant. 0=Vague or missing."
```

### Section C: PLEASURE — Top 5 Dream Outcomes (20 points)

v1.1: Reduced from 10 to 5 dream outcomes. Each scored 0-4. AI probes the top 2 for depth.

```yaml
questions:
  - id: c1
    section: C
    type: free_text
    text: "TOP Dream Outcome #1 — What does their ideal future look like?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Vivid, specific, emotionally compelling. 2=Generic but directional. 0=Vague or missing."

  - id: c2
    section: C
    type: free_text
    text: "TOP Dream Outcome #2 — What transformation would they brag about?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Vivid, specific, emotionally compelling. 2=Generic but directional. 0=Vague or missing."

  - id: c3
    section: C
    type: free_text
    text: "TOP Dream Outcome #3 — What status shift do they desire?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Vivid, specific, emotionally compelling. 2=Generic but directional. 0=Vague or missing."

  - id: c4
    section: C
    type: free_text
    text: "TOP Dream Outcome #4 — What would their business look like in 12 months?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Vivid, specific, emotionally compelling. 2=Generic but directional. 0=Vague or missing."

  - id: c5
    section: C
    type: free_text
    text: "TOP Dream Outcome #5 — What would make them recommend you to others?"
    maxScore: 4
    wordLimit: 75
    rubric_summary: "4=Vivid, specific, emotionally compelling. 2=Generic but directional. 0=Vague or missing."
```

### Section D: HERO JOURNEY — Current → Future State (20 points)

```yaml
questions:
  - id: d1
    section: D
    type: free_text
    text: "Where is your ideal client RIGHT NOW in their journey?"
    maxScore: 5
    rubric_summary: "5=Vivid, specific current state with frustration level and prior attempts. 3=Generic but relevant. 0=Vague."

  - id: d2
    section: D
    type: free_text
    text: "What does 'success' look like for them after using your solution?"
    maxScore: 5
    rubric_summary: "5=Specific 90-day outcome with metrics. 3=General improvement. 0=Vague."

  - id: d3
    section: D
    type: free_text
    text: "What are the 3 biggest obstacles preventing your client from reaching that future state WITHOUT your product?"
    maxScore: 5
    rubric_summary: "5=Real blockers mapped, not feature lists. 3=Generic obstacles. 0=Vague."

  - id: d4
    section: D
    type: free_text
    text: "How does your product bridge the gap between current state and desired state?"
    maxScore: 5
    rubric_summary: "5=Each obstacle mapped to specific solution approach. 3=Generic solution. 0=Vague."
```

### Section E: ACCESS & CONGREGATION — Where to Find Them (15 points)

```yaml
questions:
  - id: e1
    section: E
    type: free_text
    text: "Where does your ideal customer spend time online?"
    maxScore: 5
    rubric_summary: "5=Specific platforms, groups, communities with names and sizes. 3=Platform-level. 0=Vague."

  - id: e2
    section: E
    type: free_text
    text: "Where does your ideal customer gather offline?"
    maxScore: 5
    rubric_summary: "5=Specific events, associations, meetups, MENA-specific. 3=Generic. 0=Vague."

  - id: e3
    section: E
    type: free_text
    text: "How will you get in front of 100 potential buyers in the next 30 days?"
    maxScore: 5
    rubric_summary: "5=Specific plan with channels, numbers, timeline. 3=General plan. 0=No plan."
```

---

## SCORING BANDS

```yaml
bands:
  - id: CRYSTAL_CLEAR
    name: "Crystal Clear ICP"
    min_score: 80
    max_score: 100
    color: "#22C55E"
    tag: "eo-icp-clear"
    action: "Ready to execute. Scale. Stop overthinking. Sell."

  - id: GOOD_FOUNDATION
    name: "Good Foundation"
    min_score: 60
    max_score: 79
    color: "#3B82F6"
    tag: "eo-icp-decent"
    action: "Basics present, 2-3 areas need sharpening."

  - id: FUZZY
    name: "Fuzzy ICP"
    min_score: 40
    max_score: 59
    color: "#F59E0B"
    tag: "eo-icp-fuzzy"
    action: "STOP marketing. Start researching. 10+ buyer conversations needed."

  - id: NO_CLARITY
    name: "No Clarity"
    min_score: 20
    max_score: 39
    color: "#EF4444"
    tag: "eo-icp-none"
    action: "ICP Rebuild needed. 21-day sprint recommended."

  - id: CRITICAL
    name: "Critical"
    min_score: 0
    max_score: 19
    color: "#991B1B"
    tag: "eo-icp-none"
    action: "Start over. Pick 1 customer who loves your product. Study them."
```

---

## SCORING FORMULA

```yaml
scoring:
  section_score: "Sum of all question scores in section"
  total_score: "Sum of all 5 section scores: A(25) + B(20) + C(20) + D(20) + E(15) = 100"
  band_assignment: "Match total_score to bands"
  readiness_contribution: "total_score * 0.35"

  # B/C scoring note (v1.1):
  # B: 5 pains × 4 pts each = 20 pts max
  # C: 5 pleasures × 4 pts each = 20 pts max
  # AI probes top 2 in each section for depth (probing doesn't change score)

  # Priority order for focus (if section scores are low):
  priority_order:
    - "A (WHO) — If unclear, everything else breaks"
    - "B (PAIN) — If you can't articulate their pain, you can't sell"
    - "C (PLEASURE) — If no dream outcome, no aspiration pull"
    - "D (HERO JOURNEY) — If transformation isn't mapped, harder to sell"
    - "E (ACCESS) — If you can't reach them, clarity doesn't matter"
```
