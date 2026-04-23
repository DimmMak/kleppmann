# kleppmann — Schema

Quiz sessions stored as append-only JSONL under `data/quiz-sessions/`.
One file per session; filename pattern `<chapter>-<yyyymmdd>-<hhmm>.jsonl`.

`schema_version: "0.1"` — matches SKILL.md `unix_contract.schema_version`
and `config/kleppmann.config.json`.

---

## Session record types

Each line in the session file is one record with a `record_type` field.

### `session_start`

First line of every session file.

```json
{
  "schema_version": "0.1",
  "record_type": "session_start",
  "chapter": "5",                          // DDIA chapter number
  "started_at": "2026-04-23T02:00:00Z",
  "n_planned": 10,                         // questions in this session
  "mode": "quiz | eli5 | explain | compare"
}
```

### `question`

One per MCQ shown.

```json
{
  "schema_version": "0.1",
  "record_type": "question",
  "q_id": "ch5-q3",                         // unique within chapter
  "concept": "replication lag",             // tag for pattern-observer feed
  "stem": "Q text...",
  "choices": { "A": "...", "B": "...", "C": "...", "D": "..." },
  "correct": "C",                           // ONLY written to log, never shown
  "asked_at": "..."
}
```

### `answer`

User's answer submission.

```json
{
  "schema_version": "0.1",
  "record_type": "answer",
  "q_id": "ch5-q3",
  "user_choice": "B",
  "correct": false,
  "answered_at": "..."
}
```

### `hint_given`

Each time user requests `.kleppmann hint`.

```json
{
  "schema_version": "0.1",
  "record_type": "hint_given",
  "q_id": "ch5-q3",
  "hint_n": 1,                              // 1st hint, 2nd, ...
  "given_at": "..."
}
```

### `reveal`

Each time user requests `.kleppmann reveal`.

```json
{
  "schema_version": "0.1",
  "record_type": "reveal",
  "q_id": "ch5-q3",
  "revealed_at": "..."
}
```

### `session_end`

Last line of every completed session.

```json
{
  "schema_version": "0.1",
  "record_type": "session_end",
  "ended_at": "...",
  "n_answered": 10,
  "n_correct": 7,
  "score_pct": 70
}
```

---

## Consumer contract

`.kleppmann score` and `.kleppmann toc` read these files to compute
progress. pattern-observer may read `concept` tags on wrong answers to
identify repeat-miss concepts.

Readers MUST tolerate unknown `record_type` values and extra fields
(forward-compat).
