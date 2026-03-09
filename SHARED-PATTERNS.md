# SHARED PATTERNS — Copy These Exactly Into Every HTML File

**Purpose:** These utility functions MUST be character-for-character identical across all 6 HTML files. A mismatch in slugify() between SC1 and SC2 = data loss. Copy-paste, don't rewrite.

---

## 1. SLUGIFY FUNCTION

```javascript
function slugify(text) {
  return text
    .toString()
    .toLowerCase()
    .trim()
    .replace(/\s+/g, '-')           // spaces → hyphens
    .replace(/[^\w\-]+/g, '')       // remove non-word chars (except hyphens)
    .replace(/\-\-+/g, '-')        // collapse multiple hyphens
    .replace(/^-+/, '')             // trim leading hyphens
    .replace(/-+$/, '');            // trim trailing hyphens
}
```

**Test cases (all files must produce identical output):**
```
"Dubai Real Estate CRM"     → "dubai-real-estate-crm"
"My Cool SaaS v2.0"         → "my-cool-saas-v20"
"  Spaces  Everywhere  "    → "spaces-everywhere"
"Arabic عربي Mix"           → "arabic--mix" → "arabic-mix"  (Arabic chars stripped, double-hyphen collapsed)
"123 Numbers First"         → "123-numbers-first"
```

---

## 2. VENTURE REGISTRY (localStorage)

```javascript
// === VENTURE REGISTRY HELPERS ===

function getVentures(email) {
  try {
    return JSON.parse(localStorage.getItem('eo_ventures_' + email) || '[]');
  } catch(e) { return []; }
}

function saveVenture(email, ventureName) {
  const slug = slugify(ventureName);
  const ventures = getVentures(email);

  // Check for duplicate slug
  const existing = ventures.find(v => v.venture_slug === slug);
  if (existing) {
    existing.last_active = new Date().toISOString().split('T')[0];
    localStorage.setItem('eo_ventures_' + email, JSON.stringify(ventures));
    return { venture_name: existing.venture_name, venture_slug: slug, isNew: false };
  }

  // Add new venture
  const venture = {
    venture_name: ventureName.trim(),
    venture_slug: slug,
    created_at: new Date().toISOString().split('T')[0],
    last_active: new Date().toISOString().split('T')[0]
  };
  ventures.push(venture);
  localStorage.setItem('eo_ventures_' + email, JSON.stringify(ventures));
  return { ...venture, isNew: true };
}

function updateVentureActivity(email, slug) {
  const ventures = getVentures(email);
  const venture = ventures.find(v => v.venture_slug === slug);
  if (venture) {
    venture.last_active = new Date().toISOString().split('T')[0];
    localStorage.setItem('eo_ventures_' + email, JSON.stringify(ventures));
  }
}
```

---

## 3. COMPOSITE KEY HELPERS

```javascript
// === COMPOSITE KEY HELPERS ===

// Build localStorage key for any scorecard
function storageKey(type, scNumber, email, ventureSlug) {
  // type: 'answers' | 'result'
  return 'eo_sc' + scNumber + '_' + type + '_' + email + '_' + ventureSlug;
}

// Read/write cross-scorecard scores
function getScores(email, ventureSlug) {
  try {
    return JSON.parse(localStorage.getItem('eo_scores_' + email + '_' + ventureSlug) || '{}');
  } catch(e) { return {}; }
}

function saveScore(email, ventureSlug, scNumber, score) {
  const scores = getScores(email, ventureSlug);
  scores['sc' + scNumber] = score;
  localStorage.setItem('eo_scores_' + email + '_' + ventureSlug, JSON.stringify(scores));
}

// Read answers from a specific scorecard (for upstream data)
function getUpstreamAnswers(scNumber, email, ventureSlug) {
  try {
    return JSON.parse(localStorage.getItem(storageKey('answers', scNumber, email, ventureSlug)) || '{}');
  } catch(e) { return {}; }
}

// Read result from a specific scorecard
function getUpstreamResult(scNumber, email, ventureSlug) {
  try {
    return JSON.parse(localStorage.getItem(storageKey('result', scNumber, email, ventureSlug)) || 'null');
  } catch(e) { return null; }
}
```

---

## 4. AUTH SCREEN PATTERN

### SC1 (Creation Point)

