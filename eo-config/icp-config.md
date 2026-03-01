# ICP — Clarity Scoring Configuration
# Version: 1.0
# Framework: Russell Brunson + Chet Holmes
# Total Points: 100 (6 sections, weighted differently)
# Each question: 0-5 scale

---

## ASSESSMENT METADATA

```yaml
id: icp-clarity
name: ICP Clarity Scoring
short_name: ICP
version: "1.0"
total_points: 100
questions_count: 20
readiness_weight: 0.35
webhook_path: /webhook/eo-icp-score
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
    key: where
    name: "WHERE — Congregation Points"
    max_score: 20
    questions_count: 4

  - id: C
    key: capture
    name: "WHAT CAPTURE — Attraction Mechanism"
    max_score: 20
    questions_count: 4

  - id: D
    key: result
    name: "RESULT — Desired Transformation"
    max_score: 15
    questions_count: 3

  - id: E
    key: epiphany
    name: "EPIPHANY — Epiphany Bridge"
    max_score: 10
    questions_count: 2

  - id: F
    key: character
    name: "CHARACTER — Attractive Character"
    max_score: 10
    questions_count: 2
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

### Section B: WHERE — Congregation Points (20 points)

```yaml
questions:
  - id: b1
    section: B
    text: "Where do they gather in person?"
    rubric_summary: "5=Named specific events AND attended, 3=Know events but haven't attended, 1=Generic, 0=No idea"
    options:
      - label: "Named 2-3 specific events AND attended them"
        score: 5
      - label: "Know the events but haven't attended"
        score: 3
      - label: "Generic references (e.g., 'networking events')"
        score: 1
      - label: "No idea where they physically gather"
        score: 0

  - id: b2
    section: B
    text: "Where are they online? Be specific with group names, not platforms."
    rubric_summary: "5=Named specific communities AND active, 3=Know some communities, 2=Platform-level, 0=No idea"
    options:
      - label: "Named specific communities AND active in them"
        score: 5
      - label: "Know some communities but not active"
        score: 3
      - label: "Platform-level thinking (e.g., 'LinkedIn and WhatsApp')"
        score: 2
      - label: "No idea"
        score: 0

  - id: b3
    section: B
    text: "What content do they consume? Podcasts? YouTube? Newsletters?"
    rubric_summary: "5=Named specific creators AND verified, 3=Know some content, 2=Platform-level, 0=No idea"
    options:
      - label: "Named specific creators/shows AND heard them mention these"
        score: 5
      - label: "Know some content they consume, not verified"
        score: 3
      - label: "Platform-level (e.g., 'YouTube and podcasts')"
        score: 2
      - label: "No idea"
        score: 0

  - id: b4
    section: B
    text: "Who do they trust for recommendations?"
    rubric_summary: "5=Named specific people/roles AND know how to reach, 3=Know types, 2=Generic, 0=No idea"
    options:
      - label: "Named specific people/roles AND know how to reach them"
        score: 5
      - label: "Know the types of people they trust"
        score: 3
      - label: "Generic (e.g., 'peers and experts')"
        score: 2
      - label: "No idea"
        score: 0
```

### Section C: WHAT CAPTURE — Attraction Mechanism (20 points)

```yaml
questions:
  - id: c1
    section: C
    text: "Do you have a hook that stops them mid-scroll?"
    rubric_summary: "5=Tested hook with >3% CTR, 3=Strong hypothesis untested, 1=Weak/generic, 0=No hook"
    options:
      - label: "Tested hook with proven engagement (>3% CTR)"
        score: 5
      - label: "Strong hypothesis, haven't tested yet"
        score: 3
      - label: "Weak or generic hook"
        score: 1
      - label: "No hook — still describing features"
        score: 0

  - id: c2
    section: C
    text: "Do you have an origin story that creates BELIEF?"
    rubric_summary: "5=Full Epiphany Bridge tested, 3=Partial story, 1=Generic, 0=No story"
    options:
      - label: "Full Epiphany Bridge — tested, creates 'me too' moments"
        score: 5
      - label: "Partial story, 3-4 elements present"
        score: 3
      - label: "Generic: 'I saw a problem and solved it'"
        score: 1
      - label: "No story — rely on credentials or features"
        score: 0

  - id: c3
    section: C
    text: "What do you give them to enter your world?"
    rubric_summary: "5=Named specific valuable tool that teaches AND qualifies, 3=Generic offer, 1=Weak offer, 0=Nothing"
    options:
      - label: "Named, specific, valuable tool that teaches AND qualifies"
        score: 5
      - label: "Generic offer (e.g., 'free consultation')"
        score: 3
      - label: "Weak offer (e.g., 'join our newsletter')"
        score: 1
      - label: "No lead magnet"
        score: 0

  - id: c4
    section: C
    text: "What proof do you have that this works?"
    rubric_summary: "5=Published case studies + logos, 4=Video testimonials, 3=Text testimonials, 2=Credentials only, 0=Nothing"
    options:
      - label: "Published case studies with metrics AND client logos"
        score: 5
      - label: "Video testimonials with specific results"
        score: 4
      - label: "Text testimonials with results"
        score: 3
      - label: "Credentials only — no proven results"
        score: 2
