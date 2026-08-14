# Стандарт файла состояния обучения

**Файл:** `04_Progress/Learning.State.yaml`  
**Формат:** YAML  
**Статус:** Канонический стандарт

## Назначение

Определяет структуру компактного текущего состояния Progress одного обучающегося.

Файл является оперативным снимком, а не историческим источником истины.

## Каноническая структура

```yaml
course: Course.Program.SVE.SelfStudy
state_version: 1
updated_at: YYYY-MM-DDTHH:MM:SS

current:
  section: 1
  lesson: 1
  unit: 1.1
  control: null
  status: IN_PROGRESS

progress:
  units_completed: 0
  units_total: 56
  lessons_completed: 0
  lessons_total: 18
  lcps_passed: 0
  lcps_total: 18
  cps_passed: 0
  cps_total: 5

last_completed:
  unit: null
  lesson: null
  lcp: null
  cp: null

remediation:
  required: false
  target: null
  reason: null

next_action: START_UNIT
blocking_conditions: []
```

## Правила

1. Здесь хранится только текущее состояние; стенограммы чатов исключаются.
2. Счётчики должны соответствовать каноническим итоговым значениям курса.
3. `current` определяет текущую позицию обучающегося на маршруте.
4. `next_action` должен соответствовать каноническому маршруту и правилам Orchestrator.
5. Обязательный нерешённый контроль нельзя исключать из `blocking_conditions`.
6. Источник проверки при необходимости может быть указан значением `AI_VERIFIED`, `USER_CONFIRMED`, `NOT_VERIFIED`.
7. Состояние может быть восстановлено из исторических событий и записей оценивания.
8. Данные конкретного обучающегося никогда не должны записываться в канонические файлы курса.

## Отчётность

Структура должна поддерживать краткие отчёты о текущей позиции, общем Progress, последнем завершённом контроле и следующем действии.
