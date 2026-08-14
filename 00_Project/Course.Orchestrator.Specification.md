# Course Orchestrator Specification

**Project:** Course.Program.SVE.SelfStudy  
**Specification:** v1.2  
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

### Unit verification

Controls the result of one Unit.

### LCP

Controls integrated and independent use of the important material of one complete source lesson. It is mandatory after the final Unit of that lesson.

### CP

Controls integrated learning of the complete section. It is mandatory after the final lesson LCP of that section and is the transition gate to the next section.

## 4. Responsibilities

The Orchestrator:

- identifies the current section, source lesson and route element;
- validates prerequisites and route order;
- determines the next eligible action;
- coordinates Learning Sessions;
- validates Unit completion;
- starts LCP after the final Unit of a source lesson;
- evaluates LCP results and organizes targeted remediation/recheck;
- starts CP after the final LCP of a section;
- blocks the next section until CP requirements are satisfied;
- determines the next concrete learner action.

It does not rewrite the canonical course or declare mastery solely from a learner claim.

## 5. Remediation principle

Failure at LCP or CP does not automatically mean repeating the whole preceding route.

The Orchestrator should identify the demonstrated gaps, map them to relevant Unit or lesson material, organize targeted remediation and then conduct a recheck.

## 6. Learning Session architecture

A Unit is a learning object, not a required separate chat.

The default Project implementation uses a continuous Learning Session for sequential Unit work and, where practical, LCP work. A new session may be started for operational reasons such as excessive size or loss of useful context.

The learner should not be required to create a separate chat for every Unit.

## 7. States

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

## 8. Evidence

Unit evidence may include understanding, controlled practice, independent performance, verification and errors.

LCP evidence should establish integrated use of the lesson material, independent performance and critical gaps.

CP evidence should establish integrated use of the section material, critical gaps, remediation requirements and eligibility for the next section.

The exact evidence format is not fixed yet; learner-state storage will be designed separately.

## 9. Policy checks

Before a transition, verify:

1. Current canonical route element.
2. Required Unit prerequisites.
3. Required Unit verification.
4. For LCP: all Unit of the source lesson are eligible for lesson control.
5. For CP: all lessons in the section have passed their LCP.
6. Required assessment evidence is sufficient.
7. Critical unresolved deficiencies are handled.
8. The proposed transition matches the canonical route.

## 10. Logical actions

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

## 11. Separation of concerns

GitHub defines the canonical route and control objects. ChatGPT Project organizes actual learning. The mechanism and format for storing learner progress remain a separate design task.

## 12. Design principles

1. Canonical course and learner state are different things.
2. Unit, LCP and CP are different control levels.
3. Unit and chat are different concepts.
4. Completion requires evidence.
5. LCP controls progression between source lessons.
6. CP controls progression between sections.
7. Higher-level failure triggers targeted remediation, not automatic repetition of everything.
8. The learner should not manually reconstruct the route.
9. The logical protocol must remain compatible with a future software Orchestrator.