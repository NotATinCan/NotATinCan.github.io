---
title: "The Garage Memory v3 Format"
date: 2026-09-08 00:00:00 +0300
permalink: "/posts/The Garage Memory v3 Format"
categories: [Memory]
tags: [Mika, "The Garage", "Memory File v3 Format", Training, Documentation]
---

# The Garage Memory v3 Format

## Purpose

Memory v3 is the standard structure for recording The Garage training sessions so that future sessions can be compared reliably and longitudinal progress can be tracked without confusing user-reported facts with interpretation.

V3 keeps the useful session-by-session record of v2, but adds standardized exercise data, explicit progression metadata, and a separate living progress layer.

## Core Principles

1. **One session = one memory file.**
2. **Facts and interpretation are separate.**
3. **Exercise fields should use consistent names and units.**
4. **Progress should explicitly compare the current session with previous relevant sessions.**
5. **The user's actual report is the source of truth for what was performed.**
6. **Assistant analysis must never be presented as if it were user-reported fact.**

## File Naming Convention

Use:

`YYYY-MM-DD-Garage-Memv3-sNN.md`

Example:

`2026-09-08-Garage-Memv3-s37.md`

The session number is sequential across The Garage memory series.

## Front Matter

Use Jekyll front matter in this form:

```yaml
---
title: "The Garage Memory NN"
date: YYYY-MM-DD 00:00:00 +0300
permalink: "/posts/The Garage Memory sNN"
categories: [Memory]
tags: [Mika, "The Garage", "Memory File v3 Format", Training, <training tags>]
---
```

## Session Identifier

Use:

`SESSION: G-YYYYMMDD`

and:

`DATE: YYYY-MM-DD`

## STATE

Records the user's reported or explicitly stated session state.

```yaml
STATE:
  mood: not-reported
  general: completed / demanding
```

Do not invent mood, difficulty, pain, or recovery information.

## CONTEXT

Briefly identify the training session.

Example:

```yaml
CONTEXT:
  Tuesday — Push Strength + Legs training session.
```

## TRAINING

This is the factual record of what was actually performed.

Each exercise should use standardized fields where applicable:

```yaml
exercise_name:
  category: vertical_pull
  sets: 6
  reps_per_set: 4
  total_reps: 24
  load: bodyweight
  execution: strict_dead_hang / chin_clearly_over_bar
  rest_between_sets_sec: 90
  rest_before_exercise_sec: 150
  quality: good
```

### Standard field rules

- `category`: functional exercise category, such as `vertical_pull`, `horizontal_pull`, `push`, `legs`, `core`, or `grip`.
- `sets`: number of completed sets.
- `reps_per_set`: repetitions when consistent across sets.
- `reps_by_set`: use instead when repetitions differ between sets.
- `total_reps`: total completed repetitions when applicable.
- `duration_sec`: use for timed work.
- `total_hold_time_sec`: total time for timed work when useful.
- `load`: `bodyweight`, a backpack weight, dumbbell weight, band resistance, or another clearly stated load.
- `load_details`: optional detail when multiple loads are involved.
- `execution`: important technique requirement.
- `rest_between_sets_sec`: rest between sets.
- `rest_before_exercise_sec`: rest before starting the exercise.
- `quality`: only record if known from the user's report or clearly observable from the stated performance.
- `note`: factual user-reported detail that does not fit elsewhere.

### Units

Prefer seconds for rest and timed exercises:

- `90 sec` → `rest_between_sets_sec: 90`
- `2 min 30 sec` → `rest_before_exercise_sec: 150`

Use kilograms as `kg` and kilometers as `km` when recording load or walking distance.

## FACTS

V3 treats the user's training report as facts. If a separate `FACTS` section is useful, it may summarize only what the user explicitly reported.

Example:

```yaml
FACTS:
  walk_distance_km: 1.3
  completed_as_planned: true
```

Do not add conclusions here.

## OBSERVATIONS

Contains user-reported sensations or directly reported session observations.

Example:

```yaml
OBSERVATIONS:
  - Pull-ups remained strict throughout all sets.
  - The user reported that the final sets were demanding.
```

If the user reports pain, discomfort, unusual fatigue, or another physical response, record it accurately without diagnosing it.

## ANALYSIS

Contains Mika's interpretation of the session.

This is deliberately separate from FACTS and OBSERVATIONS.

Example:

```yaml
ANALYSIS:
  - The same total pull-up volume was completed with shorter rest than the previous comparable session.
  - This represents increased training density if strict form was maintained.
```

Analysis should be conservative and based on recorded sessions.

## PROGRESS

This section connects the current workout to the longitudinal training record.

Recommended structure:

