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

Examples:

- Lesson 1 → Unit 1.1–1.5 → LCP-01
- Lesson 2 → Unit 2.1–2.4 → LCP-02
- Lesson 18 → Unit 18.1–18.4 → LCP-18

## 4. Assessment purpose

The LCP should determine whether the learner can integrate and independently use the important material of the whole lesson.

It should not simply repeat the exercises already performed in the Unit.

Depending on the lesson, an LCP may assess:

- recognition and understanding;
- recall;
- accurate use of grammar and vocabulary;
- transformation or construction;
- independent production;
- reading or comprehension;
- communicative use;
- combined use of several elements from the lesson.

The exact form depends on the content of the source lesson.

## 5. Completion rule

Successful completion of an LCP means that the learner has demonstrated the required integrated result for the lesson.

If the result is insufficient, the system identifies the relevant deficiencies, organizes targeted remediation and performs an LCP recheck.

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
7. success criteria;
8. remediation guidance;
9. recheck conditions;
10. canonical references.

## 8. Separation from learner state

The LCP definition belongs to GitHub and is canonical.

The actual result of a learner's LCP belongs to the practical learning-state system and will be designed separately.

The canonical LCP file must not contain individual dates, scores, errors or completion records.

## 9. Relationship to section checkpoints

There are **18 LCP** and **5 section CP**.

LCP controls progression through the source lessons. CP controls progression through the five larger course sections.

Both are mandatory control levels of the learning architecture.