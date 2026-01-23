# iOS Workout Planning App - Design Document

**Date:** 2026-01-23
**Status:** Draft

---

## Overview

A native iOS app for workout planning and tracking that replaces the current Claude Code + markdown workflow. The app becomes the source of truth, with git serving as backup and version history.

### Core Principles

- **App-first with AI** - Embedded AI handles planning, questions, and insights
- **Reminders-style flexibility** - Drag sessions, add exercises, reschedule freely
- **Your context, your data** - AI understands your conditions, programs, and trainers
- **Apple Health integration** - Deep sync for running data, metrics, and trends
- **Data ownership** - Git backup ensures portability and history

---

## Target User

- Active individual managing rehab-to-performance transition
- Works with multiple trainers (physio, PT)
- Tracks specific conditions over time
- Uses Apple Watch for cardio
- Values flexibility over rigid plan enforcement

---

## Navigation Structure

| Tab | Purpose |
|-----|---------|
| **Today** | Current day's sessions, primary workout screen |
| **Week** | 7-day view, drag to reschedule, add sessions |
| **Progress** | Metrics, goals, running trends, condition tracking |
| **Programs** | Reference programs, trainer notes, exercise library |
| **Profile** | Personal info, conditions, team, settings |

---

## Data Model

### Week
- Week identifier (2026-W04)
- Status snapshot (energy, weight, condition ratings)
- Context notes (travel, commitments, focus)
- Contains multiple Sessions

### Session
- Date and time slot (morning, afternoon, evening)
- Type: routine, program, PT session, run, rest, other
- Source: which program it came from (or ad-hoc)
- Contains ordered Exercise Groups
- Completion state
- Notes

### Exercise Group
- Name (e.g., "McGill Big 3", "3 Rounds", "Warm-up")
- Type: sequential or circuit
- Round count (for circuits)
- Rest time between exercises/rounds
- Contains ordered Exercises

### Exercise
- Name
- Target: sets, reps, hold time, weight, duration
- Completion state (per set)
- L/R tracking (when applicable)
- Notes (voice transcriptions land here)
- Links to Exercise Library entry

### Exercise Library Entry
- Name and category
- Default parameters (sets, reps, equipment)
- Execution cues: setup, execution, coaching cue
- Why it matters (context for user)
- Media: photos, GIFs (cached from web or user-added)
- References: URLs to videos, articles
- Personal notes

### Reference Program
- Name and source (trainer name, online program, etc.)
- Active/inactive status
- Structured exercise list with frequencies
- Notes from source

### Profile
- Demographics: age, height, weight
- Sports and activities
- Medical history / conditions (user-configured)
- Training team (trainers with roles)
- Goals with targets and deadlines

---

## Key Screens

### Today Screen

Primary workout execution interface.

```
┌─────────────────────────────────────────┐
│ Today · Monday Jan 20                   │
├─────────────────────────────────────────┤
│ ┌─────────────────────────────────────┐ │
│ │ Morning Routine          ◐ 2/4     │ │
│ │ 15 mins · In Progress              │ │
│ └─────────────────────────────────────┘ │
│ ┌─────────────────────────────────────┐ │
│ │ Evening Run              ○         │ │
│ │ 5km target                         │ │
│ └─────────────────────────────────────┘ │
│ ┌─────────────────────────────────────┐ │
│ │ Upper Body              ○          │ │
│ │ 30 mins                            │ │
│ └─────────────────────────────────────┘ │
│                                         │
│                              🤖 Ask AI  │
└─────────────────────────────────────────┘
```

### Session Execution (Expanded)

```
┌─────────────────────────────────────────┐
│ ← Morning Routine            00:12:34   │
├─────────────────────────────────────────┤
│ TFL Releases                       ✓    │
│ 2-3 mins per side                       │
├─────────────────────────────────────────┤
│ Breathing Exercises                ✓    │
│ Supine → Sitting → Standing             │
├─────────────────────────────────────────┤
│ Glute Bridges                    ○ ○ ○  │
│ 10-15 reps                              │
│ [  L  ] [  R  ]              🎤    ⓘ   │
├─────────────────────────────────────────┤
│ Hip Airplanes                    ○ ○    │
│ 12-15 per side                          │
│ [  L  ] [  R  ]              🎤    ⓘ   │
├─────────────────────────────────────────┤
│                                         │
│            Ready for next set           │
│                 + 00:05                 │
│                                         │
└─────────────────────────────────────────┘
```

