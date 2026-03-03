# Code Sweep — March 3, 2026

## 📦 Git Activity (Last 24h)

### AnyDrawFinal (3 commits)
- ✅ **Vehicle regen** — Switched to gpt-image-1 stamp style + rainbow sky background  
- ✅ **Restore original animals** — Replaced by mistake in beta regen  
- ✅ **Local edits** — ColoringApp, HomeViews, MusicManager updates  

### FreeFall (27 commits) 🔥
**Major development sprint:** Physics tuning, tap routing, level complete screen, fireworks, audio session fixes, CGPoint Codable fix for level decoder, Xcode Cloud CI/CD setup.

Key fixes:
- Ball physics: gravity reduction (280 → 60), upward launch arc, vertical-only damping, velocity control  
- Tap routing via SwiftUI instead of SpriteKit touchesBegan  
- Audio session: `.playback` mode ignores silent switch  
- Level decoder: added `Codable` conformance for CGPoint/CGSize/CGVector  
- Xcode Cloud: fixed build + TestFlight distribution  
- Fireworks celebration on level complete  

### Starlet (3 commits)
- Updated HTML + UI JSON (commit messages not descriptive)

### MoneySavr, WordQuest
- No changes in last 24h

---

## 🔴 Critical Issues

**None detected** — No merge conflicts, no hardcoded secrets, no exposed credentials.

---

## 🟡 Code Quality (This Week)

### AnyDrawFinal

#### File Size — Split Candidates
- **ColoringApp.swift** (3,461 lines) 🟡  
  Should split into: ColoringViewModel, ColoringToolbar, ColoringCanvas, ColoringState  
  **Impact:** Hard to navigate, merge conflicts likely

- **DrawingEngine.swift** (2,311 lines) 🟡  
  Should split into: DrawingEngine core, BrushEngine, EraserEngine, FillEngine  
  **Impact:** Performance-critical file needs modular testing

- **HomeViews.swift** (1,990 lines) 🟡  
  Should split into: HomeScreen, CategoryCarousel, SubscriptionBanner, OnboardingFlow  
  **Impact:** Hard to review UI changes

- **Modals.swift** (1,956 lines) 🟡  
  Should split into: PaywallModal, TutorialModal, SettingsModal, ShareModal  
  **Impact:** Each modal is independent, should be separate

#### Force Unwraps — Low Risk
- **1 force unwrap in UI tests** (AnyDrawOvernightUITests.swift line: `options.randomElement()!`)  
  Risk: Test-only, acceptable  
- **All production force unwraps are guarded** (using `if let` / `guard let`)  
  ✅ Good: No crash vectors in shipping code

#### TODO Comments
- **LibraryCategoriesView.swift:** "TODO: If per-category crop factors are provided, apply them here."  
  🟢 Low priority — feature request, not a bug

#### UX Gaps
- **16 loading states** implemented ✅  
- **64 error handling cases** ✅  
- **Empty states:** Not explicitly checked — recommend audit of Library/Gallery views for "no items" messaging

### FreeFall

#### Code Structure ✅
- Largest file: GameScene.swift (690 lines) — acceptable for SpriteKit  
- Physics split into GameScenePhysics.swift (376 lines) — good separation  
- No force unwraps in production code (2 safe uses with guards)

#### UX Gaps
- **No loading state** for level JSON decoding — if level fails to load, user sees blank screen  
  🟡 Add: ProgressView + error message if `LevelDefinition.load()` fails  
- **No retry on level load failure** — user must force-quit app  
  🟡 Add: "Couldn't load level. Tap to retry." button

#### Audio Polish ✅
- Music plays on launch despite silent switch (`.playback` session)  
- World music starts when level starts  
- Good: Music loops implemented in AudioManager

### Starlet

#### HTML Size
- **index.html** (2,253 lines) 🟡  
  Should split CSS into separate file for maintainability  
  **Quick win:** Extract `<style>` block → `starlet.css`

