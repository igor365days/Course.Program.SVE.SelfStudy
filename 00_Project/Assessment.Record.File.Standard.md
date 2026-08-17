# Стандарт файла записи оценивания

**Документ:** Assessment.Record.File.Standard
**Файлы:** `04_Progress/Assessments/LCP-XX.yaml`, `04_Progress/Assessments/CP-XX.yaml`
**Формат:** YAML
**Версия:** 1.1
**Статус:** Канонический стандарт проекта
**Применяется к:** Course.Program.SVE.SelfStudy

## 1. Назначение

Assessment Record хранит результаты попыток прохождения контрольной точки `LCP` или `CP`.

Один файл соответствует одной канонической контрольной точке и содержит историю её попыток. Это позволяет сохранять предыдущие результаты без создания нового файла для каждой повторной проверки.

## 2. Каноническая структура файла

```yaml
schema_version: "1.1"
control_id: "LCP-01"
type: "LCP"
section_id: "S01"
lesson_id: "L01"

attempts:
  - assessment_id: "ASM-LCP-01-01"
    attempt_number: 1
    started_at: "2026-08-17T08:00:00Z"
    completed_at: "2026-08-17T08:30:00Z"
    status: "COMPLETED"
    result: "PASSED"

    components:
      - component_id: "grammar"
        type: "Grammar"
        required: true
        execution: "COMPLETED"
        verification: "AI_VERIFIED"
        result: "PASSED"
        deficiency_ids: []
      - component_id: "pronunciation"
        type: "Pronunciation"
        required: true
        execution: "COMPLETED"
        verification: "USER_CONFIRMED"
        result: "ACCEPTED"
        deficiency_ids: []

    summary:
      strengths: []
      deficiencies: []

    remediation:
      required: false
      target_ids: []
      reason_ids: []

    recheck:
      required: false
      previous_assessment_id: null

    decision: "OPEN_NEXT_LESSON"
```

## 3. Идентификация

`control_id` — идентификатор канонической контрольной точки.

`type` принимает только:

```text
LCP
CP
```

`assessment_id` уникален для каждой попытки.

Рекомендуемый формат:

```text
ASM-LCP-01-01
ASM-LCP-01-02
ASM-CP-01-01
```

`attempt_number` начинается с `1` и увеличивается на единицу для каждой новой попытки данного контроля.

## 4. Статусы попытки

`status` принимает:

```text
NOT_STARTED
IN_PROGRESS
COMPLETED
```

`result` принимает:

```text
PASSED
FAILED
```

Разделение обязательно: `status: COMPLETED` означает завершение попытки, а `result: PASSED` — её успешность.

Незавершённая попытка может иметь `result: null`.

## 5. Компоненты контроля

Каждый обязательный компонент представлен отдельным элементом `components`.

Обязательные поля компонента:

```yaml
component_id: "grammar"
type: "Grammar"
required: true
execution: "COMPLETED"
verification: "AI_VERIFIED"
result: "PASSED"
deficiency_ids: []
```

### execution

Допустимые значения:

```text
NOT_STARTED
IN_PROGRESS
COMPLETED
```

### verification

Допустимые значения:

```text
AI_VERIFIED
USER_CONFIRMED
NOT_VERIFIED
```

### result

Допустимые значения:

```text
PASSED
FAILED
ACCEPTED
null
```

`USER_CONFIRMED` означает подтверждение выполнения пользователем и не является AI-проверкой.

## 6. Правило завершения контроля

Обязательный компонент считается приемлемо подтверждённым только если:

1. `execution: COMPLETED`;
2. `verification` не равен `NOT_VERIFIED`;
3. `result` имеет допустимое положительное значение (`PASSED` или `ACCEPTED`).

Если хотя бы один обязательный компонент не удовлетворяет этим условиям, итог попытки не может быть `PASSED`.

Комбинация `AI_VERIFIED` и `USER_CONFIRMED` разрешена, если она соответствует центральной Verification Policy и каноническому определению контрольной точки.

## 7. Связь с Verification Policy

Стандарт не определяет, какой тип компонента должен проверяться AI или пользователем. Это определяется `Assessment.Verification.Policy.md` и каноническим определением конкретной контрольной точки.

Таким образом:

```text
тип компонента
      ↓
Verification Policy
      ↓
способ проверки
      ↓
результат Assessment
```

## 8. Summary

```yaml
summary:
  strengths: []
  deficiencies: []
```

`strengths` и `deficiencies` — краткие элементы, пригодные для отчётности и коррекции. Они не являются стенограммой.

## 9. Remediation

```yaml
remediation:
  required: false
  target_ids: []
  reason_ids: []
```

При `required: true` результат `PASSED` не должен открывать следующий этап без выполнения предусмотренной коррекции, если это требуется каноническими правилами.

## 10. Recheck

```yaml
recheck:
  required: false
  previous_assessment_id: null
```

Для повторной проверки:

- создаётся новая попытка;
- предыдущая попытка сохраняется;
- `previous_assessment_id` содержит идентификатор непосредственно предшествующей попытки;
- новая попытка получает новый `assessment_id` и увеличенный `attempt_number`.

## 11. Decision

`decision` принимает только значения, соответствующие маршруту:

```text
OPEN_NEXT_UNIT
OPEN_LCP
OPEN_NEXT_LESSON
OPEN_NEXT_SECTION
REMEDIATION_REQUIRED
RECHECK_REQUIRED
BLOCKED
```

Конкретное значение определяется типом контроля и его положительным/отрицательным результатом.

## 12. Правила хранения

1. Один файл — одна каноническая LCP или CP.
2. Одна попытка — один элемент `attempts`.
3. Старые попытки не удаляются и не переписываются новым результатом.
4. Последняя завершённая попытка не должна противоречить событиям Progress.
5. `assessment_id` должен быть уникален в пределах Progress.
6. Подробности контроля хранятся здесь, а не в `Learning.Events.jsonl`.
7. Результат Assessment должен быть достаточен для восстановления решения о продвижении.

## 13. Согласованность с Learning State и Events

Для каждой завершённой попытки:

```text
Assessment Record
      ↕
Learning Event(s)
      ↓
Learning State
```

`Learning.State.yaml.last_assessment_id` должен ссылаться на последнюю релевантную попытку, а соответствующие события должны содержать тот же `assessment_id`.

Если обнаружено противоречие, продвижение блокируется до восстановления согласованности.
