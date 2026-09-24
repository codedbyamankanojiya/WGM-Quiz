# 🏆 WGM Quiz — Who's Gonna Be Millionaire

<p align="center">
  <img src="app/src/main/assets/Millionaire.png" alt="WGM Quiz Logo" width="120" />
</p>

<p align="center">
  <strong>A modern, high-production Android quiz game inspired by the iconic <em>Kaun Banega Crorepati / Who Wants to Be a Millionaire</em> TV game show format.</strong><br>
  A personal open-source project engineered with 100% Jetpack Compose (Material 3), Clean Architecture (MVVM + UDF), Room Database, Triple MediaPlayer & SoundPool Audio Engine, and Kotlin Coroutines.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Android-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="Platform: Android" />
  <img src="https://img.shields.io/badge/Language-Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white" alt="Language: Kotlin" />
  <img src="https://img.shields.io/badge/UI-Jetpack%20Compose%20(M3)-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white" alt="Jetpack Compose" />
  <img src="https://img.shields.io/badge/Min%20SDK-24%20(Android%207.0)-00C853?style=for-the-badge" alt="Min SDK: 24" />
  <img src="https://img.shields.io/badge/Target%20SDK-37%20(Android%2015)-00B0FF?style=for-the-badge" alt="Target SDK: 37" />
  <img src="https://img.shields.io/badge/License-MIT-FACC15?style=for-the-badge" alt="License: MIT" />
</p>

---

