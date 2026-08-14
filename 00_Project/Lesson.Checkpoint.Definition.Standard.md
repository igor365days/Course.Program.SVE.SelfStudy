# Lesson Checkpoint Definition Standard

**Document:** Lesson.Checkpoint.Definition.Standard  
**Status:** Canonical project standard  
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

A Lesson Checkpoint (LCP) is the canonical control point at the end of each of the 18 source lessons of the book.

Its purpose is to verify integrated learning of the material belonging to the complete source lesson after all its Unit have been studied.

An LCP is not merely a homework task and is not a record of learner progress. It is a canonical assessment object of the course.

## 2. Route position

For every source lesson:

`Unit → Unit → ... → final Unit → LCP → next source lesson`

The LCP is conducted only after the Unit of the corresponding lesson have been completed according to their verification criteria.

## 3. LCP identity

Each LCP has a stable identifier:

`LCP-01` … `LCP-18`

Each LCP is linked to exactly one source lesson and to the corresponding range of Unit.

## 4. Assessment purpose

The LCP should determine whether the learner can integrate and independently use the important material of the whole lesson. It should not simply repeat the exercises already performed in the Unit.

The LCP must cover the important competencies of the lesson using the best available verification method. Where reliable AI verification is impossible, the LCP must contain an explicit user-confirmed task.

Verification modes are:

- `AI_VERIFIED` — directly checked by AI;
- `USER_CONFIRMED` — the learner confirms completion of a required action that AI cannot reliably verify;
- `NOT_VERIFIED` — required evidence is missing.

User confirmation must never be represented as AI verification.

Depending on the lesson, an LCP may assess recognition, recall, accurate use of grammar and vocabulary, transformation or construction, independent production, reading/comprehension, communicative use, pronunciation practice, listening work, or combined use of several elements.

## 5. Completion rule

Successful completion of an LCP means that all mandatory assessment components have sufficient evidence and the integrated lesson result meets the defined success criteria.

Where a mandatory component requires user confirmation, `USER_CONFIRMED` is sufficient for that component when the task is specifically defined as self-confirmable. It does not claim that AI independently verified the skill.

If the result is insufficient, the system identifies relevant deficiencies, organizes targeted remediation and performs an LCP recheck.

Failure of an LCP does not automatically require repeating the entire lesson.

## 6. Relationship to Unit verification

Unit verification answers:

> Has the learner demonstrated the result of this particular Unit?

LCP answers:

> Can the learner integrate and independently use the important material of this entire source lesson?

Section CP answers:

> Has the learner integrated the material of the entire section and demonstrated readiness to proceed to the next section?

Thus the control hierarchy is:

`Unit verification → LCP → Section CP`

## 7. Canonical LCP definition

Each LCP definition should contain, where applicable:

1. LCP ID;
2. source lesson;
3. covered Unit;
4. assessment purpose;
5. required competencies;
6. assessment tasks;
7. verification mode for each required component;
8. success criteria;
9. remediation guidance;
10. recheck conditions;
11. canonical references.

## 8. Separation from learner state

The LCP definition belongs to GitHub and is canonical.

The actual result of a learner's LCP belongs to the practical learning-state system and will be designed separately.

The canonical LCP file must not contain individual dates, scores, errors or completion records.

## 9. Relationship to section checkpoints

There are **18 LCP** and **5 section CP**.

LCP controls progression through the source lessons. CP controls progression through the five larger course sections.

Both are mandatory control levels of the learning architecture.