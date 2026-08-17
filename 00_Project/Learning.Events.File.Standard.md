# Стандарт файла учебных событий

**Документ:** Learning.Events.File.Standard
**Файл:** `04_Progress/Learning.Events.jsonl`
**Формат:** JSON Lines (JSONL)
**Версия:** 1.1
**Статус:** Канонический стандарт проекта
**Применяется к:** Course.Program.SVE.SelfStudy

## 1. Назначение

`Learning.Events.jsonl` — исторический append-only поток значимых событий Progress.

Он не является стенограммой Learning Session и не хранит каждое сообщение, объяснение или упражнение.

## 2. Общие правила JSONL

1. Каждая строка содержит ровно один валидный JSON-объект.
2. Порядок строк — хронологический порядок добавления событий.
3. Новые события добавляются в конец файла.
4. Исторические события не переписываются и не удаляются как способ исправления результата.
5. `event_id` уникален и неизменяем.
6. Все поля события должны соответствовать этому стандарту и каноническому Progress Protocol.
7. Подробные результаты оценивания хранятся в Assessment Records; событие содержит только необходимую ссылку и краткий результат.

## 3. Каноническая структура события

```json
{
  "event_id": "EVT-000001",
  "timestamp": "2026-08-17T08:00:00Z",
  "type": "UNIT_STARTED",
  "section_id": "S01",
  "lesson_id": "L01",
  "unit_id": "U01.01",
  "control_type": null,
  "control_id": null,
  "assessment_id": null,
  "result": null,
  "verification": null,
  "actor": "LEARNING",
  "summary": "Unit started"
}
```

## 4. Обязательные поля

Всегда обязательны:

- `event_id` — уникальный идентификатор события;
- `timestamp` — время события в ISO 8601;
- `type` — канонический тип события;
- `actor` — источник/роль, создавшая событие.

Контекстные поля `section_id`, `lesson_id`, `unit_id`, `control_type`, `control_id`, `assessment_id`, `result`, `verification` обязательны, когда они применимы к типу события.

`summary` кратко описывает событие, если одного типа события недостаточно для понимания контекста.

## 5. Допустимые значения type

```text
UNIT_STARTED
UNIT_VERIFIED
REVIEW_REQUIRED
USER_CONFIRMATION_REQUESTED
USER_CONFIRMED
LCP_STARTED
LCP_COMPLETED
REMEDIATION_STARTED
REMEDIATION_COMPLETED
RECHECK_REQUIRED
CP_STARTED
CP_COMPLETED
```

Новые типы нельзя вводить в исторический Progress без изменения канонического стандарта.

## 6. Допустимые значения result

`result` является результатом события, а не универсальным статусом записи.

Разрешены:

```text
PASSED
FAILED
ACCEPTED
REQUIRED
COMPLETED
IN_PROGRESS
BLOCKED
null
```

Конкретный тип события ограничивает применимость значения. Например, `UNIT_STARTED` обычно имеет `result: null` или `IN_PROGRESS`, а `UNIT_VERIFIED` — `PASSED` или `FAILED`.

## 7. Допустимые значения verification

```text
AI_VERIFIED
USER_CONFIRMED
NOT_VERIFIED
null
```

Поле указывает источник подтверждения конкретного результата.

`USER_CONFIRMED` не означает AI-проверку.

`NOT_VERIFIED` не может использоваться как подтверждение успешного завершения обязательного компонента.

## 8. Допустимые значения actor

```text
ORCHESTRATOR
LEARNING
USER
SYSTEM
```

`actor` описывает, от чьего действия создана запись, а не качество результата.

## 9. Связи

`assessment_id` используется, когда событие связано с конкретной попыткой оценивания.

`control_type` принимает:

```text
LCP
CP
null
```

`control_id` должен соответствовать каноническому идентификатору контрольной точки.

## 10. Семантика основных событий

### UNIT_STARTED

Начало работы с разрешённой Unit.

### UNIT_VERIFIED

Unit получила результат проверки. Для `PASSED` все обязательные компоненты должны иметь приемлемое подтверждение.

### REVIEW_REQUIRED

Зафиксирована необходимость целевой коррекции.

### USER_CONFIRMATION_REQUESTED

Система запросила пользовательское подтверждение выполнения требуемого действия.

### USER_CONFIRMED

Пользователь подтвердил выполнение действия. Событие не заменяет оценивание, если оценивание требует отдельного результата.

### LCP_STARTED / CP_STARTED

Начало соответствующей контрольной точки после проверки prerequisites.

### LCP_COMPLETED / CP_COMPLETED

Контрольный процесс завершён. Итоговый результат должен быть восстановим через связанный Assessment Record.

### REMEDIATION_STARTED / REMEDIATION_COMPLETED

Начало/завершение целевой коррекции.

### RECHECK_REQUIRED

Требуется повторная контрольная попытка.

## 11. Идентификатор события

Формат рекомендуется:

```text
EVT-000001
EVT-000002
...
```

Идентификатор должен быть уникальным во всём `Learning.Events.jsonl`.

## 12. Правила исправления

Нельзя редактировать старое событие только для отражения нового результата. Если результат изменился вследствие повторной проверки, добавляются новые события и новая Assessment Record.

Техническое исправление повреждённой записи допускается только как явная операция обслуживания Progress и не должно скрывать исторический факт.

## 13. Примеры

```json
{"event_id":"EVT-000001","timestamp":"2026-08-17T08:00:00Z","type":"UNIT_STARTED","section_id":"S01","lesson_id":"L01","unit_id":"U01.01","control_type":null,"control_id":null,"assessment_id":null,"result":null,"verification":null,"actor":"LEARNING","summary":"Unit started"}
{"event_id":"EVT-000002","timestamp":"2026-08-17T08:20:00Z","type":"UNIT_VERIFIED","section_id":"S01","lesson_id":"L01","unit_id":"U01.01","control_type":null,"control_id":null,"assessment_id":null,"result":"PASSED","verification":"AI_VERIFIED","actor":"LEARNING","summary":"Unit verification passed"}
{"event_id":"EVT-000003","timestamp":"2026-08-17T08:30:00Z","type":"USER_CONFIRMED","section_id":"S01","lesson_id":"L01","unit_id":"U01.01","control_type":"LCP","control_id":"LCP-01","assessment_id":"ASM-LCP-01-01","result":"ACCEPTED","verification":"USER_CONFIRMED","actor":"USER","summary":"Required pronunciation task confirmed"}
```

## 14. Отчётность

Events позволяют восстановить хронологию значимых переходов и проверить происхождение текущего State. Краткие отчёты не должны требовать воспроизведения стенограммы чата.
