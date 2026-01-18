# Workout Planning System Design

**Date:** 2026-01-18
**Status:** Implemented

## Overview

A git-based workout planning system for managing daily rehab exercises, personal training sessions, and athletic performance goals. The system supports tracking progress from rehab to performance phase while working with a physiotherapist (Sarah) and personal trainer (Andy).

## User Profile

- Male, Asian, 40 years old, 177cm, 77kg (±2kg)
- Active lifestyle: football, tennis, yoga, learning boxing and indoor surfing
- Medical history: Two decades back pain, recent sciatica (rehab phase), bilateral ACL reconstruction (2020-2021), double turf toes (asymptomatic)
- H1 2026 Goals: VO2Max 38→45, 5km time to 25 minutes

## Design Decisions

### 1. Storage: Git-based Markdown Files (Option D)
**Why:** Git provides complete history, easy diffs to compare weeks, and markdown is human-readable and editable. Addresses the key pain point from ChatGPT: "no sense of history."

### 2. Completion Tracking: Checkboxes in Plans (Option C)
**Why:** Quick to mark complete, visual feedback, inline notes for adjustments. Git diff shows exactly what was completed each week.

Example:
```markdown
## Monday 20 Jan 2026
- [x] Morning: Hip airplanes x 12-15
- [x] Evening: Gym with Andy - lower body focus
- [ ] ~~Breathing exercises~~ (skipped - ran late)
```

### 3. Program Management: Hybrid Approach (Option D)
**Why:** Master program file for current reference + exercises copied into weekly plans for self-contained historical records.

Structure:
- `/programs/sarah-current.md` - Updated when Sarah changes protocol
- `/programs/andy-notes.md` - PT session notes and focus areas
- `/programs/program-history/` - Archived versions when major updates occur
- Weekly plans contain specific exercises planned for that week

### 4. Planning Detail: Adaptive Detail (Option C)
**Why:** Full details for new/changing exercises, shorthand for established routines. Balances usability without overwhelming copy-paste.

### 5. PT Sessions: Flexible Support (Between B and C)
Andy's sessions are variable frequency (1-2x/week) with flexible scheduling. User prioritizes rehab progress and informs Andy of focus areas for on-site support.

### 6. Weekly Planning Context: Full Picture (Option D)
Claude considers:
- Work schedule and commitments
- Energy patterns and recovery needs
- Weekly sports commitments (e.g., football Saturday)
- Recent completion history and adjustments

### 7. Sunday Planning Workflow: Quick Chat Input (Option A)
**Why:** Fast 5-10 minute conversation. User provides natural input about the week, Claude generates complete plan.

Example:
```
User: "Plan next week. Normal work M-F, football Saturday morning,
       feeling good but lower back was tight Thursday. Seeing Andy Tuesday evening."

Claude: *reviews last week* "Schedule Andy for lower body check-in Tuesday,
         rest Sunday after football. Sound good?"
```

### 8. Metrics Tracking: Hybrid Tracking (Option D)
**Why:** Weekly subjective notes inform intensity adjustments + separate objective test log for progress timeline.

- Weekly plans include status section (back pain, energy, weight)
- `/metrics.md` logs objective tests (VO2Max, 5km times, measurements)

## Directory Structure

```
/Workout
├── profile.md                    # Master data (age, history, goals)
├── metrics.md                    # Objective test results
├── /programs
│   ├── sarah-current.md          # Current rehab program
│   ├── andy-notes.md             # PT session notes
│   └── program-history/          # Archived program versions
├── /resources
│   ├── exercises-to-try.md       # Videos, variations to try
│   └── research.md               # Papers, articles
├── /weeks
│   ├── 2026-W03.md              # Weekly plans
│   └── ...
└── /docs
    └── plans/                    # Design documentation
```

## Weekly Plan Template

Each weekly plan contains:
1. **Weekly Status** - Subjective metrics (back pain, energy, weight)
2. **This Week's Context** - Schedule, commitments, sports
3. **Daily Plans** - Day-by-day exercises with checkboxes
4. **Weekly Review** - End-of-week reflections (optional)

## Key Principles

1. **Self-contained weeks:** Each weekly file can be read independently
2. **Git history as training log:** Commits mark key events
3. **Adaptive planning:** Claude learns from completion patterns
4. **YAGNI:** Simple markdown files, no complex automation
5. **Rehab priority:** Sarah's program takes precedence, Andy supports

## Sunday Planning Flow

1. User chats with Claude Code: "Plan next week [context]"
2. Claude reviews:
   - Last week's plan and completion
   - Recent metrics and status
   - Current programs (Sarah, Andy)
3. Claude generates weekly plan incorporating:
   - Daily exercises (adaptive detail)
   - 2x/week program (scheduled optimally)
   - 1x/week program (scheduled with adequate recovery)
   - Andy session(s) if scheduled
   - Other sports/commitments
4. User reviews, makes manual edits if needed
5. Throughout week: Check off exercises, add notes
6. Git commits mark milestones

## Future Enhancements (YAGNI - only if needed)

- Automated stats from git history
- Integration with fitness trackers
- Progress visualization
- Exercise library with form videos

## Success Criteria

- Weekly planning takes < 10 minutes on Sunday
- Can review any past week by opening its file
- Clear history of program evolution
- Easy to adjust plans mid-week
- Supports both rehab focus and performance goals
