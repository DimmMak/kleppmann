# kleppmann — Architecture

## Shape (tree)

```
kleppmann/
├── SKILL.md                     # Martin Kleppmann teaching persona + protocol
├── SCHEMA.md                    # JSONL contract for quiz-sessions
├── NON_GOALS.md
├── CHANGELOG.md
├── README.md
├── config/
│   └── kleppmann.config.json    # schema_version, chapter index, TOC
├── data/
│   └── quiz-sessions/
│       └── *.jsonl              # one file per session, append-only
└── tests/
```

## Why this shape

**Persona in SKILL.md** — Claude reads SKILL.md and adopts the Kleppmann
teaching voice. No separate "prompt" files; the voice IS the skill.

**Two modes, one skill** — quiz generator + ELI5 explainer. They share the
underlying knowledge of DDIA but use different surface protocols (quizzing
vs explaining). Splitting them into two skills would force an awkward
chooser; keeping them here lets context naturally dispatch.

**Per-session JSONL** — each `.kleppmann quiz <ch>` run opens a session
file. No global mutable state. Resumable across days.

**No book text in repo** — copyright. The persona *emulates teaching style*
using the user's own understanding as the substrate. SKILL.md enforces this
in `cannot:`.

## Protocol invariants

- **No reveal until asked** — user MUST explicitly type `.kleppmann reveal`
  to see an answer. Never volunteered. Never shown in quiz prompts.
- **One MCQ at a time** — quizzes never dump N questions. One at a time,
  user answers, then next.
- **Hints before reveals** — `.kleppmann hint` gives a nudge; `.kleppmann
  reveal` gives the answer. Two-step forcing function.

## Failure modes

- **User asks for book text verbatim** → decline. Explain why (copyright).
  Offer the persona-level teaching instead.
- **Quiz state corruption** (session jsonl mangled) → start a new session
  file. Never try to repair; append-only + idempotent.
- **Concept out of scope** (not in DDIA) → redirect to general CS tutor.
  Don't fake Kleppmann commentary on topics he hasn't written about.

## Phase roadmap

- **Phase 1** (v0.1.0, current): manual quiz + ELI5 modes, one chapter at
  a time.
- **Phase 2**: cross-chapter linking (Kleppmann-style "recall Chapter 4
  before we tackle Chapter 8"). Depends on `courserafied` integration.
- **Phase 3**: adaptive difficulty. Depends on `pattern-observer` feed
  showing which concepts Danny misses repeatedly.