**Interaction patterns:**
- Tap circle to complete set
- Tap L/R to log side-specific completion
- Tap 🎤 for voice note (transcribed automatically)
- Tap ⓘ for execution cues and context
- Timer counts rest, shows "Ready for next set" when complete
- Timer continues counting (no alarm) if user needs more time

### Week Screen (Reminders-style)

```
┌─────────────────────────────────────────┐
│ Week 4 · Jan 20-26                      │
├─────────────────────────────────────────┤
│ Mon 20  ✓ Morning Routine               │
│         ✓ Evening Run (5.03km)          │
│         ✓ Upper Body                    │
├─────────────────────────────────────────┤
│ Tue 21  ○ Morning Routine               │
│         ○ Boxing Trial 6:30pm           │
├─────────────────────────────────────────┤
│ Wed 22  ○ Travel Day                    │
│         ○ Hotel Mobility                │
├─────────────────────────────────────────┤
│ ...                                     │
│                                    + Add│
└─────────────────────────────────────────┘
```

**Interactions:**
- Drag session cards to reschedule
- Tap + to add session or exercise
- Swipe to delete or duplicate
- Long-press for options (edit, copy to another day)

### Progress Screen

```
┌─────────────────────────────────────────┐
│ Progress                                │
├─────────────────────────────────────────┤
│ GOALS                                   │
│ ┌─────────────────────────────────────┐ │
│ │ VO2 Max        38 ━━━━━━━○━━━ 45   │ │
│ │ 5km Time       --:-- ━━━━━○━ 25:00 │ │
│ └─────────────────────────────────────┘ │
├─────────────────────────────────────────┤
│ RUNNING                          See all│
│ ┌─────────────────────────────────────┐ │
│ │ [Weekly volume chart]              │ │
│ │ Last: 5.03km @ 7'04"/km            │ │
│ │ Next target: 5-5.5km in 3-4 days   │ │
│ └─────────────────────────────────────┘ │
├─────────────────────────────────────────┤
│ CONDITIONS                       See all│
│ Back pain: ●●●○○ (3/5 this week)       │
│ Knee status: ●●○○○ (2/5)               │
├─────────────────────────────────────────┤
│ INSIGHTS                                │
│ "85% session completion this month"     │
│ "Running pace improved 15s/km"          │
└─────────────────────────────────────────┘
```

### Exercise Library Entry

```
┌─────────────────────────────────────────┐
│ ← Hip Airplanes                    Edit │
├─────────────────────────────────────────┤
│ ┌─────────────────────────────────────┐ │
│ │         [Exercise Photo/GIF]       │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Category: Stability / Single-leg        │
│ Default: 12-15 per side                 │
│ Equipment: None (KB for loaded)         │
├─────────────────────────────────────────┤
│ SETUP                                   │
│ Stand on one leg, hinge forward ~45°    │
│                                         │
│ EXECUTION                               │
│ Rotate pelvis open (external), then     │
│ closed (internal). Arms out for balance.│
│                                         │
│ CUE                                     │
│ "Show your pocket to the wall, then     │
│ hide it"                                │
├─────────────────────────────────────────┤
│ REFERENCES                              │
│ 📺 Squat University - Hip Airplane Demo │
│ 📄 The Why Behind Hip Airplanes         │
├─────────────────────────────────────────┤
│ YOUR NOTES                              │
│ "Left side wobblier, focus on slower    │
│ tempo"                                  │
└─────────────────────────────────────────┘
```

### AI Chat

