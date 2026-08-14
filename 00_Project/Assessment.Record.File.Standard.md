# Assessment Record File Standard

**Files:** `04_Progress/Assessments/LCP-XX.yaml`, `04_Progress/Assessments/CP-XX.yaml`  
**Format:** YAML  
**Status:** Canonical standard

## Purpose

Defines the compact learner-specific record of an actual LCP or CP assessment.

## Canonical structure

```yaml
assessment_id: LCP-01
type: LCP
section: 1
lesson: 1
date: YYYY-MM-DDTHH:MM:SS
status: PASSED

components:
  grammar:
    execution: COMPLETED
    verification: AI_VERIFIED
    result: PASSED
  pronunciation:
    execution: COMPLETED
    verification: USER_CONFIRMED
    result: ACCEPTED

summary:
  strengths: []
  deficiencies: []

remediation:
  required: false
  target: null
  reason: null

recheck:
  required: false
  previous_assessment: null

decision: OPEN_NEXT_LESSON
```

## Rules

1. One current assessment record corresponds to one control-point attempt.
2. A recheck creates a new record linked to the previous assessment; it does not erase the previous result.
3. `execution`, `verification` and `result` are separate concepts.
4. `USER_CONFIRMED` must never be represented as AI verification.
5. Every mandatory component must have acceptable evidence before the control is considered complete.
6. `NOT_VERIFIED` on a mandatory component blocks completion.
7. Deficiencies should be concise and actionable.
8. Records contain results, not full transcripts of the assessment session.
9. The record must remain compatible with the canonical verification policy and Orchestrator rules.

## Assessment status

Recommended values:

```text
NOT_STARTED
IN_PROGRESS
PASSED
FAILED
RECHECK_REQUIRED
COMPLETED
```

`PASSED` describes assessment success. `COMPLETED` describes completion of the control process.

## Reporting

The record must support concise reporting of result, verification source, main strengths/deficiencies, remediation and progression decision.
