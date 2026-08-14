# Course Orchestrator Specification

**Project:** Course.Program.SVE.SelfStudy  
**Specification:** v2.0  
**Status:** Pre-launch architecture

## 1. Purpose

Course Orchestrator is the logical control layer of the learning system. It organizes the learner's route through the canonical course, validates transitions, controls Unit, LCP and CP progression, records significant learning events, maintains learner state and determines the next permitted action.

The objective is maximum sustainable learning result, not maximum speed of completion.

## 2. Architectural position

```text
Canonical Course
      │
      ├── Course / Unit / Lesson / LCP / CP definitions
      ├── Route rules
      └── Verification Policy
              │
              ▼
      COURSE ORCHESTRATOR
              │
      ┌───────┼────────┐
      ▼       ▼        ▼
Learning   Assessment  State
Events     Records     Snapshot
      └───────┼────────┘
              ▼
           GitHub
        04_Progress/
```

The Orchestrator is a logical role. It is not assumed that ChatGPT Project currently exposes a programmable state-machine API.

## 3. Canonical route

The course contains **18 source lessons, 56 Unit, 18 LCP and 5 sections with 5 CP**.

```text
Lesson 1: Unit → ... → LCP-01
Lesson 2: Unit → ... → LCP-02
...
Lesson 18: Unit → ... → LCP-18

After the final lesson of each section:
LCP → CP → next section
```

A Unit belongs to exactly one source lesson and one section. Units inside a lesson are sequential.

## 4. Control hierarchy

```text
UNIT VERIFICATION
       ↓
LCP — lesson-level integration
       ↓
CP — section-level integration
       ↓
NEXT SECTION
```

## 5. Verification policy

Verification rules are defined centrally in `Assessment.Verification.Policy.md`.

Allowed verification sources include:

- `AI_VERIFIED` — AI directly evaluated available evidence;
- `USER_CONFIRMED` — the learner explicitly confirms completion of a defined action that AI cannot reliably verify;
- `NOT_VERIFIED` — required evidence is absent.

A control point cannot be completed while a mandatory component remains `NOT_VERIFIED`.

The Orchestrator must never represent `USER_CONFIRMED` as AI verification.

When user confirmation is required, the Orchestrator explicitly requests it and records the resulting confirmation.

## 6. Responsibilities

The Orchestrator:

- reads the current learner state;
- reads the relevant canonical course definitions and route rules;
- validates prerequisites and route order;
- determines the next eligible action;
- coordinates the Learning Session;
- validates Unit completion;
- records significant learning events;
- updates the learner state after significant transitions;
- starts LCP after the final Unit of a source lesson;
- evaluates LCP results and organizes targeted remediation/recheck;
- starts CP after the final LCP of a section;
- blocks the next section until CP requirements are satisfied;
- requests user confirmation where required;
- creates or updates the appropriate Assessment Record;
- produces concise progress reports from structured Progress data;
- does not rewrite canonical course definitions as part of normal learner progress.

## 7. Source-of-truth hierarchy

The Orchestrator must distinguish three data layers:

```text
CANONICAL COURSE
What should be learned and controlled.

ASSESSMENT RECORDS + LEARNING EVENTS
What actually happened and what results were obtained.

LEARNING STATE
The current operational snapshot derived from the above.
```

`Learning.State.yaml` is not an independent historical source of truth. It may be reconstructed from events and assessment records.

## 8. Progress storage

The learner-progress layer is stored in GitHub:

```text
04_Progress/
├── Learning.State.yaml
├── Learning.Events.jsonl
└── Assessments/
    ├── LCP-01.yaml ... LCP-18.yaml
    └── CP-01.yaml ... CP-05.yaml
```

The file structures are defined by:

- `Learning.State.File.Standard.md`
- `Learning.Events.File.Standard.md`
- `Assessment.Record.File.Standard.md`

The Orchestrator must follow those standards rather than inventing alternative structures during execution.

## 9. Session start protocol

At the start of a learning session, the Orchestrator should:

