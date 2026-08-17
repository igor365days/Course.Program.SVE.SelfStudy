# Машина состояний Progress — Course.Program.SVE.SelfStudy

**Документ:** Learning.State.Machine
**Версия:** 1.0
**Статус:** Каноническая спецификация проекта
**Применяется к:** Course.Program.SVE.SelfStudy

## 1. Назначение

Этот документ формализует допустимые состояния и переходы фактического прохождения курса.

Машина состояний не заменяет каноническую программу, Verification Policy, Learning.Progress.Protocol, Learning State, Events или Assessment Records. Она связывает их в единую модель поведения Orchestrator.

## 2. Основной принцип

Курс является последовательным маршрутом:

`Unit → Unit → ... → LCP → следующий Lesson → ... → LCP → CP → следующий Section`

Orchestrator не имеет права открывать следующий обязательный объект, пока текущий объект не удовлетворяет его prerequisites.

## 3. Состояния учебного объекта

Для Unit, LCP и CP используются следующие логические состояния:

```text
NOT_STARTED
IN_PROGRESS
PASSED
FAILED
BLOCKED
REMEDIATION
RECHECK
```

`NOT_STARTED` — объект ещё не открыт.

`IN_PROGRESS` — работа с объектом начата.

`PASSED` — обязательные требования успешно выполнены и подтверждены.

`FAILED` — контроль завершён, но обязательные требования не выполнены.

`BLOCKED` — продвижение невозможно из-за отсутствия обязательного условия, доказательства или согласованного состояния.

`REMEDIATION` — выполняется целевая коррекция выявленного недостатка.

`RECHECK` — выполняется повторная проверка после коррекции.

## 4. Состояния Progress

`Learning.State.yaml.progress_status` описывает состояние всего курса:

```text
NOT_STARTED
IN_PROGRESS
BLOCKED
COMPLETED
```

`COMPLETED` допускается только после успешного CP последнего раздела и закрытия всех обязательных требований курса.

## 5. Разрешённые действия

Канонический набор действий:

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

Действие всегда имеет целевой объект, кроме случаев, когда это не требуется состоянием.

## 6. Переходы Unit

```text
NOT_STARTED
    │ START_UNIT
    ▼
IN_PROGRESS
    │
    ├── CONTINUE_UNIT ──► IN_PROGRESS
    │
    └── VERIFY_UNIT
            │
            ├── все обязательные компоненты подтверждены
            │       ▼
            │     PASSED
            │       │ UNIT_VERIFIED
            │       ▼
            │   следующий Unit
            │   или LCP
            │
            └── есть обязательный недостаток
                    ▼
                  BLOCKED / REMEDIATION
```

### Правила

1. `START_UNIT` разрешён только для следующего канонического Unit.
2. `CONTINUE_UNIT` не меняет маршрут и обычно не создаёт Event.
3. `VERIFY_UNIT` разрешён только после выполнения учебной работы, предусмотренной каноническим Unit.
4. `PASSED` возможен только при приемлемом подтверждении каждого обязательного компонента.
5. `NOT_VERIFIED` обязательного компонента запрещает `PASSED`.
6. После `PASSED` Unit нельзя снова открыть как новый Unit; повторная работа выполняется как коррекция только при необходимости.
7. Если Unit не пройден, следующий обязательный Unit не открывается.

## 7. Переходы LCP

Prerequisite:

`все Unit соответствующего Lesson = PASSED`.

```text
NOT_STARTED
    │ START_LCP
    ▼
IN_PROGRESS
    │
    └── COMPLETE_LCP
            │
            ├── PASSED
            │     │ LCP_COMPLETED
            │     ▼
            │  следующий Lesson
            │
            └── FAILED
                  │
                  ▼
              REMEDIATION
                  │ REMEDIATION_COMPLETED
                  ▼
                RECHECK
                  │
                  ├── PASSED → следующий Lesson
                  └── FAILED → REMEDIATION / RECHECK
```

Каждая попытка LCP сохраняется отдельным Assessment Record внутри файла соответствующей LCP. Предыдущая попытка не удаляется.

## 8. Переходы CP

Prerequisite:

`все LCP соответствующего Section = PASSED`.

```text
NOT_STARTED
    │ START_CP
    ▼
IN_PROGRESS
    │
    └── COMPLETE_CP
            │
            ├── PASSED
            │     │ CP_COMPLETED
            │     ▼
            │  следующий Section
            │
            └── FAILED
                  │
                  ▼
              REMEDIATION
                  │ REMEDIATION_COMPLETED
                  ▼
                RECHECK
                  │
                  ├── PASSED → следующий Section
                  └── FAILED → REMEDIATION / RECHECK
```

После успешного CP последнего Section:

```text
IN_PROGRESS → COMPLETED
```

## 9. Таблица переходов

| Текущее состояние | Действие | Условие | Результат | Обязательное событие |
|---|---|---|---|---|
| NOT_STARTED Unit | START_UNIT | Unit следующий в маршруте | IN_PROGRESS | UNIT_STARTED |
| IN_PROGRESS Unit | CONTINUE_UNIT | учебная работа продолжается | IN_PROGRESS | нет автоматически |
| IN_PROGRESS Unit | VERIFY_UNIT | работа выполнена | PASSED или REMEDIATION/BLOCKED | UNIT_VERIFIED или REVIEW_REQUIRED |
| NOT_STARTED LCP | START_LCP | все Unit Lesson PASSED | IN_PROGRESS | LCP_STARTED |
| IN_PROGRESS LCP | COMPLETE_LCP | все обязательные компоненты проверены | PASSED или FAILED | LCP_COMPLETED |
| FAILED LCP | REMEDIATION | есть выявленные недостатки | REMEDIATION | REMEDIATION_STARTED |
| REMEDIATION LCP | RECHECK | коррекция завершена | RECHECK | RECHECK_REQUIRED |
| NOT_STARTED CP | START_CP | все LCP Section PASSED | IN_PROGRESS | CP_STARTED |
| IN_PROGRESS CP | COMPLETE_CP | все обязательные компоненты проверены | PASSED или FAILED | CP_COMPLETED |
| FAILED CP | REMEDIATION | есть выявленные недостатки | REMEDIATION | REMEDIATION_STARTED |
| REMEDIATION CP | RECHECK | коррекция завершена | RECHECK | RECHECK_REQUIRED |

