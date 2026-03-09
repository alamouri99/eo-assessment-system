# BLIND SPOTS & RISK REGISTER

**Read this before starting any HTML work. Each item is a silent failure mode.**

---

## 1. DESIGN SYSTEM MISMATCH (CRITICAL)

**Risk:** The Change Spec (Section 1D) references colors `#1A1A2E`, `#FAF5EF`, `#E94D1B` and font `Inter`. The LIVE deployed HTML uses completely different values: `#050A12`, `#111827`, `#FF6600` and `DM Sans`.

**Resolution:** USE THE LIVE HTML VALUES. The CLAUDE.md documents the correct design tokens. The Change Spec colors are from an earlier design draft and are WRONG.

**Impact if missed:** HTML files look visually inconsistent — old files use one palette, new files use another.

---

## 2. VENTURE SLUG CONSISTENCY (CRITICAL)

**Risk:** The `slugify()` function must produce identical output across all 6 HTML files. If SC1 generates `dubai-real-estate-crm` and SC2 generates `dubai-real-estate--crm` (double hyphen from extra space), the localStorage lookup silently fails and SC2 says "No assessment found."

**Resolution:** Copy the exact `slugify()` function from SHARED-PATTERNS.md into every file. Do not rewrite or "improve" it. Test with edge cases: Arabic text, special characters, leading/trailing spaces, multiple spaces.

**Impact if missed:** Data loss. User completes SC1 but SC2-SC5 can't find their data.

---

## 3. OLD SPEC FILES CONFLICT (HIGH)

**Risk:** The `specs/` directory contains `SCORECARD-REDESIGN-SPEC.md` and `ASSESSMENT-IMPLEMENTATION-SPEC.md` which have OUTDATED information (wrong question counts, wrong localStorage keys, wrong execution order). If Claude Code reads these, it will follow conflicting instructions.

**Resolution:** The CLAUDE.md explicitly marks these as DEPRECATED. But to be safe, rename them:
```bash
mv specs/SCORECARD-REDESIGN-SPEC.md specs/_DEPRECATED-SCORECARD-REDESIGN-SPEC.md
mv specs/ASSESSMENT-IMPLEMENTATION-SPEC.md specs/_DEPRECATED-ASSESSMENT-IMPLEMENTATION-SPEC.md
```

**Impact if missed:** Claude Code builds HTML using old 23-question format or wrong data flow.

---

## 4. OLD SKILL.md FILES AS SOURCE OF TRUTH (HIGH)

**Risk:** The old CLAUDE.md said "SKILL.md is source of truth — if HTML and SKILL.md conflict, SKILL.md wins." The SKILL.md files still have old question counts (SC1: 23 questions in v1.1, SC4: 20 in v2.1, SC5: 22 in v2.1). The new CLAUDE.md overrides this: "The Change Spec is LAW."

**Resolution:** The new CLAUDE.md explicitly deprioritizes SKILL.md files for HTML generation. But Claude Code might still read them. Consider adding a header warning to each SKILL.md:
```
⚠️ THIS SKILL.MD IS FOR THE CLAUDE CONVERSATION SKILL, NOT FOR HTML GENERATION.
FOR HTML SPEC, SEE: EO-Assessment-System-Change-Spec.md
```

**Impact if missed:** HTML built with wrong question counts.

---

## 5. SC5 DYNAMIC QUESTIONS WITHOUT UPSTREAM DATA (MEDIUM)

**Risk:** SC5 Questions 3-7 show specific motion names (e.g., "For Signal Sniper: what do you already have in place?"). These names come from pre-ranking 13 motions using upstream data. If user somehow reaches SC5 without completing SC1-SC4, or if upstream data is corrupted, the pre-ranking fails.

**Resolution:** SHARED-PATTERNS.md includes a prerequisite check. But also add a FALLBACK: if pre-ranking can't produce 5 motions, show a list of all 13 motions and let the user select their top 5. The Change Spec mentions this fallback in Step 6.

**Impact if missed:** SC5 shows blank question text or crashes.

---

## 6. WEBHOOK URL DISCREPANCY (MEDIUM)

**Risk:** The old CLAUDE.md listed `https://ai.mamounalamouri.smorchestra.com/webhook/eo-{scorecard}` (per-scorecard endpoints). The live HTML uses `https://smorchestra.app.n8n.cloud/webhook/eo-assessment` (single endpoint).

