# Learning Event Model

**Document:** Learning.Event.Model  
**Status:** Canonical project model  
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

A Learning Event is a significant, state-relevant event in the actual learning process. It records what happened, not the full chat transcript.

Learning Events belong to the learner-state layer and must not be placed in canonical course definitions.

## 2. Event principles

1. Record significant learning events, not every message.
2. Events are chronological.
3. An event describes an occurrence; it does not replace an assessment record or current state.
4. Historical events must not be silently rewritten because the current state changed.
5. Every event is associated with the relevant canonical object when applicable: Section, Lesson, Unit, LCP or CP.

## 3. Core event fields

A Learning Event should contain, where applicable:

- Event ID;
- timestamp;
- event type;
- Section ID;
- source Lesson ID;
- Unit ID;
- LCP/CP ID;
- event status/result;
- verification source when relevant;
- short evidence/reference;
- remediation or transition information when relevant.

The exact storage representation is implementation-dependent and is not fixed by this document.

## 4. Event categories

### Navigation

- `SECTION_STARTED`
- `LESSON_STARTED`
- `UNIT_STARTED`
- `LCP_STARTED`
- `CP_STARTED`
- `NEXT_UNIT_OPENED`
- `NEXT_LESSON_OPENED`
- `NEXT_SECTION_OPENED`

### Learning and remediation

- `UNIT_PRACTICE`
- `UNIT_REVIEW`
- `REMEDIATION_STARTED`
- `REMEDIATION_COMPLETED`

### Verification and assessment

- `UNIT_VERIFIED`
- `LCP_COMPLETED`
- `CP_COMPLETED`
- `RECHECK_REQUIRED`

### User confirmation

- `USER_CONFIRMATION_REQUESTED`
- `USER_CONFIRMED`

## 5. Event versus assessment

A Learning Event says **what happened**.

An Assessment Record says **what the control result was**.

A Learning State says **where the learner is now**.

These must remain separate concepts.

## 6. Event versus chat transcript

A Learning Session may contain many messages and interactions. These are not automatically Learning Events.

Example:

```text
Learning Session
├── questions
├── explanations
├── exercises
├── corrections
├── discussion
└── significant events
       ├── UNIT_STARTED
       ├── UNIT_VERIFIED
       └── REVIEW_REQUIRED
```

The protocol must remain compact enough to represent a long course without becoming a transcript.
