# COURSE.MANIFEST

## Course

**Name:** Course.Program.SVE.SelfStudy  
**Status:** Pre-launch  
**Current version:** 1.1 structural baseline

## Canonical route

The course contains **18 source lessons, 56 Unit, 18 lesson checkpoints (LCP) and 5 section checkpoints (CP)**. Unit counts are intentionally variable between lessons.

Each Unit belongs to exactly one source lesson and exactly one course section. Units inside a lesson are sequential. After the final Unit of each source lesson, its LCP is conducted. After the final lesson of a section, its CP is conducted. A passed CP opens the next section.

| Section | Source lessons | Units | Lesson checkpoints | Section checkpoint |
|---|---|---:|---|---|
| 1. Основы шведского языка | 1–4 | 17 | LCP-01–04 | CP-1 |
| 2. Повседневная коммуникация | 5–8 | 12 | LCP-05–08 | CP-2 |
| 3. Путешествия и ориентирование | 9–11 | 8 | LCP-09–11 | CP-3 |
| 4. Общественные и культурные ситуации | 12–15 | 9 | LCP-12–15 | CP-4 |
| 5. Швеция, культура и продвинутые грамматические темы | 16–18 | 10 | LCP-16–18 | CP-5 |

## Source basis

The source structure is documented in `02_Source/Book.Course.Structure.v1.0.md`. The book contains 18 lessons; Unit boundaries are a project-level decomposition of the book's thematic and grammatical blocks, not source-native units.

## Route rule

```text
Unit → Unit → ... → LCP
                 ↓
          final lesson of section
                 ↓
                CP
                 ↓
           next section
```

LCP verifies integrated use of the material of its source lesson. CP integrates the material of the whole section and controls transition to the next section. Failure at either level triggers targeted remediation and recheck.

## Repository map

- `00_Project/` — project architecture and rules.
- `01_Course/` — canonical course definition.
- `02_Source/` — source analysis and source-derived structure.
- `03_Lessons/` — canonical Unit/LCP/CP definitions.
- `04_Resources/` — supporting resources.

## Pre-launch rule

The project is still pre-launch. Structural changes may be made deliberately and versioned.
