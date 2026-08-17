# Стандарт файла состояния обучения

**Документ:** Learning.State.File.Standard
**Файл:** `04_Progress/Learning.State.yaml`
**Формат:** YAML
**Версия:** 1.1
**Статус:** Канонический стандарт проекта
**Применяется к:** Course.Program.SVE.SelfStudy

## 1. Назначение

`Learning.State.yaml` — компактный оперативный снимок текущего состояния прохождения курса.

Он не является историческим источником истины. История восстанавливается из `Learning.Events.jsonl` и Assessment Records.

## 2. Каноническая структура

```yaml
schema_version: "1.1"
project: "Course.Program.SVE.SelfStudy"
progress_status: "NOT_STARTED"
updated_at: "2026-08-17T00:00:00Z"
last_event_id: null
last_assessment_id: null

current:
  section_id: "S01"
  lesson_id: "L01"
  unit_id: "1.1"
  control_type: null
  control_id: null
  phase: "UNIT"
  status: "IN_PROGRESS"

completed:
  units: []
  lcps: []
  cps: []

remediation:
  active: false
  target_type: null
  target_id: null
  reason_ids: []

blocking:
  active: false
  reason: null
  required_action: null

next_action:
  action: "START_UNIT"
  target_type: "UNIT"
  target_id: "1.1"
```

При `NOT_STARTED` поля текущей позиции могут быть `null` до инициализации Progress.

## 3. Идентификаторы

Идентификаторы являются ссылками на канонические объекты курса и не создаются этим стандартом.

Для текущей канонической программы используются:

```text
Section: S01 ... S05
Lesson: L01 ... L18
Unit: 1.1, 1.2 ... 18.4
LCP: LCP-01 ... LCP-18
CP: CP-1 ... CP-5
```

Фактический идентификатор всегда должен точно соответствовать каноническому определению курса. Нельзя самостоятельно преобразовывать `1.1` в `U01.01` или другой формат.

## 4. Допустимые значения progress_status

```text
NOT_STARTED
IN_PROGRESS
COMPLETED
BLOCKED
```

`COMPLETED` используется только после успешного завершения всего курса.

## 5. Поле current

`control_type` принимает:

```text
null
LCP
CP
```

`phase` принимает:

```text
UNIT
LCP
CP
REMEDIATION
RECHECK
```

`status` принимает:

```text
NOT_STARTED
IN_PROGRESS
PASSED
FAILED
BLOCKED
```

Для обычной Unit `control_type` и `control_id` равны `null`.

## 6. Поле completed

```yaml
completed:
  units: []
  lcps: []
  cps: []
```

Массивы содержат только идентификаторы объектов, завершение которых подтверждено историческими данными.

Unit считается завершённой только после `UNIT_VERIFIED` с приемлемыми обязательными компонентами.

LCP/CP считаются завершёнными для маршрута только при успешном результате соответствующей контрольной попытки.

## 7. Поле remediation

```yaml
remediation:
  active: false
  target_type: null
  target_id: null
  reason_ids: []
```

`target_type` принимает `UNIT`, `LCP`, `CP` или `null`.

`reason_ids` содержит краткие стабильные идентификаторы выявленных дефицитов, если они предусмотрены Assessment Record.

## 8. Поле blocking

```yaml
blocking:
  active: false
  reason: null
  required_action: null
```

Если `active: true`, `next_action` не должен разрешать продвижение через блокирующий обязательный этап.

## 9. Поле next_action

```yaml
next_action:
  action: "START_UNIT"
  target_type: "UNIT"
  target_id: "1.1"
```

`action` принимает только значения, определённые `Learning.Progress.Protocol`:

```text
START_UNIT
CONTINUE_UNIT
VERIFY_UNIT
START_LCP
COMPLETE_LCP
START_CP
COMPLETE_CP
REMEDIATION
RECHECK
```

`target_type` принимает `UNIT`, `LCP`, `CP` или `null`.

## 10. Правила согласованности

1. `current` должен соответствовать каноническому маршруту.
2. `next_action` должен быть достижим из `current` без пропуска обязательного этапа.
3. `completed` не может содержать объект, не подтверждённый Events/Assessments.
4. `last_event_id`, если указан, должен существовать в `Learning.Events.jsonl`.
5. `last_assessment_id`, если указан, должен существовать в Assessment Records.
6. При `blocking.active: true` продвижение блокируется.
7. При `remediation.active: true` следующий шаг должен вести к коррекции или повторной проверке.
8. State не должен содержать результат, которого нет в исторических данных.
9. Счётчики не являются источником истины и не должны вводиться в State отдельно от канонического маршрута; отчётность вычисляется из списков `completed` и Assessment Records.

## 11. Обновление

State обновляется после значимого перехода, а не после каждого сообщения чата.

Канонический порядок:

`Event/Assessment → State → READ BACK → VERIFY`.

При конфликте SHA файл сначала перечитывается. Нельзя вслепую перезаписывать более новую версию.
