# EO Assessment System: n8n Integration Architecture

**Document Version:** 2.0 (Supabase + Claude Code Build)
**Last Updated:** February 2026
**Purpose:** Complete technical blueprint for integrating the 3 EO Assessment tools with n8n workflows and Claude AI intelligence

---

## 1. SYSTEM OVERVIEW

The EO Assessment System operates as a three-layer architecture designed to deliver AI-powered founder readiness scoring and personalized improvement recommendations.

### Architecture Layers

```
┌─────────────────────────────────────────────────────────────────┐
│ LAYER 1: FRONTEND (Questionnaire UIs)                           │
│ • Market Attractiveness Scoring (MAS)                           │
│ • ICP Clarity Scoring (ICP)                                     │
│ • GTM Fitness Scoring (GTM)                                     │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ↓ POST assessment answers + contact info
┌─────────────────────────────────────────────────────────────────┐
│ LAYER 2: BACKEND ORCHESTRATION (n8n Workflows)                 │
│ • Webhook receivers (3 assessment endpoints)                    │
│ • Score calculation engine                                      │
│ • Claude API orchestration                                      │
│ • Data validation & transformation                              │
│ • Integration dispatcher                                        │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ↓ System prompt + validated answers
┌─────────────────────────────────────────────────────────────────┐
│ LAYER 3: INTELLIGENCE ENGINE (Claude AI + Skills)              │
│ • MAS Skill (scoring rubric + recommendations)                 │
│ • ICP Skill (clarity framework + buyer persona analysis)       │
│ • GTM Skill (go-to-market strategy + market positioning)       │
│ • Consolidated analysis (holistic founder readiness)           │
└────────────────┬────────────────────────────────────────────────┘
                 │
                 ↓ Structured analysis + recommendations
┌─────────────────────────────────────────────────────────────────┐
│ LAYER 4: DATA & AUTOMATION (GHL, Supabase, Instantly, HeyReach)│
│ • Contact creation & scoring tags                              │
│ • Pipeline segmentation                                        │
│ • Nurture sequence activation                                  │
│ • LinkedIn outreach campaigns                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Complete Request-Response Flow

```
[Founder loads MAS questionnaire]
    ↓
[Fills 20-question assessment]
    ↓
[Clicks "Get My Score"]
    ↓
[Web app calculates section scores]
    ↓
[Web app POSTs to webhook: /webhook/eo-mas-score]
    ↓
n8n Workflow:
    • Node 1: Validate webhook payload
    • Node 2: Calculate raw section scores
    • Node 3: Call Claude API with MAS skill as system prompt
    • Node 4: Parse Claude's analysis
    • Node 5: Create/update GHL contact + apply tags
    • Node 6: Store results in Supabase
    • Node 7: Format response for web app
    • Node 8: Return JSON to webhook
    • Node 9: Schedule follow-up emails
    ↓
[Web app receives structured results]
    ↓
[Renders personalized score band + recommendations]
    ↓
[Shows "Email me full analysis" CTA]
    ↓
[Founder enters email → stored in GHL]
    ↓
n8n Trigger:
    • Check if all 3 assessments completed
    • If yes: Run consolidated workflow
    • Send nurture sequence emails
    • Add to appropriate pipeline
    ↓
[GHL automation]
    • Tag contact with score bands
    • Create assessment opportunity
    • Trigger email sequence
    ↓
