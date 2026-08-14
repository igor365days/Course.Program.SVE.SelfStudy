# Assessment Record Model

**Document:** Assessment.Record.Model  
**Status:** Canonical project model  
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

An Assessment Record represents the actual result of a Unit verification, LCP or CP for one learner.

It is part of the learner-state layer and is separate from the canonical definition of the assessment.

## 2. Assessment identity

Each record identifies:

- Assessment Record ID;
- control type: `UNIT`, `LCP` or `CP`;
- target ID;
- Section ID;
- source Lesson ID when applicable;
- Unit ID when applicable;
- date/time;
- assessment status;
- component results;
- verification source;
- evidence summary;
- deficiencies;
- remediation;
- recheck information;
- progression decision.

## 3. Component result

A control may contain several mandatory components.

Each component should distinguish at least:

```text
Execution status
Verification source
Assessment result
```

For example:

```text
Pronunciation
Execution: COMPLETED
Verification: USER_CONFIRMED
Assessment: ACCEPTED
```

or:

```text
Grammar
Execution: COMPLETED
Verification: AI_VERIFIED
Assessment: FAILED
```

## 4. Verification source

Allowed verification sources are defined by `Assessment.Verification.Policy.md`.

At minimum:

- `AI_VERIFIED`
- `USER_CONFIRMED`
- `NOT_VERIFIED`

A record must not claim AI verification when the result was only confirmed by the learner.

## 5. Assessment status

Recommended control statuses:

```text
NOT_STARTED
IN_PROGRESS
PASSED
FAILED
RECHECK_REQUIRED
COMPLETED
```

`PASSED` describes assessment success. `COMPLETED` describes completion of the control process. They are not interchangeable.

## 6. Deficiencies and remediation

A failed or insufficient assessment should identify relevant deficiencies when possible.

The Orchestrator uses these deficiencies to organize targeted remediation rather than automatically repeating the entire preceding route.

## 7. Recheck

A recheck is a new assessment event/record linked to the previous assessment. Historical results must remain available.

A recheck does not erase the original failed result.

## 8. Progression decision

The record may include the resulting route decision:

```text
STAY
REVIEW_REQUIRED
RECHECK_REQUIRED
OPEN_NEXT_UNIT
OPEN_NEXT_LESSON
OPEN_NEXT_SECTION
```

The decision must comply with the canonical course route and Orchestrator rules.

## 9. Separation from canonical assessment

Canonical Unit/LCP/CP definitions describe what must be assessed.

Assessment Records describe what actually happened for a learner.

Individual dates, scores, errors and results must never be written into canonical course definitions.