## 10. Правила запрета переходов

Следующие переходы запрещены:

- START_UNIT для Unit, который не является следующим разрешённым Unit;
- переход к следующему Unit при незавершённом текущем Unit;
- START_LCP при незавершённом Unit соответствующего Lesson;
- переход к следующему Lesson при непройденном LCP;
- START_CP при непройденном LCP соответствующего Section;
- переход к следующему Section при непройденном CP;
- признание обязательного компонента завершённым при `NOT_VERIFIED`;
- использование одного результата Assessment как подтверждения другой попытки;
- изменение исторического Event для исправления результата вместо добавления нового события;
- изменение Assessment Record прошлой попытки для имитации повторной проверки;
- изменение канонического курса для обхода блокировки Progress.

## 11. Правило Verification

Для каждого обязательного компонента оцениваются независимо:

```text
execution
verification
result
```

Приемлемый положительный компонент:

```text
execution = COMPLETED
verification = AI_VERIFIED или USER_CONFIRMED
result = PASSED или ACCEPTED
```

Точное распределение между AI и пользователем определяется `Assessment.Verification.Policy.md` и каноническим определением контрольной точки.

## 12. Связь с Progress-файлами

Каждый значимый переход должен быть отражён согласованно:

```text
Transition
   │
   ├── Learning Event
   │
   ├── Assessment Record (если относится к контролю)
   │
   └── Learning State
```

Не каждый переход требует Assessment Record. Assessment Record обязателен для контрольной попытки LCP/CP и создаётся согласно модели контроля.

`Learning.State.yaml.next_action` должен соответствовать единственному разрешённому следующему переходу.

## 13. Правило атомарной фиксации

Логический переход считается сохранённым только после:

```text
READ
→ MODIFY
→ WRITE
→ READ BACK
→ VERIFY
```

Если запись Event, Assessment или State не подтверждена, Orchestrator не должен сообщать, что Progress надёжно сохранён.

При частичном сбое сначала определяется фактическое состояние GitHub, затем выполняется восстановление согласованности.

## 14. Восстановление состояния

При противоречии State с историческими данными:

1. остановить продвижение;
2. прочитать Events;
3. прочитать связанные Assessment Records;
4. сопоставить их с каноническим маршрутом;
5. определить последнее подтверждённое состояние;
6. восстановить State;
7. повторно проверить `next_action`.

Память модели и история отдельного чата не являются достаточным основанием для восстановления Progress.

## 15. Инварианты системы

Всегда должны выполняться:

1. Нельзя пройти объект, не пройдя его обязательные prerequisites.
2. `PASSED` требует приемлемого подтверждения всех обязательных компонентов.
3. `NOT_VERIFIED` обязательного компонента блокирует успешное завершение контроля.
4. История попыток не теряется.
5. State не может содержать результат, отсутствующий в Events/Assessments.
6. `next_action` не может обходить обязательный этап.
7. Канонический курс не изменяется ради текущего Progress.
8. Один и тот же Progress используется всеми чатами Project.
9. Тестовый Progress не смешивается с реальным Progress.
10. Любой восстановленный State должен быть проверен против исторических данных и маршрута.

## 16. Минимальная проверка Orchestrator

Перед выдачей следующего действия Orchestrator должен проверить:

```text
1. CHAT ROLE
2. актуальный Progress
3. канонический текущий объект
4. prerequisites
5. обязательные результаты контроля
6. blocking/remediation/recheck
7. допустимость следующего перехода
```

Если хотя бы одна проверка не может быть выполнена достоверно, продвижение блокируется или запрашивается минимально необходимое уточнение.

## 17. Отчётность

Краткий отчёт должен строиться из State + Events + Assessments и показывать:

- текущий Section/Lesson/Unit;
- текущую фазу;
- последние значимые результаты;
- активную коррекцию/блокировку;
- следующий разрешённый переход.

Полная стенограмма чата для отчёта не требуется.

## 18. Связь документов

```text
Project Specification
        │
        ├── Course Orchestrator Specification
        │          │
        │          └── Learning.State.Machine
        │
        ├── Assessment Verification Policy
        │
        └── Learning.Progress.Protocol
                   │
                   ├── Learning.State.File.Standard
                   ├── Learning.Events.File.Standard
                   └── Assessment.Record.File.Standard
```

`Learning.State.Machine.md` определяет допустимые переходы.

`Learning.Progress.Protocol.md` определяет процедуру фиксации этих переходов.

Стандарты файлов определяют физическую структуру данных.

Verification Policy определяет допустимый способ подтверждения.

Course Orchestrator Specification определяет обязанности управляющего слоя.

## 19. Критерий завершения курса

Курс может перейти в `COMPLETED` только если:

- все 56 Unit имеют подтверждённое завершение;
- все 18 LCP имеют успешный результат;
- все 5 CP имеют успешный результат;
- отсутствуют активные обязательные блокировки, коррекции и повторные проверки;
- последнее состояние согласовано с историческими Events и Assessment Records;
- следующий обязательный объект отсутствует, потому что канонический маршрут полностью завершён.