[Optionally: Add to Instantly, HeyReach campaigns]
```

---

## 2. WEBHOOK ENDPOINTS (Three Assessment Workflows)

### Workflow 1: Market Attractiveness Scoring (MAS) Assessment

**Webhook Details:**
- **URL:** `{n8n_base_url}/webhook/eo-mas-score`
- **Method:** POST
- **Authentication:** Bearer token in header (optional but recommended)
- **Response Time:** 3-5 seconds typical

**Request Payload Schema:**

```json
{
  "assessment": "market-attractiveness",
  "answers": {
    "pain_specificity": 4,
    "pain_frequency": 5,
    "pain_quantification": 3,
    "current_workarounds": 4,
    "pain_urgency": 3,
    "budget_authority": 4,
    "price_sensitivity": 3,
    "procurement_friction": 2,
    "buyer_consensus": 5,
    "willingness_to_change": 4,
    "switching_cost": 2,
    "market_size_awareness": 4,
    "market_growth_awareness": 3,
    "competitive_awareness": 3,
    "timing_readiness": 4,
    "macro_tailwinds": 3,
    "regulatory_tailwinds": 2,
    "technology_tailwinds": 4,
    "founder_timing": 5,
    "team_timing": 3
  },
  "contact": {
    "name": "Sarah Chen",
    "email": "sarah.chen@example.com",
    "company": "TechStartup Inc",
    "phone": "+1-555-0123",
    "title": "Co-Founder & CEO",
    "linkedin_url": "https://linkedin.com/in/sarahchen"
  },
  "metadata": {
    "timestamp": "2026-02-25T14:30:00Z",
    "source": "eo-web-app",
    "version": "1.0",
    "session_id": "sess_abc123def456"
  }
}
```

**Expected Response:**

```json
{
  "success": true,
  "assessment_id": "mas_20260225_001",
  "contact_id": "contact_ghl_12345",
  "results": {
    "score": {
      "total": 72,
      "band": "VIABLE",
      "sections": {
        "pain_reality": {
          "score": 19,
          "max": 25,
          "band": "good",
          "percentile": 76
        },
        "purchasing_power": {
          "score": 15,
          "max": 25,
          "band": "moderate",
          "percentile": 60
        },
        "market_timing": {
          "score": 18,
          "max": 25,
          "band": "good",
          "percentile": 72
        },
        "founder_timing": {
          "score": 20,
          "max": 25,
          "band": "excellent",
          "percentile": 80
        }
      }
    },
    "recommendations": [
      {
        "section": "purchasing_power",
        "priority": 1,
        "title": "Build Trust in Buying Process",
        "description": "Your target buyers are slightly skeptical of vendors. Implement customer success stories and case studies to reduce perceived risk.",
        "impact": "Potential +4 points on purchasing_power section",
        "timeline": "30 days"
      },
      {
        "section": "pain_reality",
        "priority": 2,
        "title": "Document Quantified Pain Points",
        "description": "While you've identified the pain, get specific numbers: 'We waste 15 hours per week' vs 'We waste time'. This improves perceived solution value.",
        "impact": "Potential +3 points on pain_reality section",
        "timeline": "14 days"
      }
    ],
    "roadmap": {
      "days_1_7": [
        "Interview 5 power users about quantified pain metrics",
        "Create 2 customer case studies with before/after numbers",
        "Map decision-making unit (who has budget authority)"
      ],
      "days_8_14": [
        "Test messaging with 3 target buyers (adjust based on feedback)",
        "Build trust signals page on website",
        "Document competitive differentiation"
      ],
      "days_15_30": [
        "Run proof-of-concept with early adopter",
        "Gather testimonials & quotes for sales collateral",
        "Calculate ROI model for target segment"
      ]
    },
    "ai_insights": "Your market has strong tailwinds (AI/automation adoption), but your buyer has low procurement authority. This is your bottleneck. Focus on finding the economic buyer (usually Operations or Finance) rather than the user buyer. Once you know who controls budget, your pain reality score will jump significantly.",
    "matrix_position": "BUILD_LEARN",
    "next_steps": [
      "Complete ICP Clarity assessment (3-5 min)",
      "Complete GTM Fitness assessment (2 min)",
      "Book a 30-minute strategy call to discuss results"
    ]
  },
  "timestamps": {
    "received_at": "2026-02-25T14:30:05Z",
    "processed_at": "2026-02-25T14:30:08Z",
    "ai_analysis_completed_at": "2026-02-25T14:30:12Z"
  }
}
```

---

### Workflow 2: ICP Clarity Assessment

**Webhook Details:**
- **URL:** `{n8n_base_url}/webhook/eo-icp-score`
- **Method:** POST
- **Answer Fields:** 20 questions about target buyer clarity

**Request Payload Schema:**

```json
{
  "assessment": "icp-clarity",
  "answers": {
    "buyer_role_clarity": 5,
    "industry_focus": 4,
    "company_size_range": 4,
    "geographic_scope": 3,
    "revenue_range": 3,
    "growth_stage": 4,
    "pain_point_clarity": 5,
    "success_metrics": 4,
    "buying_timeline": 3,
    "decision_process": 4,
    "stakeholder_map": 3,
    "budget_cycle": 2,
    "existing_solution_use": 4,
    "switching_triggers": 4,
    "competitor_awareness": 3,
    "value_perception": 4,
    "implementation_readiness": 3,
    "support_expectations": 3,
    "contract_preferences": 2,
    "pricing_sensitivity": 3,
    "expansion_potential": 4
  },
  "contact": {
    "name": "Sarah Chen",
    "email": "sarah.chen@example.com",
    "company": "TechStartup Inc"
  },
  "metadata": {
    "timestamp": "2026-02-25T14:35:00Z",
    "source": "eo-web-app",
    "version": "1.0"
  }
}
```

**Expected Response Structure:** Same as MAS, with ICP-specific sections:
- Buyer Profile Clarity
- Buying Journey Understanding
- Economic Model Knowledge
- Expansion & Retention Potential

---

### Workflow 3: GTM Fitness Assessment

**Webhook Details:**
- **URL:** `{n8n_base_url}/webhook/eo-gtm-score`
- **Method:** POST
- **Answer Fields:** 14 questions + motion score calculations

**Request Payload Schema:**

```json
{
  "assessment": "gtm-fitness",
  "answers": {
    "positioning_clarity": 4,
    "messaging_resonance": 3,
    "channel_strategy": 4,
    "sales_motion": 4,
    "sales_enablement": 3,
    "pipeline_generation": 3,
    "pipeline_conversion": 4,
    "customer_acquisition_cost": 3,
    "customer_lifetime_value": 4,
    "unit_economics": 3,
    "marketing_brand_presence": 3,
    "partnership_leverage": 2,
    "distribution_network": 3,
    "market_penetration": 3
  },
  "motion_scores": {
    "inbound_motion_score": 35,
    "outbound_motion_score": 42,
    "partnership_motion_score": 28
  },
  "contact": {
    "name": "Sarah Chen",
    "email": "sarah.chen@example.com",
    "company": "TechStartup Inc"
  },
  "metadata": {
    "timestamp": "2026-02-25T14:40:00Z",
    "source": "eo-web-app",
    "version": "1.0"
  }
}
```

---

## 3. n8n WORKFLOW NODE ARCHITECTURE

Each assessment workflow follows this standardized node structure. Below is the complete implementation guide for the **MAS Assessment Workflow** (ICP and GTM follow the same pattern).

### Node 1: Webhook Trigger

**Configuration:**
- **Node Type:** Webhook
- **Method:** POST
- **Full Path:** `/eo-mas-score`
- **Response Mode:** "Using 'Respond to Webhook' node"
- **Authentication:** None (or JWT if desired)

**Purpose:** Listen for incoming assessment submissions

```
Node 1: Webhook Trigger
├── Wait for POST request
├── Extract JSON payload
├── Pass to Node 2
```

---

### Node 2: Payload Validation

**Node Type:** Code (JavaScript)

**Purpose:** Validate incoming data structure and transform for processing

**Implementation:**

```javascript
// Node 2: Validate Assessment Payload
const payload = $input.first().json;

// Validate required fields
const errors = [];

if (!payload.assessment) errors.push("Missing 'assessment' field");
if (!payload.answers || typeof payload.answers !== 'object') errors.push("Missing or invalid 'answers'");
if (!payload.contact || !payload.contact.email) errors.push("Missing contact email");

