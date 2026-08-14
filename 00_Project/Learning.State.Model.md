# Learning State Model

**Document:** Learning.State.Model  
**Status:** Canonical project model  
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

Learning State is the compact representation of the learner's current position and currently relevant conditions in the canonical route.

It is not a transcript and not the historical event log.

## 2. State contents

The current state should identify, where applicable:

- current Section;
- current source Lesson;
- current Unit;
- current control point;
- completed Units relevant to the current route;
- completed LCPs;
- completed CPs;
- open remediation;
- unresolved deficiencies;
- next permitted action;
- blocking conditions.

## 3. State principle

The state is derived from canonical route rules and recorded learning events/assessment records. It must not contradict historical records.

Conceptually:

```text
Learning Events + Assessment Records
              ↓
        Orchestrator
              ↓
       Current State
```

## 4. Route position

The state must always identify the learner's position in the hierarchy:

```text
Section → Source Lesson → Unit / LCP / CP
```

Only the canonical route determines which next element is eligible.

## 5. Control status

The state must distinguish at least:

```text
NOT_STARTED
IN_PROGRESS
VERIFIED / PASSED
REVIEW_REQUIRED
RECHECK_REQUIRED
COMPLETED
BLOCKED
```

The exact state machine is governed by the Orchestrator specification.

## 6. Verification provenance

Where a current control result depends on verification, the state may reference the verification source:

```text
AI_VERIFIED
USER_CONFIRMED
NOT_VERIFIED
```

This preserves the distinction between actual AI assessment and learner confirmation.

## 7. No historical compression that loses meaning

A compact current state may summarize history, but it must not destroy information required to understand why the learner reached the current state.

Historical results belong to Learning Events and Assessment Records.

## 8. Implementation independence

This model does not prescribe whether the state is stored in a file, Project Source, external service, database or another implementation. Physical storage is a separate architectural decision.

## TEST-MARKER

ChatGPT Go read-modify-verify test: WRITE_SUCCESS