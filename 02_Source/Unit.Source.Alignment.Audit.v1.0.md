# Unit Source Alignment Audit

**Version:** 2.4  
**Status:** `AVAILABLE_SOURCE_REBUILT`  
**Source:** `02_Source/Book.Course.Structure.v1.0.md`  
**Date:** 2026-08-17

## Purpose

This audit controls Unit-to-book alignment against the single canonical book map and direct inspection of the supplied PDF.

## Current result

For every Unit whose required body pages are present in the supplied PDF, the direct source re-audit is complete.

- **40 Units `PAGE_VERIFIED`** — Lessons 1–12 plus Unit 13.1.
- **1 Unit `PARTIAL_PAGE_VERIFIED`** — Unit 13.2.
- **15 Units `SOURCE_NOT_AVAILABLE`** — Lessons 14–18.
- **0 Units `REBUILD_REQUIRED`** within the currently available source.

Total: **56 Units**.

## Lesson inventory

| Lesson | Units | Status |
|---|---|---|
| 1 | 1.1–1.5 | `PAGE_VERIFIED` |
| 2 | 2.1–2.4 | `PAGE_VERIFIED` |
| 3 | 3.1–3.4 | `PAGE_VERIFIED` |
| 4 | 4.1–4.4 | `PAGE_VERIFIED` |
| 5 | 5.1–5.3 | `PAGE_VERIFIED` |
| 6 | 6.1–6.3 | `PAGE_VERIFIED` |
| 7 | 7.1–7.3 | `PAGE_VERIFIED` |
| 8 | 8.1–8.3 | `PAGE_VERIFIED` |
| 9 | 9.1–9.4 | `PAGE_VERIFIED` |
| 10 | 10.1–10.2 | `PAGE_VERIFIED` |
| 11 | 11.1–11.2 | `PAGE_VERIFIED` |
| 12 | 12.1–12.2 | `PAGE_VERIFIED` |
| 13 | 13.1 | `PAGE_VERIFIED`; 13.2 `PARTIAL_PAGE_VERIFIED` |
| 14 | 14.1–14.2 | `SOURCE_NOT_AVAILABLE` |
| 15 | 15.1–15.3 | `SOURCE_NOT_AVAILABLE` |
| 16 | 16.1–16.4 | `SOURCE_NOT_AVAILABLE` |
| 17 | 17.1–17.2 | `SOURCE_NOT_AVAILABLE` |
| 18 | 18.1–18.4 | `SOURCE_NOT_AVAILABLE` |

## Source availability boundary

The current PDF contains printed pages through **146**.

The book's table of contents states:

- Lesson 13: pp. 140–149;
- Lesson 14: pp. 150–160;
- Lesson 15: pp. 161–171;
- Lesson 16: pp. 172–182;
- Lesson 17: pp. 183–192;
- Lesson 18: pp. 193–202.

Therefore:

- Unit 13.1 is fully supported by available pages 140–141.
- Unit 13.2 is only partially supported because its comparison block continues into missing pages 147–149.
- Lessons 14–18 cannot receive body-level source verification until the missing pages are supplied.

## Verified Unit batches

### Lessons 1–3
13 Units directly checked.

### Lessons 4–6
10 Units directly checked, with legacy broad page ranges narrowed to actual source blocks.

### Lessons 7–9
10 Units directly checked, including separated grammar/vocabulary blocks.

### Lessons 10–12
6 Units directly checked, including transport/hotel, future/weather/orientation, bank/post and the associated grammar blocks.

### Lesson 13
`13.1` directly checked on pp. 140–141. `13.2` partially checked on pp. 141–146; missing pp. 147–149 remain explicit.

## Integrity rules

1. A project Unit file is not evidence of book content by itself.
2. A Lesson-level page range is not an exact Unit citation.
3. A Unit can be `PAGE_VERIFIED` only when every source page needed for its canonical content is present and directly inspected.
4. A Unit requiring a missing page cannot be promoted to `PAGE_VERIFIED`.
5. Source-derived content and project-added pedagogy must remain distinguishable.
6. No legacy source alignment statement overrides the canonical book map or this audit.

## Next stage

The Unit layer is now rebuilt for the currently available source. The next work package is the **LCP layer**, followed by the **CP layer**.

LCPs and CPs covering Lessons 14–18 must remain explicitly provisional until the missing source pages are recovered.