// Validate answer structure (20 questions for MAS)
const answerCount = Object.keys(payload.answers).length;
if (answerCount !== 20) {
  errors.push(`Expected 20 answers, got ${answerCount}`);
}

// Validate answer values are 0-5
Object.entries(payload.answers).forEach(([key, value]) => {
  if (typeof value !== 'number' || value < 0 || value > 5) {
    errors.push(`Invalid score for ${key}: ${value}`);
  }
});

if (errors.length > 0) {
  return {
    valid: false,
    errors: errors,
    statusCode: 400
  };
}

return {
  valid: true,
  assessment: payload.assessment,
  answers: payload.answers,
  contact: payload.contact,
  metadata: payload.metadata,
  statusCode: 200
};
```

---

### Node 3: Calculate Raw Scores

**Node Type:** Code (JavaScript)

**Purpose:** Calculate section totals and overall score from individual answers

**Implementation:**

```javascript
// Node 3: Calculate MAS Scores
const { answers, contact } = $input.first().json;

// Define section groupings
const sections = {
  pain_reality: ['pain_specificity', 'pain_frequency', 'pain_quantification', 'current_workarounds', 'pain_urgency'],
  purchasing_power: ['budget_authority', 'price_sensitivity', 'procurement_friction', 'buyer_consensus', 'willingness_to_change', 'switching_cost'],
  market_timing: ['market_size_awareness', 'market_growth_awareness', 'competitive_awareness', 'timing_readiness'],
  founder_timing: ['macro_tailwinds', 'regulatory_tailwinds', 'technology_tailwinds', 'founder_timing', 'team_timing']
};

// Calculate section scores
const sectionScores = {};
const sectionMaxes = {};

Object.entries(sections).forEach(([section, fields]) => {
  const total = fields.reduce((sum, field) => sum + answers[field], 0);
  const max = fields.length * 5;
  sectionScores[section] = total;
  sectionMaxes[section] = max;
});

// Calculate overall score
const totalScore = Object.values(sectionScores).reduce((sum, score) => sum + score, 0);
const maxScore = Object.values(sectionMaxes).reduce((sum, max) => sum + max, 0);
const scorePercentage = (totalScore / maxScore) * 100;

// Determine band
let band = 'RISK';
if (scorePercentage >= 80) band = 'STRONG';
else if (scorePercentage >= 60) band = 'VIABLE';
else if (scorePercentage >= 40) band = 'WEAK';

return {
  answers: answers,
  contact: contact,
  rawScores: {
    total: totalScore,
    percentage: scorePercentage,
    band: band,
    sections: sectionScores,
    sectionMaxes: sectionMaxes
  },
  timestamp: new Date().toISOString()
};
```

---

### Node 4: Claude API Call

**Node Type:** HTTP Request

**Purpose:** Call Claude Sonnet with the assessment skill as system prompt

**Configuration:**

- **Method:** POST
- **URL:** `https://api.anthropic.com/v1/messages`
- **Authentication:** API Key (stored in n8n credentials)
- **Headers:**
  ```
  Content-Type: application/json
  x-api-key: {{$credentials.anthropicApi.apiKey}}
  anthropic-version: 2023-06-01
  ```

**Body (JSON):**

```json
{
  "model": "claude-sonnet-4-5-20250929",
  "max_tokens": 4000,
  "system": "You are the EO Market Attractiveness Scoring (MAS) engine. Your role is to analyze founder assessments and provide actionable recommendations for improving market opportunity readiness.\n\n[FULL MAS SKILL.md CONTENT INSERTED HERE]\n\nWhen you receive assessment answers, you will:\n1. Validate the scores and identify the strongest and weakest sections\n2. Provide 2-3 specific, actionable recommendations prioritized by impact\n3. Create a 30-day improvement roadmap\n4. Share a key insight unique to this founder's situation\n\nFormat your response as valid JSON.",
  "messages": [
    {
      "role": "user",
      "content": "Please analyze this MAS assessment and provide scoring analysis and recommendations.\n\nAssessment Answers:\n{{$input.first().json.answers}}\n\nRaw Calculated Scores:\n- Pain Reality: {{$input.first().json.rawScores.sections.pain_reality}}/{{$input.first().json.rawScores.sectionMaxes.pain_reality}}\n- Purchasing Power: {{$input.first().json.rawScores.sections.purchasing_power}}/{{$input.first().json.rawScores.sectionMaxes.purchasing_power}}\n- Market Timing: {{$input.first().json.rawScores.sections.market_timing}}/{{$input.first().json.rawScores.sectionMaxes.market_timing}}\n- Founder Timing: {{$input.first().json.rawScores.sections.founder_timing}}/{{$input.first().json.rawScores.sectionMaxes.founder_timing}}\n\nFull Score: {{$input.first().json.rawScores.total}}/{{$input.first().json.rawScores.sectionMaxes | Object.values}}\n\nContact: {{$input.first().json.contact.name}} at {{$input.first().json.contact.company}}\n\nPlease provide:\n1. Validation of the scores (are they correctly calculated?)\n2. Your top 2-3 recommendations, prioritized by estimated impact\n3. A 30-day roadmap with weekly milestones\n4. One key insight unique to this founder's situation\n\nReturn your analysis as JSON with keys: validatedScores, recommendations, roadmap, keyInsight, matrixPosition"
    }
  ]
}
```

**Alternative: Using n8n Code Node for Claude Call**

If you prefer to control the Claude call within JavaScript:

```javascript
// Node 4: Call Claude AI for MAS Analysis
const { answers, contact, rawScores } = $input.first().json;

const anthropicApiKey = process.env.ANTHROPIC_API_KEY;
const masSkillPrompt = `[FULL MAS SKILL.md CONTENT]`;

const payload = {
  model: "claude-sonnet-4-5-20250929",
  max_tokens: 4000,
  system: `${masSkillPrompt}\n\nYou are analyzing a founder's market attractiveness. Return valid JSON with keys: recommendations (array), roadmap (object), keyInsight (string), matrixPosition (string).`,
  messages: [
    {
      role: "user",
      content: `Analyze this MAS assessment:\nAnswers: ${JSON.stringify(answers)}\nRaw Scores: ${JSON.stringify(rawScores)}\nFounder: ${contact.name} at ${contact.company}\n\nProvide recommendations, roadmap, insight, and matrix position.`
    }
  ]
};

