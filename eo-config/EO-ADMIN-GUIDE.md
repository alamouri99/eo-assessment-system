# EO Assessment System — Admin Guide

> How to manage, update, and troubleshoot your assessment system.

---

## System Architecture (Quick Reference)

```
User takes assessment (HTML)
        ↓
Frontend sends answers to n8n webhook
        ↓
n8n scores answers + calls Claude AI for analysis
        ↓
n8n stores results in GHL (CRM) + Supabase (DB)
        ↓
Dashboard loads results from consolidated webhook
```

---

## File Map — What Controls What

### Config Files (Questions, Scoring, Bands)

| File | Controls |
|------|----------|
| `eo-config/mas-config.md` | MAS 20 questions, 4 sections, band thresholds, scoring weights |
| `eo-config/icp-config.md` | ICP 20 questions, 6 sections, band thresholds, scoring weights |
| `eo-config/gtm-config.md` | GTM 14 questions, 13 motions, MENA viability, composite formula |
| `eo-config/strategy-selector-config.md` | Strategy Selector 7 questions, 4 paths, scoring matrix |
| `eo-config/consolidated-config.md` | Readiness formula weights, bands, bottleneck rules, archetypes |

### AI Analysis Prompts (SKILL.md Files)

| File | Controls |
|------|----------|
| `market-attractiveness-scoring/SKILL.md` | How Claude analyzes MAS results |
| `icp-clarity-scoring/SKILL.md` | How Claude analyzes ICP results |
| `gtm-fitness-scoring/SKILL.md` | How Claude analyzes GTM results |
| `strategy-selector/SKILL.md` | How Claude does consolidated cross-pillar analysis |

### Frontend HTML Files

| File | Assessment |
|------|-----------|
| `EO-Strategy-Selector-Lite.html` | Strategy Selector (lite version) |
| `EO-Strategy-Selector.html` | Strategy Selector (full version) |
| `EO-Market-Attractiveness-Scoring.html` | Market Attractiveness Scoring (MAS) |
| `EO-ICP-Clarity-Scoring.html` | ICP Clarity Scoring |
| `EO-GTM-Fitness-Scoring.html` | GTM Fitness Scoring |
| `EO-Assessment-Dashboard.html` | Dashboard (hub + scorecard) |

### n8n Workflows

| Workflow | ID | Webhook Path |
|----------|----|-------------|
| EO - Strategy Selector | `VcSpRfjQwGVUGPzR` | `/webhook/eo-strategy-selector` |
| EO - MAS Assessment | `bujeKbwxAp7DLblv` | `/webhook/eo-mas-score` |
| EO - ICP Assessment | `wrgTi0mbAhwgTvsc` | `/webhook/eo-icp-score` |
| EO - GTM Assessment | `7cQNjdQ6CFPfODLY` | `/webhook/eo-gtm-score` |
| EO - Consolidated Assessment | `V05bffaa8nxjDMMq` | `/webhook/eo-consolidated` |

### External Services

| Service | Purpose | Access |
|---------|---------|--------|
| n8n Cloud | Workflow automation | `ai.mamounalamouri.smorchestra.com` |
| Supabase | Assessment data storage | Project `odjuqweiyzicqmcqozsu` |
| GHL (GoHighLevel) | CRM contact management | Location `UNw9DraGO3eyEa5l4lkJ` |
| Anthropic API | Claude AI analysis | API key in n8n workflows |

---

## How to Change Questions

### Step 1: Edit the Config File

Open the relevant config file (e.g., `eo-config/mas-config.md`) and find the `questions:` section.

Each question looks like this:

```yaml
- id: a1
  section: A
  text: "Your question text here"
  options:
    - label: "Best answer"
      score: 5
    - label: "Good answer"
      score: 3
    - label: "Weak answer"
      score: 1
    - label: "No answer"
      score: 0
```

**To change a question:** Edit the `text` field.

**To change answer options:** Edit the `label` and `score` values.

**To add a question:** Add a new entry following the same format. Update `questions_count` in the metadata section and adjust `max_score` for the relevant section.

**To remove a question:** Delete the entry. Update `questions_count` and `max_score`.

### Step 2: Update the HTML (if questions changed)

If you added or removed questions, the corresponding HTML file needs to know about the change. The HTML files dynamically render questions from the config, but verify:

