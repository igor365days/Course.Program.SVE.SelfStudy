# Course Orchestrator Specification

**Project:** Course.Program.SVE.SelfStudy  
**Specification:** v1.0  
**Status:** Pre-launch architecture

## 1. Purpose

Course Orchestrator is the logical control layer of the learning system.

Its purpose is to organize the learner's route through the canonical course, validate transitions between learning states, coordinate Unit and Checkpoint sessions, and maintain an accurate representation of the learner's actual progress.

The Orchestrator does not replace the canonical course, does not teach the entire course itself, and does not treat a user's statement that a Unit is "finished" as sufficient evidence of mastery.

The primary objective is **maximum sustainable learning result**, not maximum speed of course completion.

## 2. System Boundary

The system has four principal layers:

```text
GitHub — Canonical Course
        ↓
Course Orchestrator
        ↓
Learning Sessions / Checkpoints
        ↓
Learning Progress + Evidence
```

### 2.1 Canonical Course

GitHub defines what must be learned, in what order, and what each Unit and Checkpoint is expected to accomplish.

The Orchestrator must not silently modify this layer.

### 2.2 Orchestrator

The Orchestrator determines what action is currently permitted or required based on the canonical route, learner state, prerequisites, evidence and verification results.

### 2.3 Learning Session

A Unit chat conducts the actual learning activity: explanation, practice, tasks and verification appropriate to the Unit.

A Checkpoint chat conducts an integrated assessment of the required accumulated material.

### 2.4 Learning Progress

Progress represents the actual state of this learner's course participation. It is not a copy of the canonical course.

## 3. Core Principle

Separate **reasoning** from **state transition**.

The LLM may analyze the learner's work and propose an action. The Orchestrator validates whether that action is allowed by the course state and rules before treating it as a state transition.

Conceptually:

```text
LLM analysis
    ↓
proposed action
    ↓
Policy / State validation
    ↓
Course Orchestrator
    ↓
state transition
    ↓
updated Progress
```

A proposed action is not automatically a valid transition.

## 4. Responsibilities

The Orchestrator is responsible for:

- identifying the current route position;
- identifying the current Unit or Checkpoint;
- validating prerequisites;
- determining the next eligible action;
- coordinating Unit sessions;
- receiving and evaluating completion evidence;
- deciding whether review/remediation is required;
- controlling transitions to the next Unit;
- initiating Checkpoints at the canonical route position;
- recording relevant evidence and progress state;
- preventing invalid or premature completion states;
- providing the learner with the next concrete action.

The Orchestrator is not responsible for:

- rewriting the canonical course without authorization;
- replacing the Unit's teaching process;
- storing the entire history of a chat in Progress;
- declaring mastery solely from the learner's assertion;
- optimizing the course structure merely for ChatGPT convenience.

## 5. Core Actions

The logical action vocabulary is:

### Navigation

- `GET_CURRENT_STATE`
- `GET_CURRENT_UNIT`
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

### Progress and Evidence

- `READ_PROGRESS`
- `RECORD_EVIDENCE`
- `UPDATE_PROGRESS`

These actions are a logical protocol. They do not imply that ChatGPT Project currently exposes a programmable API for executing them.

## 6. Learning State Machine

### 6.1 Unit states

```text
NOT_STARTED
    ↓
IN_PROGRESS
    ├── REVIEW_REQUIRED ──→ IN_PROGRESS
    │
    └── verification passed → COMPLETED
                                  ↓
                              NEXT UNIT
```

A Unit may only become `COMPLETED` when the required learning and verification criteria are satisfied.

### 6.2 Checkpoint states

```text
NOT_STARTED
    ↓
IN_PROGRESS
    ├── FAILED → REMEDIATION → RECHECK
    │
    └── PASSED → COMPLETED
```

## 7. Preconditions for Unit Completion

Before `COMPLETE_UNIT`, the system should establish, as applicable to the Unit:

