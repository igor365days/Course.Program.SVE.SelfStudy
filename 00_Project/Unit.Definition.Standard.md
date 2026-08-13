# Unit Definition Standard

**Document:** Unit.Definition.Standard
**Status:** Canonical project standard
**Applies to:** Course.Program.SVE.SelfStudy

## 1. Purpose

This document defines the standard structure of a canonical learning-unit definition stored in `03_Lessons`.

A Unit file describes **what the learner must study, the intended learning result, how the unit is to be conducted, and how mastery is verified**.

It does not record the personal history or actual result of a particular learner. That information belongs to the ChatGPT Project and its Learning Progress system.

## 2. Identity

Each Unit must have a stable canonical identifier corresponding to the course program, for example:

- `1.1`
- `1.2`
- `8.3`
- `18.4`

The identifier must not be changed merely for organizational convenience.

Each Unit file should use a predictable filename based on its identifier, for example:

`03_Lessons/01/1.1.md`

## 3. Standard Unit Structure

Each canonical Unit file should contain the following sections, where applicable.

### 3.1. Identity

- Unit ID
- Unit title
- Course version
- Source lesson/chapter
- Position in the course

### 3.2. Learning Objective

State clearly what the learner should be able to know, recognize, understand, produce, or use after completing the Unit.

The objective must describe an observable learning result rather than merely list topics.

### 3.3. Canonical Content

Describe the material that belongs to this Unit according to the canonical course program and source material.

Include, as applicable:

- vocabulary;
- grammar;
- pronunciation;
- structures and patterns;
- texts;
- communicative situations;
- cultural or contextual information.

Do not introduce unrelated material merely to make the Unit more comprehensive.

### 3.4. Learning Sequence

Describe the intended progression through the Unit. The normal model is:

1. Introduction
2. Explanation / analysis
3. Guided practice
4. Independent or communicative task
5. Verification

The sequence may be adapted to the specific Unit while preserving its learning objective and canonical position.

### 3.5. Practice Requirements

Specify the practice required to establish the intended skill or knowledge.

Practice should, where appropriate, progress from controlled work toward independent use.

### 3.6. Verification Criteria

Define what evidence is sufficient to regard the Unit as successfully completed from a learning perspective.

Verification should test actual ability rather than simple exposure to the material.

Depending on the Unit, verification may include:

- recognition;
- recall;
- accurate reproduction;
- transformation;
- independent production;
- communicative use;
- application without continuous reference to the source material.

### 3.7. Typical Difficulties

Record known or anticipated difficulties that are useful for conducting the Unit.

This section describes expected learning risks, not the personal errors of a particular learner.

Personal errors belong in Learning Progress.

### 3.8. Transition

State the conditions or knowledge that connect this Unit to the following part of the course.

Where relevant, identify prerequisites from earlier Units.

### 3.9. Canonical References

List the authoritative sources used to define the Unit, such as:

- the canonical course program;
- the corresponding source lesson;
- approved source materials;
- approved course resources.

## 4. Separation of Responsibilities

The Unit definition and the learner's actual progress must remain separate.

```text
Canonical Unit
    ↓
What should be learned
    ↓
ChatGPT working session
    ↓
What the learner actually did
    ↓
Learning Progress
    ↓
What the learner actually mastered
```

A Unit file must not become a progress journal.

A working chat must not become the canonical definition of the Unit.

Learning Progress must not redefine the canonical Unit.

## 5. Integrity Rules

- Preserve the canonical Unit identifier.
- Preserve the Unit's position in the course.
- Do not silently merge Units.
- Do not silently split Units.
- Do not silently reorder Units.
- Do not add material that changes the intended scope of the Unit.
- Improvements to the course itself must be treated as explicit changes to the canonical course.

## 6. Relationship to ChatGPT Project

The ChatGPT Project uses the Unit definition as the authoritative plan for a particular learning session.

The Project may adapt the delivery method, amount of practice, explanations, pacing, and repetition to the learner, provided that the canonical learning objective and required learning result are preserved.

The Project must use the Unit definition together with the learner's current Learning Progress to determine the next appropriate action.
