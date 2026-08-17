# Unit Source Alignment Audit

**Basis:** `02_Source/Book.Course.Structure.v1.0.md` — единственная каноническая карта книги, построенная непосредственно из присланного PDF.  
**Scope:** 56 проектных Unit.

## Important distinction

`Book.Course.Structure.v1.0.md` описывает **книгу**.  
Этот файл описывает **проектные Unit** и их соответствие книге.

Unit/LCP/CP не являются структурой автора книги. Они являются проектной декомпозицией и должны быть трассируемы к темам канонической карты.

## Status vocabulary

- `TOC_CONFIRMED` — содержание Unit подтверждается соответствующим пунктом/пунктами раздела «Содержание» PDF.
- `PAGE_VERIFIED` — соответствующие страницы PDF непосредственно проверены и подтверждают содержание Unit.
- `REQUIRES_REAUDIT` — прежняя отметка больше не считается доказательством после замены карты книги и должна быть проверена заново.

## Current status

**Все прежние результаты alignment/page verification считаются подлежащими повторной проверке.** Причина — прежняя карта смешивала содержание книги с проектной Unit-декомпозицией.

Новая последовательность проверки:

1. сопоставить Unit с пунктами единственной PDF-derived карты;
2. проверить фактические страницы PDF;
3. зафиксировать трассировку `Lesson → source topic → Unit`;
4. только после этого присвоить `PAGE_VERIFIED`.

## Unit inventory

| Lesson | Unit count | Status |
|---|---:|---|
| 1 | 5 | REQUIRES_REAUDIT |
| 2 | 4 | REQUIRES_REAUDIT |
| 3 | 4 | REQUIRES_REAUDIT |
| 4 | 4 | REQUIRES_REAUDIT |
| 5 | 3 | REQUIRES_REAUDIT |
| 6 | 3 | REQUIRES_REAUDIT |
| 7 | 3 | REQUIRES_REAUDIT |
| 8 | 3 | REQUIRES_REAUDIT |
| 9 | 4 | REQUIRES_REAUDIT |
| 10 | 2 | REQUIRES_REAUDIT |
| 11 | 2 | REQUIRES_REAUDIT |
| 12 | 2 | REQUIRES_REAUDIT |
| 13 | 2 | REQUIRES_REAUDIT |
| 14 | 2 | REQUIRES_REAUDIT |
| 15 | 3 | REQUIRES_REAUDIT |
| 16 | 4 | REQUIRES_REAUDIT |
| 17 | 2 | REQUIRES_REAUDIT |
| 18 | 4 | REQUIRES_REAUDIT |
| **Total** | **56** | **REQUIRES_REAUDIT** |

## Integrity rule

Нельзя использовать старую проектную декомпозицию как доказательство содержания книги. Если Unit не совпадает с формулировкой карты, это не означает автоматически ошибку книги или Unit: сначала проводится трассировка к одному или нескольким исходным пунктам.

Проектная педагогика может расширять способ обучения, практики и проверки, но не должна выдаваться за материал источника.

## Next step

Начать повторную верификацию с Lesson 1 и последовательно пройти все 56 Unit по новой единственной карте. После завершения Unit alignment повторно проверить LCP и CP.