#### JS Bundling
- All logic inline in HTML — should move to `starlet.js`  
  **Impact:** Hard to debug, no source maps

---

## 🟢 Ideas & Quick Wins

### AnyDrawFinal

#### Quick Wins
1. **Empty state messaging** (2h)  
   Add "No coloring pages yet! Tap + to create one." to LibraryCategoriesView when manifest is empty  

2. **Animation polish** (1h)  
   Add `.bounce` effect when drawing tool switches (already used in Starlet)

3. **Accessibility labels** (3h)  
   Audit all Image/Button views for `.accessibilityLabel()` — required for VoiceOver support

#### Ideas
1. **Color by Number mode** 🎨  
   Competitor: Bimi Boo app launched this in Feb 2026 (App Store update notes)  
   Effort: 3-5 days to build regions + number labels  
   Revenue: Premium feature, high engagement in kids apps

2. **Animated stickers** 🌟  
   Competitor trend: Kids apps adding animated GIF stickers to coloring pages  
   Effort: 1 week to build Lottie integration + premium library  
   Revenue: Premium upsell, high parent appeal

### FreeFall

#### Quick Wins
1. **Level load retry** (1h)  
   Wrap LevelDefinition.load() in do-catch, show alert with retry button

2. **Debug overlay toggle** (30m)  
   Currently on-screen debug stats hardcoded — move to Settings toggle

3. **Haptic feedback on flip** (30m)  
   Add `.impact(.medium)` when ball flips gravity — feels juicier

#### Ideas
1. **Slow-motion replay** on level complete (like golf games)  
   Show final 3 seconds in slow-mo before fireworks  
   Effort: 2 days (SpriteKit SKAction.speed)  
   Impact: High polish, viral-worthy

### Starlet

#### Quick Wins
1. **Extract CSS** (30m)  
   Move `<style>` → `starlet.css`, link in HTML  
   Impact: Easier to edit colors/layout

2. **Extract JS** (1h)  
   Move inline `<script>` → `starlet.js`  
   Impact: Debuggable, source maps work

---

## 📊 Competitor Intel

### Kids Coloring Apps (AnyDrawFinal space)
**Trend:** Color by Number mode  
- Bimi Boo launched Feb 2026  
- "Drawing mode simplified for kids" — simplified brush controls for toddlers  
- Sound + animation feedback on color complete (like AnyDraw current design ✅)

**Recommendation:** AnyDraw already ahead with AI generation, but Color by Number would be easy premium add-on.

### Casual Physics Games (FreeFall space)
**Steam releases:** Gravity Game, Gravity Flip X, Free Yourself  
- Gravity flip mechanic common (FreeFall ✅ has this)  
- Story-driven progression (FreeFall needs this — current design is pure arcade)  
- "Real Newtonian Physics" marketing angle (FreeFall can use this)

**Differentiation:** FreeFall's neon glow + music-driven worlds unique. Double down on music sync.

---

## 🎯 Action Summary

### Critical (Do Today)
- None ❤️

### This Week
1. **FreeFall:** Add level load retry + error messaging (1h)  
2. **AnyDrawFinal:** Add empty state messaging to Library views (2h)  
3. **Starlet:** Extract CSS/JS for maintainability (1.5h)

### Ideas Backlog
1. **AnyDrawFinal:** Color by Number mode (competitor trend, 3-5 days)  
2. **FreeFall:** Slow-motion replay on level complete (2 days, high polish)  
3. **AnyDrawFinal:** Animated stickers (1 week, premium upsell)

---

**Total repos scanned:** 5 active (AnyDrawFinal, FreeFall, Starlet, MoneySavr, WordQuest)  
**Total commits (24h):** 33  
**Critical issues:** 0  
**This week tasks:** 3  
**Ideas flagged:** 3

---

*Generated by Taurus Code Sweep*  
*Next sweep: March 4, 2026 @ 07:00*
