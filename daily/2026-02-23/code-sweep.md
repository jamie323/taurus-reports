# Code Sweep — Monday, Feb 23, 2026

## 📊 Git Activity

### WordQuest
**3 new commits** (Feb 22):
- `9edaa80` Add files via upload (+151, -78 in index.html)
- `43462eb` Add files via upload  
- `5e44939` Add files via upload

### AnyDrawFinal, MoneySavr, Taurus
✅ All up to date, no new commits

### Branch Status Notes
- AnyDrawFinal on `fix/force-unwraps` (local branch, no remote tracking)
- MoneySavr on `feature/subscription-hit-list`
- anydraw-feedback-api: no remote tracking configured

---

## 🔴 Critical Issues

None.

---

## 🟡 This Week

### WordQuest — Massive Data Files
**Issue:** Audio data files are 10-11 MB each (p3_audio_data.js, p4_audio_data.js, audio_data.js)

**Impact:**
- Initial page load will be slow on mobile
- Poor UX for kids on cellular data
- Browser memory pressure

**Fix:**
- Move audio to lazy-loaded chunks or external CDN
- Consider on-demand fetch per pack/level
- OR: Use compressed audio formats (Opus/AAC) instead of base64

**Effort:** Medium (2-3 hours to refactor)

---

### MoneySavr — Unfinished IAP Integration
**Locations:**
- `src/services/purchases.ts:123` — TODO: Replace with real IAP call
- `src/services/purchases.ts:157` — TODO: Replace with real restore
- `moneysavr-app/src/screens/HomeScreen.tsx:47` — TODO: Check actual purchase status

**Impact:**
- App shows purchase UI but does nothing when tapped
- Users can't unlock unlimited analyses

**Fix:**
- Implement react-native-iap purchase flow
- Wire up to App Store Connect product IDs
- Test with sandbox account

**Effort:** High (6-8 hours end-to-end with testing)

---

### MoneySavr — Console Logging in Production
**Locations:**
- 8+ `console.log` / `console.error` statements in production code

**Impact:**
- Performance drain on production builds
- Potential user data exposure in logs

**Fix:**
- Remove or gate behind `__DEV__` flag
- Use proper error reporting service (Sentry, etc.)

**Effort:** Low (30 min to audit and clean)

---

## 🟢 Ideas

### AnyDrawFinal — Missing TODOs
**Locations:**
- `DrawerViews.swift:565` — Replace with custom Animate PNG icon
- `HomeViews.swift:1846` — Confirm vertical gap spec
- `LibraryCategoriesView.swift:884` — Per-category crop factors

**Impact:** Low (minor UX polish)

**Effort:** Low per item (1-2 hours total)

---

### WordQuest — Error Handling Coverage
**Good news:** Audio playback has fallback to TTS on error (`currentAudio.play().catch(() => speakTTS(...))`)

**Observation:** No visible loading states between packs or levels. Consider adding shimmer/skeleton for pack transitions.

**Effort:** Low (2 hours)

---

### AnyDrawFinal — Accessibility
**Observation:** `.accessibilityIdentifier` present on key UI elements (tokens, home buttons). Good for UI testing.

**Gap:** No obvious VoiceOver labels or accessibility hints found in scanned files. Kids apps benefit from strong accessibility.

**Effort:** Medium (4-6 hours to audit and add labels)

---

## 📊 Competitor Intel

### Kids Drawing Apps (Feb 2026)
**Trending features:**
- **Drawing replay animation** — Reddit users highlight this as a standout feature (kids watch their drawing recreated stroke-by-stroke). AnyDraw currently lacks this.
- **Multiplayer drawing rooms** — Drawly app added real-time collaborative drawing. Could be interesting for AnyDraw's social layer.

**Relevance:** 🟢 Idea
- Replay animation is low-hanging fruit (save stroke data, replay on tap)
- Multiplayer is complex but differentiating

---

### Educational Word Games (Feb 2026)
**Trending:**
- Minecraft Education Edition still dominates (coding + teamwork angle)
- Prodigy English gaining traction (free for educators)
- Vocab Scrabble — simple digital Scrabble for vocab building

**Relevance:** Low for WordQuest (different audience, not classroom-focused)

---

## ✅ Quick Wins

1. **Remove console.log from MoneySavr** (30 min) → cleaner production builds
2. **Add loading spinner to WordQuest pack transitions** (2 hours) → better perceived performance
3. **Set up remote tracking for AnyDraw branches** (10 min) → easier collaboration

---

## Summary for Morning Briefing

**🟡 Action This Week:**
- WordQuest: Lazy-load audio files (10-11 MB blocking initial load)
- MoneySavr: Finish IAP integration (users can't purchase)
- MoneySavr: Remove console logs

**🟢 Nice-to-Have:**
- AnyDraw: Add drawing replay animation (competitor insight)
- WordQuest: Loading states between packs

**✅ Git Health:** All repos synced, 3 commits in WordQuest (UI updates)
