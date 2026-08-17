# Unit Source Alignment Audit

**Version:** 2.0  
**Status:** `REBUILD_REQUIRED`  
**Source:** `02_Source/Book.Course.Structure.v1.0.md`  
**Date:** 2026-08-17

## Purpose

This audit is the controlled reset of Unit-to-book alignment after eliminating the previous dual-map situation.

The 56 Unit files are project design artifacts. They are **not** evidence of what the book contains. Their source alignment must be established against the single canonical book map and, where possible, direct inspection of the supplied PDF pages.

## Status vocabulary

- `REBUILD_REQUIRED` — the Unit must be rechecked against the canonical source map before being treated as source-aligned.
- `PAGE_VERIFIED` — direct inspection of the corresponding source pages in the current PDF supports the Unit's canonical content.
- `PARTIAL_PAGE_VERIFIED` — only part of the required source range is available in the current PDF.
- `SOURCE_NOT_AVAILABLE` — the required book pages are outside the current PDF.
- `PROJECT_ONLY` — content is project-added and must not be presented as book-derived.

## Current reset

**All 56 Units are reset to `REBUILD_REQUIRED`.**

No Unit is currently considered `PAGE_VERIFIED` merely because an earlier audit said so.

## Unit inventory

| Lesson | Units | Current status |
|---|---|---|
| 1 | 1.1–1.5 | `REBUILD_REQUIRED` |
| 2 | 2.1–2.4 | `REBUILD_REQUIRED` |
| 3 | 3.1–3.4 | `REBUILD_REQUIRED` |
| 4 | 4.1–4.4 | `REBUILD_REQUIRED` |
| 5 | 5.1–5.3 | `REBUILD_REQUIRED` |
| 6 | 6.1–6.3 | `REBUILD_REQUIRED` |
| 7 | 7.1–7.3 | `REBUILD_REQUIRED` |
| 8 | 8.1–8.3 | `REBUILD_REQUIRED` |
| 9 | 9.1–9.4 | `REBUILD_REQUIRED` |
| 10 | 10.1–10.2 | `REBUILD_REQUIRED` |
| 11 | 11.1–11.2 | `REBUILD_REQUIRED` |
| 12 | 12.1–12.2 | `REBUILD_REQUIRED` |
| 13 | 13.1–13.2 | `REBUILD_REQUIRED` |
| 14 | 14.1–14.2 | `REBUILD_REQUIRED` |
| 15 | 15.1–15.3 | `REBUILD_REQUIRED` |
| 16 | 16.1–16.4 | `REBUILD_REQUIRED` |
| 17 | 17.1–17.2 | `REBUILD_REQUIRED` |
| 18 | 18.1–18.4 | `REBUILD_REQUIRED` |

**Total: 56 Units.**

## Source availability boundary

The current PDF contains printed pages through **146**.

Therefore:

- Units assigned to Lessons 1–12 can be fully re-audited against the current PDF.
- Units assigned to Lesson 13 can be re-audited only where their evidence falls within pages 140–146.
- Units assigned to Lessons 14–18 cannot receive body-level source verification until the missing pages are supplied.

## Rebuild method

For every Unit the audit must establish:

1. Unit ID.
2. Source Lesson.
3. Exact item(s) from `Book.Course.Structure.v1.0.md` represented by the Unit.
4. Printed page range.
5. Whether those pages are physically present in the current PDF.
6. Direct source evidence where available.
7. What is source-derived versus project-added pedagogy.
8. Verification status.
9. Transition to the next Unit.

## Non-negotiable rule

A broad Lesson page range is not an adequate Unit citation. For example, assigning `6–12` to several Units does not prove that each Unit is supported by every page in that range.

The final matrix must point each Unit to the smallest useful source range that supports its content.

## Legacy material

Existing Unit files may contain useful project work, but any legacy `Source pages`, `Source Alignment`, or `PAGE_VERIFIED` statement is provisional until this audit is completed.

No legacy assertion may override the canonical PDF map.

## Completion criterion

The audit is complete only when all 56 Units have one of these defensible terminal states:

- `PAGE_VERIFIED`;
- `PARTIAL_PAGE_VERIFIED` with an explicit missing-page boundary;
- `SOURCE_NOT_AVAILABLE`;
- `PROJECT_ONLY`.

`REBUILD_REQUIRED` must be zero for the audit to be considered complete.