**Resolution:** Use the LIVE URL: `https://smorchestra.app.n8n.cloud/webhook/eo-assessment`. Single endpoint, `scorecard` field in payload distinguishes SC1-SC5.

**Impact if missed:** Webhook 404s or data goes to wrong endpoint.

---

## 7. localStorage RESULT KEY NOT SCOPED TO EMAIL (MEDIUM)

**Risk:** Current live SC1 stores results as `eo_sc1_result` (NOT scoped to email or venture). This means only ONE user's result is stored at a time. If two people use the same browser, they overwrite each other.

**Resolution:** New schema scopes everything: `eo_sc1_result_[email]_[venture_slug]`. Migration code in SHARED-PATTERNS.md handles the old format.

**Impact if missed:** Multi-user or multi-venture data overwrites.

---

## 8. RESULTS PAGE VISUALIZATIONS (MEDIUM)

**Risk:** The Change Spec describes complex visualizations: gauge rings, radar charts, 4-dimension bars, 90-day roadmap columns, motion ranking tables. These need to be built in pure vanilla JS/CSS (no Chart.js, no D3 — single-file constraint).

**Resolution:** Use CSS-only approaches:
- Gauge ring: SVG `<circle>` with `stroke-dasharray` animation
- Bar charts: CSS `width` percentage on `<div>` elements
- Radar: Skip it, use horizontal bars instead (simpler, more accessible)
- Tables: Standard HTML `<table>` with styled rows
- Cards: Flexbox card layout

**Impact if missed:** Attempting to import Chart.js violates single-file rule. Or results page is empty.

---

## 9. RTL FOR VENTURE NAME (LOW)

**Risk:** Users might enter venture names in Arabic. The auth screen, localStorage, and slug generation need to handle this. `slugify()` will strip Arabic chars, so the slug becomes empty or very short.

**Resolution:** The slug is for internal use only (localStorage key). If slugify produces a string shorter than 2 chars after processing, fallback to a numeric hash or transliteration.

**Better fix:** Add a minimum slug length check:
```javascript
let slug = slugify(text);
if (slug.length < 2) {
  slug = 'venture-' + Date.now().toString(36);
}
```

**Impact if missed:** Arabic venture names produce empty slugs → localStorage keys break.

---

## 10. MOBILE KEYBOARD PUSHES CONTENT (LOW)

**Risk:** Free-text `<textarea>` questions on mobile trigger the virtual keyboard, which pushes content up and can hide the question text or submit button.

**Resolution:** Add `scroll-margin-top: 120px` to question containers. When textarea gets focus, scroll it into view with adequate padding above.

**Impact if missed:** Mobile users can't see what they're typing or find the "Next" button.

---

## 11. NO eo-config UPDATE PATH (LOW)

**Risk:** The `eo-config/` directory has config files per scorecard. The old CLAUDE.md had a Step 7 to update these. The new workflow doesn't address config files.

**Resolution:** Ignore `eo-config/` for now. These are supplementary reference files. Update them AFTER all HTML is working. They are not load-bearing.

**Impact if missed:** None immediately. Config files become stale but nothing references them at runtime.

---

## RISK PRIORITY MATRIX

| # | Risk | Severity | Likelihood | Action |
|---|------|----------|-----------|--------|
| 1 | Design system mismatch | CRITICAL | HIGH | CLAUDE.md documents correct values |
| 2 | Slugify inconsistency | CRITICAL | MEDIUM | Exact copy from SHARED-PATTERNS.md |
| 3 | Old specs conflict | HIGH | HIGH | Rename with _DEPRECATED prefix |
| 4 | SKILL.md as source of truth | HIGH | MEDIUM | CLAUDE.md overrides, add warnings |
| 5 | SC5 no upstream data | MEDIUM | LOW | Fallback UI for motion selection |
| 6 | Webhook URL wrong | MEDIUM | MEDIUM | Documented in CLAUDE.md |
| 7 | Result key not scoped | MEDIUM | LOW | Migration code handles it |
| 8 | Complex visualizations | MEDIUM | MEDIUM | CSS-only approach documented |
| 9 | Arabic venture names | LOW | LOW | Slug fallback added |
| 10 | Mobile keyboard | LOW | MEDIUM | CSS scroll-margin fix |
| 11 | eo-config stale | LOW | HIGH | Defer, non-blocking |