const response = await $http.request({
  method: 'POST',
  url: 'https://api.anthropic.com/v1/messages',
  headers: {
    'Content-Type': 'application/json',
    'x-api-key': anthropicApiKey,
    'anthropic-version': '2023-06-01'
  },
  body: payload
});

// Extract Claude's response
const claudeText = response.content[0].text;

// Parse JSON response
let aiAnalysis;
try {
  aiAnalysis = JSON.parse(claudeText);
} catch (e) {
  // If Claude didn't return valid JSON, extract key points manually
  aiAnalysis = {
    recommendations: [],
    roadmap: {},
    keyInsight: claudeText,
    matrixPosition: 'BUILD_LEARN'
  };
}

return {
  ...aiAnalysis,
  rawResponse: claudeText,
  timestamp: new Date().toISOString()
};
```

---

### Node 5: Parse Claude Response

**Node Type:** Code (JavaScript)

**Purpose:** Extract structured data from Claude's analysis

```javascript
// Node 5: Parse Claude Response
const { rawScores, contact } = $input.first().json;
let aiData = {};

try {
  const responseText = $input.items[0].json.rawResponse || $input.items[0].json.text || '';

  // Try to extract JSON from Claude's response
  const jsonMatch = responseText.match(/\{[\s\S]*\}/);
  if (jsonMatch) {
    aiData = JSON.parse(jsonMatch[0]);
  }
} catch (e) {
  console.log("Could not parse Claude response as JSON");
  aiData = {
    recommendations: [],
    roadmap: { week1: [], week2: [], week3: [], week4: [] },
    keyInsight: "Assessment complete",
    matrixPosition: "BUILD_LEARN"
  };
}

return {
  contact: contact,
  rawScores: rawScores,
  aiAnalysis: aiData,
  timestamp: new Date().toISOString()
};
```

---

### Node 6: GHL Integration (Create/Update Contact)

**Node Type:** HTTP Request

**Purpose:** Create or update contact in GoHighLevel with assessment results and tags

**Configuration:**

- **Method:** POST
- **URL:** `https://rest.gohighlevel.com/v1/contacts/` (or PUT for update)
- **Headers:**
  ```
  Content-Type: application/json
  Authorization: Bearer {{$credentials.ghlApi.accessToken}}
  ```

**Body (Create New Contact):**

```json
{
  "firstName": "{{$input.first().json.contact.name.split(' ')[0]}}",
  "lastName": "{{$input.first().json.contact.name.split(' ').slice(1).join(' ')}}",
  "email": "{{$input.first().json.contact.email}}",
  "phone": "{{$input.first().json.contact.phone}}",
  "companyName": "{{$input.first().json.contact.company}}",
  "customFields": {
    "eo_mas_score": "{{$input.first().json.rawScores.total}}",
    "eo_mas_band": "{{$input.first().json.rawScores.band}}",
    "eo_assessment_date": "{{$input.first().json.timestamp}}",
    "eo_pain_reality": "{{$input.first().json.rawScores.sections.pain_reality}}",
    "eo_purchasing_power": "{{$input.first().json.rawScores.sections.purchasing_power}}",
    "eo_market_timing": "{{$input.first().json.rawScores.sections.market_timing}}",
    "eo_founder_timing": "{{$input.first().json.rawScores.sections.founder_timing}}"
  },
  "tags": [
    "eo-assessed",
    "eo-mas-assessed",
    "eo-mas-{{$input.first().json.rawScores.band | lower}}",
    "eo-assessment-{{$input.first().json.timestamp | toDate | 'yyyy-MM'}}"
  ]
}
```

---

### Node 7: Supabase Integration (Store Results)

**Node Type:** Supabase (native n8n node) or HTTP Request

**Purpose:** Store full assessment data in Postgres for analytics, cohort analysis, and historical tracking

**Supabase Setup:**

1. Create project at https://supabase.com (free tier: 500MB, 50K rows)
2. Create table `eo_assessments` with this SQL:

```sql
CREATE TABLE eo_assessments (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  assessment_type TEXT NOT NULL CHECK (assessment_type IN ('mas', 'icp', 'gtm')),
  contact_name TEXT NOT NULL,
  contact_email TEXT NOT NULL,
  contact_company TEXT,
  total_score INTEGER NOT NULL,
  score_percentage DECIMAL(5,2),
  band TEXT NOT NULL,
  section_scores JSONB NOT NULL,
  ai_recommendations JSONB,
  ai_key_insight TEXT,
  matrix_position TEXT,
  raw_answers JSONB NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Index for fast lookups by email (cross-assessment queries)
CREATE INDEX idx_assessments_email ON eo_assessments(contact_email);
CREATE INDEX idx_assessments_type ON eo_assessments(assessment_type);
CREATE INDEX idx_assessments_band ON eo_assessments(band);

-- Consolidated view for dashboard queries
CREATE VIEW eo_founder_readiness AS
SELECT
  contact_email,
  contact_name,
  contact_company,
  MAX(CASE WHEN assessment_type = 'mas' THEN total_score END) AS mas_score,
  MAX(CASE WHEN assessment_type = 'mas' THEN band END) AS mas_band,
  MAX(CASE WHEN assessment_type = 'icp' THEN total_score END) AS icp_score,
  MAX(CASE WHEN assessment_type = 'icp' THEN band END) AS icp_band,
  MAX(CASE WHEN assessment_type = 'gtm' THEN total_score END) AS gtm_score,
  MAX(CASE WHEN assessment_type = 'gtm' THEN band END) AS gtm_band,
  COUNT(DISTINCT assessment_type) AS assessments_completed,
  CASE WHEN COUNT(DISTINCT assessment_type) = 3 THEN
    ROUND(
      (MAX(CASE WHEN assessment_type = 'mas' THEN score_percentage END) * 0.35) +
      (MAX(CASE WHEN assessment_type = 'icp' THEN score_percentage END) * 0.35) +
      (MAX(CASE WHEN assessment_type = 'gtm' THEN score_percentage END) * 0.30),
    1)
  END AS founder_readiness_score
FROM eo_assessments
GROUP BY contact_email, contact_name, contact_company;
```

