# Course Structure Manifest

**Course:** `Course.Program.SVE.SelfStudy`
**Status:** Pre-launch structural baseline
**Purpose:** Каноническая карта всех 18 уроков, 56 Unit, 18 LCP и 5 CP.

Этот файл фиксирует только структуру и маршрут. Он не содержит персональный Progress и не заменяет подробные определения Unit/LCP/CP.

## Route

```text
Lesson → Unit → LCP → Lesson → ... → LCP → CP → next Section
```

Unit внутри урока проходят последовательно. LCP проводится после последней Unit урока. CP проводится после последнего урока раздела.

## Section 1 — Основы шведского языка

- Lessons: 1–4
- CP: `CP-1`
- Units: `1.1–1.5`, `2.1–2.4`, `3.1–3.4`, `4.1–4.4`
- LCP: `LCP-01`, `LCP-02`, `LCP-03`, `LCP-04`

## Section 2 — Повседневная коммуникация

- Lessons: 5–8
- CP: `CP-2`
- Units: `5.1–5.3`, `6.1–6.3`, `7.1–7.3`, `8.1–8.3`
- LCP: `LCP-05`, `LCP-06`, `LCP-07`, `LCP-08`

## Section 3 — Путешествия и ориентирование

- Lessons: 9–11
- CP: `CP-3`
- Units: `9.1–9.4`, `10.1–10.2`, `11.1–11.2`
- LCP: `LCP-09`, `LCP-10`, `LCP-11`

## Section 4 — Общественные и культурные ситуации

- Lessons: 12–15
- CP: `CP-4`
- Units: `12.1–12.2`, `13.1–13.2`, `14.1–14.2`, `15.1–15.3`
- LCP: `LCP-12`, `LCP-13`, `LCP-14`, `LCP-15`

## Section 5 — Швеция, культура и продвинутые грамматические темы

- Lessons: 16–18
- CP: `CP-5`
- Units: `16.1–16.4`, `17.1–17.2`, `18.1–18.4`
- LCP: `LCP-16`, `LCP-17`, `LCP-18`

## Completeness requirement

Для каждого из 56 Unit должен существовать канонический файл, соответствующий `Unit.Definition.Standard.md`.

Для каждого из 18 LCP должен существовать отдельный канонический файл, соответствующий `Checkpoint.Definition.Standard.md`, с обязательными assessment components.

Для каждого из 5 CP должен существовать отдельный канонический файл, соответствующий `Checkpoint.Definition.Standard.md`, с обязательными assessment components.

До заполнения содержанием структурный файл не считается доказательством готовности соответствующего Unit/LCP/CP.