```

### Section D: RESULT — Desired Transformation (15 points)

```yaml
questions:
  - id: d1
    section: D
    text: "Can you show a measurable before/after?"
    rubric_summary: "5=Specific transformation with metrics, 3=Clear but vague metrics, 1=Generic, 0=No transformation"
    options:
      - label: "Specific transformation with metrics (e.g., 'From 3hrs to 15min/week')"
        score: 5
      - label: "Transformation clear, metrics vague"
        score: 3
      - label: "Generic (e.g., 'more efficient')"
        score: 1
      - label: "No transformation articulated"
        score: 0

  - id: d2
    section: D
    text: "How fast do they see the transformation?"
    rubric_summary: "5=Same day, 4=Week 1, 3=30 days, 2=90 days, 0=Vague"
    options:
      - label: "Same-day or next-day proof"
        score: 5
      - label: "Week 1 results"
        score: 4
      - label: "30-day results"
        score: 3
      - label: "90+ days or vague timeline"
        score: 1

  - id: d3
    section: D
    text: "Do you de-risk their decision?"
    rubric_summary: "5=Performance guarantee, 4=Money-back, 3=Pilot/trial, 2=Soft guarantee, 0=No guarantee"
    options:
      - label: "Performance guarantee with clawback"
        score: 5
      - label: "Money-back guarantee"
        score: 4
      - label: "Pilot/trial structure"
        score: 3
      - label: "No guarantee"
        score: 0
```

### Section E: Epiphany Bridge (10 points)

```yaml
questions:
  - id: e1
    section: E
    text: "What false belief stops your buyer from buying?"
    rubric_summary: "5=Specific limiting belief verified from multiple buyers, 3=Suspected but unverified, 0=None identified"
    options:
      - label: "Specific limiting belief articulated AND heard from multiple buyers"
        score: 5
      - label: "Suspect a limiting belief but haven't verified"
        score: 3
      - label: "No limiting belief identified"
        score: 0

  - id: e2
    section: E
    text: "Have you reframed the solution as a NEW opportunity, not just an improvement?"
    rubric_summary: "5=Clear new category/vehicle, 2=Better version pitch, 0=Same-as-competitor"
    options:
      - label: "Clear new category/vehicle — buyers see this as NEW"
        score: 5
      - label: "Better version pitch (e.g., 'Our CRM is 3x better')"
        score: 2
      - label: "Same-as-competitor pitch"
        score: 0
```

### Section F: Attractive Character (10 points)

```yaml
questions:
  - id: f1
    section: F
    text: "Which archetype are you? (Expert, Everyman, Mentor, Visionary, Rebel, Lover)"
    rubric_summary: "5=Chosen AND content consistent, 3=Natural but not intentional, 0=No persona"
    options:
      - label: "Consciously chosen AND content/messaging consistent with it"
        score: 5
      - label: "Natural archetype but not intentionally designed"
        score: 3
      - label: "No public persona — blank slate"
        score: 0

  - id: f2
    section: F
    text: "Does your backstory create authority AND relatability?"
    rubric_summary: "5=Tested backstory that generates 'me too' responses, 3=Untested story, 1=Generic bio, 0=No backstory"
    options:
      - label: "Tested backstory generating 'me too' responses"
        score: 5
      - label: "Have a story, haven't tested resonance"
        score: 3
      - label: "Generic bio (e.g., '10 years in industry')"
        score: 1
      - label: "No backstory — just credentials"
        score: 0
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
  total_score: "Sum of all 6 section scores (max 100)"
  band_assignment: "Match total_score to bands"
  readiness_contribution: "total_score * 0.35"

  # Priority order for focus (if section scores are low):
  priority_order:
    - "A (WHO) — If unclear, everything else breaks"
    - "B (WHERE) — If you can't reach them, clarity doesn't matter"
    - "C (CAPTURE) — If no one's listening, specificity doesn't help"
    - "D (RESULT) — If transformation isn't clear, harder to sell"
    - "E (EPIPHANY) — If unaddressed, stalls sales cycles"
    - "F (CHARACTER) — If not consistent, message dilutes"
```
