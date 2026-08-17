# Course Structure Audit

**Status:** Single-source map established; project-to-source alignment requires re-audit  
**Version:** 2.0

## Canonical source rule

`02_Source/Book.Course.Structure.v1.0.md` is now the **single canonical source map of the book**.

It was rebuilt directly from the «Содержание» pages of the user-supplied PDF. It contains only material and structure stated by the book. It does not contain the project's Unit/LCP/CP decomposition.

Any previous derived book map is no longer an authority and must not be used to resolve discrepancies.

## What the PDF directly establishes

The PDF's contents pages establish the sequence and named content of Lessons 1–18, including their printed starting pages and the grammar/topic headings through Lesson 18. The same contents section also lists post-lesson material: answer keys, strong/irregular verb forms and dictionary.

The PDF metadata available to the project reports 150 PDF pages. The contents pages themselves reference printed book pages through 218. Therefore **table-of-contents structure and page-level source evidence are separate concepts** and must not be conflated.

## Current status

- Book structure from PDF contents: **VERIFIED**.
- Project route: **18 Lessons / 56 Unit / 18 LCP / 5 CP** — project architecture, not book structure.
- Unit-to-source alignment: **REQUIRES RE-AUDIT against the new single source map**.
- LCP source coverage: **REQUIRES RE-AUDIT** after Unit alignment.
- CP source coverage: **REQUIRES RE-AUDIT** after LCP alignment.

## Integrity rule

The book does not define our Unit/LCP/CP architecture. Those are project design decisions.

A project Unit may combine several headings from the book, but it must be traceable to the canonical source map. Project-added pedagogy must remain distinguishable from source-derived content.

`PAGE_VERIFIED` may be assigned only after the corresponding source pages have actually been inspected. Existence of a topic in the contents page is sufficient for **TOC_CONFIRMED**, not automatically for **PAGE_VERIFIED**.

## Next verification sequence

1. Re-audit all 56 Unit against this single source map.
2. Correct Unit boundaries/content where necessary.
3. Verify each Unit against the actual source pages available in the PDF.
4. Re-audit all 18 LCP against the verified Unit coverage.
5. Re-audit all 5 CP against the verified LCP/lesson coverage.
6. Only then run the final end-to-end Progress/State Machine test again.