**n8n Configuration (Supabase Node):**

- **Credentials:** Supabase API (Project URL + Service Role Key)
- **Operation:** Insert
- **Table:** eo_assessments

**Request Body (if using HTTP Request node):**

```javascript
// Node 7: Store in Supabase via REST API
const data = $input.first().json;
const { contact, rawScores, aiAnalysis, answers } = data;

const supabaseUrl = process.env.SUPABASE_URL;
const supabaseKey = process.env.SUPABASE_SERVICE_KEY;

const record = {
  assessment_type: 'mas',
  contact_name: contact.name,
  contact_email: contact.email,
  contact_company: contact.company || '',
  total_score: rawScores.total,
  score_percentage: rawScores.percentage,
  band: rawScores.band,
  section_scores: rawScores.sections,
  ai_recommendations: aiAnalysis.recommendations || [],
  ai_key_insight: aiAnalysis.keyInsight || '',
  matrix_position: aiAnalysis.matrixPosition || 'BUILD_LEARN',
  raw_answers: answers
};

const response = await $http.request({
  method: 'POST',
  url: `${supabaseUrl}/rest/v1/eo_assessments`,
  headers: {
    'Content-Type': 'application/json',
    'apikey': supabaseKey,
    'Authorization': `Bearer ${supabaseKey}`,
    'Prefer': 'return=representation'
  },
  body: record
});

return { ...data, supabase_id: response[0].id };
```

---

### Node 8: Format Response for Web App

**Node Type:** Code (JavaScript)

**Purpose:** Transform internal data into web-app-friendly JSON structure

```javascript
// Node 8: Format Response
const data = $input.first().json;
const { contact, rawScores, aiAnalysis } = data;

const formattedResponse = {
  success: true,
  assessment: "market-attractiveness",
  contact: {
    name: contact.name,
    email: contact.email,
    company: contact.company
  },
  results: {
    score: {
      total: rawScores.total,
      percentage: Math.round(rawScores.percentage * 10) / 10,
      band: rawScores.band,
      sections: {
        pain_reality: {
          score: rawScores.sections.pain_reality,
          max: rawScores.sectionMaxes.pain_reality,
          percentage: Math.round((rawScores.sections.pain_reality / rawScores.sectionMaxes.pain_reality) * 100)
        },
        purchasing_power: {
          score: rawScores.sections.purchasing_power,
          max: rawScores.sectionMaxes.purchasing_power,
          percentage: Math.round((rawScores.sections.purchasing_power / rawScores.sectionMaxes.purchasing_power) * 100)
        },
        market_timing: {
          score: rawScores.sections.market_timing,
          max: rawScores.sectionMaxes.market_timing,
          percentage: Math.round((rawScores.sections.market_timing / rawScores.sectionMaxes.market_timing) * 100)
        },
        founder_timing: {
          score: rawScores.sections.founder_timing,
          max: rawScores.sectionMaxes.founder_timing,
          percentage: Math.round((rawScores.sections.founder_timing / rawScores.sectionMaxes.founder_timing) * 100)
        }
      }
    },
    recommendations: (aiAnalysis.recommendations || []).slice(0, 3).map(rec => ({
      section: rec.section,
      priority: rec.priority || 1,
      title: rec.title,
      description: rec.description,
      impact: rec.impact,
      timeline: rec.timeline
    })),
    roadmap: aiAnalysis.roadmap || {
      week1: [],
      week2: [],
      week3: [],
      week4: []
    },
    matrix_position: aiAnalysis.matrixPosition || 'BUILD_LEARN',
    ai_insights: aiAnalysis.keyInsight || '',
    next_steps: [
      'Complete ICP Clarity assessment (3-5 min)',
      'Complete GTM Fitness assessment (2 min)',
      'Email results to review recommendations'
    ]
  },
  metadata: {
    assessment_id: `mas_${Date.now()}`,
    processed_at: new Date().toISOString()
  }
};

return formattedResponse;
```

---

### Node 9: Webhook Response

**Node Type:** Respond to Webhook

**Purpose:** Send formatted results back to web app

**Configuration:**
- **Status Code:** 200
- **Response Body:**
  ```
  {{$input.first().json}}
  ```

---

### Node 10: Create GHL Opportunity

**Node Type:** HTTP Request

**Purpose:** Create assessment opportunity in GHL pipeline

**Configuration:**

- **Method:** POST
- **URL:** `https://rest.gohighlevel.com/v1/pipelines/{pipelineId}/opportunities`

**Body:**

```json
{
  "contactId": "{{$input.first().json.contact_id}}",
  "stageId": "{{$input.first().json.initialStageId}}",
  "title": "EO Assessment - {{$input.first().json.contact.name}}",
  "customFields": {
    "eo_mas_score": "{{$input.first().json.rawScores.total}}",
    "eo_assessment_band": "{{$input.first().json.rawScores.band}}",
    "assessment_type": "market-attractiveness",
    "assessment_date": "{{$input.first().json.timestamp}}"
  }
}
```

---

### Node 11: Schedule Follow-Up Emails

**Node Type:** Schedule (or Wait + Send via GHL)

**Purpose:** Trigger automated follow-up sequences

**Configuration:**

- **At 24 hours:** Send summary email
- **At 7 days:** Send follow-up reminder if assessments incomplete
- **At 30 days:** Send re-assessment prompt

---

## 4. CONSOLIDATED VIEW WORKFLOW

**Trigger:** Contact completes all 3 assessments

