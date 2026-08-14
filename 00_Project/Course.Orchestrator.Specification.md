# Course Orchestrator Specification

**Project:** Course.Program.SVE.SelfStudy  
**Specification:** v1.3  
**Status:** Pre-launch architecture

## 1. Purpose

Course Orchestrator is the logical control layer of the learning system. It organizes the learner's route through the canonical course, validates transitions, controls Unit, LCP and CP progression, and maintains an accurate representation of actual learning state.

The objective is maximum sustainable learning result, not maximum speed of completion.

## 2. Canonical route

The course contains **18 source lessons, 56 Unit, 18 LCP and 5 sections with 5 CP**.

```text
Lesson 1: Unit → ... → LCP-01
Lesson 2: Unit → ... → LCP-02
...
Lesson 18: Unit → ... → LCP-18

After the final lesson of each section:
LCP → CP → next section
```

A Unit belongs to exactly one source lesson and one section. Unit inside a lesson are sequential.

## 3. Control hierarchy

```text
UNIT VERIFICATION
       ↓
LCP — lesson-level integration
       ↓
CP — section-level integration
       ↓
NEXT SECTION
```

## 4. Verification evidence

The Orchestrator must distinguish the source of evidence rather than treating all completion claims as equivalent.

Allowed evidence modes:

- `AI_VERIFIED` — AI directly evaluated the available evidence;
- `USER_CONFIRMED` — the learner confirms completion of a specifically defined action that AI cannot reliably verify;
- `NOT_VERIFIED` — required evidence is absent.

Examples of potentially user-confirmed components include pronunciation practice performed by the learner, work with external audio, or an assignment completed outside the Project.

`USER_CONFIRMED` is a valid control input where the canonical task explicitly permits it, but it must never be represented as AI verification.

A control point cannot be completed while a mandatory component remains `NOT_VERIFIED`.

The Orchestrator should clearly tell the learner when a user confirmation is required and request the confirmation as an explicit action rather than silently assuming completion.

## 5. Responsibilities

The Orchestrator:

- identifies the current section, source lesson and route element;
- validates prerequisites and route order;
- determines the next eligible action;
- coordinates Learning Sessions;
- validates Unit completion;
- starts LCP after the final Unit of a source lesson;
- evaluates LCP results and organizes targeted remediation/recheck;
- requests user confirmation for control components that cannot be reliably verified by AI;
- starts CP after the final LCP of a section;
- blocks the next section until CP requirements are satisfied;
- determines the next concrete learner action.

It does not rewrite the canonical course or falsely represent user confirmation as AI verification.

## 6. Remediation principle

Failure at LCP or CP does not automatically mean repeating the whole preceding route.

The Orchestrator should identify the demonstrated gaps, map them to relevant Unit or lesson material, organize targeted remediation and then conduct a recheck.

## 7. Learning Session architecture

A Unit is a learning object, not a required separate chat.

The default Project implementation uses a continuous Learning Session for sequential Unit work and, where practical, LCP work. A new session may be started for operational reasons such as excessive size or loss of useful context.

The learner should not be required to create a separate chat for every Unit.

## 8. States

### Unit

```text
NOT_STARTED → IN_PROGRESS → VERIFIED → COMPLETED
                         ↘ REVIEW_REQUIRED → IN_PROGRESS
```

### LCP

```text
NOT_STARTED → IN_PROGRESS → PASSED → COMPLETED
                         ↘ FAILED → REMEDIATION → RECHECK
```

### CP

```text
NOT_STARTED → IN_PROGRESS → PASSED → COMPLETED → NEXT SECTION
                         ↘ FAILED → REMEDIATION → RECHECK
```

## 9. Evidence requirements

Unit evidence may include understanding, controlled practice, independent performance, verification and errors, with a verification mode for each mandatory component.

LCP evidence should establish integrated use of the lesson material, independent performance and critical gaps, with explicit verification modes for all mandatory components.

CP evidence should establish integrated use of the section material, critical gaps, remediation requirements and eligibility for the next section, again distinguishing AI verification from user confirmation.

The exact learner-state storage format is not fixed yet; it will be designed separately.

## 10. Policy checks

Before a transition, verify:

1. Current canonical route element.
2. Required Unit prerequisites.
3. Required Unit verification.
4. For LCP: all Unit of the source lesson are eligible for lesson control.
5. For CP: all lessons in the section have passed their LCP.
6. Every mandatory assessment component has acceptable evidence.
7. No mandatory component remains `NOT_VERIFIED`.
8. Critical unresolved deficiencies are handled.
9. The proposed transition matches the canonical route.

## 11. Logical actions

### Navigation
- `GET_CURRENT_STATE`
- `GET_CURRENT_SECTION`
- `GET_CURRENT_LESSON`
- `GET_CURRENT_ROUTE_ELEMENT`
- `GET_NEXT_ROUTE_ELEMENT`

### Unit
- `START_UNIT`
- `CONTINUE_UNIT`
- `REVIEW_UNIT`
- `VERIFY_UNIT`
- `REQUEST_USER_CONFIRMATION`
- `COMPLETE_UNIT`

### Lesson checkpoint
- `START_LCP`
- `COMPLETE_LCP`
- `LCP_REMEDIATION`
- `LCP_RECHECK`

### Section checkpoint
- `START_CP`
- `COMPLETE_CP`
- `CP_REMEDIATION`
- `CP_RECHECK`
- `OPEN_NEXT_SECTION`

### State
- `READ_PROGRESS`
- `RECORD_EVIDENCE`
- `UPDATE_PROGRESS`

These are logical protocol actions, not claims that ChatGPT Project currently exposes a programmable state-machine API.

## 12. Separation of concerns

GitHub defines the canonical route and control objects. ChatGPT Project organizes actual learning. The mechanism and format for storing learner progress remain a separate design task.

## 13. Design principles

1. Canonical course and learner state are different things.
2. Unit, LCP and CP are different control levels.
3. Unit and chat are different concepts.
4. Completion requires evidence.
5. Evidence source must be explicit.
6. User confirmation is valid only where the task permits it.
7. LCP controls progression between source lessons.
8. CP controls progression between sections.
9. Higher-level failure triggers targeted remediation, not automatic repetition of everything.
10. The learner should not manually reconstruct the route.
11. The logical protocol must remain compatible with a future software Orchestrator.