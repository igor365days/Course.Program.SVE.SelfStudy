# Learning Events File Standard

**File:** `04_Progress/Learning.Events.jsonl`  
**Format:** JSON Lines (JSONL)  
**Status:** Canonical standard

## Purpose

Defines the append-oriented historical event stream of significant learner progress events.

This file is not a transcript of the Learning Session.

## Event record

Each line contains exactly one JSON object.

Minimum recommended fields:

```json
{"event_id":"EVT-001","timestamp":"YYYY-MM-DDTHH:MM:SS","type":"UNIT_VERIFIED","section":1,"lesson":1,"unit":"1.1","result":"PASSED","verification":"AI_VERIFIED"}
```

## Core fields

- `event_id` — unique event identifier;
- `timestamp` — event time;
- `type` — canonical event type;
- `section` — section when applicable;
- `lesson` — source lesson when applicable;
- `unit` — Unit when applicable;
- `assessment` — LCP/CP identifier when applicable;
- `result` — event result/status when applicable;
- `verification` — verification source when applicable;
- `summary` — short human-readable context when needed.

## Rules

1. One event per JSONL line.
2. Events are chronological.
3. New events are appended; historical events are not silently rewritten.
4. Events represent significant state-relevant occurrences, not every chat message.
5. Assessment details belong in Assessment Records; the event may reference the assessment.
6. Verification values must follow `Assessment.Verification.Policy`.
7. Event IDs are immutable.

## Event examples

```json
{"event_id":"EVT-001","timestamp":"2026-08-20T10:15:00","type":"UNIT_STARTED","unit":"1.1"}
{"event_id":"EVT-002","timestamp":"2026-08-20T10:42:00","type":"UNIT_VERIFIED","unit":"1.1","result":"PASSED","verification":"AI_VERIFIED"}
{"event_id":"EVT-003","timestamp":"2026-08-20T11:10:00","type":"USER_CONFIRMED","assessment":"LCP-01","summary":"Pronunciation task completed"}
```

## Reporting

The event stream supports historical reconstruction and concise reporting of recent progress without reproducing the conversation transcript.