**Webhook URL:** `{n8n_base_url}/webhook/eo-consolidated`

**Nodes:**

1. **Check Assessment Status** — Verify contact has completed MAS, ICP, and GTM
2. **Fetch Scores from Supabase** — Query `eo_founder_readiness` view for all 3 scores
3. **Call Claude (Consolidated Mode)** — Pass all 3 assessments for holistic analysis
4. **Calculate Founder Readiness Score** — Formula: `(MAS × 0.35) + (ICP × 0.35) + (GTM × 0.30)`
5. **Map to Demand-First Matrix** — Position in "BUILD", "VALIDATE", "SCALE", "OPTIMIZE"
6. **Format Consolidated Results** — Return integrated analysis
7. **Update GHL with Overall Score** — Add tag `eo-full-assessed`, set overall band
8. **Send Consolidated Email** — Email founder full results + recommended training path

**Claude Prompt for Consolidated Analysis:**

```
You are analyzing a founder's overall readiness based on three assessments:

1. MARKET ATTRACTIVENESS (weight: 35%)
   - Score: {{MAS_TOTAL}}/100, Band: {{MAS_BAND}}
   - Pain Reality: {{pain_reality}}
   - Purchasing Power: {{purchasing_power}}
   - Market Timing: {{market_timing}}
   - Founder Timing: {{founder_timing}}

2. ICP CLARITY (weight: 35%)
   - Score: {{ICP_TOTAL}}/100, Band: {{ICP_BAND}}
   - Buyer Profile Clarity: {{buyer_clarity}}
   - Buying Journey Understanding: {{buying_journey}}
   - Economic Model Knowledge: {{economic_model}}
   - Expansion Potential: {{expansion}}

3. GTM FITNESS (weight: 30%)
   - Score: {{GTM_TOTAL}}/100, Band: {{GTM_BAND}}
   - Sales Motion: {{sales_motion}}
   - Channel Strategy: {{channels}}
   - Unit Economics: {{unit_economics}}
   - Market Penetration: {{market_penetration}}

Calculated Founder Readiness Score: {{OVERALL_SCORE}}/100

Please provide:
1. Overall assessment of readiness (is this founder ready to scale?)
2. Which pillar is strongest and should be leveraged?
3. Which pillar is the bottleneck (biggest improvement opportunity)?
4. Specific cross-pillar insights (e.g., strong market but unclear ICP)
5. Recommended EO training path based on all 3 scores
6. Go-to-market strategy recommendations
7. Timeline projection for reaching GTM stage readiness
```

---

## 5. LEAD MAGNET INTEGRATION

The assessment system serves as a lead magnet and founder onboarding tool.

### The Flow

1. **Discovery:** Founder finds assessment via:
   - LinkedIn post / ads
   - Landing page
   - Email sequence
   - Referred by friend

2. **Assessment:** Founder takes 5-10 minute questionnaire
   - No login required
   - Progress saved in browser
   - Instant score calculation on completion

3. **Email Gate:** To see full Claude AI analysis, founder enters email
   - n8n webhook triggered on submission
   - Claude generates recommendations
   - Results stored in GHL

4. **Delivery:** Email with full results
   - Score breakdown
   - Top 3 recommendations
   - 30-day roadmap
   - Key insights from Claude

5. **Segmentation:** Based on score band, founder is tagged in GHL:
   - **STRONG (80-100):** Add to VIP nurture, book strategy call
   - **VIABLE (60-79):** Add to standard nurture, promote bootcamp
   - **WEAK (40-59):** Add to educational sequence, free resources
   - **RISK (<40):** Add to fundamentals sequence, book consultation

6. **Nurture:** Based on all 3 assessments:
   - All 3 complete → Qualified prospect, schedule Free Hour
   - 1-2 complete → Reminder emails to complete others
   - Low overall score → Educational content before selling

---

## 6. CLAUDE API IMPLEMENTATION DETAILS

### Anthropic API Credentials in n8n

1. **Create API Key:** https://console.anthropic.com/api_keys
2. **In n8n:**
   - Go to Credentials
   - Create "Anthropic API" type (if using native credential type)
   - Or use Generic HTTP Request with header `x-api-key`

### Model Selection

**Recommended:** `claude-sonnet-4-5-20250929`
- Fast: ~1 second latency
- Capable: Excellent at structured output, reasoning
- Cost: ~$0.01-0.03 per assessment
- Input: 50,000 tokens
- Output: 40,000 tokens

**Alternative:** `claude-opus-4-6`
- Slower: ~2-3 seconds latency
- More capable: Better for complex analysis
- Cost: ~$0.03-0.05 per assessment
- Only use if Sonnet insufficient

### Token Budget

For a typical assessment:
- System prompt (with full SKILL.md): ~1,500 tokens
- User message (answers + context): ~800 tokens
- Claude response (analysis + recommendations): ~1,500 tokens
- **Total: ~3,800 tokens**
- Safe max_tokens setting: 4,000

### Error Handling

```javascript
// Node: Handle Claude API Errors
try {
  const response = await callClaude();
  return { success: true, data: response };
} catch (error) {
  if (error.status === 429) {
    // Rate limited — retry in 60 seconds
    return { retry: true, waitSeconds: 60 };
  }

  if (error.status === 401) {
    // Invalid API key
    return { error: 'API key invalid', statusCode: 401 };
  }

  // Fallback: Return basic analysis without Claude
  return {
    success: true,
    usedFallback: true,
    recommendations: [],
    keyInsight: 'Assessment scored successfully. Full AI analysis unavailable.'
  };
}
```

---

## 7. GHL TAG STRATEGY FOR SEGMENTATION

### Assessment Result Tags

**MAS Bands:**
- `eo-mas-strong` (80-100)
- `eo-mas-viable` (60-79)
- `eo-mas-weak` (40-59)
- `eo-mas-risk` (<40)

