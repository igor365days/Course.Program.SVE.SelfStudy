# Unit Source Alignment Audit

**Version:** 2.2  
**Status:** `PARTIALLY_REBUILT`  
**Source:** `02_Source/Book.Course.Structure.v1.0.md`  
**Date:** 2026-08-17

## Purpose

This audit controls the rebuild of Unit-to-book alignment after eliminating the previous dual-map situation.

The 56 Unit files are project design artifacts. They are **not** evidence of what the book contains. Source alignment is established against the single canonical book map and, where possible, direct inspection of the supplied PDF pages.

## Current result

Two direct re-audit batches are complete:

- **23 Units `PAGE_VERIFIED`** — Lessons 1–6.
- **2 Units `PARTIAL_PAGE_VERIFIED`** — Lesson 13, because only printed pages 140–146 are present.
- **16 Units `REBUILD_REQUIRED`** — Lessons 7–12.
- **15 Units `SOURCE_NOT_AVAILABLE`** — Lessons 14–18.

Total: **56 Units**.

## Verified batches

### Lessons 1–3

All 13 Units were directly checked against the supplied PDF and assigned exact source-page ranges in the traceability matrix.

### Lessons 4–6

All 10 Units were directly checked against the supplied PDF. Several legacy broad page ranges were narrowed to the actual source blocks; Unit 4.4 correctly uses a non-contiguous page range because the adjective block and 4th/5th declension block are separated in the book.

## Status vocabulary

- `REBUILD_REQUIRED` — the Unit must be rechecked against the canonical source map.
- `PAGE_VERIFIED` — direct inspection of the corresponding source pages in the current PDF supports the Unit's canonical content.
- `PARTIAL_PAGE_VERIFIED` — only part of the required source range is available.
- `SOURCE_NOT_AVAILABLE` — the required book pages are outside the current PDF.
- `PROJECT_ONLY` — content is project-added and must not be presented as book-derived.

## Unit inventory

| Lesson | Units | Current status |
|---|---|---|
| 1 | 1.1–1.5 | `PAGE_VERIFIED` |
| 2 | 2.1–2.4 | `PAGE_VERIFIED` |
| 3 | 3.1–3.4 | `PAGE_VERIFIED` |
| 4 | 4.1–4.4 | `PAGE_VERIFIED` |
| 5 | 5.1–5.3 | `PAGE_VERIFIED` |
| 6 | 6.1–6.3 | `PAGE_VERIFIED` |
| 7 | 7.1–7.3 | `REBUILD_REQUIRED` |
| 8 | 8.1–8.3 | `REBUILD_REQUIRED` |
| 9 | 9.1–9.4 | `REBUILD_REQUIRED` |
| 10 | 10.1–10.2 | `REBUILD_REQUIRED` |
| 11 | 11.1–11.2 | `REBUILD_REQUIRED` |
| 12 | 12.1–12.2 | `REBUILD_REQUIRED` |
| 13 | 13.1–13.2 | `PARTIAL_PAGE_VERIFIED` |
| 14 | 14.1–14.2 | `SOURCE_NOT_AVAILABLE` |
| 15 | 15.1–15.3 | `SOURCE_NOT_AVAILABLE` |
| 16 | 16.1–16.4 | `SOURCE_NOT_AVAILABLE` |
| 17 | 17.1–17.2 | `SOURCE_NOT_AVAILABLE` |
| 18 | 18.1–18.4 | `SOURCE_NOT_AVAILABLE` |

## Source availability boundary

The current PDF contains printed pages through **146**.

Therefore:

- Lessons 1–12 can be fully re-audited against the current PDF.
- Lesson 13 can be re-audited only where evidence falls within pages 140–146.
- Lessons 14–18 cannot receive body-level source verification until the missing pages are supplied.

## Rebuild method

For every Unit the audit must establish:

1. Unit ID.
2. Source Lesson.
3. Exact item(s) from `Book.Course.Structure.v1.0.md` represented by the Unit.
4. Exact printed page range.
5. PDF page number(s), where useful.
6. Direct source evidence.
7. Source-derived content versus project-added pedagogy.
8. Verification status.
9. Transition to the next Unit.

## Non-negotiable rule

A broad Lesson page range is not an adequate Unit citation. The final matrix must point each Unit to the smallest useful source range that supports its content.

## Legacy material

Existing Unit files may contain useful project work, but any legacy source claim is provisional until its Unit appears in the traceability matrix with a defensible status.

No legacy assertion may override the canonical PDF map.

## Completion criterion

The audit is complete only when `REBUILD_REQUIRED` is zero and every Unit has a defensible terminal status.
