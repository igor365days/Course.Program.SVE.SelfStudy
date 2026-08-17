# Шаблоны Progress

**Документ:** Progress.Templates
**Версия:** 1.0
**Статус:** Канонические шаблоны, не являющиеся фактическим Progress

Эти шаблоны предназначены для первоначальной инициализации `04_Progress/`. Они не должны содержать данные реального обучения до официального запуска курса.

## 1. Learning.State.yaml — начальное состояние

```yaml
schema_version: "1.1"
project: "Course.Program.SVE.SelfStudy"
progress_status: "NOT_STARTED"
updated_at: null
last_event_id: null
last_assessment_id: null

current:
  section_id: null
  lesson_id: null
  unit_id: null
  control_type: null
  control_id: null
  phase: null
  status: "NOT_STARTED"

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

`1.1` является первым каноническим Unit согласно текущей программе курса. Фактические идентификаторы Unit всегда берутся из канонического курса.

## 2. Learning.Events.jsonl — начальное состояние

Файл должен существовать как пустой JSONL-файл. До первого реального события строки не добавляются.

Первое событие создаётся только при фактическом `START_UNIT`.

## 3. Assessment Records

До прохождения первого LCP/CP файлы Assessment Records не создаются без необходимости.

При первой попытке создаётся соответствующий файл:

```text
04_Progress/Assessments/LCP-01.yaml
```

или соответствующий `CP-XX.yaml`.

## 4. Правило инициализации

При официальном запуске:

1. создать `04_Progress/Learning.State.yaml` по шаблону;
2. создать пустой `04_Progress/Learning.Events.jsonl`;
3. создать `04_Progress/Assessments/`;
4. проверить, что Progress не содержит тестовых данных;
5. выполнить валидацию;
6. только затем выполнить `START_UNIT` для первого канонического Unit.

## 5. Запрет

Этот документ не является самим Progress и не должен читаться как история обучения. Он содержит только шаблоны структуры.
