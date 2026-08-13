# COURSE.MANIFEST

## Course

**Name:** Course.Program.SVE.SelfStudy  
**Status:** Pre-launch  
**Current version:** 1.0

## Purpose

This manifest is the navigation map of the canonical course repository.

It identifies the authoritative course definition, the source materials, the canonical definitions of learning units and checkpoints, and the resources used by the course.

The manifest does not contain the learning state of a particular learner. Learning state belongs to the ChatGPT Project.

## Source of Truth

The canonical course program is:

`01_Course/Course.Program.SVE.SelfStudy.md`

The frozen version 1.0 of the program is:

`01_Course/Course.Program.SVE.SelfStudy.v1.0.md`

## Canonical Course Structure

The course is based on:

- **18 source lessons** from the selected textbook;
- **56 canonical learning units (Unit)**;
- **5 checkpoints (CP)**.

The existing Unit boundaries are part of the canonical course design. They must not be merged, split, or reordered merely for the convenience of the AI assistant or the ChatGPT Project.

## Repository Map

### `00_Project/`

Project-level specifications, methodology, learning objectives, AI regulations, and course-design documents.

These documents define how the course is designed and how the AI learning system is expected to operate. They are not learner progress data.

### `01_Course/`

Canonical course definition and versioned course programs.

Primary files:

- `Course.Program.SVE.SelfStudy.md` — current canonical program;
- `Course.Program.SVE.SelfStudy.v1.0.md` — frozen version 1.0;
- `COURSE.MANIFEST.md` — this navigation map.

### `02_Source/`

Source analysis and source materials from which the canonical course was developed.

### `03_Lessons/`

Canonical definitions of individual learning units and checkpoints.

Each Unit has its own canonical definition. These files describe what the Unit is intended to accomplish and how it is to be conducted. They do not contain the learner's actual progress or chat history.

### `04_Resources/`

Canonical supporting resources used by the course.

## Unit Identification

Each learning unit retains its canonical identifier from the course program:

`1.1`, `1.2`, `1.3`, ... `18.4`

The identifier is stable within the course version and is used to connect:

- the canonical program;
- the Unit definition in `03_Lessons/`;
- the corresponding ChatGPT Project working chat;
- the learner's progress record.

## Checkpoints

The five checkpoints are canonical course elements and are maintained separately from Units.

Their definitions belong in `03_Lessons/` alongside the Unit definitions, using the identifiers `CP-1` through `CP-5`.

## Separation of Concerns

The repository defines the course.

The ChatGPT Project defines the practical state of a particular learner's progression through that course.

Therefore the following do **not** belong in the canonical repository:

- current learner status;
- completion dates;
- individual errors;
- personal learning difficulties;
- results of individual exercises;
- chat history;
- personal repetition plans.

Those belong to the learning state maintained by the ChatGPT Project.

## Pre-launch Rule

The course is currently in pre-launch state. Structural and content changes may be made freely while the canonical architecture is being finalized.

Once real learning begins, changes to the canonical course structure should be versioned and handled deliberately.
