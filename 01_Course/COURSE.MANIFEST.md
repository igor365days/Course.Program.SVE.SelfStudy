# COURSE.MANIFEST

## Course

**Name:** Course.Program.SVE.SelfStudy  
**Status:** Pre-launch  
**Current version:** 1.0

## Canonical route

The course contains **18 source lessons, 56 Unit, 18 lesson checkpoints (LCP) and 5 section checkpoints (CP)**.

Each Unit belongs to exactly one source lesson and exactly one course section. Units inside a lesson are sequential. After the final Unit of each source lesson, its **LCP** is conducted. After the final lesson of a section, its **CP** is conducted. A passed CP opens the next section.

| Section | Source lessons | Units | Lesson checkpoints | Section checkpoint |
|---|---|---:|---:|---|
| 1. Основы шведского языка | 1–4 | 17 | LCP-01–04 | CP-1 |
| 2. Повседневная коммуникация | 5–8 | 12 | LCP-05–08 | CP-2 |
| 3. Путешествия и ориентирование | 9–11 | 8 | LCP-09–11 | CP-3 |
| 4. Общественные и культурные ситуации | 12–15 | 9 | LCP-12–15 | CP-4 |
| 5. Швеция, культура и продвинутые грамматические темы | 16–18 | 10 | LCP-16–18 | CP-5 |

## Route rule

```text
Unit → Unit → ... → LCP → next lesson
                       ↓
             final lesson of section
                       ↓
                      CP
                       ↓
                next section
```

LCP is an integral control point for the corresponding source lesson. It verifies integrated use of the material of that lesson and is not a learner-progress log.

CP is an integral control point for the whole section and is the mandatory transition gate between sections.

Failure or insufficient performance at either level triggers targeted remediation and recheck. It does not automatically require repeating material that has already been demonstrated as mastered.

## Source-lesson mapping

Unit identifiers retain the book's lesson numbering (`1.1` … `18.4`). The number before the dot identifies the source lesson and the number after the dot identifies the Unit within that lesson.

## Repository map

### `00_Project/`
Project architecture, methodology, objectives, regulations, Unit standard, lesson-checkpoint standard and Orchestrator specification.

### `01_Course/`
Canonical course definition and versioned programs.

### `02_Source/`
Source analysis and materials used to develop the course.

### `03_Lessons/`
Canonical definitions of all 56 Unit, 18 LCP and 5 CP, grouped by the five course sections.

### `04_Resources/`
Canonical supporting resources.

## Separation of concerns

**GitHub:** canonical course and rules.  
**ChatGPT Project:** practical learning process and learner state.  
**Learning Session:** actual study interaction.  
**Course Orchestrator:** route control and transition validation.

The mechanism and format for storing learner progress are intentionally **not fixed by this structural definition** and will be designed separately.

## Pre-launch rule

The project is still pre-launch. Structural changes may be made freely. Once real learning begins, canonical route changes require deliberate versioning.