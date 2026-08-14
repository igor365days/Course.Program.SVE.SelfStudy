# Learning State File Standard

**File:** `04_Progress/Learning.State.yaml`  
**Format:** YAML  
**Status:** Canonical standard

## Purpose

Defines the structure of the compact current state of one learner's course progress.

The file is an operational snapshot, not the historical source of truth.

## Canonical structure

```yaml
course: Course.Program.SVE.SelfStudy
state_version: 1
updated_at: YYYY-MM-DDTHH:MM:SS

current:
  section: 1
  lesson: 1
  unit: 1.1
  control: null
  status: IN_PROGRESS

progress:
  units_completed: 0
  units_total: 56
  lessons_completed: 0
  lessons_total: 18
  lcps_passed: 0
  lcps_total: 18
  cps_passed: 0
  cps_total: 5

last_completed:
  unit: null
  lesson: null
  lcp: null
  cp: null

remediation:
  required: false
  target: null
  reason: null

next_action: START_UNIT
blocking_conditions: []
```

## Rules

1. Only the current state is stored here; chat transcripts are excluded.
2. Counters must be consistent with canonical course totals.
3. `current` identifies the learner's current route position.
4. `next_action` must comply with the canonical route and Orchestrator rules.
5. A mandatory unresolved control cannot be omitted from `blocking_conditions`.
6. Verification provenance may be included where relevant: `AI_VERIFIED`, `USER_CONFIRMED`, `NOT_VERIFIED`.
7. State may be regenerated from historical events and assessment records.
8. Learner-specific data must never be written into canonical course files.

## Reporting

The structure must support concise reports covering current position, overall progress, latest completed control and next action.