**ICP Bands:**
- `eo-icp-clear` (80-100)
- `eo-icp-decent` (60-79)
- `eo-icp-fuzzy` (40-59)
- `eo-icp-none` (<40)

**GTM Bands:**
- `eo-gtm-elite` (80-100)
- `eo-gtm-strong` (60-79)
- `eo-gtm-emerging` (40-59)
- `eo-gtm-weak` (<40)

### Completion & Readiness Tags

- `eo-assessed` — Completed at least 1 assessment
- `eo-mas-assessed` — Completed MAS
- `eo-icp-assessed` — Completed ICP
- `eo-gtm-assessed` — Completed GTM
- `eo-full-assessed` — Completed all 3
- `eo-readiness-strong` — Overall score 80-100
- `eo-readiness-viable` — Overall score 60-79
- `eo-readiness-weak` — Overall score 40-59
- `eo-readiness-risk` — Overall score <40

### Bottleneck Tags

Applied by consolidated workflow:
- `eo-bottleneck-market` — MAS is weakest area
- `eo-bottleneck-icp` — ICP is weakest area
- `eo-bottleneck-gtm` — GTM is weakest area

### Engagement Tags

- `eo-assessment-2026-02` — Date of assessment
- `eo-needs-follow-up` — Incomplete assessments
- `eo-ready-for-bootcamp` — Score >= 60 on all
- `eo-needs-coaching` — Score < 50 on any

### GHL Automation Rules

| Condition | Action |
|-----------|--------|
| Tag: `eo-full-assessed` AND `eo-readiness-strong` | Move to "Qualified" stage, book Free Hour |
| Tag: `eo-full-assessed` AND `eo-readiness-viable` | Send bootcamp promotion email |
| Tag: `eo-mas-assessed` AND NOT `eo-icp-assessed` (7 days) | Send reminder to complete ICP |
| Tag: `eo-readiness-risk` | Send educational content series |
| Tag: `eo-bottleneck-icp` | Email focused on customer clarity |

---

## 8. IMPLEMENTATION ROADMAP (Claude Code Same-Day Build)

> This build is designed for execution in a single session using Claude Code.
> Prerequisites: n8n instance running (cloud or self-hosted), Supabase project created, GHL API key ready, Anthropic API key ready.

### Phase 1: Infrastructure Setup (30 min)

**What Claude Code builds:**
- Supabase table creation (run SQL above via Supabase dashboard or CLI)
- n8n credential setup (Anthropic API, GHL API, Supabase API)
- Environment variables configured in n8n
- Webhook endpoints created and tested with curl

**Verification:**
- `curl -X POST {n8n_url}/webhook/eo-mas-score` returns 400 (expected, no payload)
- Supabase table exists and accepts test INSERT

---

### Phase 2: MAS Workflow Build (45 min)

**What Claude Code builds:**
- Complete MAS workflow (Nodes 1-11) as n8n JSON
- Import workflow JSON into n8n
- Wire up all node connections
- Configure Claude system prompt with full MAS SKILL.md

**Verification:**
- Submit test payload via webhook
- Confirm score calculation matches expected output
- Confirm Claude returns structured JSON analysis
- Confirm Supabase record created
- Confirm GHL contact created with correct tags

---

### Phase 3: ICP + GTM Workflow Replication (45 min)

**What Claude Code builds:**
- Clone MAS workflow, adapt for ICP (20 questions, ICP sections, ICP SKILL.md)
- Clone MAS workflow, adapt for GTM (14 questions + motion scores, GTM SKILL.md)
- Update validation node question counts (ICP: 20, GTM: 14)
- Update section groupings and score calculations per assessment type

**Verification:**
- Submit test payloads for ICP and GTM
- Confirm all 3 workflows store to Supabase correctly
- Confirm GHL tags applied per assessment type

---

### Phase 4: Consolidated Workflow + Response Formatting (30 min)

**What Claude Code builds:**
- Consolidated workflow: triggered when email has all 3 assessment records in Supabase
- Supabase query: `SELECT * FROM eo_founder_readiness WHERE contact_email = ?`
- Claude consolidated analysis call with all 3 scores
- GHL update with overall readiness score and bottleneck tags
- Email trigger for full results delivery

**Verification:**
- Complete all 3 assessments for same email
- Confirm consolidated score = (MAS * 0.35) + (ICP * 0.35) + (GTM * 0.30)
- Confirm GHL contact has `eo-full-assessed` tag and bottleneck tag

---

### Phase 5: End-to-End Integration Test (30 min)

**What gets tested:**
- Full flow: web app submission → n8n webhook → score calc → Claude analysis → Supabase storage → GHL contact + tags → webhook response to frontend
- Error handling: invalid payloads, Claude API timeout, duplicate contacts
- Response time: target < 5 seconds end-to-end
- Supabase view `eo_founder_readiness` returns correct consolidated data

**Post-build optimization (next day):**
- Monitor Claude token usage and response quality
- Tune system prompts based on first 10 real submissions
- Add email nurture sequences in GHL based on score bands
- Create landing page to drive traffic to assessments

---

## 9. COST ANALYSIS

### Per-Assessment Costs

| Component | Cost |
|-----------|------|
| Claude API call (Sonnet) | $0.015 |
| n8n workflow execution | $0.00 (self-hosted) or $0.003 (cloud) |
| GHL contact creation | $0.00 (included in plan) |
| Supabase record | $0.00 (free tier: 500MB, 50K rows) |
| **Total per assessment** | **~$0.02** |

### Scale Economics

| Volume/Month | Monthly Cost | Cost Per Lead |
|--------------|--------------|---------------|
| 100 | $2 | $0.02 |
| 500 | $10 | $0.02 |
| 1,000 | $20 | $0.02 |
| 5,000 | $100 | $0.02 |
| 10,000 | $200 | $0.02 |

**Note:** GHL, Supabase (free tier up to 50K rows), and Instantly have fixed monthly costs that don't scale with assessments. Claude API scales linearly. Supabase Pro ($25/mo) only needed above 500MB storage or if you need daily backups.

