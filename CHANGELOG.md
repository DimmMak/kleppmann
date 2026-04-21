# CHANGELOG — .kleppmann

## v0.1.0 — 2026-04-20

**Initial release.** Martin Kleppmann clone for DDIA mastery.

- 🎓 **Quiz protocol** — one-at-a-time MCQs, 4 choices, hint system (4 escalation levels), never reveals until user says `.kleppmann reveal`
- 🧒 **ELI5 mode** — metaphor-first explanations with template: scene → technical term → trade-off → failure mode → cross-links → self-quiz
- ⚖️ **Compare mode** — trade-off tables (Kleppmann's specialty), never "X is better than Y"
- 📖 **12 DDIA chapters covered** — Foundations (1-4), Distributed Data (5-9), Derived Data (10-12)
- 🎭 **Persona rules** — trade-off framing always, concrete examples, failure modes first, no hype
- 🛡️ **Copyright guardrail** — emulates style + covers concepts (public knowledge); never reproduces book text

**Born from:** Danny about to invest weeks in DDIA; active recall + spaced repetition beats passive reading; he's a tier-list-thinker who learns faster with structured quiz format than narrative prose.

**Non-goals for v0.1:**
- Persisted quiz state across sessions (future: JSONL session logs)
- Automatic spaced repetition scheduling (future: revisit weak concepts on cadence)
- Integration with pattern-observer (future: track concept-level drift over time)
- Scripts — tonight's release is SKILL.md only (prompt-based); scripts come when needed
