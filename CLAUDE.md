# EO Assessment System — Claude Code Execution Guide

**Version:** 3.0 — POST-REVAMP (reflects actual live code state as of 2026-03-10)
**Author:** SMOrchestra / Mamoun
**Status:** All 5 scorecards + dashboard are BUILT and DEPLOYED. This doc is for MAINTENANCE and BUG FIXES only.

---

## CRITICAL: THIS IS A MAINTENANCE GUIDE, NOT A BUILD GUIDE

The previous CLAUDE.md (v2.0) instructed you to REBUILD all scorecards from scratch. **That work is DONE.** All 6 HTML files are live and functional at `https://score.entrepreneursoasis.me/`. This guide tells you how the system actually works so you can fix bugs, add features, and maintain it.

### Source of Truth Hierarchy

```
1. THE LIVE HTML FILES IN THIS REPO   ← Ground truth (read before changing anything)
2. THIS FILE (CLAUDE.md)              ← Architecture reference + maintenance guide
3. EO-Assessment-n8n-Architecture.md  ← Backend webhook/n8n workflow reference
4. eo-config/*.md                     ← Scoring rubrics and band definitions
5. SHARED-PATTERNS.md                 ← Reusable code patterns (auth, slugify, localStorage)
```

**IGNORE these files — they are OUTDATED:**
- `specs/_DEPRECATED-*.md` — Old specs, wrong question counts
- `EO-Assessment-System-Change-Spec.md` — Was the build spec; work is complete
- Previous CLAUDE.md versions that say "REBUILD" or reference DM Sans / #050A12 / #FF6600

---

## REPO STRUCTURE

```
├── CLAUDE.md                              ← YOU ARE HERE (maintenance guide)
├── EO-Assessment-Dashboard.html           ← Hub: progress tracking, history, navigation
├── EO-Project-Definition-Scoring.html     ← SC1: Project Definition (7 MC + free-text)
├── EO-ICP-Clarity-Scoring.html            ← SC2: ICP Clarity (6 MC + free-text)
├── EO-Market-Attractiveness-Scoring.html  ← SC3: Market Attractiveness (6 MC + free-text)
├── EO-Strategy-Selector.html             ← SC4: Strategy Selector (10 MC + free-text)
├── EO-GTM-Fitness-Scoring.html           ← SC5: GTM Fitness (20 MC, NO free-text)
│
├── EO-Assessment-n8n-Architecture.md     ← n8n backend reference
├── SHARED-PATTERNS.md                    ← Reusable code patterns
├── BLIND-SPOTS.md                        ← Known issues tracker
│
├── eo-config/                            ← Scoring rubrics per assessment
│   ├── consolidated-config.md
│   ├── gtm-config.md
│   ├── icp-config.md
│   ├── mas-config.md
│   ├── project-files-config.md
│   ├── strategy-selector-config.md
│   └── EO-ADMIN-GUIDE.md
│
├── specs/                                ← DEPRECATED build specs
├── gtm-fitness-scoring/                  ← SC5 supporting files
├── icp-clarity-scoring/                  ← SC2 supporting files
├── market-attractiveness-scoring/        ← SC3 supporting files
├── project-files-scoring/                ← SC1 supporting files
├── strategy-selector/                    ← SC4 supporting files
│
├── _DEPRECATED-EO-Project-Files-Scoring.html
└── _DEPRECATED-EO-Strategy-Selector-Lite.html
```

---

## DESIGN SYSTEM (ACTUAL VALUES FROM LIVE CODE)

