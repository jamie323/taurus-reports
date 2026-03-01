# Morning Code Sweep — March 1, 2026

## 📊 Repository Status

| Repo | Status | Language | Last Commit |
|------|--------|----------|-------------|
| AnyDrawFinal | ✅ Clean | Swift/iOS | No new commits (24h) |
| MoneySavr | 🟡 IAP Stubs | TypeScript/React Native | No new commits (24h) |
| anydraw-feedback-api | ✅ Clean | JavaScript/Vercel | No new commits (24h) |
| WordQuest | ✅ Clean | HTML/JS | No new commits (24h) |
| taurus | ✅ Clean | Mixed | No new commits (24h) |
| starlet | ✅ Clean | Mixed | No new commits (24h) |
| freefall-app | ✅ Clean | HTML/JS | No new commits (24h) |

---

## 🔴 Critical Issues

**None detected.**

---

## 🟡 This Week

### MoneySavr — IAP Implementation Stubs
**File:** `src/services/purchases.ts`
**Lines:** Contains `TODO` markers for production IAP integration

```typescript
// TODO: Replace with real IAP call
// TODO: Replace with real restore
// DEBUG (remove in production)
```

**Impact:** High — App cannot monetize without real IAP
**Effort:** Medium (2-3 hours)
**Action:** Implement real StoreKit/RevenueCat integration before launch

---

## 🟢 Ideas & Quick Wins

### AnyDrawFinal — Loading States Present ✅
**Status:** Good UX coverage
- Uses `ProgressView` in modals, prompt generation, and recents gallery
- Has empty state handling for library categories
- Drawing canvas has blocked mask validation

**No action needed** — loading/empty states are implemented.

---

### MoneySavr — UX Gaps to Fill

1. **Error State on Screenshot Extraction Failure**
   - File: `core/extractor/screenshot-extractor.ts`
   - Current: Throws error
   - Suggested: Add user-friendly error message + retry UI

2. **Empty State for Zero Transactions**
   - Check if onboarding flow handles "no transactions yet" gracefully
   - Effort: 30 min

3. **Loading State During CSV Parse**
   - Large files may cause UI freeze
   - Add spinner for files > 50 rows
   - Effort: 20 min

---

### WordQuest — Accessibility Audit
**Status:** No obvious accessibility attributes detected in HTML
**Suggestion:** Add ARIA labels for screen reader support (kids may use VoiceOver)
**Effort:** 1-2 hours

---

### AnyDraw Feedback API — Environment Variable Validation
**Status:** Uses `process.env.GH_TOKEN` without fallback
**Suggestion:** Add runtime check + friendly error if missing
**Effort:** 10 min

```javascript
const GH_TOKEN = process.env.GH_TOKEN;
if (!GH_TOKEN) {
  return res.status(500).json({ error: 'Server config missing' });
}
```

---

## 📊 Competitor Intel

### AI Drawing Apps (AnyDraw)
- **Trend (Feb 2026):** TikTok viral trend — "sketch to image AI" and "convert kids drawing to digital art"
- **Competitor Feature:** AI transforms children's drawings in minutes (ChatGPT/Copilot/Gemini integrations)
- **Gap Analysis:** AnyDraw already does this with custom server — potential marketing angle: "we're already viral-ready"
- **Action:** Consider TikTok marketing push highlighting the "child drawing to real art" transformation

### Expense Trackers (MoneySavr)
- **New Features (Feb 2026):**
  - **Auto-categorization** (ReceiptsAI, Webgility)
  - **Multi-currency posting** (Webgility AI)
  - **Export to Excel/PDF** (ReceiptsAI)
  - **Vendor normalization** (Webgility)

- **MoneySavr Status:**
  - ✅ Has categorizer (merchant dictionary + recurring detector)
  - ✅ Has screenshot extraction (via OpenAI vision)
  - ❌ No PDF/Excel export yet
  - ❌ No multi-currency support

- **Quick Win:** Add CSV export with categorized data (already has parser, just need reverse)
  - Effort: 1-2 hours
  - High value for users who want to import into QuickBooks/Excel

---

## 🛡️ Security Scan

### ✅ No Hardcoded Secrets
- All API keys properly use environment variables
- `anydraw-feedback-api` correctly uses `process.env.GH_TOKEN`
- No plaintext passwords detected

### ✅ No Large Files Detected
- All repos under healthy size limits
- No binaries committed to git (assets properly gitignored)

---

## 🧹 Code Quality Notes

### AnyDrawFinal (Swift)
- **Good:** Proper use of optionals (`isEmpty` checks before access)
- **Good:** Sound asset validation with missing file detection
- **Good:** Environment variable handling in UI tests
- **No unused imports detected** in sample files

### MoneySavr (TypeScript)
- **Good:** Strong typing with `/core/types/` separation
- **Good:** Modular pipeline (extractor → parser → categorizer → analyzer)
- **Potential improvement:** Add error boundaries in React Native components

### anydraw-feedback-api (JavaScript)
- **Good:** CORS properly configured
- **Good:** Method validation (POST/OPTIONS)
- **Good:** Emoji-driven UX in GitHub issue titles (visual triage)

---

## 📋 Actionable Summary

### Today (Sunday, Light Work)
1. Nothing critical — all systems green

### This Week
1. **MoneySavr:** Implement real IAP (removes DEBUG stubs)
2. **MoneySavr:** Add CSV export feature (competitive gap)
3. **AnyDraw Feedback API:** Add env var validation (10 min)

### Nice to Have
1. **WordQuest:** Accessibility audit (ARIA labels)
2. **MoneySavr:** Multi-currency support (future-proofing)
3. **AnyDraw:** TikTok marketing push (ride the "sketch-to-AI" trend)

---

## 🎯 Repo Health Score

| Repo | Score | Notes |
|------|-------|-------|
| AnyDrawFinal | 🟢 9/10 | Production-ready, good UX patterns |
| MoneySavr | 🟡 7/10 | Solid core, needs IAP + export |
| anydraw-feedback-api | 🟢 9/10 | Simple, works well, minor hardening |
| WordQuest | 🟢 8/10 | Functional, could use a11y boost |
| taurus | 🟢 8/10 | No issues detected |
| starlet | 🟢 8/10 | No issues detected |
| freefall-app | 🟢 8/10 | Prototype stage, clean |

---

**Generated:** Sunday, March 1, 2026 — 07:00 AM (Europe/Athens)  
**Next Sweep:** Monday, March 2, 2026 — 07:00 AM