```javascript
// === AUTH: SC1 VENTURE CREATION ===

let userEmail = '';
let ventureSlug = '';
let ventureName = '';

function handleAuth() {
  const emailInput = document.getElementById('auth-email');
  const ventureInput = document.getElementById('auth-venture');

  const email = emailInput.value.trim().toLowerCase();
  const name = ventureInput.value.trim();

  if (!email || !email.includes('@')) {
    showError('Please enter a valid email address');
    return;
  }
  if (!name || name.length < 3) {
    showError('Venture name must be at least 3 characters');
    return;
  }

  userEmail = email;
  ventureName = name;
  const result = saveVenture(email, name);
  ventureSlug = result.venture_slug;

  // Check for existing results (retrieval)
  const existingResult = getUpstreamResult(1, email, ventureSlug);
  if (existingResult) {
    showRetrievalBanner(existingResult);
  } else {
    startQuestions();
  }
}
```

```html
<!-- AUTH SCREEN HTML (SC1) -->
<div id="auth-screen" class="screen active">
  <div class="intro">
    <div class="intro-badge">STEP 1 OF 5</div>
    <h1>Project <em>Definition</em></h1>
    <p class="intro-sub">7 questions. ~15 minutes. Build your venture foundation.</p>

    <div class="email-box">
      <label>YOUR EMAIL</label>
      <input type="email" id="auth-email" class="email-input"
             placeholder="founder@company.com" required>

      <label style="margin-top:16px">VENTURE NAME</label>
      <input type="text" id="auth-venture" class="email-input"
             placeholder="e.g., Dubai Real Estate CRM"
             minlength="3" required>
      <div class="q-hint">Give your venture a working name. This identifies your assessment across all 5 scorecards.</div>

      <button class="btn btn-primary btn-full" onclick="handleAuth()">
        Begin Assessment →
      </button>

      <div id="auth-error" style="color:var(--red);font-size:13px;margin-top:12px;display:none"></div>
    </div>
  </div>
</div>
```

### SC2-SC5 (Selector Pattern)

```javascript
// === AUTH: SC2-SC5 VENTURE SELECTOR ===

let userEmail = '';
let ventureSlug = '';
let ventureName = '';
const SC_NUMBER = 2; // Change per file: 2, 3, 4, 5

function handleEmailEntry() {
  const email = document.getElementById('auth-email').value.trim().toLowerCase();
  if (!email || !email.includes('@')) {
    showError('Please enter a valid email address');
    return;
  }

  userEmail = email;
  const ventures = getVentures(email);

  if (ventures.length === 0) {
    showError('No assessment found for this email. <a href="EO-Project-Definition-Scoring.html" style="color:var(--accent)">Complete Step 1 first →</a>');
    return;
  }

  if (ventures.length === 1) {
    // Auto-select
    selectVenture(ventures[0]);
  } else {
    // Show dropdown
    showVentureSelector(ventures);
  }
}

function showVentureSelector(ventures) {
  const selector = document.getElementById('venture-selector');
  selector.innerHTML = '<label>SELECT VENTURE</label>' +
    '<select id="venture-select" class="email-input" onchange="handleVentureSelect()">' +
    '<option value="">— Choose your venture —</option>' +
    ventures.map(v => '<option value="' + v.venture_slug + '">' + v.venture_name + '</option>').join('') +
    '</select>';
  selector.style.display = 'block';
}

function handleVentureSelect() {
  const slug = document.getElementById('venture-select').value;
  if (!slug) return;
  const ventures = getVentures(userEmail);
  const venture = ventures.find(v => v.venture_slug === slug);
  if (venture) selectVenture(venture);
}

function selectVenture(venture) {
  ventureSlug = venture.venture_slug;
  ventureName = venture.venture_name;
  updateVentureActivity(userEmail, ventureSlug);

  // Check for existing results (retrieval)
  const existingResult = getUpstreamResult(SC_NUMBER, userEmail, ventureSlug);
  if (existingResult) {
    showRetrievalBanner(existingResult);
  } else {
    // Check prerequisites
    checkPrerequisites();
  }
}
```

