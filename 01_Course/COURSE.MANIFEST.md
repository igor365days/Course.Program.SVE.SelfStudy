# COURSE.MANIFEST

## Course

**Name:** Course.Program.SVE.SelfStudy  
**Status:** Pre-launch  
**Current version:** 1.0

## Purpose

This manifest is the navigation map of the canonical course repository. It identifies the authoritative course definition, source materials, Unit and Checkpoint definitions, and project-level specifications.

The manifest does not contain learner state. Learner state belongs to the ChatGPT Project.

## Source of Truth

The current canonical program is:

`01_Course/Course.Program.SVE.SelfStudy.md`

The frozen historical version is:

`01_Course/Course.Program.SVE.SelfStudy.v1.0.md`

While the project is pre-launch, the current canonical program may be redesigned. The historical v1.0 file is retained as an archive/reference and is not the active route.

## Canonical Route

The course contains **18 source lessons, 56 Unit and 5 Checkpoints**.

The 18 source lessons are grouped into five sequential sections:

| Section | Source lessons | Unit count | Checkpoint |
|---|---|---:|---|
| 1. Основы шведского языка | 1–4 | 17 | CP-1 |
| 2. Повседневная коммуникация | 5–8 | 12 | CP-2 |
| 3. Путешествия и ориентирование | 9–11 | 8 | CP-3 |
| 4. Общественные и культурные ситуации | 12–15 | 9 | CP-4 |
| 5. Швеция, культура и продвинутые грамматические темы | 16–18 | 10 | CP-5 |

**Route rule:** Unit inside a section are sequential. The final Unit of a section is followed by that section's CP. The next section is not opened until the CP is passed or its remediation protocol is completed.

## Repository Map

### `00_Project/`

Project architecture, methodology, learning objectives, AI regulations, Unit standard and Orchestrator specification.

### `01_Course/`

Canonical course definition and versioned programs.

### `02_Source/`

Source analysis and materials used to develop the course.

### `03_Lessons/`

Canonical definitions of all 56 Unit and 5 Checkpoints. Files are grouped by the five course sections.

### `04_Resources/`

Canonical supporting resources.

## Unit Identity

Unit identifiers retain the source-lesson numbering (`1.1` … `18.4`). Their section membership is defined by the current canonical program.

A Unit file describes what the learner must learn and how mastery is verified. It does not contain individual learner progress or chat history.

## Separation of Concerns

**GitHub:** canonical course and rules.  
**ChatGPT Project:** practical learning process and learner state.  
**Learning Session:** actual study interaction.  
**Course Orchestrator:** route control and transition validation.

## Pre-launch Rule

The project is still pre-launch. Structural changes may be made freely. Once real learning begins, canonical route changes require deliberate versioning.