**⚠️ The old CLAUDE.md v2.0 listed wrong values (DM Sans, #050A12, #FF6600). Those are WRONG. Below are the ACTUAL values from the live deployed HTML files.**

```css
:root {
  --eo-dark: #1A1A2E;
  --eo-orange: #E94D1B;
  --eo-beige: #FAF5EF;
  --eo-card-bg: #FFFFFF;
  --eo-gray-text: #6B7280;
  --eo-gray-border: #E5E7EB;
  --eo-radius: 16px;
  --eo-radius-sm: 12px;
  --eo-shadow: 0 1px 3px rgba(0,0,0,0.08);
  --eo-transition: all 0.2s ease;
}
```

**Font:** `'Inter', -apple-system, BlinkMacSystemFont, sans-serif`
**Import:** `https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap`

**Color roles:**
- `#1A1A2E` — Dark backgrounds (nav, hero, results header, auth overlay)
- `#E94D1B` — Primary accent (buttons, progress bar, selected states, score highlights)
- `#FAF5EF` — Page background (warm off-white)
- `#FFFFFF` — Card backgrounds
- `#6B7280` — Secondary text
- `#E5E7EB` — Borders, dividers

**Layout:**
- `max-width: 760px` centered container
- `16px` border radius on cards, `12px` on smaller elements
- Sticky nav with `backdrop-filter: blur(12px)`
- Progress bar: 4px height, orange fill
- MC options: stacked cards with hover/selected states (orange border + light orange bg)

---

## WEBHOOK URLS (PRODUCTION)

Each scorecard POSTs to its own n8n webhook endpoint:

| Scorecard | Webhook URL |
|-----------|-------------|
| SC1: Project Definition | `https://ai.mamounalamouri.smorchestra.com/webhook/eo-project-definition` |
| SC2: ICP Clarity | `https://ai.mamounalamouri.smorchestra.com/webhook/eo-icp-clarity` |
| SC3: Market Attractiveness | `https://ai.mamounalamouri.smorchestra.com/webhook/eo-market-attractiveness` |
| SC4: Strategy Selector | `https://ai.mamounalamouri.smorchestra.com/webhook/eo-strategy-selector` |
| SC5: GTM Fitness | `https://ai.mamounalamouri.smorchestra.com/webhook/eo-gtm-fitness` |
| Dashboard (consolidated) | `https://ai.mamounalamouri.smorchestra.com/webhook/eo-consolidated` |

**n8n Instance:** `https://ai.mamounalamouri.smorchestra.com` (self-hosted)

---

## ARCHITECTURE: HOW EACH SCORECARD WORKS

### SC1-SC4: Hybrid MC + AI Scoring

All four scorecards follow the same pattern:

```
1. User authenticates (name + company + email)
2. User answers MC questions → scored locally (each option has a score value)
3. User answers free-text questions → sent to n8n webhook for AI scoring
4. Webhook payload: { contact, answers: { mc: [...], freeText: [...] }, scores: { sections, total } }
5. n8n workflow:
   a. Validates payload
   b. Sends free-text answers + MC scores to Claude API
   c. Claude returns: AI scores for free-text, recommendations, band assignment
   d. n8n creates/updates GHL contact with tags
   e. Returns JSON response to frontend
6. Frontend renders results: score band, section breakdown, recommendations
7. User can download MD summary + "Feed to Claude" next steps
8. Completion saved to localStorage for dashboard
```

### SC5: GTM Fitness (COMPLETELY DIFFERENT — Revamped 2026-03-10)

SC5 was completely rewritten. Key differences from SC1-SC4:

- **20 MC questions only** — NO free-text questions
- **3 sections:** A (Your Business, 4Q, 20pts), B (Capabilities, 10Q, 50pts), C (Readiness, 6Q, 30pts) = **100pts total**
- **Linear flow** — no dynamic questions, no branching logic
- **13 GTM motions** scored automatically from answer weights (not asked directly)
- **AbortController timeout** — 15-second webhook timeout to prevent infinite hang

**Motion Scoring Formula:**
```
For each of 13 motions:
  fit = defaultFit + contextBonus adjustments (from A-section answers)
  readiness = sum(B-answers × capWeights) + sum(C-answers × readyWeights) → scaled 0-10
  menaScore = baseMena + geoBonus + arabicBonus

  composite = (fit × 0.4 + readiness × 0.3 + menaScore × 0.3) / 2
  → Range: 0.0 to 5.0
```

**Motion Tiers:**
- PRIMARY: composite ≥ 4.0 (deploy now)
- SECONDARY: 3.0 – 3.9 (build capacity)
- CONDITIONAL: 2.0 – 2.9 (needs prerequisites)
- SKIP: < 2.0 (not viable yet)

**The 13 GTM Motions:**
1. Signal-Based Outbound (cold email)
2. LinkedIn Thought Leadership
3. Founder-Led Content (YouTube/podcasts)
4. Community & Events
5. Referral & Partner Programs
6. Paid Ads (LinkedIn/Google)
7. SEO & Inbound Content
8. Account-Based Marketing (ABM)
9. Product-Led Growth (PLG)
10. Channel & Reseller Partnerships
11. Webinars & Virtual Events
12. Direct Sales (Enterprise)
13. WhatsApp/Social Selling

---

## LOCALSTORAGE KEYS

```javascript
// Dashboard completion tracking
'eo_completion_status'  // JSON: { project: score, icp: score, market: score, strategy: score, gtm: score }

// Assessment history (for dashboard chart)
'eo-history'            // JSON array: [{ date, scores: { project, icp, market, strategy, gtm } }]

// Individual scorecard data
'eo-scores'             // Used by SC1-SC4 for score persistence
'eo-gtm-fitness'        // Used by SC5 for GTM-specific data
'eo-strategy-selector'  // Used by SC4 for strategy path data

// Auth
'eo_auth_*'             // Various auth-related keys
```

---

## KNOWN BUGS & ISSUES

### 1. SCORE CAP AT 85 (CRITICAL — BACKEND)
**Symptom:** SC1 (Project Definition) and SC2 (ICP Clarity) scores are capped at 85/100 regardless of answers.
**Location:** n8n webhook backend — NOT in frontend HTML.
**Root cause:** Unknown. Likely in one of:
- A Code node doing `Math.min(score, 85)` or similar clamping
- The Claude system prompt instructing AI to never score above 85
- Band assignment logic that maps everything above 85 → 85
**Fix:** See `EO-CLAUDE-CODE-GUIDE.md` for investigation steps.

### 2. WEBHOOK TIMEOUT (FIXED in SC5)
SC5 now has a 15-second AbortController timeout. SC1-SC4 do NOT have this yet — if the webhook hangs, the loading overlay stays forever.
**To add to SC1-SC4:** Wrap each `fetch()` call in an AbortController pattern (see SC5's `submitContact()` function).

### 3. DESIGN SYSTEM INCONSISTENCY
The old CLAUDE.md (v2.0) and EO-Assessment-System-Change-Spec.md reference a completely different design system (DM Sans + dark theme with #050A12). The actual live files use Inter + warm theme with #1A1A2E/#FAF5EF/#E94D1B. The old docs should not be used for design reference.

---

## HOW TO MAKE CHANGES

### Before Editing Any File:
1. Read THIS document (you're doing it)
2. Open the specific HTML file you're editing — read the CSS variables, JS structure
3. Check `eo-config/` for the relevant scoring rubric if touching score logic
4. Test changes locally by opening the HTML file in a browser

### CSS Changes:
- All CSS is inline in `<style>` tags within each HTML file
- Use the CSS variables defined above — don't hardcode colors
- Every file uses the same design system; keep them consistent

### JS Changes:
- All JS is inline in `<script>` tags at the bottom of each HTML file
- SC1-SC4 use similar patterns (auth → questions → webhook → results)
- SC5 has a different structure (see GTM Fitness section above)
- Always use `var` not `let`/`const` for IE11 compat (though this may not matter)

### Adding Webhook Timeout to SC1-SC4:
```javascript
// Pattern from SC5 — adapt for each scorecard:
var controller = new AbortController();
var timeoutId = setTimeout(function() { controller.abort(); }, 15000);

fetch(WEBHOOK_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload),
    signal: controller.signal
})
.then(function(r) { return r.json(); })
.then(function(data) { /* handle response */ })
.catch(function(err) {
    if (err.name === 'AbortError') {
        console.warn('Webhook timeout — proceeding with local scores only');
    }
})
.finally(function() {
    clearTimeout(timeoutId);
    // Remove loading overlay, show results
});
```

### Deploying Changes:
1. Commit changes to this repo
2. Push to GitHub: `git push origin main`
3. The site at `score.entrepreneursoasis.me` pulls from this repo (verify deployment method)

---

## TESTING CHECKLIST

Before deploying any changes:

- [ ] Open each modified HTML file in browser
- [ ] Complete auth flow (enter name, company, email)
- [ ] Answer all questions
- [ ] Verify score calculation matches expected ranges
- [ ] Verify webhook fires (check n8n execution log)
- [ ] Verify results page renders correctly
- [ ] Verify "Download MD" button works
- [ ] Verify dashboard shows completion badge after finishing
- [ ] Check localStorage values in DevTools → Application → Local Storage
- [ ] Test on mobile viewport (375px width)
