# Course Structure Manifest

**Course:** `Course.Program.SVE.SelfStudy`  
**Status:** Structural baseline v1.2 — source rebuild in progress  
**Purpose:** canonical project route derived from, but distinct from, the supplied book source.

## Canonical source

The **only canonical map of the book** is:

`02_Source/Book.Course.Structure.v1.0.md`

It is built directly from the «Содержание» of the supplied PDF.

The current PDF contains 150 PDF pages and reaches printed page 146. Therefore its table of contents establishes the complete 18-lesson book route, while body-level source verification is currently complete only through printed page 146.

## Route

```text
PDF → canonical book map → Lesson → Unit → LCP → Lesson → … → LCP → CP → next Section
```

The Unit/LCP/CP layers are **project architecture**, not claims about the author's internal organization.

## Sections

### Section 1
- Lessons: 1–4
- Units: 17 (`1.1–1.5`, `2.1–2.4`, `3.1–3.4`, `4.1–4.4`)
- LCP: `LCP-01` … `LCP-04`
- CP: `CP-1`

### Section 2
- Lessons: 5–8
- Units: 12 (`5.1–5.3`, `6.1–6.3`, `7.1–7.3`, `8.1–8.3`)
- LCP: `LCP-05` … `LCP-08`
- CP: `CP-2`

### Section 3
- Lessons: 9–11
- Units: 8 (`9.1–9.4`, `10.1–10.2`, `11.1–11.2`)
- LCP: `LCP-09` … `LCP-11`
- CP: `CP-3`

### Section 4
- Lessons: 12–15
- Units: 9 (`12.1–12.2`, `13.1–13.2`, `14.1–14.2`, `15.1–15.3`)
- LCP: `LCP-12` … `LCP-15`
- CP: `CP-4`

### Section 5
- Lessons: 16–18
- Units: 10 (`16.1–16.4`, `17.1–17.2`, `18.1–18.4`)
- LCP: `LCP-16` … `LCP-18`
- CP: `CP-5`

## Lesson → Unit map

| Lesson | Units | LCP | Book printed pages |
|---|---|---|---:|
| 1 | `1.1–1.5` | `LCP-01` | 6–15 |
| 2 | `2.1–2.4` | `LCP-02` | 16–26 |
| 3 | `3.1–3.4` | `LCP-03` | 27–38 |
| 4 | `4.1–4.4` | `LCP-04` | 39–50 |
| 5 | `5.1–5.3` | `LCP-05` | 51–62 |
| 6 | `6.1–6.3` | `LCP-06` | 63–73 |
| 7 | `7.1–7.3` | `LCP-07` | 74–85 |
| 8 | `8.1–8.3` | `LCP-08` | 86–96 |
| 9 | `9.1–9.4` | `LCP-09` | 97–107 |
| 10 | `10.1–10.2` | `LCP-10` | 108–117 |
| 11 | `11.1–11.2` | `LCP-11` | 118–128 |
| 12 | `12.1–12.2` | `LCP-12` | 129–139 |
| 13 | `13.1–13.2` | `LCP-13` | 140–149* |
| 14 | `14.1–14.2` | `LCP-14` | 150–160* |
| 15 | `15.1–15.3` | `LCP-15` | 161–171* |
| 16 | `16.1–16.4` | `LCP-16` | 172–182* |
| 17 | `17.1–17.2` | `LCP-17` | 183–192* |
| 18 | `18.1–18.4` | `LCP-18` | 193–202* |

`*` The page range is stated by the book's table of contents; the corresponding body pages are not present in the current PDF. Lesson 13 is available only through printed page 146.

## Integrity rules

- Every Unit belongs to exactly one source Lesson and one LCP.
- Every Lesson ends with its LCP.
- Every Section ends with its CP.
- Unit boundaries are project design and must be explicitly justified against the canonical book map.
- Detailed Unit files are not source authority; their source claims require the traceability audit.
- No legacy page range may be treated as verified until re-audited.
- Source gaps must remain explicit.

## Active rebuild documents

- `02_Source/Book.Course.Structure.v1.0.md` — canonical book map.
- `02_Source/Course.Structure.Audit.md` — source coverage audit.
- `02_Source/Unit.Source.Alignment.Audit.v1.0.md` — Unit alignment reset and rules.
- `02_Source/Unit.Source.Traceability.Matrix.v2.0.md` — working Unit traceability matrix.
