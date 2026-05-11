---
name: grill-with-docs
description: Grilling session that challenges each plan against the existing domain model, sharpens terminology, and updates documentation (CONTEXT.md, ADRs) inline as decisions crystallise. Use when user wants to stress-test a plan against their project's language and documented decisions, especially when a new topic may need fresh concept clarification.
---

# Grill With Docs

Challenge the user's plan until the current topic is precise enough to act on.
Every invocation is a new grilling session unless the user explicitly says it
continues the previous one.

## Session Protocol

### 1. Start Session

Classify the request before asking or editing:

- **New topic**: different feature, domain area, workflow, data model, user role,
  integration, or architectural decision from the prior session.
- **Continuation**: user explicitly continues the same unresolved plan or answers
  the previous question.
- **Documentation-only**: user only asks to record an already-resolved decision
  or term.

For a new topic, reset the shared understanding. Do not assume earlier
conversation, existing glossary entries, or previous ADRs fully answer the new
topic. Start a fresh question queue.

### 2. Locate Domain Docs

Use the path logic in [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md):

- Default to root `CONTEXT.md` for single-context repos.
- If root `CONTEXT-MAP.md` exists, use it to choose the relevant context file.
- If no domain docs exist, create root `CONTEXT.md` lazily when the first term is
  resolved.
- Only introduce `CONTEXT-MAP.md` after multiple independent business contexts
  actually exist.

Also read relevant ADRs in `docs/adr/` or the context-specific `docs/adr/`
listed by `CONTEXT-MAP.md`.

### 3. Audit Relevance

Before relying on existing docs, sort prior knowledge into:

- **Directly relevant**: applies to this topic as written.
- **Possibly stale or overloaded**: same words appear, but the current topic may
  use them differently.
- **Not applicable**: belongs to a different context or decision.

Treat "possibly stale or overloaded" as unresolved. Ask the user to confirm it
instead of silently reusing it.

### 4. Build Question Queue

For each new topic, generate unresolved questions across these categories:

- Terms: overloaded or missing domain words.
- Boundaries: what belongs inside or outside the concept.
- Relationships: cardinality, ownership, lifecycle, ordering.
- Scenarios: concrete happy path, edge cases, failure cases.
- Constraints: business, compliance, performance, operational, migration.
- Trade-offs: hard-to-reverse decisions and rejected alternatives.
- Code/doc conflicts: places where implementation, docs, or user statements
  disagree.

Ask one question at a time and include your recommended answer. If code or docs
can answer a factual question, inspect them first; do not use code exploration
to replace user judgment on intent, naming, boundaries, or trade-offs.

For a new topic, ask at least one high-value calibration question unless the
stop conditions are already satisfied by directly relevant docs. If skipping the
question, state that reason explicitly.

### 5. Stop Conditions

Continue asking until all are true for the current topic:

- Core terms are defined or explicitly reused from relevant docs.
- Important boundaries and counterexamples have been tested.
- Relationships and lifecycle rules are clear enough to guide implementation.
- Code, docs, and user statements have no unresolved conflict.
- No ADR-worthy decision is left unrecorded or unoffered.

If you ask no question in a grilling session, say why: the topic is a clear
continuation, documentation-only, or already fully covered by directly relevant
docs.

## Documentation Updates

Update docs inline as decisions crystallize:

- Add or revise terms in the selected `CONTEXT.md` using
  [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md).
- Do not couple `CONTEXT.md` to implementation details. Only include terms that
  are meaningful to domain experts.
- Create an ADR only when all three are true:
  1. **Hard to reverse** - the cost of changing later is meaningful.
  2. **Surprising without context** - a future reader would wonder why.
  3. **Real trade-off** - genuine alternatives existed and one was chosen.
- Use [ADR-FORMAT.md](./ADR-FORMAT.md) for ADRs.