- Section `max_score` values still add up to `total_points` (100 for MAS/ICP)
- Question IDs are sequential within their section (a1, a2, a3...)

### Step 3: Verify

Load the assessment in a browser and confirm the new question appears with correct options.

---

## How to Change Scoring Formulas

### Band Thresholds

In any config file, find the `bands:` section:

```yaml
bands:
  - id: STRONG
    min_score: 80
    max_score: 100
```

Change `min_score` / `max_score` to shift band boundaries.

### Section Weights (ICP)

ICP sections have different max scores that act as weights:

```yaml
sections:
  - id: A
    key: who
    name: "WHO — Dream Customer Definition"
    max_score: 25   # ← Change this to reweight
```

All section `max_score` values must add up to 100.

### Readiness Formula Weights (Consolidated)

In `eo-config/consolidated-config.md`:

```yaml
weights:
  mas_weight: 0.35
  icp_weight: 0.35
  gtm_weight: 0.30
```

These must add up to 1.0.

### GTM Composite Formula

In `eo-config/gtm-config.md`, the motion composite is:

```yaml
composite_formula: "Fit * 0.4 + Readiness * 0.3 + MENA * 0.3"
```

Adjust the weights as needed (must sum to 1.0).

### GTM MENA Viability Scores

In `eo-config/gtm-config.md`, each motion has a `mena_viability` score (1-5):

```yaml
- id: dream100
  name: "Dream 100"
  mena_viability: 4.5  # ← Change this
```

Higher = more viable in MENA markets.

---

## How to Change AI Analysis

### What to Edit

The SKILL.md files are the system prompts sent to Claude. They control:
- Analysis tone and depth
- What recommendations Claude gives
- Output JSON structure
- Framework references

### Example: Change MAS Analysis

1. Open `market-attractiveness-scoring/SKILL.md`
2. Edit the analysis instructions, rubrics, or output format
3. Save the file
4. The very next assessment submission will use the updated prompt (n8n reads the SKILL.md content fresh each time via the system prompt embedded in the workflow)

**Important:** The SKILL.md content is embedded directly in the n8n workflow Code nodes as the Claude system prompt. If you edit SKILL.md on disk, you also need to update the corresponding n8n workflow's "BuildPrompt" or "ClaudeAPI" node to reference the new content. The simplest approach is to update the system prompt string in the n8n Code node.

### Output Format

Claude returns JSON. If you change the expected output fields, update:
1. The SKILL.md instructions for what JSON to return
2. The n8n "ProcessResults" Code node that parses Claude's response
3. The Dashboard HTML `renderAIAnalysis()` function if it displays those fields

---

## How to Change Readiness Bands

In `eo-config/consolidated-config.md`:

```yaml
bands:
  - id: LAUNCH_READY
    name: "Launch Ready"
    min_score: 80
    max_score: 100
    color: "#22C55E"
    tag: "eo-readiness-strong"
    action: "Full speed ahead. Execute primary GTM motions. Scale."
```

You can change:
- `min_score` / `max_score` — Band boundaries
- `name` — Display name
- `color` — Hex color for UI
- `action` — Recommendation text
- `tag` — GHL tag name (also update in GHL if tag name changes)

---

## How to Add/Remove an Assessment Section

### Adding a Section

1. Add the section definition in the config file under `sections:`
2. Add questions for that section under `questions:`
3. Update `total_points` to include the new section's `max_score`
4. Update `questions_count` in the metadata
5. Update the n8n workflow's score calculation Code node
6. Update the HTML rendering if sections are hardcoded

### Removing a Section

1. Remove the section from `sections:` and its questions from `questions:`
2. Update `total_points` and `questions_count`
3. Update the n8n score calculation
4. Update HTML rendering

---

## GHL Custom Fields Reference

