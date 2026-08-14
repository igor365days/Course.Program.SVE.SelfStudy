# Стандарт файла записи оценивания

**Файлы:** `04_Progress/Assessments/LCP-XX.yaml`, `04_Progress/Assessments/CP-XX.yaml`  
**Формат:** YAML  
**Статус:** Канонический стандарт

## Назначение

Определяет компактную запись конкретного результата оценивания LCP или CP для обучающегося.

## Каноническая структура

```yaml
assessment_id: LCP-01
type: LCP
section: 1
lesson: 1
date: YYYY-MM-DDTHH:MM:SS
status: PASSED

components:
  grammar:
    execution: COMPLETED
    verification: AI_VERIFIED
    result: PASSED
  pronunciation:
    execution: COMPLETED
    verification: USER_CONFIRMED
    result: ACCEPTED

summary:
  strengths: []
  deficiencies: []

remediation:
  required: false
  target: null
  reason: null

recheck:
  required: false
  previous_assessment: null

decision: OPEN_NEXT_LESSON
```

## Правила

1. Одна текущая Assessment Record соответствует одной попытке прохождения контрольной точки.
2. Повторная проверка создаёт новую запись, связанную с предыдущим оцениванием; предыдущий результат не стирается.
3. `execution`, `verification` и `result` являются отдельными понятиями.
4. `USER_CONFIRMED` никогда нельзя представлять как AI-проверку.
5. Каждый обязательный компонент должен иметь приемлемые доказательства до признания контроля завершённым.
6. `NOT_VERIFIED` для обязательного компонента блокирует завершение.
7. Недостатки должны быть краткими и пригодными для практического действия.
8. Записи содержат результаты, а не полные стенограммы сессии оценивания.
9. Запись должна оставаться совместимой с канонической политикой проверки и правилами Orchestrator.

## Статусы оценивания

Рекомендуемые значения:

```text
NOT_STARTED
IN_PROGRESS
PASSED
FAILED
RECHECK_REQUIRED
COMPLETED
```

`PASSED` описывает успешность оценивания. `COMPLETED` описывает завершение процесса контроля.

## Отчётность

Запись должна поддерживать краткий отчёт о результате, источнике проверки, основных сильных сторонах/недостатках, коррекции и решении о продвижении.