```
┌─────────────────────────────────────────┐
│ ← AI Assistant                          │
├─────────────────────────────────────────┤
│                                         │
│ ┌─────────────────────────────────────┐ │
│ │ You: Plan next week. Normal work   │ │
│ │ M-F, football Saturday, feeling    │ │
│ │ good but left hip a bit tight.     │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ ┌─────────────────────────────────────┐ │
│ │ AI: Here's your Week 5 plan based  │ │
│ │ on your programs and recent        │ │
│ │ progress:                          │ │
│ │                                    │ │
│ │ Monday: Morning routine + 5.5km    │ │
│ │ run (10% increase from last week)  │ │
│ │ ...                                │ │
│ │                                    │ │
│ │ I've added extra hip mobility on   │ │
│ │ Tuesday given your tight left hip. │ │
│ │                                    │ │
│ │ [Apply Plan] [Adjust] [Cancel]     │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ ┌─────────────────────────────────────┐ │
│ │ 🎤 Type or speak...          Send  │ │
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

---

## AI Integration

### Capabilities

| Task | Description |
|------|-------------|
| Weekly planning | Generate plan from programs, history, Health data, context |
| Mid-week adjustments | Reschedule, simplify, modify based on how you feel |
| Exercise questions | Explain any exercise, provide cues, context |
| Progress insights | Analyze trends, surface patterns from notes |
| Program updates | Parse trainer updates, modify stored programs |

### Architecture (Hybrid)

| Query Type | Handler | Rationale |
|------------|---------|-----------|
| Simple questions | On-device (Apple Intelligence) | Fast, free, offline |
| Planning & complex | Claude API | Full reasoning capability |
| Offline fallback | Cached + on-device | Graceful degradation |

### Context Available to AI

- Full profile (conditions, history, goals)
- All reference programs
- Exercise library
- Session history (past 12 weeks)
- Apple Health data (runs, HR, VO2 Max)
- Current week context
- Trainer notes

---

## Apple Health Integration

### Read from Health

| Data | Usage |
|------|-------|
| Running workouts | Auto-import to run sessions (distance, pace, HR, splits, cadence) |
| VO2 Max | Goal tracking |
| Resting heart rate | Trends, recovery indicator |
| Weight | Weekly snapshots |
| Sleep | Context for AI planning |

### Write to Health

| Data | Workout Type |
|------|--------------|
| Strength sessions | Strength Training |
| Mobility sessions | Flexibility |
| Session duration | All types |

### Auto-linking Runs

1. User completes run with Apple Watch
2. App detects new running workout in HealthKit
3. Matches to planned run session by date/time proximity
4. Auto-populates metrics (distance, pace, HR, splits)
5. User adds notes if desired

---

## Data Sync & Backup

### Sync Layers

| Layer | Technology | Purpose |
|-------|------------|---------|
| Local | SwiftData | Primary storage, offline capable |
| Cross-device | CloudKit | iPhone ↔ iPad sync |
| Backup | Git (GitHub API) | Markdown export, version history |

### Git Backup

**What's exported:**
- Weekly journals (completed sessions, notes)
- Reference programs
- Exercise library
- Profile data

**Format:** Markdown files matching current repo structure

**Frequency options:**
- Daily auto-commit
- Weekly auto-commit
- Manual trigger only

**Commit message:** "Weekly journal: 2026-W04 (85% completion)"

---

## Technical Stack

| Component | Technology |
|-----------|------------|
| Language | Swift |
| UI Framework | SwiftUI |
| Persistence | SwiftData |
| Cloud Sync | CloudKit |
| Health | HealthKit |
| Voice | Speech framework |
| AI (cloud) | Anthropic Claude API |
| AI (on-device) | Apple Intelligence / Core ML |
| Git integration | GitHub REST API |

**Minimum iOS:** 17.0

---

## MVP Scope (v1.0)

### Included

- Today + Week + Session execution screens
- Exercise library with manual entry
- Reference programs (manual entry)
- Apple Health read (runs) + write (workouts)
- Claude API for planning + questions
- Local storage + CloudKit sync
- Basic profile and condition tracking

### Excluded (v1.x)

- Git backup integration
- Full progress dashboard with charts
- Photo/link references in exercise library
- On-device AI fallback
- iPad-optimized layout
- Apple Watch companion app
- Trainer sharing/collaboration

---

## Open Questions

1. **App name** - TrainLog? SessionKit? Other suggestions?
2. **Monetization** - Free with API costs passed through? Subscription?
3. **AI API costs** - How to handle Claude API usage costs?
4. **Watch app priority** - How important is a Watch companion for v1?

---

## Next Steps

1. Validate design with potential users
2. Create detailed implementation plan
3. Set up iOS project structure
4. Build data model and persistence layer
5. Implement core screens (Today, Week, Session)
6. Integrate HealthKit
7. Add AI integration
8. Beta testing