---

## 10. SECURITY & COMPLIANCE

### Webhook Security

```javascript
// Node: Verify Webhook Signature
const crypto = require('crypto');
const secret = process.env.WEBHOOK_SECRET;
const signature = $request.headers['x-webhook-signature'];

const payload = JSON.stringify($request.body);
const hash = crypto
  .createHmac('sha256', secret)
  .update(payload)
  .digest('hex');

if (hash !== signature) {
  return { error: 'Invalid signature', statusCode: 401 };
}

return { valid: true };
```

### Rate Limiting

Configure n8n webhook to limit:
- Max 10 requests per second per IP
- Max 1,000 requests per day per email
- Block if >100 submissions from same IP in 1 hour

### Data Privacy

- **Email:** Store in GHL only (encrypted in transit)
- **Answers:** Store in Supabase for analytics (no PII in Claude prompts)
- **Claude API:** Do NOT send full names or emails in system prompts
- **GDPR:** Implement data deletion on request

### Example GDPR-Compliant Claude Prompt

```
Founder at {{company}} (omit name) has the following assessment scores:
- Pain Reality: {{section_score}}/25
- Purchasing Power: {{section_score}}/25
...

[Analysis without referencing PII]
```

---

## 11. MONITORING & TROUBLESHOOTING

### Key Metrics to Track

1. **Assessment Completion Rate**
   - Total starts
   - Total completions
   - Drop-off by question

2. **Claude API Performance**
   - Response time (target <3s)
   - Error rate (target <1%)
   - Token usage vs. budget

3. **Lead Quality**
   - % completing all 3 assessments
   - Average readiness score
   - % moving to next stage

4. **Cost Tracking**
   - Claude API monthly spend
   - Cost per qualified lead
   - Cost per assessment

### Common Issues & Solutions

**Issue:** Webhook returns 500 error
- **Cause:** Invalid API key or malformed payload
- **Solution:** Check API credentials, validate JSON schema

**Issue:** Claude response is not JSON
- **Cause:** System prompt not clear enough
- **Solution:** Add "Return valid JSON" to system prompt, add JSON schema

**Issue:** GHL contact creation fails
- **Cause:** Duplicate email or invalid phone
- **Solution:** Add validation before GHL call, catch and retry

**Issue:** Assessment takes 10+ seconds
- **Cause:** Claude API slow response
- **Solution:** Switch to faster model (Sonnet), reduce max_tokens, optimize prompt

---

## 12. EXTENSION & FUTURE ENHANCEMENTS

### Planned Features

1. **Assessment Versioning**
   - Allow founders to re-take assessments
   - Track progress over time
   - Show improvement roadmap completion

2. **Cohort Analysis**
   - "Your score compares to: 73% of founders"
   - Industry benchmarking
   - Stage-based comparisons

3. **Integration Expansions**
   - Slack notifications on new qualified leads
   - Zapier integration for HubSpot
   - Direct calendar integration for Free Hour booking

4. **Advanced Analytics**
   - Correlation analysis (does MAS predict GTM success?)
   - Predictive scoring (will this founder succeed?)
   - Recommendation effectiveness tracking

5. **Conversational Assessment**
   - Replace linear questionnaire with Claude AI chatbot
   - Multi-turn conversation
   - Contextual follow-up questions

### API Enhancements

- Public API for accessing assessment results
- Webhooks for external systems (send results to CRM)
- GraphQL endpoint for analytics queries

---

## 13. QUICK START CHECKLIST (Claude Code Build Day)

**Before you start:**
- [ ] n8n instance running (cloud or self-hosted)
- [ ] Anthropic API key ready
- [ ] GHL API key ready
- [ ] Supabase project created (free tier)

**Phase 1: Infrastructure (30 min)**
- [ ] Run Supabase SQL to create `eo_assessments` table + view
- [ ] Configure n8n credentials (Anthropic, GHL, Supabase)
- [ ] Test webhook endpoint responds

**Phase 2: MAS Workflow (45 min)**
- [ ] Build MAS workflow (Nodes 1-11)
- [ ] Test with sample payload
- [ ] Verify Supabase record + GHL contact created

**Phase 3: ICP + GTM Workflows (45 min)**
- [ ] Clone and adapt for ICP (20 questions)
- [ ] Clone and adapt for GTM (14 questions + motion scores)
- [ ] Test both with sample payloads

**Phase 4: Consolidated + Final (30 min)**
- [ ] Build consolidated workflow
- [ ] Test end-to-end with all 3 assessments
- [ ] Verify founder readiness score calculation

**Post-build (next day):**
- [ ] Set up GHL custom fields and tag automation rules
- [ ] Create landing page for assessments
- [ ] Set up email nurture sequences
- [ ] Monitor first 10 real submissions

---

## 14. SUPPORT & DOCUMENTATION

### Key Files to Create

1. **MAS_SKILL.md** — Scoring rubric + recommendation framework
2. **ICP_SKILL.md** — Clarity framework + buyer persona analysis
3. **GTM_SKILL.md** — Go-to-market strategy + market positioning
4. **n8n_workflow_backups/** — JSON exports of all workflows
5. **API_TEST_SUITE.md** — Example webhook payloads for testing
6. **TROUBLESHOOTING.md** — Common issues and fixes

### External Resources

- n8n Documentation: https://docs.n8n.io
- Anthropic API Docs: https://docs.anthropic.com
- GoHighLevel API: https://developer.gohighlevel.com
- Supabase Docs: https://supabase.com/docs
- Supabase n8n Node: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.supabase/

---

**Document Complete**

This architecture is designed for same-day deployment using Claude Code. The 5-phase build (Section 8) targets ~3 hours of focused execution. Supabase provides free hosted Postgres with native n8n integration, SQL analytics via the `eo_founder_readiness` view, and zero rate limits on reads.

For questions or updates, refer to the Claude Code Build Roadmap (Section 8) and Troubleshooting Guide (Section 11).