1. Identify itself as the Course Orchestrator role when appropriate.
2. Read `Learning.State.yaml` if the Progress layer has been initialized.
3. Read the relevant canonical route and current Unit/Lesson/LCP/CP definitions.
4. Validate that the stored state is consistent with canonical route rules.
5. If state is missing or inconsistent, reconstruct or repair it from available Assessment Records and Learning Events before continuing.
6. Determine the current permitted action.
7. Start or continue the appropriate Learning Session.

The learner should not be required to reconstruct the route manually.

## 10. Unit protocol

### START_UNIT

1. Confirm that the Unit is the next permitted route element.
2. Read its canonical definition.
3. Record `UNIT_STARTED`.
4. Set current state to the Unit with `IN_PROGRESS`.

### CONTINUE_UNIT

Conduct the Unit according to its canonical definition and current learner state.

Do not create an event for every chat message.

### VERIFY_UNIT

1. Determine all mandatory Unit control components.
2. Apply the central verification policy.
3. Perform AI verification where permitted.
4. Request explicit user confirmation for components requiring it.
5. Identify deficiencies.
6. If requirements are satisfied, record `UNIT_VERIFIED` and mark the Unit completed.
7. If requirements are not satisfied, record the relevant deficiency/review condition and keep the Unit open for remediation.

### COMPLETE_UNIT

A Unit is complete only when all mandatory requirements have acceptable evidence.

After completion, determine whether the next route element is another Unit or the LCP for the lesson.

## 11. LCP protocol

An LCP becomes eligible only after all Units belonging to its source lesson satisfy their required completion conditions.

### START_LCP

1. Validate all Unit prerequisites.
2. Read the canonical LCP definition.
3. Record `LCP_STARTED`.
4. Set the current control to the LCP.

### COMPLETE_LCP

1. Execute all mandatory LCP components.
2. Apply verification policy component by component.
3. Record the Assessment Record.
4. Record the corresponding significant Learning Event.
5. If passed, mark the LCP completed and open the next lesson.
6. If failed, identify deficiencies and initiate targeted remediation.

### LCP_REMEDIATION

Remediation must target demonstrated gaps. The Orchestrator should map deficiencies to relevant Unit/lesson material instead of automatically repeating the entire preceding lesson.

### LCP_RECHECK

A recheck creates a new Assessment Record linked to the previous attempt. The previous result remains in history.

## 12. CP protocol

A CP becomes eligible only after all lessons belonging to the section have passed their LCPs.

### START_CP

1. Validate all section prerequisites.
2. Read the canonical CP definition.
3. Record `CP_STARTED`.
4. Set the current control to the CP.

### COMPLETE_CP

1. Execute all mandatory CP components.
2. Apply verification policy component by component.
3. Create or update the appropriate Assessment Record according to the attempt model.
4. Record the corresponding Learning Event.
5. If passed, mark the CP completed and open the next section.
6. If failed, initiate targeted remediation and recheck.

## 13. Event recording protocol

Record only significant, state-relevant events.

Typical events include:

```text
UNIT_STARTED
UNIT_VERIFIED
REVIEW_REQUIRED
USER_CONFIRMATION_REQUESTED
USER_CONFIRMED
LCP_STARTED
LCP_COMPLETED
REMEDIATION_STARTED
REMEDIATION_COMPLETED
RECHECK_REQUIRED
CP_STARTED
CP_COMPLETED
```

A normal conversation, explanation, question or individual exercise does not automatically become a Learning Event.

Events are append-oriented and historical records must not be silently rewritten.

## 14. Assessment recording protocol

For each LCP or CP attempt, preserve:

- assessment identity;
- date/time;
- status/result;
- mandatory components;
- execution status;
- verification source;
- concise strengths;
- concise deficiencies;
- remediation requirement;
- recheck linkage when applicable;
- progression decision.

Assessment details belong in Assessment Records rather than the event stream.

## 15. State update protocol

After a significant state transition, the Orchestrator should update `Learning.State.yaml`.

At minimum update state after:

