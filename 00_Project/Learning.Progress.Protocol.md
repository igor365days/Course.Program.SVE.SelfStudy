# Learning Progress Protocol

**Document:** Learning.Progress.Protocol  
**Status:** Canonical project protocol  
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

This protocol defines how actual learner progress is conceptually represented and how learning events, assessment records and current state interact.

It does not define the physical storage mechanism.

## 2. Three-layer learner-state model

```text
LEARNING EVENT
What happened?
        ↓
ASSESSMENT RECORD
What was the result of control?
        ↓
LEARNING STATE
Where is the learner now?
        ↓
ORCHESTRATOR DECISION
What is the next permitted action?
```

## 3. Learning Event

A Learning Event records a significant state-relevant occurrence. It is not a transcript of the chat.

Events should be compact, chronological and associated with the relevant canonical object.

## 4. Assessment Record

An Assessment Record captures the actual result of a Unit verification, LCP or CP.

It must preserve the distinction between:

- task execution;
- verification source;
- assessment result;
- deficiencies;
- remediation;
- progression decision.

## 5. Learning State

Learning State is the current operational picture derived from events and assessment records. It identifies the current route position, completed prerequisites, unresolved conditions and next permitted action.

## 6. Verification policy

The applicable verification method is determined by the canonical `Assessment.Verification.Policy` according to the type of control component.

The principal methods are:

```text
AI_VERIFIED
USER_CONFIRMED
COMBINED
```

Actual learner records use the applicable verification source and must never misrepresent user confirmation as AI verification.

## 7. User confirmation

When a required task cannot be reliably verified by AI, the Orchestrator must request explicit user confirmation.

Conceptually:

```text
Required task
    ↓
AI cannot reliably verify
    ↓
REQUEST_USER_CONFIRMATION
    ↓
USER_CONFIRMED
    ↓
Assessment may continue
```

A user confirmation confirms execution of the required action. It is not automatically equivalent to proof of mastery.

## 8. Assessment completion

A control point can be completed only when all mandatory components have acceptable evidence according to the canonical verification policy.

`NOT_VERIFIED` on a mandatory component blocks completion.

Assessment success and verification source are separate fields.

## 9. Remediation

If a control fails or identifies a material deficiency:

```text
FAILED / DEFICIENCY
        ↓
TARGETED REMEDIATION
        ↓
RECHECK
        ↓
UPDATED ASSESSMENT RECORD
```

The original result remains part of history.

## 10. Historical integrity

Learning history is append-oriented. A new result or recheck must not silently erase an earlier result.

Current state may change, but historical events and assessment results remain distinguishable.

## 11. Canonical versus learner state

```text
GITHUB
  = canonical course, route and verification policy

CHATGPT PROJECT / OTHER STATE LAYER
  = actual learner events, assessment results and current state
```

The physical implementation of the learner-state layer is intentionally deferred until the capabilities and constraints of the chosen platform are fully evaluated.

## 12. Non-goals

This protocol does not:

- define a database schema;
- require one file per Unit;
- require one chat per Unit;
- treat Project Sources as a mutable database;
- store chat transcripts as Learning Events;
- place learner-specific results into canonical course files.
