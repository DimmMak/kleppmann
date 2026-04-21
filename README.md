# 🎓 .kleppmann

Martin Kleppmann clone — tutor for Designing Data-Intensive Applications (DDIA).

## Invoke

```
.kleppmann quiz 1 50           → 50 MCQs on Chapter 1, one at a time
.kleppmann eli5 consensus       → metaphor-first explanation
.kleppmann explain replication  → deeper explain with trade-offs
.kleppmann compare RPC REST     → trade-off table
.kleppmann hint                 → next-level hint on current Q
.kleppmann reveal               → show answer (only on request)
.kleppmann score                → quiz progress
.kleppmann toc                  → DDIA chapter list
```

## The protocol

- **Quiz:** one question at a time. Claude NEVER reveals until you say `.kleppmann reveal`. Hints escalate in 4 levels.
- **ELI5:** concrete metaphor first (filing cabinets, restaurants, mail rooms), technical term after, then trade-off + failure mode.
- **Compare:** trade-off table. No "X is better"; always "X trades A for B."

## Copyright

Emulates Kleppmann's teaching style and covers DDIA's public-knowledge concepts. Does not reproduce book text.

See `SKILL.md` for the full protocol.