```html
<!-- AUTH SCREEN HTML (SC2-SC5) -->
<div id="auth-screen" class="screen active">
  <div class="intro">
    <div class="intro-badge">STEP 2 OF 5</div> <!-- Change per file -->
    <h1>ICP <em>Clarity</em></h1> <!-- Change per file -->
    <p class="intro-sub">6 questions. ~12 minutes. Define your ideal customer.</p> <!-- Change per file -->

    <div class="email-box">
      <label>YOUR EMAIL</label>
      <input type="email" id="auth-email" class="email-input"
             placeholder="founder@company.com" required>
      <button class="btn btn-primary btn-full" onclick="handleEmailEntry()"
              style="margin-bottom:0">
        Continue →
      </button>

      <div id="venture-selector" style="display:none;margin-top:16px"></div>
      <div id="auth-error" style="color:var(--red);font-size:13px;margin-top:12px;display:none"></div>
    </div>
  </div>
</div>
```

---

## 5. RETRIEVAL BANNER

```javascript
// === RETRIEVAL BANNER ===

function showRetrievalBanner(result) {
  const banner = document.getElementById('retrieval-banner');
  banner.innerHTML = `
    <div style="background:var(--surface);border:1px solid var(--border);border-left:4px solid var(--green);border-radius:var(--radius);padding:20px;max-width:440px;margin:24px auto 0">
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:12px">
        <div style="width:44px;height:44px;border-radius:50%;background:var(--accent-dim);display:flex;align-items:center;justify-content:center;font-size:18px;font-weight:800;color:var(--accent)">${result.score}</div>
        <div>
          <div style="font-weight:700;color:var(--text);font-size:15px">Previously Completed</div>
          <div style="font-size:12px;color:var(--text-3)">${result.band || ''} — ${result.completed_at || ''}</div>
        </div>
      </div>
      <div style="display:flex;gap:10px">
        <button class="btn btn-secondary" onclick="viewPreviousResults()" style="flex:1;padding:10px">View Results</button>
        <button class="btn btn-primary" onclick="startFresh()" style="flex:1;padding:10px">Start Fresh</button>
      </div>
    </div>
  `;
  banner.style.display = 'block';
}

function viewPreviousResults() {
  const result = getUpstreamResult(SC_NUMBER, userEmail, ventureSlug);
  if (result) renderResults(result);
}

function startFresh() {
  localStorage.removeItem(storageKey('answers', SC_NUMBER, userEmail, ventureSlug));
  localStorage.removeItem(storageKey('result', SC_NUMBER, userEmail, ventureSlug));
  document.getElementById('retrieval-banner').style.display = 'none';
  startQuestions();
}
```

```html
<!-- Add this inside the auth screen div, after the email-box -->
<div id="retrieval-banner" style="display:none"></div>
```

---

## 6. PREREQUISITE CHECK (SC2-SC5)

```javascript
// === PREREQUISITE CHECK ===

function checkPrerequisites() {
  const scores = getScores(userEmail, ventureSlug);

  // SC2 needs SC1, SC3 needs SC1+SC2, etc.
  const prerequisites = {
    2: [1],
    3: [1, 2],
    4: [1, 2, 3],
    5: [1, 2, 3, 4]
  };

  const required = prerequisites[SC_NUMBER] || [];
  const missing = required.filter(n => !scores['sc' + n] && scores['sc' + n] !== 0);

  if (missing.length > 0) {
    const names = { 1: 'Project Definition', 2: 'ICP Clarity', 3: 'Market Attractiveness', 4: 'Strategy Selector' };
    const files = { 1: 'EO-Project-Definition-Scoring.html', 2: 'EO-ICP-Clarity-Scoring.html', 3: 'EO-Market-Attractiveness-Scoring.html', 4: 'EO-Strategy-Selector.html' };
    const firstMissing = missing[0];
    showError('Please complete <a href="' + files[firstMissing] + '" style="color:var(--accent)">' + names[firstMissing] + '</a> first.');
    return;
  }

  startQuestions();
}
```

---

## 7. SAVE ANSWERS + RESULTS

```javascript
// === SAVE ON COMPLETION ===

function saveAnswers(answers) {
  localStorage.setItem(
    storageKey('answers', SC_NUMBER, userEmail, ventureSlug),
    JSON.stringify(answers)
  );
}

function saveResults(resultObj) {
  // resultObj = { score, band, sections, polished_output/recommendations, completed_at }
  resultObj.completed_at = new Date().toISOString().split('T')[0];

  localStorage.setItem(
    storageKey('result', SC_NUMBER, userEmail, ventureSlug),
    JSON.stringify(resultObj)
  );

  // Update cross-scorecard scores
  saveScore(userEmail, ventureSlug, SC_NUMBER, resultObj.score);
}
```