- required content was covered;
- required practice was performed;
- verification was conducted;
- the learner demonstrated the required level of independent performance;
- no critical unresolved deficiency prevents progression.

The exact criteria come from the canonical Unit definition.

## 8. Evidence Model

Completion must be based on evidence rather than a binary claim.

A logical Unit result should contain at least:

```text
unit_id
status
understanding
controlled_practice
independent_performance
verification
errors
review_required
recommended_next_action
```

Not every field needs to be displayed to the learner, and the exact evidence requirements depend on the Unit.

## 9. Policy Layer

Before a state transition, the following questions should be checked:

1. Is this the current canonical route element?
2. Are prerequisites satisfied?
3. Are mandatory learning stages complete?
4. Is sufficient evidence available?
5. Has the required verification passed?
6. Are there critical unresolved errors?
7. Is the proposed transition consistent with the canonical route?

If a condition fails, the Orchestrator should reject or defer the transition and produce a corrective action.

Example:

```text
PROPOSED: COMPLETE_UNIT(1.1)

POLICY CHECK:
✓ current unit
✓ required practice
✓ verification performed
✗ independent performance insufficient

RESULT: DENY
NEXT ACTION: REVIEW_UNIT(1.1)
```

## 10. Unit Chat Protocol

A Unit chat is a learning session, not the course controller.

At start it receives or determines:

- Unit ID;
- canonical Unit definition;
- relevant prerequisites;
- current learner state;
- current learning objective.

During the session it produces learning activity and evidence.

At the end it produces a structured result for the Orchestrator, for example:

```text
UNIT RESULT
unit: 1.1
learning_completed: true
verification: passed
independent_performance: sufficient
errors: []
review_required: false
recommended_next: 1.2
```

The recommended next Unit is advisory. The Orchestrator validates the actual transition.

## 11. Orchestrator → Learner Protocol

The Orchestrator should normally give the learner one clear next action.

Examples:

- start the current Unit;
- continue the current Unit;
- perform a specific remediation task;
- create/open the next Unit chat;
- begin a Checkpoint;
- repeat a required verification.

The learner should not have to reconstruct the course route manually.

## 12. Progress Model

Progress should contain current state, not full conversation history.

At minimum it should be possible to determine:

- current route element;
- status of completed Unit and Checkpoints;
- unresolved remediation;
- important persistent errors;
- review requirements;
- latest verified evidence;
- next eligible action.

The Progress model must remain aligned with the canonical route but must never become a second copy of canonical Unit definitions.

## 13. ChatGPT Project Implementation

In the initial implementation, Course Orchestrator is a **logical role implemented with ChatGPT Project instructions, a dedicated Orchestrator working chat, structured Progress and canonical GitHub materials**.

The current ChatGPT Project does not need to be assumed to have a programmable state machine, automatic cross-chat write access, or automatic chat creation.

Therefore the protocol must work even when a learner performs a small explicit interface action, such as creating the next Unit chat.

The learner-facing experience should nevertheless make such actions minimal and unambiguous.

## 14. Future Software Implementation

The architecture must remain compatible with a future programmatic implementation:

```text
LLM
 ↓
proposed action / tool call
 ↓
Policy Layer
 ↓
Course Orchestrator
 ↓
Course State / Progress Store
 ↓
Learning Session / external tools
 ↓
Evidence
 ↓
Orchestrator
```

The logical actions, states, evidence model and policies should therefore be designed independently of the current ChatGPT UI.

## 15. Design Principles

1. Canonical course and learner state are different things.
2. Learning sessions and orchestration are different roles.
3. LLM reasoning and state transition are different responsibilities.
4. Completion requires evidence.
5. The Orchestrator validates transitions.
6. The learner should not have to manage the learning route manually.
7. Adapt the learning process without silently changing the canonical course.
8. Prefer learning quality and sustainability over speed.
9. Keep Progress compact and operational.
10. Design the logical protocol so that it can later become a real software orchestrator.
