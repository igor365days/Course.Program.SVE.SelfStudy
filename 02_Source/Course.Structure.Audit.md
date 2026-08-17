# Course Structure Audit

**Status:** Rebuilt from the supplied PDF source map  
**Version:** 2.0  
**Date:** 2026-08-17

## Result

The project route currently contains **18 Lessons, 56 Unit files, 18 LCP and 5 CP**. This is the **project architecture**, not a claim that the book itself uses these Unit/LCP/CP boundaries.

The single canonical book map is:

`02_Source/Book.Course.Structure.v1.0.md`

All source-derived project work must use that file as the first structural reference.

## Source coverage

The supplied PDF `Шведский язык, самоучитель_copy(1).pdf` contains **150 PDF pages**. The last available scanned page shows printed book page **146**.

The PDF's «Содержание» is available and lists the complete route of the book through Lesson 18 and the reference sections after it. Therefore the project can establish the complete **table-of-contents structure**, but cannot claim complete body-page verification.

### Evidence status by lesson

| Lesson | Printed pages in book | Current PDF evidence | Status |
|---|---:|---:|---|
| 1 | 6–15 | available | `SOURCE_AVAILABLE` |
| 2 | 16–26 | available | `SOURCE_AVAILABLE` |
| 3 | 27–38 | available | `SOURCE_AVAILABLE` |
| 4 | 39–50 | available | `SOURCE_AVAILABLE` |
| 5 | 51–62 | available | `SOURCE_AVAILABLE` |
| 6 | 63–73 | available | `SOURCE_AVAILABLE` |
| 7 | 74–85 | available | `SOURCE_AVAILABLE` |
| 8 | 86–96 | available | `SOURCE_AVAILABLE` |
| 9 | 97–107 | available | `SOURCE_AVAILABLE` |
| 10 | 108–117 | available | `SOURCE_AVAILABLE` |
| 11 | 118–128 | available | `SOURCE_AVAILABLE` |
| 12 | 129–139 | available | `SOURCE_AVAILABLE` |
| 13 | 140–149 | only 140–146 | `PARTIAL_SOURCE` |
| 14 | 150–160 | unavailable | `SOURCE_NOT_AVAILABLE` |
| 15 | 161–171 | unavailable | `SOURCE_NOT_AVAILABLE` |
| 16 | 172–182 | unavailable | `SOURCE_NOT_AVAILABLE` |
| 17 | 183–192 | unavailable | `SOURCE_NOT_AVAILABLE` |
| 18 | 193–202 | unavailable | `SOURCE_NOT_AVAILABLE` |

## Important correction

The previous audit incorrectly marked all 56 Units as `PAGE_VERIFIED`. That assertion is withdrawn.

A Unit may be marked `PAGE_VERIFIED` only after direct inspection of the corresponding source pages in the supplied PDF. A project Unit file or a page range copied from an earlier audit is not evidence of page verification.

## Rebuild state

The 56 Unit files remain as **project design artifacts** so that the route and file structure are preserved. Their source alignment is being rebuilt from the canonical book map.

Current source-alignment state:

- Lessons 1–12: eligible for direct page-by-page re-audit.
- Lesson 13: eligible only for pages 140–146; pages 147–149 require source recovery.
- Lessons 14–18: source recovery required before body-level verification.
- LCP-01…LCP-18: source-dependent claims require re-audit after Unit alignment.
- CP-1…CP-5: source-dependent claims require re-audit after LCP alignment.

## Integrity rule

The route is:

`PDF → canonical book map → Lesson → Unit → LCP → next Lesson → … → CP`

But the arrows do not mean that the book defines Unit/LCP/CP boundaries. They mean that every project element must be traceable to the source lesson and, where applicable, to one or more items in the canonical book map.

No source-derived claim may be silently filled from general linguistic knowledge.

## Next automatic work package

1. Re-audit the 56 Unit definitions against the canonical book map.
2. Assign exact source topics/pages to every Unit.
3. Remove or correct legacy source-page ranges.
4. Re-audit all 18 LCPs against their Units.
5. Re-audit all 5 CPs against the resulting LCP chain.
6. Run a final structural integrity check: 18 Lessons → 56 Units → 18 LCP → 5 CP.
7. Record unresolved source gaps separately so they cannot contaminate verified material.
