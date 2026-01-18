# CLAUDE.md - AI Assistant Guide

This document provides guidance for AI assistants working with this workout planning repository.

## Repository Overview

A git-based workout planning system for a 40-year-old male athlete managing:
- **Rehab-to-performance transition** (chronic back pain, sciatica recovery)
- **H1 2026 Goals:** VO2Max 38→45, 5km in 25 minutes
- **Active lifestyle:** Football, tennis, yoga, boxing (learning), indoor surfing (learning)

### Training Team
- **Sarah (Physiotherapist):** Primary rehab program authority. Her exercises take precedence.
- **Andy (Personal Trainer):** Supports rehab-focused program with on-site gym coaching (1-2x/week, flexible)

## Directory Structure

```
/workout
├── CLAUDE.md              # This file - AI assistant guidance
├── profile.md             # Athlete demographics, medical history, goals
├── metrics.md             # Objective test results (VO2Max, 5km times)
├── /programs
│   ├── sarah-current.md   # Current rehab program from physiotherapist
│   └── andy-notes.md      # PT session notes and focus areas
├── /resources
│   ├── exercises-to-try.md    # Exercise variations to explore
│   └── research.md            # Papers and articles
├── /weeks
│   └── YYYY-WXX.md        # Weekly plans (e.g., 2026-W04.md)
└── /docs
    └── plans/             # Design documentation
```

## Key Files to Read

When helping with workout planning, always review:
1. `profile.md` - Current goals, medical constraints, training team
2. `programs/sarah-current.md` - Active rehab exercises (PRIORITY)
3. Most recent `weeks/YYYY-WXX.md` - Last week's completion and notes
4. `metrics.md` - Recent performance data

## Weekly Planning Workflow

### Sunday Planning Session
1. User provides context: schedule, energy levels, recent symptoms, commitments
2. Assistant reviews:
   - Last week's plan completion (checked boxes)
   - Weekly review notes and adjustments
   - Current status (back pain, pelvic floor, energy)
   - Sarah's program requirements
   - Andy's session schedule if known
3. Generate new weekly plan with:
   - Daily exercises with checkboxes
   - Appropriate program scheduling (2x/week, 1x/week)
   - Context-aware intensity adjustments

### Weekly Plan Structure
```markdown
# Week X: [Date Range]

## Weekly Status
- **Back Pain:** [Baseline/Elevated/etc]
- **Energy:** [Good/Low/etc]
- **Weight:** XXkg
- **Notable:** [Any symptoms or context]

## This Week's Context
- [Travel, commitments, sports, sessions]

---

## [Day] [Date] - [Focus]

**Morning:**
- [ ] Exercise 1
- [ ] Exercise 2

**Evening:**
- [ ] Exercise 3

**Notes:** [Day-specific context]

---

## Weekly Review (Complete end of week)
[Reflection prompts]
```

## Exercise Programs

### Sarah's Program (Primary)
- **Daily exercises:** Breathing, hip airplanes, TFL releases, glute bridges
- **2x/week program:** Cossacks, McGill Big 3, hip CARs, planks, 3-round circuit
- **1x/week program:** Single-leg work (squats, hops, Bulgarian squats)

### Key Constraints
- Avoid lumbar extension during hip extension work
- Monitor pelvic floor response to loading
- No more than 10% running volume increase per week
- Running every 4-5 days during progression phase

## Conventions

### Completion Tracking
- `[ ]` - Planned, not completed
- `[x]` - Completed
- `~~text~~` - Skipped (with reason in notes)

### Intensity Scaling
When fatigue, travel, or symptoms present:
- Reduce rounds (3→2)
- Reduce load/reps
- Substitute with mobility-only work
- Skip optional exercises

### File Naming
- Weekly plans: `YYYY-WXX.md` (ISO week number)
- Dates in files: `YYYY-MM-DD` format

### Commit Messages
Descriptive commits that mark training milestones:
- "Add Week X plan with [focus]"
- "Complete Week X - [summary]"
- "Update Sarah's program - [changes]"

## Important Context

### Medical Considerations
- **Back pain/sciatica:** Two decades of issues, currently in rehab
- **ACL reconstruction:** Bilateral (2020-2021), maintain lower body strength
- **Pelvic floor:** Recent sensitivity, monitor response to loading
- **Turf toes:** Historical, currently asymptomatic

### Recovery Priorities
1. Pelvic floor health (recent spike from indoor cycling + farmers walk)
2. Lumbar spine stability (McGill Big 3)
3. Hip stability and control (single-leg work)
4. VO2Max improvement (progressive cardio)

## Assistant Behavior Guidelines

### DO
- Prioritize Sarah's rehab program over performance goals
- Scale intensity based on reported symptoms and energy
- Include rest days after high-intensity sessions or travel
- Ask clarifying questions about symptoms before planning
- Reference specific exercises from `programs/sarah-current.md`
- Consider weekly context (travel, sports, work schedule)

### DON'T
- Increase running volume more than 10% per week
- Schedule heavy lower body work on consecutive days
- Plan intense sessions during travel days
- Ignore reported symptoms or fatigue
- Add exercises not in Sarah's current program without discussion
- Skip daily exercises (they're non-negotiable)

### Response Style
- Concise, actionable plans
- Use checkboxes for all exercises
- Include "Notes:" for day-specific context
- Add monitoring cues for new activities
- Structure for easy scanning during workout

## Example Planning Input

```
User: "Plan next week. Normal work M-F, football Saturday morning,
       feeling good but lower back was tight Thursday. Seeing Andy Tuesday evening."

Assistant reviews: last week's completion, current program, user context
Assistant generates: complete weekly plan with appropriate scheduling
```

## Git Workflow

- Weekly plans committed after Sunday planning
- Mid-week updates committed as needed
- End-of-week reviews captured in the weekly file
- Git history serves as the training log