```yaml
PROGRESS:
  primary_goal: pull_up_strength
  progression_status: maintained / improved / regressed / new / not_comparable
  previous_session: G-YYYYMMDD
  comparison:
    pull_ups: "6 x 4 maintained"
    rest: "90 sec maintained"
  next_target:
    pull_ups: "6 x 4 with strict form"
```

Rules:

- Compare with the most relevant previous session, not merely the immediately preceding calendar session.
- Do not call something an improvement unless the recorded data supports it.
- If sessions are not directly comparable, use `not_comparable`.
- `next_target` should normally be modest and consistent with the established program rather than introducing an unnecessary change.

## PATTERNS

Use this section for longer-term trends visible across multiple sessions.

Example:

```yaml
PATTERNS:
  - Pull-up strength volume remains stable at 6 x 4.
  - Pulling density has increased compared with earlier sessions.
  - Core training consistently combines hanging work with anti-extension work.
```

Patterns are interpretation, not raw facts, and should be supported by the existing memory files.

## OPEN_THREADS

Records items that should be monitored in future sessions.

Example:

```yaml
OPEN_THREADS:
  - Monitor whether 90 sec rest remains sustainable for 6 x 4 strict pull-ups.
  - Continue monitoring any recurring discomfort reported during hanging leg raises.
```

Do not create medical diagnoses or unsupported concerns.

## VIBE

A short closing characterization of the session.

Example:

`VIBE: disciplined / strong / completed`

This should reflect the session rather than inventing an emotional state.

# Living Progress File

V3 is designed to work alongside a separate living progress file:

`_posts/Garage-Progress.md`

This file should summarize current longitudinal status rather than duplicate every session.

Recommended structure:

```yaml
PULL_UPS:
  baseline: "..."
  current: "..."
  best: "..."
  trend: "..."
  target: "..."

WEIGHTED_PUSH_UPS:
  baseline: "..."
  current: "..."
  best: "..."
  trend: "..."
  target: "..."

DIPS:
  current: "..."
  trend: "..."
  target: "..."

LEGS:
  current: "..."
  trend: "..."
  target: "..."

CORE:
  current: "..."
  trend: "..."
  target: "..."

PROGRAM:
  phase: "..."
  week: "..."
  adherence: "..."
  primary_goal: "..."
```

The living progress file should be updated only when the accumulated training record justifies a change.

# How to Ask Mika to Check a Future File

When a new workout is provided, ask:

> Please prepare this as a Garage Memory v3 file and check it against the V3 format specification.

Mika should then verify:

1. Correct filename and session number.
2. Correct Jekyll front matter.
3. Correct `SESSION` and `DATE`.
4. Consistent exercise field names.
5. Correct conversion of rest times into seconds.
6. Accurate sets, reps, duration, loads, and total volume.
7. Clear separation of FACTS, OBSERVATIONS, and ANALYSIS.
8. A justified `PROGRESS` comparison with the most relevant prior session.
9. Useful `PATTERNS` and `OPEN_THREADS` only when supported by the record.
10. No invented training details, sensations, conclusions, or diagnoses.
11. Consistency with the established Garage program and previous memory files.

# V3 vs V2

V2 remains valid as historical memory and should not be silently rewritten.

V3 improves the structure by adding:

- standardized exercise metadata;
- explicit units for rest and timed work;
- separation of factual record from interpretation;
- a dedicated progression layer;
- longer-term pattern tracking;
- open threads for future sessions;
- a separate living progress file for longitudinal status.

Future sessions should use V3 when requested. Existing V2 files should remain unchanged unless Kaan explicitly asks for migration or conversion.

# Canonical V3 Session Skeleton

```yaml
---
title: "The Garage Memory NN"
date: YYYY-MM-DD 00:00:00 +0300
permalink: "/posts/The Garage Memory sNN"
categories: [Memory]
tags: [Mika, "The Garage", "Memory File v3 Format", Training]
---

SESSION: G-YYYYMMDD
DATE: YYYY-MM-DD

STATE:
  mood: not-reported
  general: completed

CONTEXT:
  [Training session description]

TRAINING:
  warm_up:
    duration_min: 5
    ...

  main_work:
    exercise_name:
      category: ...
      sets: ...
      reps_per_set: ...
      total_reps: ...
      load: ...
      execution: ...
      rest_between_sets_sec: ...
      rest_before_exercise_sec: ...

FACTS:
  ...

OBSERVATIONS:
  ...

ANALYSIS:
  ...

PROGRESS:
  primary_goal: ...
  progression_status: ...
  previous_session: ...
  comparison:
    ...
  next_target:
    ...

PATTERNS:
  ...

OPEN_THREADS:
  ...

VIBE: ...
```

## Version Control Rule

This document is the reference specification for **Memory File v3 Format**. If Kaan asks Mika in the future to “check the V3 format,” this file should be treated as the canonical specification before creating or reviewing a V3 session memory file.