| Field ID | Key | Type | Description |
|----------|-----|------|-------------|
| `yyat2W4IqrAf9piY3Fjf` | eo_strategy_path | TEXT | Primary strategy path |
| `hYwk45eyboKv43LGFrvx` | eo_strategy_path_score | NUMERICAL | Strategy path fit % |
| `0eH1C0RfGHeKflRrnpC3` | eo_mas_score | NUMERICAL | MAS total (0-100) |
| `SfquJFPKxRrvXJZ5Hre4` | eo_mas_band | TEXT | MAS band name |
| `aHCQXBpGmjFQNjZLtDAz` | eo_icp_score | NUMERICAL | ICP total (0-100) |
| `wbIfncEgUeiULTTp2QxC` | eo_icp_band | TEXT | ICP band name |
| `vtyYvMOpUmWiQF2mx23v` | eo_gtm_score | NUMERICAL | GTM total (0-100) |
| `Ongo4W7Ddj68Pdl2zwqP` | eo_gtm_band | TEXT | GTM band name |
| `t6VEmEglBtOsMepK1rQV` | eo_readiness_score | NUMERICAL | Readiness (0-100) |
| `M14oG4bt9YnuJR1CQ6j1` | eo_readiness_band | TEXT | Readiness band name |
| `AXAJ4DEKuHIv85dFnmSM` | eo_assessment_date | TEXT | Last assessment date |
| `MvjDBGzlLVtO3urq42vG` | eo_bottleneck | TEXT | Bottleneck pillar |
| `9XltCYGMAw1Q2dlTjKUV` | eo_matrix_position | TEXT | Matrix quadrant |

---

## GHL Tags Reference

### Strategy Tags
| Tag | ID |
|-----|----|
| eo-strategy-assessed | `py9DKFSCD4sXmMTZBWSS` |
| eo-path-replicate | `4WrcWo9NMdzD7tgnOkXB` |
| eo-path-consulting | `nsNDV93z14ohYkXmdbaE` |
| eo-path-boring | `boEs0Rj1LpUKCh1oGhsE` |
| eo-path-hammering | `jWmXpwCw9q9RGp9CWPmi` |

### MAS Band Tags
| Tag | ID |
|-----|----|
| eo-mas-assessed | `PlelxlC3F3jiikwDvsYZ` |
| eo-mas-strong | `m320s50YQK99I8vcPO3Z` |
| eo-mas-viable | `ghyzROEs4BHRGHSdnRts` |
| eo-mas-weak | `jKakbqAGWdy7mvs10xbF` |
| eo-mas-risk | `2LFjyT6q4Mxt71Z12QSx` |

### ICP Band Tags
| Tag | ID |
|-----|----|
| eo-icp-assessed | `XmweCoofcN55vBK6KXUH` |
| eo-icp-clear | `B6gmLeqOYd5Z5JGab5YH` |
| eo-icp-decent | `pTx29yS1ue8uKnaKr627` |
| eo-icp-fuzzy | `bUiqLEkMRIQp84TCpDu9` |
| eo-icp-none | `Q6vdaLvvOOiI0mvWEOh8` |

### GTM Band Tags
| Tag | ID |
|-----|----|
| eo-gtm-assessed | `yqqX7XDhtlTl2G4S3ULf` |
| eo-gtm-elite | `WZpVdGyxn2z4XfbzJr75` |
| eo-gtm-strong | `oCLqRccowaCc37veUEUt` |
| eo-gtm-emerging | `SK54tyaEqiT0uMgpul3s` |
| eo-gtm-weak | `4Wh8odlENZwLVUSa2PzT` |

### Readiness & Completion Tags
| Tag | ID |
|-----|----|
| eo-full-assessed | `JYBJ9NPRVWlmQPh2IiIr` |
| eo-readiness-strong | `PvorQFF3McHftjJzO5ME` |
| eo-readiness-viable | `m69s8u72EN0blpYk29Bz` |
| eo-readiness-weak | `do8F7FES6AM1WPCXzVWF` |
| eo-readiness-risk | `sPQKNjKLgmtkjLt18Fzg` |

### Bottleneck Tags
| Tag | ID |
|-----|----|
| eo-bottleneck-market | `984xRg2ks4USkuvvfH9q` |
| eo-bottleneck-icp | `fQPej5zvtvSIPZ7Nhhh5` |
| eo-bottleneck-gtm | `z73fyHmMmrk4PHO6dfoF` |

---

## Supabase Database Reference

### Table: `eo_assessments`

| Column | Type | Description |
|--------|------|-------------|
| id | uuid | Auto-generated primary key |
| assessment_type | text | `strategy_selector`, `mas`, `icp`, `gtm`, `consolidated` |
| contact_name | text | User's name |
| contact_email | text | User's email (lookup key) |
| contact_company | text | User's company |
| total_score | integer | Assessment score (0-100) |
| score_percentage | numeric | Score as decimal |
| band | text | Band assignment |
| section_scores | jsonb | Per-section score breakdown |
| ai_recommendations | jsonb | Claude's full analysis |
| ai_key_insight | text | Claude's one-line insight |
| matrix_position | text | Demand-First Matrix quadrant |
| raw_answers | jsonb | Original answers submitted |
| created_at | timestamptz | When record was created |
| updated_at | timestamptz | When record was last updated |

