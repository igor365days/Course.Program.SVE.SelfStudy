# Unit Definition Standard

**Document:** Unit.Definition.Standard  
**Status:** Canonical project standard  
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

A Unit file defines what the learner must study, the intended learning result, the learning sequence, practice and Unit-level verification.

It does not contain individual learner progress, chat history or actual assessment results.

## 2. Identity

Each Unit has a stable identifier such as `1.1`, `8.3` or `18.4`.

The first number identifies the **source lesson of the book**; the second identifies the Unit within that lesson.

Each Unit definition must identify:

- Unit ID;
- Unit title;
- source lesson;
- course section;
- position in the route;
- related LCP.

## 3. Standard Unit structure

Each Unit should contain, where applicable:

1. Identity
2. Learning Objective
3. Canonical Content
4. Learning Sequence
5. Practice Requirements
6. Verification Criteria
7. Typical Difficulties
8. Transition / prerequisites
9. Canonical References

The normal learning sequence is:

`Introduction → Explanation/analysis → Guided practice → Independent/communicative task → Verification`.

The sequence may adapt to the material without changing the Unit's canonical position or purpose.

## 4. Unit verification

Unit verification determines whether the learner has demonstrated the result required by that Unit.

It may test recognition, recall, accurate reproduction, transformation, independent production, communicative use or other skills appropriate to the Unit.

Completion of a Unit does not by itself replace the LCP of its source lesson.

## 5. Relationship to lesson checkpoint

Every Unit belongs to exactly one source lesson and therefore to exactly one **LCP (Lesson Checkpoint)**.

The LCP is conducted after the final Unit of that source lesson and tests integrated use of the important material of the whole lesson.

```text
Unit 1.1 ─┐
Unit 1.2  │
Unit 1.3  ├── LCP-01
Unit 1.4  │
Unit 1.5 ─┘
```

Unit verification answers: **Can the learner demonstrate the result of this Unit?**

LCP answers: **Can the learner integrate and independently use the important material of the whole source lesson?**

## 6. Relationship to section checkpoint

The LCP is below the section-level CP in the control hierarchy:

`Unit verification → LCP → CP`

CP integrates the material of all source lessons in the section and controls transition to the next section.

## 7. Separation of responsibilities

```text
Canonical Unit
    ↓
Learning Session
    ↓
Unit verification
    ↓
LCP of source lesson
    ↓
Section CP
    ↓
Learning Progress
```

The canonical definitions remain in GitHub. Actual learner results are handled separately.

## 8. Integrity rules

- Preserve Unit ID and route position.
- Do not silently merge, split or reorder Units.
- Do not move a Unit between source lessons merely for convenience.
- Do not remove the Unit's relation to its LCP.
- Do not place learner progress in the canonical Unit file.
- Changes to the canonical route are explicit course changes.