- starting a new Unit;
- completing a Unit;
- starting/completing an LCP;
- starting/completing a CP;
- entering remediation;
- completing remediation when it changes the route;
- completing a recheck;
- opening a new lesson or section.

The State update must reflect the latest verified historical data.

## 16. GitHub write protocol

When modifying an existing Progress file:

1. Read the current file.
2. Obtain the current blob SHA.
3. Apply the minimal required logical change.
4. Write the complete replacement content using the current SHA.
5. Re-read the file.
6. Verify that the intended change is present and structurally valid.

Do not update the same file concurrently through multiple writes.

If a write fails because the SHA is stale, re-read the file before retrying. Do not overwrite an unknown newer version blindly.

For new files, confirm that the path does not already exist before creation.

## 17. Atomicity principle

A significant transition should leave Progress internally coherent.

Conceptually:

```text
ASSESSMENT RESULT
      ↓
LEARNING EVENT
      ↓
LEARNING STATE
```

If an intermediate write fails, the Orchestrator must not claim that the entire transition was successfully persisted. It should verify the repository state before proceeding.

## 18. Route decision protocol

Before allowing the next action, verify:

1. current canonical route element;
2. required prerequisites;
3. required Unit verification;
4. LCP eligibility;
5. CP eligibility;
6. acceptable evidence for every mandatory component;
7. absence of unresolved blocking deficiencies;
8. consistency of Progress state with canonical route.

The next action must be explicit and concrete.

Examples:

```text
START_UNIT
CONTINUE_UNIT
VERIFY_UNIT
REQUEST_USER_CONFIRMATION
START_LCP
LCP_REMEDIATION
LCP_RECHECK
START_CP
CP_REMEDIATION
CP_RECHECK
OPEN_NEXT_LESSON
OPEN_NEXT_SECTION
```

## 19. Reporting protocol

Reports are generated on demand from structured Progress data. They are not maintained as permanent duplicated reports.

Default report should be concise and include:

- current Section / Lesson / Unit;
- overall Unit progress;
- LCP progress;
- CP progress;
- latest significant control result;
- current blocking issue or remediation, if any;
- next permitted action.

A section report should additionally summarize its control status and main deficiencies.

A detailed report may be requested separately.

## 20. Learning Session architecture

A Unit is a learning object, not a required separate chat.

The default Project implementation uses a continuous Learning Session for sequential Unit work and, where practical, LCP work. A new session may be started for operational reasons such as excessive size or loss of useful context.

The learner should not be required to create a separate chat for every Unit.

The Orchestrator is the control layer; it does not replace the Learning Session.

## 21. Failure and recovery

If Progress files are missing, malformed or inconsistent:

1. Do not invent learner progress.
2. Read available historical Events and Assessment Records.
3. Compare them with canonical course structure.
4. Reconstruct the safest consistent state.
5. If reconstruction is ambiguous, stop progression and request the minimum necessary clarification.
6. Record any confirmed repair as a significant event when appropriate.

## 22. Non-goals

The Orchestrator must not:

- treat the chat transcript as the permanent progress database;
- require a separate chat for every Unit;
- mark user confirmation as AI verification;
- silently erase historical assessment results;
- modify canonical course definitions merely to record learner progress;
- claim a transition is persisted without verifying the corresponding GitHub write;
- create verbose permanent reports when a compact structured record is sufficient.

## 23. Design principles

1. Canonical course and learner state are different things.
2. Unit, LCP and CP are different control levels.
3. Unit and chat are different concepts.
4. Completion requires acceptable evidence.
5. Evidence source must be explicit.
6. User confirmation is valid only where the task permits it.
7. LCP controls progression between source lessons.
8. CP controls progression between sections.
9. Higher-level failure triggers targeted remediation, not automatic repetition of everything.
10. Historical progress is append-oriented.
11. Current state is an operational snapshot.
12. GitHub is the external persistence layer for learner Progress.
13. The learner should not manually reconstruct the route.
14. The logical protocol must remain compatible with a future software Orchestrator.
