# Checkpoint Definition Standard

**Document:** `Checkpoint.Definition.Standard`
**Status:** Canonical project standard
**Applies to:** `Course.Program.SVE.SelfStudy`

## 1. Purpose

Defines the canonical structure of lesson checkpoints (`LCP`) and section checkpoints (`CP`). It contains course requirements only, never learner Progress.

## 2. Identity

Each checkpoint must define:

- control ID;
- control type: `LCP` or `CP`;
- source lesson(s) or section;
- exact route position;
- preceding Unit/LCP prerequisites;
- next route target after successful completion.

## 3. Learning and control scope

The definition must state:

- integrated learning result being checked;
- knowledge and skills covered;
- required assessment components;
- assessment tasks/evidence;
- verification mode for every required component;
- success criteria;
- failure criteria;
- remediation and recheck conditions.

Allowed verification values are only:

- `AI_VERIFIED`
- `USER_CONFIRMED`
- `NOT_VERIFIED`

## 4. LCP

An LCP checks integrated use of the important material of one source lesson. It is performed after all Units of that lesson are successfully completed.

An LCP must not be reduced to a copy of Unit verifications. Its required components must provide evidence of integrated lesson-level performance.

## 5. CP

A CP checks integrated mastery of the lessons belonging to one section. It is performed after the final LCP of the section and is required to open the next section.

## 6. Assessment integrity

A checkpoint may be `PASSED` only when every required component has acceptable evidence according to the verification policy. Missing mandatory evidence means the checkpoint cannot be considered fully verified.

Assessment attempts are stored separately from this canonical definition. Historical attempts must not be written into checkpoint definition files.

## 7. Reassessment

Rules for reassessment of an already passed checkpoint are governed by `Assessment.Reassessment.Policy.md`.

A negative reassessment does not by itself erase historical successful completion.

## 8. Route

```text
all required Unit PASSED
        ↓
START_LCP
        ↓
LCP assessment
        ├─ FAILED → remediation → recheck
        └─ PASSED → next lesson

all required LCP PASSED
        ↓
START_CP
        ↓
CP assessment
        ├─ FAILED → remediation → recheck
        └─ PASSED → next section
```

## 9. Canonical references

- `00_Project/Assessment.Verification.Policy.md`
- `00_Project/Assessment.Record.File.Standard.md`
- `00_Project/Assessment.Reassessment.Policy.md`
- `00_Project/Learning.State.Machine.md`
- `00_Project/Learning.Progress.Protocol.md`
- `00_Project/Unit.Definition.Standard.md`