## 📑 Table of Contents
1. [Overview & Visual Aesthetic](#-overview--visual-aesthetic)
2. [Game Features & Mechanics](#-game-features--mechanics)
3. [Lifeline System](#-lifeline-system)
4. [Audio Engine Architecture](#-audio-engine-architecture)
5. [Architecture & Technical Blueprint](#-architecture--technical-blueprint)
6. [Tech Stack & Dependencies](#-tech-stack--dependencies)
7. [Directory & Project Structure](#-directory--project-structure)
8. [Setup, Build & Execution Guide](#-setup-build--execution-guide)
9. [Author & License](#-author--license)

---

## 🌟 Overview & Visual Aesthetic

**WGM Quiz** delivers the suspenseful, adrenaline-fueled atmosphere of primetime TV quiz shows directly to Android. 

Key visual & sensory elements:
- **Atmospheric Studio Lighting**: Midnight-blue and deep navy canvas with animated radial spotlight glows and pulsing golden halo effects around the Millionaire seal.
- **Hexagonal Broadcast Badges**: Custom hexagonal cards and buttons reflecting the classic international game-show branding.
- **Dynamic Audio Orchestration**: An audio engine that synchronizes ambient loop tracks with instantaneous sound effects for locks, reveals, timeouts, and jackpot celebrations.

---

## 🎮 Game Features & Mechanics

### 1. 🪜 15-Tier Progressive Money Ladder
Players advance across 15 escalating tiers from **₹1,000** to the ultimate jackpot of **₹7 Crores**, earning coins at every milestone:

| Level | Prize Money | Coin Reward | Milestone Status |
|:---:|:---:|:---:|:---:|
| **15** | **₹7,00,00,000** | 2,000 Coins | 🏆 **Grand Jackpot** |
| 14 | ₹5,00,00,000 | 1,800 Coins | — |
| 13 | ₹3,00,00,000 | 1,600 Coins | — |
| 12 | ₹1,00,00,000 | 1,400 Coins | — |
| 11 | ₹50,00,000 | 1,200 Coins | — |
| **10** | **₹3,20,000** | 1,000 Coins | 🛡️ **Guaranteed Safe-Haven 2** |
| 9 | ₹1,60,000 | 900 Coins | — |
| 8 | ₹80,000 | 800 Coins | — |
| 7 | ₹40,000 | 700 Coins | — |
| 6 | ₹20,000 | 600 Coins | — |
| **5** | **₹10,000** | 500 Coins | 🛡️ **Guaranteed Safe-Haven 1** |
| 4 | ₹5,000 | 400 Coins | — |
| 3 | ₹3,000 | 300 Coins | — |
| 2 | ₹2,000 | 200 Coins | — |
| 1 | ₹1,000 | 100 Coins | Starting Tier |

- **Guaranteed Safe-Havens**: Reaching Level 5 (₹10,000) and Level 10 (₹3,20,000) locks in guaranteed cash payouts even if a later question is missed.
- **30-Second Pressure Timer**: Circular countdown timer with real-time arc animation that dynamically shifts color from Gold (`#FACC15`) to Warning Orange (`#FB923C`) and Urgent Red (`#EF4444`).
- **Persistent Economy & High Scores**: Player coins, best level reached, games played, and total earnings are persisted via Jetpack DataStore across sessions.

---

## 🛟 Lifeline System

Players have access to 4 strategically designed lifelines:

| Lifeline | Icon | Functionality |
|---|:---:|---|
| **50:50** | `50:50` | Eliminates two incorrect choices, leaving only the right answer and one random distractor. |
| **Audience Poll** | `👥` | Simulates a live studio audience voting distribution weighted by question tier difficulty. |
| **Flip Question** | `🔄` | Discards the current question and serves a fresh alternative from the same difficulty tier. |
| **Extra Life** | `❤️` | Automatically activates when a wrong answer is selected, offering an option to revive or walk away. |

---

## 🔊 Audio Engine Architecture

The game incorporates a dedicated **Dual Audio Engine** combining Android `MediaPlayer` for atmospheric loops and `SoundPool` for ultra-low latency response SFX:

```
┌─────────────────────────────────────────────────────────────┐
│                    WgmSoundManager                          │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │          MediaPlayer Engine (Looping BGMs)          │   │
│   │  • WGM Home.mp3      (Lobby Theme)                  │   │
│   │  • Question.mp3      (Tension Question Background)  │   │
│   │  • Timer.mp3         (30s Urgent Countdown Loop)    │   │
│   └─────────────────────────────────────────────────────┘   │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │           SoundPool Engine (Zero-Latency SFX)       │   │
│   │  • Lock.mp3          (Option Selection / Lock)      │   │
│   │  • Right Answer.mp3  (Correct Reveal & Fanfare)     │   │
│   │  • Wrong Answer.mp3  (Incorrect Reveal Cue)         │   │
│   │  • Time Up.mp3       (Clock Expiry Gong)            │   │
│   └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

- **Lifecycle Aware**: Automatically pauses and resumes audio during `onPause`, `onResume`, and `onDestroy` lifecycle events.
- **Software Synthesizer Fallback (`WgmSynthesizer`)**: Pure Kotlin `AudioTrack` sine-wave generator to provide fallback sound cues in low-resource environments.

---

## 🏛️ Architecture & Technical Blueprint

WGM Quiz strictly adheres to **Clean Architecture** with **Unidirectional Data Flow (UDF)**:

```
┌────────────────────────────────────────────────────────────────────────┐
│                        PRESENTATION LAYER                              │
│   • WgmHomeScreen (Hero Banner, High Score, Start CTA)                 │
│   • WgmGameScreen (Question Card, 4 Option Hexagons, Timer, Lifelines) │
│   • WgmMoneyLadderScreen (Interactive 15-Level Tier Overlay)           │
│                                  ▲                                     │
│                     StateFlow    │    Intents / Actions                │
│                   (GamePhase)    │   (SelectAnswer, UseLifeline, Walk) │
│                                  ▼                                     │
│                            WgmViewModel                                │
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
                                   ▼
┌────────────────────────────────────────────────────────────────────────┐
│                           DOMAIN LAYER                                 │
│   • WgmQuestion (Domain Model)                                         │
│   • WgmQuizRepository (Interface Contract)                             │
│   • GamePhase (State Machine: Loading, InProgress, Correct, GameOver)  │
└──────────────────────────────────▲─────────────────────────────────────┘
                                   │
                                   ▼
┌────────────────────────────────────────────────────────────────────────┐
│                            DATA LAYER                                  │
│   • WgmQuizRepositoryImpl (Data Provider & Room Orchestrator)          │
│   ├── Room Database v2 (45 Pre-Seeded Tiered Questions)               │
│   ├── WgmQuestionDao (SQLite Entity Mapping)                           │
│   └── DataStore (Player Economy & High Score Persistence)              │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack & Dependencies

| Category | Technology / Library | Purpose |
|---|---|---|
| **Language** | Kotlin 2.0 | Core programming language with Coroutines & StateFlow |
| **UI Toolkit** | Jetpack Compose (BOM 2024.02.02) | 100% declarative UI with Material 3 styling |
| **Architecture** | MVVM + Clean Architecture + UDF | Scalable, testable state management (`GamePhase`) |
| **Local Database** | Room Database v2 + KSP | SQLite caching & pre-seeded 45-question bank |
| **State Persistence** | Jetpack DataStore Preferences | Player high scores, coins, and economy persistence |
| **Audio** | Android MediaPlayer + SoundPool | Low-latency audio playback & ambient loops |
| **Navigation** | Navigation Compose | Composable screen transitions |
| **Target SDK** | Android 15 (API Level 37) | Latest Android SDK capabilities |
| **Min SDK** | Android 7.0 (API Level 24) | Broad backward compatibility |

---

## 📁 Directory & Project Structure

```
WGM Quiz/
├── app/
│   ├── build.gradle                          # Module-level build script & dependencies
│   ├── proguard-rules.pro                    # R8 / ProGuard optimization rules
│   └── src/main/
│       ├── AndroidManifest.xml               # App declarations & configurations
│       ├── assets/                           # Audio tracks (7 MP3s) & Millionaire.png logo
│       ├── java/com/wgm/quiz/
│       │   ├── MainActivity.kt               # Main entry Activity hosting NavHost
│       │   ├── SplashActivity.kt             # Animated luxury splash screen
│       │   ├── WgmApplication.kt             # Application class initializing Room DB
│       │   ├── audio/
│       │   │   ├── WgmSoundManager.kt        # Triple MediaPlayer + SoundPool engine
│       │   │   └── WgmSynthesizer.kt         # AudioTrack sine-wave audio generator
│       │   ├── data/
│       │   │   ├── local/                    # Room Database, DAO, Entity, ScoreRepository
│       │   │   └── repository/               # WgmQuizRepositoryImpl & 45-question seed
│       │   ├── domain/
│       │   │   ├── model/                    # WgmQuestion domain model
│       │   │   └── repository/               # WgmQuizRepository interface
│       │   ├── ui/
│       │   │   ├── components/               # Hexagon cards, Timer, Dialogs, Lifelines
│       │   │   ├── screens/                  # WgmHomeScreen, WgmGameScreen, WgmMoneyLadder
│       │   │   └── theme/                    # Color tokens, gradients, typography
│       │   └── viewmodel/                    # WgmViewModel with GamePhase state machine
│       └── res/                              # Drawables, mipmaps, colors & themes
├── build.gradle                              # Root build script
├── settings.gradle                           # Module & repository declarations
├── gradle.properties                         # JVM arguments & compiler properties
├── local.properties                          # Local SDK path configuration
└── README.md                                 # Project documentation
```

---

## 🚀 Setup, Build & Execution Guide

### Prerequisites
- **Android Studio**: Ladybug / Koala / Hedgehog or newer.
- **JDK**: Java Development Kit 17 (recommended: Android Studio bundled JDK).
- **Android SDK**: API Level 24 to 37.

### Quick Start
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/codedbyamankanojiya/WGM-Quiz.git
   cd WGM-Quiz
   ```

2. **Open in Android Studio**:
   - Launch Android Studio, select **Open**, and navigate to the `WGM Quiz` directory.
   - Wait for Gradle to download dependencies and sync the project.

3. **Build & Run**:
   - Select an emulator or physical device.
   - Press **`Shift + F10`** (or click the green **Run** button).

4. **Generate Debug APK**:
   ```bash
   ./gradlew assembleDebug
   ```
   The compiled APK will be generated at:
   `app/build/outputs/apk/debug/app-debug.apk`

---

## 👨‍💻 Author & License

This application is personally developed and maintained by **Aman Kanojiya**:
- **GitHub**: [@codedbyamankanojiya](https://github.com/codedbyamankanojiya)
- **LinkedIn**: [Aman Kanojiya](https://linkedin.com/in/aman-kanojiya-7386822b0)

This project is open-source and licensed under the **MIT License** — feel free to explore, fork, and star the repository!