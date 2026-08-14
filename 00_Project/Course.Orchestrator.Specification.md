# Course Orchestrator Specification

**Project:** Course.Program.SVE.SelfStudy  
**Specification:** v1.1  
**Status:** Pre-launch architecture

## 1. Purpose

Course Orchestrator is the logical control layer of the learning system. It organizes the learner's route through the canonical course, validates transitions, controls Unit and Checkpoint progression, and maintains an accurate representation of actual learning state.

The objective is maximum sustainable learning result, not maximum speed of completion.

## 2. Canonical Route

The canonical course contains 18 source lessons, 56 Unit and 5 sections. Each Unit belongs to exactly one section. Unit inside a section are sequential. Each section ends with exactly one Checkpoint.

```text
SECTION 1 → Unit → ... → Unit → CP-1
SECTION 2 → Unit → ... → Unit → CP-2
SECTION 3 → Unit → ... → Unit → CP-3
SECTION 4 → Unit → ... → Unit → CP-4
SECTION 5 → Unit → ... → Unit → CP-5
```

A passed CP is the transition gate to the next section. Failed or insufficient CP results require remediation and recheck before transition.

## 3. System Layers

```text
GitHub — Canonical Course
        ↓
Course Orchestrator
        ↓
Learning Session / Checkpoint Session
        ↓
Learning State + Evidence
```

GitHub defines what and in what order to learn. The Project organizes the practical learning process for one learner.

## 4. Core Principle

Separate LLM reasoning from state transition.

```text
LLM analysis
    ↓
proposed action
    ↓
Policy / State validation
    ↓
Orchestrator
    ↓
state transition
```

A proposed action is not automatically a valid transition.

## 5. Responsibilities

The Orchestrator:

- identifies the current section and route element;
- identifies the current Unit or CP;
- validates prerequisites and route order;
- determines the next eligible action;
- coordinates the Learning Session;
- receives and evaluates evidence;
- organizes review/remediation;
- controls Unit completion;
- starts the section CP after the final Unit;
- blocks the next section until CP requirements are satisfied;
- records or requests recording of relevant learning state;
- gives the learner one clear next action.

It does not rewrite the canonical course, teach the whole course itself, or declare mastery solely from a learner claim.

## 6. Learning Session Architecture

A Unit is a **learning object**, not a required separate chat.

The default Project implementation uses a continuous Learning Session chat for sequential Unit work. A new Learning Session may be started only when the current chat becomes too large, loses useful context, or another operational reason makes rotation appropriate.

The learner should not be required to create a new chat for every Unit.

A Checkpoint may use the same Learning Session or a separate Checkpoint Session when that is operationally preferable. This does not change the canonical route.

## 7. Unit States

```text
NOT_STARTED
    ↓
IN_PROGRESS
    ├── REVIEW_REQUIRED → IN_PROGRESS
    └── VERIFIED → COMPLETED
```

A Unit becomes `COMPLETED` only when its canonical verification criteria are satisfied.

## 8. Checkpoint States

```text
NOT_STARTED
    ↓
IN_PROGRESS
    ├── FAILED → REMEDIATION → RECHECK
    └── PASSED → COMPLETED → NEXT SECTION
```

## 9. Unit Completion Evidence

A logical result should contain, as applicable:

```text
unit_id
section_id
status
understanding
controlled_practice
independent_performance
verification
errors
review_required
recommended_next_action
```

The exact evidence requirements come from the Unit definition.

## 10. Checkpoint Evidence

A CP result should contain:

```text
checkpoint_id
section_id
covered_route_range
status
knowledge_result
skill_result
critical_gaps
remediation_required
next_section_eligible
```

## 11. Policy Checks

Before a transition, verify:

1. Is the requested element the current canonical route element?
2. Are prerequisites satisfied?
3. Are mandatory learning stages complete?
4. Is sufficient evidence available?
5. Has required verification passed?
6. Are critical unresolved deficiencies absent?
7. If this is a CP, has the whole section route been completed?
8. Is the next section locked or unlocked according to the CP result?

Example:

```text
PROPOSED: OPEN SECTION 2

POLICY CHECK:
✓ Section 1 Unit completed
✓ CP-1 completed
✓ CP-1 passed

RESULT: ALLOW
```

## 12. Logical Actions

### Navigation
- `GET_CURRENT_STATE`
- `GET_CURRENT_SECTION`
- `GET_CURRENT_ROUTE_ELEMENT`
- `GET_NEXT_ROUTE_ELEMENT`

### Learning
- `START_UNIT`
- `CONTINUE_UNIT`
- `REVIEW_UNIT`
- `RETRY_UNIT`

### Verification
- `VERIFY_UNIT`
- `COMPLETE_UNIT`

### Checkpoints
- `START_CHECKPOINT`
- `COMPLETE_CHECKPOINT`
- `REMEDIATION`
- `RECHECK`
- `OPEN_NEXT_SECTION`

### State and Evidence
- `READ_PROGRESS`
- `RECORD_EVIDENCE`
- `UPDATE_PROGRESS`

These are logical protocol actions, not claims that ChatGPT Project currently exposes a programmable state-machine API.

## 13. Progress Model

Progress is the compact current state of the learner, not a copy of the course and not a transcript of conversations.

At minimum it must allow the Orchestrator to determine:

- current section;
- current route element;
- Unit/CP statuses;
- unresolved remediation;
- persistent important errors;
- latest verified evidence;
- next eligible action;
- section/CP transition status.

## 14. Project Implementation

The initial implementation uses Project Instructions, a dedicated Orchestrator chat, a compact Progress representation and canonical GitHub materials.

Project Sources can preserve useful snapshots, but ordinary Project chats cannot be assumed to edit an existing Source or automatically create a new Source. Therefore Sources are not treated as the transactional state store.

The learner should perform as little interface administration as possible. In particular, creating a separate chat for every Unit is not a requirement.

## 15. Future Software Implementation

The logical protocol remains compatible with a real software implementation:

```text
LLM
 ↓
proposed action / tool call
 ↓
Policy Layer
 ↓
Course Orchestrator
 ↓
State Store
 ↓
Learning Session / tools
 ↓
Evidence
 ↓
Orchestrator
```

## 16. Design Principles

1. Canonical course and learner state are different things.
2. Sections are route-control units; CP is the section transition gate.
3. Unit and chat are different concepts.
4. One Learning Session may contain many sequential Unit.
5. LLM reasoning and state transition are different responsibilities.
6. Completion requires evidence.
7. CP completion controls section transition.
8. The learner should not manually manage the learning route.
9. Progress remains compact and operational.
10. The architecture must remain transferable to a future software Orchestrator.
