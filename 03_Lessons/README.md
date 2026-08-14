# Canonical Lesson Definitions

## Назначение

Каталог `03_Lessons` содержит канонические определения всех **56 Unit** и **5 контрольных точек** курса `Course.Program.SVE.SelfStudy`.

Это не журнал прохождения обучения и не история работы пользователя.

## Архитектура

Каждая Unit принадлежит ровно одному из пяти разделов. Unit внутри раздела идут строго последовательно. После последней Unit раздела следует его CP.

```text
03_Lessons/
├── 01_Foundation/
│   ├── 1.1.md ... 4.4.md
│   └── CP-1.md
├── 02_Everyday_Communication/
│   ├── 5.1.md ... 8.3.md
│   └── CP-2.md
├── 03_Travel_Orientation/
│   ├── 9.1.md ... 11.2.md
│   └── CP-3.md
├── 04_Social_Cultural/
│   ├── 12.1.md ... 15.3.md
│   └── CP-4.md
└── 05_Sweden_Culture_Advanced/
    ├── 16.1.md ... 18.4.md
    └── CP-5.md
```

## Разделы

| Раздел | Источниковые уроки | Unit | CP |
|---|---|---|---|
| 01 | 1–4 | 17 | CP-1 |
| 02 | 5–8 | 12 | CP-2 |
| 03 | 9–11 | 8 | CP-3 |
| 04 | 12–15 | 9 | CP-4 |
| 05 | 16–18 | 10 | CP-5 |

## Стандарт Unit

Каждый файл Unit должен соответствовать `00_Project/Unit.Definition.Standard.md` и определять:

- Identity;
- Section and route position;
- Source lesson;
- Learning Objective;
- Canonical Content;
- Learning Sequence;
- Practice Requirements;
- Verification Criteria;
- Typical Difficulties;
- Transition;
- Canonical References.

Файл описывает **план и требования к обучению**, а не фактический результат конкретного пользователя.

## Стандарт Checkpoint

CP является каноническим элементом маршрута и завершает соответствующий раздел.

Его определение содержит:

- Unit, которые он охватывает;
- цели интеграционной проверки;
- проверяемые знания и навыки;
- формат проверки;
- критерии прохождения;
- правила корректирующей работы;
- условия открытия следующего раздела.

## Правило маршрута

```text
Unit → Unit → ... → Unit → CP
                         │
                         ├─ FAIL → remediation → recheck
                         │
                         └─ PASS → next section
```

Unit нельзя пропускать ради удобства ChatGPT Project. Фактический прогресс, ошибки, даты и история чатов находятся вне `03_Lessons`.