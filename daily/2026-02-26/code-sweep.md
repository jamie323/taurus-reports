# Code Sweep — February 26, 2026

## 📊 Summary
**Active repos:** 5 (AnyDrawFinal, MoneySavr, WordQuest, freefall-app, anydraw-feedback-api)  
**New commits (yesterday):** 11 commits in AnyDrawFinal  
**Critical issues:** 1  
**This week:** 3  
**Ideas:** 4  
**Competitor intel:** 1

---

## 🔴 CRITICAL

### AnyDrawFinal: Force unwrap crash risk in ArtworkStore
**File:** `ArtworkStore.swift` (lines 83, 92, 101, 206, 212, 243, 251, 270)  
**Issue:** Multiple `UIImage(contentsOfFile:)` force unwraps could crash if file is missing/corrupted  
**Impact:** Potential crash when loading saved artwork, thumbnails, or recent gallery  
**Fix:** Use guard-let or if-let pattern instead of force unwraps  
**Example pattern:**
```swift
// ❌ Current (crash risk)
let image = UIImage(contentsOfFile: outlinePath.path)!

// ✅ Safer
guard let image = UIImage(contentsOfFile: outlinePath.path) else {
    return nil // or default placeholder
}
```

---

## 🟡 THIS WEEK

### AnyDrawFinal: Large files need splitting
**File:** `ColoringApp.swift` (3,461 lines), `DrawingEngine.swift` (2,311 lines), `HomeViews.swift` (1,948 lines), `Modals.swift` (1,956 lines)  
**Issue:** God objects make collaboration harder, increase merge conflict risk  
**Fix:** Extract into smaller feature files (e.g., split ColoringApp into AppState, Subscriptions, TokenManager)  
**Priority:** Medium — not blocking but tech debt  

### AnyDrawFinal: Missing loading states
**Files:** `GenerationService.swift`, `TokenService.swift`  
**Issue:** Network calls lack user-visible loading indicators for AI generation and token sync  
**Impact:** Users may tap multiple times or think app is frozen during API calls  
**Fix:** Add loading states to UI layer when calling these services  

### anydraw-feedback-api: No error handling for missing GH_TOKEN
**File:** `api/submit.js` (line 1)  
**Issue:** If `GH_TOKEN` env var is missing, endpoint will fail with unclear error  
**Impact:** Beta feedback submissions fail silently  
**Fix:** Add startup validation and return clear error message  

---

## 🟢 IDEAS

### AnyDrawFinal: Empty state for first-time users
**Context:** HomeViews, RecentsGalleryView  
**Opportunity:** No explicit "welcome" or "create your first artwork" prompt when gallery is empty  
**Suggestion:** Show friendly empty state with CTA to browse library or generate AI art  

### AnyDrawFinal: Accessibility audit
**Context:** Canvas tools, color picker, undo/redo  
**Opportunity:** VoiceOver labels and Dynamic Type support not explicitly confirmed  
**Suggestion:** Run Xcode Accessibility Inspector pass to ensure WCAG Level AA compliance  

### AnyDrawFinal: Undo history limit unclear
**Context:** DrawingEngine handles undo stack, but no visible indicator of stack depth  
**Opportunity:** Users don't know how many steps back they can go  
**Suggestion:** Show undo count badge or disable button when stack is empty  

### WordQuest: Repo cleanup needed
**Context:** Root directory has duplicate data files (`p2_image_data.js`, `p3_image_data.js`, `p4_update_image_data.js`)  
**Issue:** Unclear which is source of truth for production assets  
**Suggestion:** Archive old versions to `/archive/` or delete if no longer needed  

---

## 📊 COMPETITOR INTEL

### Adobe Project Aqua continues to dominate kids drawing space
**Source:** [Adobe Aqua Learn Page](https://aqua.adobe.com/learn/drawing-apps-for-kids) (updated Feb 6, 2026)  
**Key features:**
- **3D Dunes:** 2D drawings → 3D models with AR viewing
- **Magic Filters (Firefly AI):** Transform sketches into claymation, origami, neon styles
- **Capture Cove:** Scan paper drawings, digitize, and store in personal museum
- **Price:** Free (no ads, no paywall)

**Implications for AnyDraw:**
- ✅ **AnyDraw advantage:** AI generation from text prompts (not just filters on existing art)
- ⚠️ **Gap:** No AR or 3D features (but may be overkill for toddler audience)
- ⚠️ **Gap:** No physical-to-digital scan feature (parents deal with paper pile)
- **Positioning opportunity:** Lean into AI *creation* (not just transformation), simpler UI for younger kids (2-5 vs Aqua's 5-12 target)

---

## 🚀 QUICK WINS

1. **AnyDrawFinal:** Add TODO completion for per-category crop factors (`LibraryCategoriesView.swift` line 93) — 15 min  
2. **anydraw-feedback-api:** Add GH_TOKEN validation at startup — 5 min  
3. **AnyDrawFinal:** Add empty state view to RecentsGalleryView — 30 min  
4. **WordQuest:** Archive duplicate data files — 10 min  

---

## 📦 GIT STATUS

### AnyDrawFinal
**Status:** ✅ Up to date  
**Recent commits (yesterday):** 11 commits  
- Canvas rendering optimizations
- Undo snapshot fixes
- Color retention improvements
- Splash branding updates
- Palette expansion + smart fill tools
- Beta fixes: music, voice, colours, AI prompt, animations

### MoneySavr
**Status:** ✅ Up to date  
**Recent commits:** None (yesterday)

### WordQuest
**Status:** ✅ Up to date  
**Recent commits:** None (yesterday)

### freefall-app
**Status:** ✅ Up to date  
**Recent commits:** None (yesterday)  
**Note:** Repo appears empty (no Swift/TS files found)

### anydraw-feedback-api
**Status:** 🟡 No remote tracking configured for `main` branch  
**Recent commits:** None (yesterday)  
**Action needed:** Set upstream with `git branch --set-upstream-to=origin/main main`

---

## 🎯 RECOMMENDED FOCUS TODAY

1. **🔴 Fix force unwrap crash risk in ArtworkStore** (30 min, high ROI)
2. **📊 Analyze Adobe Aqua positioning** (15 min, inform roadmap)
3. **🟡 Add loading states to AI generation UI** (45 min, better UX)
4. **🚀 Quick wins:** GH_TOKEN validation + empty state view (35 min)

---

*Generated by Taurus Code Sweep · 07:00 EET · Next run: Feb 27, 07:00*