---

## 8. WEBHOOK CALL

```javascript
// === WEBHOOK ===

function sendToWebhook(answers, scores, resultObj) {
  const upstream = {};
  for (let i = 1; i < SC_NUMBER; i++) {
    upstream['sc' + i + '_score'] = getScores(userEmail, ventureSlug)['sc' + i] || null;
    upstream['sc' + i + '_answers'] = getUpstreamAnswers(i, userEmail, ventureSlug);
  }

  const payload = {
    email: userEmail,
    venture_name: ventureName,
    venture_slug: ventureSlug,
    scorecard: 'SC' + SC_NUMBER,
    answers: answers,
    scores: scores,
    upstream_data: upstream,
    timestamp: new Date().toISOString()
  };

  fetch('https://smorchestra.app.n8n.cloud/webhook/eo-assessment', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  }).catch(err => console.warn('Webhook failed:', err));
}
```

---

## 9. localStorage MIGRATION (OLD → NEW FORMAT)

```javascript
// === MIGRATION: Run on page load ===

function migrateOldData() {
  // Check for old-format keys
  for (let i = 0; i < localStorage.length; i++) {
    const key = localStorage.key(i);

    // Pattern: eo_sc1_answers_email@domain.com (no venture slug)
    const match = key.match(/^eo_sc(\d)_answers_([^_]+@[^_]+\.[^_]+)$/);
    if (match) {
      // Old format detected — we can't auto-migrate because we don't know the venture name
      // Store a flag so the auth screen can prompt for migration
      const email = match[2];
      const scNum = match[1];

      let migrationNeeded = JSON.parse(localStorage.getItem('eo_migration_pending') || '{}');
      if (!migrationNeeded[email]) migrationNeeded[email] = [];
      if (!migrationNeeded[email].includes(parseInt(scNum))) {
        migrationNeeded[email].push(parseInt(scNum));
      }
      localStorage.setItem('eo_migration_pending', JSON.stringify(migrationNeeded));
    }
  }
}

function executeMigration(email, ventureName) {
  const slug = slugify(ventureName);

  for (let sc = 1; sc <= 5; sc++) {
    // Migrate answers
    const oldAnswers = localStorage.getItem('eo_sc' + sc + '_answers_' + email);
    if (oldAnswers) {
      localStorage.setItem(storageKey('answers', sc, email, slug), oldAnswers);
      localStorage.removeItem('eo_sc' + sc + '_answers_' + email);
    }

    // Migrate results
    const oldResult = localStorage.getItem('eo_sc' + sc + '_result');
    if (oldResult) {
      localStorage.setItem(storageKey('result', sc, email, slug), oldResult);
      localStorage.removeItem('eo_sc' + sc + '_result');
    }
  }

  // Migrate global scores
  const oldScores = localStorage.getItem('eo-scores');
  if (oldScores) {
    localStorage.setItem('eo_scores_' + email + '_' + slug, oldScores);
    localStorage.removeItem('eo-scores');
  }

  // Register venture
  saveVenture(email, ventureName);

  // Clear migration flag
  let pending = JSON.parse(localStorage.getItem('eo_migration_pending') || '{}');
  delete pending[email];
  if (Object.keys(pending).length === 0) {
    localStorage.removeItem('eo_migration_pending');
  } else {
    localStorage.setItem('eo_migration_pending', JSON.stringify(pending));
  }
}

// Call on page load
migrateOldData();
```

---

## 10. ERROR DISPLAY HELPER

```javascript
function showError(msg) {
  const el = document.getElementById('auth-error');
  el.innerHTML = msg;
  el.style.display = 'block';
  setTimeout(() => { el.style.display = 'none'; }, 8000);
}
```

---

## USAGE NOTES

1. **Every HTML file** must include ALL of the above: slugify, venture registry, composite key helpers, save/webhook functions, migration.
2. **SC1** uses the "Creation Point" auth pattern. **SC2-SC5** use the "Selector" auth pattern.
3. **Dashboard** uses a hybrid: it has both "Start New" (creation) and "Resume" (selector) flows.
4. **SC_NUMBER** constant must be set correctly per file (1, 2, 3, 4, 5).
5. **Do not rename functions.** Other scorecards may deep-link or share patterns. Keep names identical.
