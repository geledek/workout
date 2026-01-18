# Claude Code Instructions for Workout Planning

## Overview

This is Ray's workout planning system. Ray is working with:
- **Sarah** (Physiotherapist) - Rehab program, main authority on exercises
- **Andy** (Personal Trainer) - Weekly gym sessions, supports Sarah's program

## Key Context About Ray

**Always Remember:**
- 40yo male, 177cm, 77kg (±2kg)
- Two decades of back pain, recent sciatica episode
- Bilateral ACL reconstruction (2020, 2021) - maintenance focus
- Recent pelvic floor spike (indoor cycling + farmers walk) - monitor closely
- Walking imbalance and pelvic tension during football - key issues to address
- Phase: Transitioning from rehab to performance

**H1 2026 Goals:**
- VO2Max: 38 → 45
- 5km: → 25 minutes

## Weekly Planning Workflow

**Every Sunday:**
1. Ray provides week context (schedule, how he feels, commitments)
2. Claude reviews:
   - Last week's plan and completion (check git history)
   - Current programs (`programs/sarah-current.md`, `programs/andy-notes.md`)
   - Recent metrics and status
3. Claude generates new weekly plan
4. Plan goes in `weeks/YYYY-WXX.md`

**Quick Input Format:**
Ray will say something like: "Plan next week. Normal work M-F, football Saturday, feeling good but lower back tight Thursday. Seeing Andy Tuesday."

## Weekly Plan Structure

Every weekly plan MUST have two sections:

### 1. QUICK REFERENCE (Top)
- All checkboxes for the week
- Compact, scannable
- Used during actual training
- Includes note-taking prompts (L/R differences, pelvic floor response, etc.)

### 2. DETAILED GUIDE (Bottom)
- Execution cues for every exercise
- WHY each exercise is in the program
- Progressions and relationships between exercises
- What to monitor and check
- Pelvic floor checkpoints
- Equipment adaptations when traveling

## Exercise Analysis Requirements

**NEVER just copy Sarah's program verbatim.** Always analyze and add value:

### Unpack Shorthand
- "McGill Big 3" → List all three exercises with dosage, setup, execution cues
- "Hip CARs" → Explain what CARs means, how to perform

### Provide Dosage
- If Sarah says "McGill Big 3" without sets/reps, use standard: 6→4→2 reps x 8-second holds
- Always specify sets, reps, hold times, rest periods

### Explain Progressions
When an exercise appears multiple times (e.g., hip airplanes):
- Morning: x12-15 bodyweight (wake up/activate)
- 2x/week: x15 bodyweight (volume accumulation)
- 3-rounds: x8-10 with KB (intensity/load)
- EXPLAIN why this progression exists

### Show Relationships
- McGill side plank (base) → Extended side plank (progression)
- Explain how exercises build on each other within a session

### Optimize Sequencing
General order: Release → Breathe → Activate → Integrate → Load
- TFL releases FIRST (release before activation)
- Breathing exercises (establish core/pelvic floor connection)
- Glute bridges (activate)
- Hip airplanes (integrate)
- Loaded work (strength circuits)

### Add Execution Cues
Every exercise needs:
- **Setup:** Starting position
- **Execution:** How to perform
- **Cue:** 1-2 coaching cues
- **Why:** Why this exercise matters for Ray specifically
- **Check:** Quality indicators, common mistakes

### Include Ray-Specific Context
- Pelvic floor checkpoints (when to monitor for bearing down)
- Back pain considerations (avoid lumbar extension, etc.)
- L/R tracking prompts (identify imbalance patterns)

## Running Progression

**Sarah's Current Guidelines (as of Jan 2025):**
- Frequency: Every 4-5 days
- Volume: Max 10% increase per week
- Duration: 3-week protocol, then reassess

Always calculate and show the next run target based on these rules.

## Pelvic Floor Monitoring

**Key Checkpoints:**
- Breathing exercises: Gentle lift on exhale
- Glute bridges: No bearing down
- Planks: No pressure/heaviness
- Running: No urgency or heaviness
- Hopping: Exhale on landing

**If Issues Occur:** Scale back, rest, note for Sarah

## Travel Adaptations

When Ray travels:
- Scale 3-round circuits to 2 rounds
- Provide equipment alternatives (hotel gym variations)
- Focus on mobility and maintenance, not progression
- Massage = active recovery + assessment opportunity

## File Locations

```
/profile.md                    - Master data (update when goals change)
/metrics.md                    - Test results (Ray uploads)
/programs/sarah-current.md     - Current rehab program (update when Sarah changes it)
/programs/andy-notes.md        - PT session notes
/resources/exercises-to-try.md - Future exercise ideas
/resources/research.md         - Papers and articles
/weeks/YYYY-WXX.md            - Weekly plans
```

## Git Workflow

- Commit each new weekly plan
- Commit program updates from Sarah
- Commit metrics when Ray uploads test results
- Use descriptive commit messages

## What NOT To Do

- Don't copy Sarah's program without analysis
- Don't leave shorthand unexplained (McGill Big 3, NCM, CARs, etc.)
- Don't forget dosage (sets, reps, hold times)
- Don't ignore the progression logic between exercises
- Don't skip pelvic floor checkpoints
- Don't forget to track L/R differences
- Don't overload Ray during travel weeks

## Example: Bad vs Good

**Bad (lazy):**
```markdown
- [ ] McGill Big 3
- [ ] Hip airplanes x 15 per side
```

**Good (analyzed):**
```markdown
**McGill Big 3:** (Sets: 6 reps → 4 reps → 2 reps, 8-second holds each)
- [ ] Curl-ups: 3 sets
- [ ] Side planks: 3 sets per side
- [ ] Bird-dogs: 3 sets per side

*See Detailed Guide for execution cues. This is the BASE side plank - you'll do the PROGRESSION version (extended leg) in the 3-round circuit.*
```

## Updating This File

If Ray establishes new patterns or preferences, update this file to capture them. This is the living document for how workout planning should work.
