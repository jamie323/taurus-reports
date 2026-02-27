# Code Sweep — Friday, February 27, 2026

## 📊 Git Activity

### WordQuest
- ✅ **1 new commit** (94fd942 → cddc947)
  - File: `index.html` (+56/-25 lines)
  - Change: "Add files via upload"
  - Impact: HTML structure changes

### Starlet
- ✅ **67 commits since yesterday**
  - Heavy asset generation activity
  - Curator tool workflow (GPT Image 1 integration)
  - Asset merges, outfit positioning fixes, new SVG assets
  - Nightly backup automation working

### All Other Repos
- ✅ AnyDrawFinal, MoneySavr, FreeFall: up to date, no new commits

### anydraw-feedback-api
- 🔴 **CRITICAL: Broken tracking** — `git pull` fails, no upstream branch set
  - Fix: `cd ~/.openclaw/workspace/repos/anydraw-feedback-api && git branch --set-upstream-to=origin/main main`

---

## 🔴 Critical Issues

### 1. AnyDrawFinal: Force Unwrap Risk (178 instances)
**Severity:** 🔴 Critical  
**Location:** Across Swift files  
**Risk:** Force unwraps (`!`) can crash the app if optional is nil  
**Fix:** Run audit to convert to `guard let` or `if let` pattern  
**Effort:** 2-3 hours (semi-automated with regex + spot-check)

### 2. anydraw-feedback-api: Git Broken
**Severity:** 🔴 Critical  
**Location:** `~/.openclaw/workspace/repos/anydraw-feedback-api`  
**Risk:** Can't pull updates, sync issues  
**Fix:** Set upstream branch  
**Effort:** 30 seconds

---

## 🟡 This Week

### 3. WordQuest: Missing Error Handling Context
**Severity:** 🟡 This week  
**Location:** `index.html` (audio playback, localStorage, state serialization)  
**Issue:** 
- Silent `catch(e) {}` blocks — no logging, no user feedback
- Audio errors fall through with no recovery UX
- Example: Line 1534-1538 — audio error just silently switches to TTS
**Fix:** Add error state UI + log to console for debugging  
**Effort:** 1 hour

### 4. Starlet: No Loading/Empty States
**Severity:** 🟡 This week  
**Location:** `index.html` (item grid, wardrobe modal)  
**Issue:** 
- No feedback while assets load
- Empty wardrobe shows generic text, no illustration
- No error state for failed asset loads
**Fix:** Add shimmer loaders, empty state illustration, retry button  
**Effort:** 2 hours (design + implement)

### 5. MoneySavr: Missing Input Validation
**Severity:** 🟡 This week  
**Location:** `App.tsx` + core pipeline  
**Issue:** 
- No file size limits before processing (could crash on huge images)
- No validation for CSV structure before parsing
- API key stored but not validated before first use
**Fix:** Add pre-flight checks with friendly error messages  
**Effort:** 1 hour

---

## 🟢 Ideas

### 6. AnyDrawFinal: Accessibility Audit
**Severity:** 🟢 Idea  
**Location:** All SwiftUI views  
**Opportunity:** 
- Already has `Motion.swift` for reduce motion
- Missing: VoiceOver labels, dynamic type support, haptic consistency
**Fix:** Accessibility pass (VoiceOver, contrast, hit targets)  
**Effort:** 3-4 hours  
**Impact:** App Store feature consideration, broader audience

### 7. WordQuest: Offline-First Architecture
**Severity:** 🟢 Idea  
**Location:** Audio + state management  
**Opportunity:** 
- All assets are local
- Add service worker for instant load
- Cache audio files aggressively
**Fix:** Progressive Web App upgrade  
**Effort:** 2 hours  
**Impact:** Better performance, especially on repeat plays

### 8. Starlet: Undo/Redo Stack
**Severity:** 🟢 Idea  
**Location:** Canvas state management  
**Opportunity:** 
- Kids make mistakes, want to go back
- No undo currently (only delete stickers one-by-one)
**Fix:** Implement state history (last 10 actions)  
**Effort:** 3 hours  
**Impact:** Major UX win, reduces frustration

### 9. MoneySavr: Transaction Tagging
**Severity:** 🟢 Idea  
**Location:** Results screen  
**Opportunity:** 
- Let users add custom tags (e.g., "business", "vacation", "gift")
- Filter/group by tags in history
**Fix:** Add tag UI + persistence layer  
**Effort:** 4 hours  
**Impact:** Power user feature, better long-term tracking

---

## 📊 Competitor Intel

### Dress-Up Games (Starlet)
- **Roblox Dress to Impress** still dominating in Feb 2026
- New codes system: seasonal items (balloons, star headpiece, glasses for 2026)
- **Insight:** Timed/seasonal content drives engagement — consider event-based asset drops for Starlet

### Word Learning Games (WordQuest)
- Phonics learning market: heavy focus on gamification + multi-sensory (audio + visual)
- No breakout narrative-driven word games detected this week
- **Insight:** WordQuest's storybook format remains differentiated — lean into quest progression UX

### Finance Apps (MoneySavr)
- No significant competitor moves this week
- AI receipt scanning trend continues (multiple new entrants)
- **Insight:** MoneySavr's screenshot→categorization flow is unique — emphasize speed/simplicity in marketing

---

## ✅ Quick Wins

### 10. AnyDrawFinal: Add Loading Spinner to GenerationService
**Location:** `GenerationService.swift`  
**Fix:** Show spinner during API call (currently just waits silently)  
**Effort:** 15 minutes  
**Impact:** Reduces perceived wait time

### 11. WordQuest: Add Retry Button to Audio Errors
**Location:** `index.html` audio error handler  
**Fix:** Instead of silent fallback, show "Audio failed. Retry?" button  
**Effort:** 20 minutes  
**Impact:** Better user control

### 12. Starlet: Add Haptic Feedback to Buttons
**Location:** All `.cattab`, `.ic`, `.mbt` buttons  
**Fix:** Add `navigator.vibrate(10)` on tap (mobile only)  
**Effort:** 10 minutes  
**Impact:** More tactile, premium feel

### 13. MoneySavr: Show File Size Before Processing
**Location:** `App.tsx` image picker callback  
**Fix:** Display "Processing 2.3 MB..." before starting  
**Effort:** 10 minutes  
**Impact:** Transparency, sets expectations

---

## 🧹 Dead Code Cleanup Candidates

- **AnyDrawFinal:** 1 `fatalError` call (low priority, likely in debug-only path)
- **Starlet:** Multiple HTML files in root (old curator versions) — consider archiving to `/archive/`
- **FreeFall:** Empty repo (just README + docs) — confirm if active or can be archived

---

## 🎯 Recommended Action Order

1. 🔴 Fix anydraw-feedback-api git tracking (30 seconds)
2. 🔴 AnyDrawFinal force unwrap audit (2-3 hours, schedule for next week)
3. ✅ Quick wins 10-13 (1 hour total, do today)
4. 🟡 WordQuest error handling + Starlet loading states (3 hours, do this week)
5. 🟡 MoneySavr input validation (1 hour, do this week)

---

**Total Issues Found:** 13  
**Critical:** 2 | **This Week:** 3 | **Ideas:** 4 | **Quick Wins:** 4  
**Estimated Fix Time (Priority Items):** ~7 hours
