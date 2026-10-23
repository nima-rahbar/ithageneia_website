# Changelog

All notable changes to the **Greek Citizenship Exam Prep (Προετοιμασία Π.Ε.Γ.Π. - Ιθαγένεια)** application are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.2] - 2026-10-23

### Added
- **Interactive Relation Tables (`sorting`)**:
  - Full support and interactive UI for categorization and classification table questions (e.g., Question 99 in Geography — `geografia_q44`, sorting items into two distinct columns: *Στήλη Ι: Ποταμοί* and *Στήλη ΙΙ: Λίμνες*).
  - Built `SortingQuestionContent` featuring an unassigned items pool chip grid, interactive destination columns/tables, tap-to-place and tap-to-remove mechanics, and per-item validation badges (✅ / ❌).
- **Two-Column Matching Tables (`matching`)**:
  - Full interactive support for pairing questions across Geography, History, Institutions, and Culture (e.g., `geografia_matching_45`, `politismos_matching_*`, `istoria_matching_*`, `thesmoi_matching_*`).
  - Built `MatchingQuestionContent` with Column I target slot cards, docked match chips, Column II option source cards with pairing tags (`↳ Συνδέθηκε με...`), tap-to-pair / tap-to-detach controls, and pairing progress indicators.
- **Map & Multi-Select Question Support**:
  - Added `MapQuestionContent` with structured location tables (number badges, place names, regions) and self-evaluation reveal flow.
  - Added `MultiSelectQuestionContent` with multi-choice checkbox selection, RTL translation support, and set-based answer verification.
- **Data Model Enhancements**:
  - Added `CategoryDef` data class and `categories` mapping to the `Question` model to deserialize category table headers and items.
  - Extended `UserAnswer` with `matchingPairs: Map<String, String>?` and `sortingResult: Map<String, List<String>>?` to persist user matching and sorting states across app restarts.
- **System Default Theme Option**:
  - Added full support for System Theme Mode (`AppThemeMode.SYSTEM`) alongside Light and Dark modes, set as the default out of the box.
  - Dynamically adapts to Android OS system day/night mode, dark mode schedules, and battery saver.
  - Added a 3-way theme selector in Settings (*Προεπιλογή Συστήματος*, *Φωτεινό Θέμα*, *Σκοτεινό Θέμα*) across all 5 supported languages.
  - Updated the top bar quick toggle to cycle through System, Light, and Dark modes.
- **Multilingual UI Strings**:
  - Added localized strings for relation tables, pairing instructions, column headers, and action buttons (*Επαλήθευση*, *Καθαρισμός*, *Συνδέθηκαν*, *Διαθέσιμα Στοιχεία*) in Greek, English, Persian, Arabic, and Turkish.

### Changed
- **Answer Persistence**:
  - Wired `onAnswerSubmitted` in `StudyScreen` (both phone single-pane and tablet dual-pane layouts) and `BookmarksScreen` to persist matching and sorting answers to `MainViewModel` and SharedPreferences.
- **Result Feedback Banner**:
  - Refined answer display in `QuestionCard` to cleanly format non-multiple-choice answers without duplicate labels.
- **Exam Simulator Balancing**:
  - Updated `QuestionRepository.generateExamQuestions` to ensure test simulations pick standard multiple-choice questions with valid options.
- **Memory & Bitmap Optimization (Google Play Recommendation)**:
  - Replaced unmanaged full-resolution `BitmapFactory.decodeStream()` with a custom `BitmapUtils` utility implementing Google's recommended two-pass `inSampleSize` downsampling and `RGB_565` color config.
  - Added an in-memory `LruCache` (capped at 1/8th max heap) and offloaded bitmap decoding to `Dispatchers.IO` to eliminate UI stutter and prevent `OutOfMemoryError` on oral exam images.

### Fixed
- Fixed an issue where questions with relation and classification tables appeared completely blank with no items or options displayed.
- Resolved Java/Kotlin deprecation warning for `GsonBuilder.setLenient()` by migrating to `GsonBuilder.setStrictness(Strictness.LENIENT)` in `QuestionRepository` and `TranslationRepository`.
- Resolved Java deprecation warning for `Locale("el", "GR")` constructor by migrating to `Locale.forLanguageTag("el-GR")` in `MainViewModel`.
- Migrated deprecated `Icons.Default.VolumeUp` and `Icons.Default.List` to their `AutoMirrored` counterparts (`Icons.AutoMirrored.Filled.*`) for bidirectional / RTL layout support.
- Migrated deprecated Material 3 `Divider` to `HorizontalDivider` in `OralScreen`.
- Addressed Google Play Console performance recommendation regarding unconstrained `BitmapFactory` allocations without downsampling.
- Configured `ndk.debugSymbolLevel = "FULL"` in `app/build.gradle.kts` to package native crash and ANR debug symbols directly into the release App Bundle (.aab), resolving Google Play Console's missing native symbols warning.
- **Continuous Audio Playback in Akoustika**: Fixed an issue where navigating to the next or previous question in the listening comprehension section caused the audio player to stop and restart from 0:00; audio now continues playing seamlessly across all questions sharing the same audio track in a unit.

---

## [1.0.1] - 2026-10-22

### Added
- Right-to-Left (RTL) layout support for Arabic and Persian translations.
- Dual-pane layout support for foldables and large-screen tablet devices.
- Audio streaming fallback and caching for listening comprehension exercises.

### Changed
- Improved TTS (Text-to-Speech) pronunciation and playback controls.
- Optimized app bundle size and ProGuard / R8 keep rules.

### Fixed
- Fixed audio player UI state desynchronization when jumping between questions.
- Fixed translation drawer toggle state retention during screen rotation.

---

## [1.0.0] - 2026-10-20

### Added
- **Initial Release** of Greek Citizenship Exam Prep (Προετοιμασία Π.Ε.Γ.Π. - Ιθαγένεια) on Android.
- Comprehensive question bank covering 840+ official questions across all exam domains (Geography, History, Institutions, Culture, Language).
- Timed 20-question official Exam Simulation mode with detailed scorecards and history.
- Oral exam practice modules with 26 speaking scenarios and authentic visual stimuli.
- Written exam workshop with 100 modules including reading comprehension and live essay word counters.
- Multilingual translation companions in English, Persian, Arabic, and Turkish.
- Bookmark management and dark/light Material 3 theme support.