### View: `eo_founder_readiness`

Pivots the `eo_assessments` table by `contact_email`, pulling the latest MAS, ICP, and GTM scores into a single row. Calculates `founder_readiness_score` using the formula: `(mas * 0.35) + (icp * 0.35) + (gtm * 0.30)`.

---

## Testing After Changes

### Quick Smoke Test

1. Open the modified assessment HTML in a browser
2. Complete the assessment with test answers
3. Submit and verify:
   - n8n workflow executes (check n8n execution log)
   - GHL contact is created/updated with correct fields and tags
   - Supabase record is inserted (check via SQL: `SELECT * FROM eo_assessments ORDER BY created_at DESC LIMIT 1`)
   - Response displays correctly in the frontend

### Dashboard Test

1. Open `EO-Assessment-Dashboard.html`
2. Click "My Scorecard"
3. Enter a test email that has assessment records
4. Click "Fetch My Scores"
5. Verify scores populate, radar chart renders, matrix highlights correct quadrant

### Full Pipeline Test

1. Complete all 4 assessments (Strategy + MAS + ICP + GTM) with the same email
2. After the 3rd scored assessment (MAS/ICP/GTM), the consolidated workflow should auto-trigger
3. Check GHL contact has `eo-full-assessed` tag and readiness score
4. Load the Dashboard with that email and verify AI analysis sections appear

---

## Troubleshooting

### "Webhook returned an error"

- Check n8n workflow is **active** (green toggle)
- Check n8n execution log for the specific error
- Common cause: Anthropic API key is invalid or missing (`YOUR_ANTHROPIC_API_KEY_HERE` placeholder needs to be replaced with a real key)

### "No scores found" on Dashboard

- Verify the email matches exactly (case-sensitive)
- Check Supabase has records for that email: `SELECT * FROM eo_assessments WHERE contact_email = 'test@example.com'`
- Check the consolidated webhook is active

### Assessment scores look wrong

- Verify section `max_score` values in config add up to `total_points`
- Check n8n score calculation Code node matches config formulas
- Look at `section_scores` in Supabase to identify which section is off

### Claude analysis is empty or wrong

- Check the Anthropic API key is valid
- Check the SKILL.md content in the n8n workflow's system prompt
- Check n8n execution data for the Claude API response (look for error messages)
- Claude model ID should be `claude-sonnet-4-5-20250929`

### GHL contact not updating

- Verify GHL API key is valid (`pit-524c6c6b-...`)
- Check custom field IDs match the table above
- Check tag IDs match the table above
- Verify location ID is `UNw9DraGO3eyEa5l4lkJ`

### Anthropic API Key Setup

The n8n workflows contain a placeholder `YOUR_ANTHROPIC_API_KEY_HERE`. To activate AI analysis:

1. Get an API key from `console.anthropic.com`
2. In each n8n workflow (MAS, ICP, GTM, Consolidated), find the "ClaudeAPI" HTTP Request node
3. Replace the placeholder in the `x-api-key` header with your real key
4. Save and test

---

## Assessment Flow Summary

```
Strategy Selector (7 questions)
    → Determines best business path
    → Tags: eo-strategy-assessed + eo-path-{path}

Market Attractiveness (20 questions)
    → Scores market opportunity (0-100)
    → Tags: eo-mas-assessed + eo-mas-{band}
    → Claude AI: key insight + recommendations

ICP Clarity (20 questions)
    → Scores buyer clarity (0-100)
    → Tags: eo-icp-assessed + eo-icp-{band}
    → Claude AI: key insight + recommendations

GTM Fitness (14 questions)
    → Scores go-to-market readiness (0-100)
    → Tags: eo-gtm-assessed + eo-gtm-{band}
    → Claude AI: motion rankings + recommendations

Consolidated (auto-triggered when MAS + ICP + GTM complete)
    → Calculates weighted readiness score
    → Identifies bottleneck pillar
    → Determines archetype + matrix position
    → Tags: eo-full-assessed + eo-readiness-{band} + eo-bottleneck-{pillar}
    → Claude AI: cross-pillar analysis + 90-day plan
```
